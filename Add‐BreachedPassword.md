## Description
The ```Add-BreachedPassword``` cmdlet and a string into the breached password store. When the password filter is configured to check against breached passwords, any password that is an exact match to this string will rejected.

## Syntax
```
Add-BreachedPassword -Password "thisisabadpassword"
```
## Parameters
##### Password
Required. The password to add to the breached password store 

## Examples
The following example adds a single breached password to the store
```powershell
Add-BreachedPassword -Password "password"
```

To import a file of breached passwords, use the [[Import‐BreachedPasswords]] or [[Import‐BreachedPasswordHashes]] cmdlets