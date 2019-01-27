## Testing the password filter using Active Directory
The best way to test the password filter is by changing or resetting a user's password in Active Directory. If you attempt to change the password to one that does not meet the requirements, it will be rejected, and you'll see the less-than-helpful standard error message from AD
```
The password does not meet the length, complexity, or history requirement of the domain
```

In order to determine the exact reason for the rejection, you can examine the event logs on the domain controller that processed the password change request. The `Application` log will contain events from `LithnetPasswordProtection` for each password change or set attempt.

```
Event ID: 8196
Event Source: LithnetPasswordProtection
Message:
The password set request for rnew0001 (Ryan Newington) was rejected because it matched a password in the compromised password store.
```

The [[event logging and reporting]] page details all the various event codes the filter can return.

> Note: While the password filter may approve the password, it may still be rejected by Active Directory for reasons such as the minimum password age and password history. If you have other password filters installed, they also may reject the password before it reaches the Lithnet password Filter

## Testing the password filter using PowerShell
You can also test the password filter using PowerShell, on any machine that has the PowerShell module installed, and the password filter group policy applied to it. Using the [[Get‐PasswordFilterResult]] cmdlet, you can call the password filter DLL, and return the exact reason for the rejection, without having to process the password change through Active Directory. 

Next: [[Audit existing passwords]]