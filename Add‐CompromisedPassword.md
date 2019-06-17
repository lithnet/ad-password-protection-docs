## Description
The ```Add-CompromisedPassword``` cmdlet adds a string into the compromised password store. When the password filter is configured to check against compromised passwords, any password that is an exact match to this string will rejected.

## Syntax
```
Add-CompromisedPassword -Value <string>

Add-CompromisedPassword -SecureString <SecureString>
```
## Parameters
##### `Value`
Required. The password to add to the compromised password store 

##### `SecureString`
Required. The password to add to the compromised password store as a secure string

## Examples
The following example adds a single compromised password to the store
```powershell
Add-CompromisedPassword -Value "password"
```

The following example prompts for a password to add to the compromised password
```powershell
Add-CompromisedPassword -SecureString (Read-Host -Prompt "Enter the compromised password to add to the store" -AsSecureString)
```

To import a file of compromised passwords, use the [[Import‐CompromisedPasswords]] or [[Import‐CompromisedPasswordHashes]] cmdlets
