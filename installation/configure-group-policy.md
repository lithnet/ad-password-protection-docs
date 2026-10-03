# Configure the password group policy

The password filter must be enabled and configured using group policy before it will process password changes. When installing the application, you have the option of installing the ADMX group policy template files.

The group policy templates should be installed on any machine that you need to configure the password settings group policy on. We recommend copying the ADMX files to a [central policy store](https://support.microsoft.com/en-au/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), which will enable you to see and manage the group policy settings from any machine in the domain.

If you do not copy the ADMX/ADML files to the central policy story in the domain, you'll only be able to see and edit the group policy settings from the machine where you installed the ADMX files.

The files that need to be copied are as follows

```
%WINDIR%\PolicyDefinitions\lithnet.activedirectory.passwordfilter.admx
%WINDIR%\PolicyDefinitions\lithnet.admx
%WINDIR%\PolicyDefinitions\en-us\lithnet.activedirectory.passwordfilter.adml
%WINDIR%\PolicyDefinitions\en-us\lithnet.adml
```

Please ensure that the ADML files are places into the `en-us` folder of the central policy store.

{% hint style="info" %}
If you don't see the group policy settings for Lithnet Password Protection in the group policy editor after installing them, it may be because you have a central policy store configured. Copy the group policy files to the central policy store, and restart the group policy editor.
{% endhint %}

Once you have installed the templates, create a new GPO, which you will link to the OU containing your domain controllers in Active Directory. If you have other computers that you want to be able to use the [Get‐PasswordFilterResult](../advanced-help/powershell-reference/get-passwordfilterresult.md) cmdlet on, they will need to have the group policy applied to them as well.

Do note that Active Directory will still process its own password policy rules, so ensure that the built-in Active Directory password policy settings do not conflict with those that you set in the Lithnet Password Protection settings. For example if you are using password complexity settings in this LPP, then it's recommended to disable Active Directory's complexity settings.

The group policy settings are found under `Computer Configuration\Policies\Administrative Templates\Lithnet\Password Filter`.

## Settings Reference

### General settings

| Setting                 | Explanation                                                                                                                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Disable password filter | When enabled, prevents the password filter from evaluating password change requests. If disabled, or set to not configured, the password filter will evaluate password change requests |

### Regular expression policies

| Setting                                                 | Explanation                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Passwords must match a specified regular expression     | When enabled, passwords that do not match the specified regular expression will be rejected. If disabled, or set to not configured, the password filter will not evaluate passwords against the regular expression. The regular expression only needs to match part of the password. For example, `[0-9]` rejects `Summer` but not `Summer2026`, because only `Summer2026` contains a digit. To require the regular expression to match the entire password, start it with `^` and end it with `$`. |
| Passwords must not match a specified regular expression | When enabled, passwords that match the specified regular expression will be rejected. If disabled, or set to not configured, the password filter will not evaluate passwords against the regular expression. The password is rejected if the regular expression matches any part of it. For example, `password` rejects `MyPassword1`. To reject only passwords that the regular expression matches in full, start it with `^` and end it with `$`, so that `^password$` rejects `Password` but not `MyPassword1`. |

{% hint style="info" %}
Regular expression matching isn't case-sensitive, so `[A-Z]` matches lowercase letters as well as uppercase letters. To require uppercase or lowercase letters, use a [length-based complexity policy](../advanced-help/configuring-a-length-based-complexity-policy.md) instead.

If you anchor a regular expression that uses `|`, put the alternatives in parentheses. For example, `^(summer|winter)$` matches only `summer` and `winter`, but `^summer|winter$` matches any password that starts with `summer` or ends with `winter`.
{% endhint %}

### Complexity policies

| Setting                                                       | Explanation                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Passwords must meet the specified number of complexity points | The password filter allows you to set a points-based threshold for password complexity. You must specify the number of points a password must reach to be approved. You can then assign points based on the character make up of the password. See the page on [configuring a points-based complexity policy](../advanced-help/configuring-a-points-based-complexity-policy.md) for more information |
| Enable length-based complexity rules                          | When enabled, enforces password complexity rules based on the length of the supplied password. This policy allows you to provide granular complexity requirements based on password length. You can reward longer passwords with less complex requirements. See the page on [configuring a length-based complexity policy](../advanced-help/configuring-a-length-based-complexity-policy.md)         |
| Minimum password length                                       | When enabled, specifies the minimum password length to enforce. If disabled or not configured, no minimum password length is enforced                                                                                                                                                                                                                                                                |

### Password content policies

| Setting                                                             | Explanation                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Reject passwords that contain the user's account name               | When enabled, the filter will reject any password that contains the user's account name, provided the account name is greater than 3 characters in length. If disabled, or set to not configured, the password filter will not reject the password if it contains the user's account name |
| Reject passwords that contain any part of the user's display name   | When enabled, the filter will reject any password that contains all or part of the user's display name. If disabled, or set to not configured, the password filter will not reject the password if it contains the user's display name                                                    |
| Reject passwords found in the compromised password store            | When enabled, passwords will be rejected if they are found in the compromised password store. If disabled, or set to not configured, the password filter will not evaluate passwords against the compromised password store                                                               |
| Reject normalized passwords found in the compromised password store | When enabled, incoming passwords will be normalized according to the [normalization rules](../advanced-help/normalization-rules.md) before being compared to the compromised password store                                                                                            |
| Reject normalized passwords found in the banned word store          | When enabled, incoming passwords will be normalized according to the [normalization rules](../advanced-help/normalization-rules.md) before being compared to the banned word store.                                                                                                    |
