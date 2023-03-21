# Testing the password filter

## Validating installation
The first step to ensure the password filter is working, is to check to see if it is loaded at startup. Reboot the computer, and open the event viewer. 

In the `Application` log, make sure you can see event ID 3, from `LithnetPasswordProtection` with the message shown below

```
The password filter has been successfully loaded.
```

If this does not appear, check in the `System` log for any directory services, or LSA error messages about problems loading the password filter.

## Testing the password filter by changing a user's password

The best way to test the password filter is by changing or resetting a user's password in Active Directory. If you attempt to change the password to one that does not meet the requirements, it will be rejected, and you'll see the less-than-helpful standard error message from AD

```
The password does not meet the length, complexity, or history requirement of the domain
```

In order to determine the exact reason for the rejection, you can examine the event logs on the domain controller that processed the password change request. The `Application` log will contain events from `LithnetPasswordProtection` for each password change or set attempt.

```
Event ID: 8196
Event Source: LithnetPasswordProtection
Message:
The password set request for jsmi0001 (John Smith) was rejected because it matched a password in the compromised password store.
```

The [event logging and reporting](../advanced-help/event-logging-and-reporting.md) page details all the various event codes the filter can return.

{% hint style="info" %}
While the password filter may approve the password, it may still be rejected by Active Directory for reasons such as the minimum password age and password history. If you have other password filters installed, they also may reject the password before it reaches the Lithnet password filter.

If you do not see an event for LithnetPasswordProtection explaining why the password was rejected, then something else rejected the password before LPP could process it.
{% endhint %}

If the password change was not blocked as expected, run the [Get-PasswordFilterConfig](../advanced-help/powershell-reference/get-passwordfilterconfig.md) and [Get-PasswordFilterPolicy](../advanced-help/powershell-reference/get-passwordfilterpolicy.md) cmdlets on the server that processed the password change, and ensure the correct configuration and policy is applied.

## Testing the password filter using PowerShell

You can also test the password filter using PowerShell, on any machine that has the PowerShell module installed, and the password filter group policy applied to it. Using the [Get‐PasswordFilterResult](../advanced-help/powershell-reference/get-passwordfilterresult.md) cmdlet, you can call the password filter DLL, and return the exact reason for the rejection, without having to process the password change through Active Directory.
