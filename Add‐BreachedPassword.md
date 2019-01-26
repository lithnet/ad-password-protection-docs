## Description
The ```Add-BreachedPassword``` cmdlet and a string into the breached password store. When the password filter is configured to check against breached passwords, any password that is an exact match to this string will rejected.

## Syntax
```
Add-BreachedPassword -Value <string>

Add-BreachedPassword -SecureString <SecureString>
```
## Parameters
##### `Value`
Required. The password to add to the breached password store 

##### `SecureString`
Required. The password to add to the breached password store as a secure string

## Examples
The following example adds a single breached password to the store
```powershell
Add-BreachedPassword -Value "password"
```

The following example prompts for a password to add to the breached password
```powershell
Add-BreachedPassword -SecureString (Read-Host -Prompt "Enter the breached password to add to the store" -AsSecureString)
```

To import a file of breached passwords, use the [[Import‐BreachedPasswords]] or [[Import‐BreachedPasswordHashes]] cmdlets