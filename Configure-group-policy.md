The password filter must be enabled and configured using group policy before it will process password changes. When installing the application, you have the option of installing the ADMX group policy template files. 

The group policy templates should be installed on any machine that you need to configure the password settings group policy on. We recommend copying the ADMX files to a [central policy store](https://support.microsoft.com/en-au/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), which will enable you to see and manage the group policy settings from any machine in the domain.

Once you have installed the templates, create a new GPO, which you will link to the OU containing your domain controllers in Active Directory. If you have other computers that you want to be able to use the [[Get‐PasswordFilterResult]] cmdlet on, they will need to have the group policy applied to them as well.

Do note that Active Directory will still process its own password policy rules, so ensure that the built-in Active Directory password policy settings do not conflict with those that you set in the Lithnet Password Protection settings. For example if you are using password complexity settings in this LPPAD, then its recommended to disable Active Directory's complexity settings.

The group policy settings are found under `Computer Configuration\Policies\Administrative Templates\Lithnet\Password Filter`.

### Settings Reference
#### General settings
| Setting | Explanation |
| --- | --- |
| Disable password filter | When enabled, prevents the password filter from evaluating password change requests. If disabled, or set to not configured, the password filter will evaluate password change requests |

#### Regular expression policies
| Setting | Explanation | 
| --- | --- |
| Password must match a specified regular expression | When enabled, passwords that do not match the specified regular expression will be rejected. If disabled, or set to not configured, the password filter will not evaluate passwords against the regular expression |
| Passwords must not match a specified regular expression | When enabled, passwords that match the specified regular expression will be rejected. If disabled, or set to not configured, the password filter will not evaluate passwords against the regular expression |

#### Complexity policies
| Setting | Explanation |
| --- | --- |
| Passwords must meet the specified number of complexity points | The password filter allows you to set a points-based threshold for password complexity. You must specify the number of points a password must reach to be approved. You can then assign points based on the character make up of the password. See the page on [[configuring a points-based complexity policy]] for more information | 
| Enable length-based complexity rules | When enabled, enforces password complexity rules based on the length of the supplied password. This policy allows you to provide granular complexity requirements based on password length. You can reward longer passwords with less complex requirements. See the page on [[configuring a length-based complexity policy]] for more information |
| Minimum password length | When enabled, specifies the minimum password length to enforce. If disabled or not configured, no minimum password length is enforced | 

#### Password content policies
| Setting | Explanation |
| --- | --- |
| Reject passwords that contain the user's account name | When enabled, the filter will reject any password that contains the user's account name, provided the account name is greater than 3 characters in length. If disabled, or set to not configured, the password filter will not reject the password if it contains the user's account name |
| Reject passwords that contain any part of the user's display name | When enabled, the filter will reject any password that contains all or part of the user's display name. If disabled, or set to not configured, the password filter will not reject the password if it contains the user's display name |
| Reject passwords found in the compromised password store | When enabled, passwords will be rejected if they are found in the compromised password store. If disabled, or set to not configured, the password filter will not evaluate passwords against the compromised password store |
| Reject normalized passwords found in the compromised password store | When enabled, incoming passwords will be normalized according to the [[normalization rules]] before being compared to the compromised password store | 
| Reject normalized passwords found in the banned word store | When enabled, incoming passwords will be normalized according to the [[normalization rules]] before being compared to the banned word store. |

Next: [[Test the password filter|Testing the password filter]]