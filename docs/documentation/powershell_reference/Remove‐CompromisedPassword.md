## Description
The ```Remove-CompromisedPassword``` cmdlet removes a string of text from the compromised password store. 

## Syntax
```
Remove-CompromisedPassword -Value <string>

Remove-CompromisedPassword -SecureString <SecureString>
```
## Parameters
##### `Value`
Required. The password to remove from the compromised password store 

##### `SecureString`
Required. The password to remove from the compromised password store as a secure string

## Examples
The following example removes a single compromised password from the store
```powershell
Remove-CompromisedPassword -Value "password"
```

The following example prompts for a password to remove from the compromised password store
```powershell
Remove-CompromisedPassword -SecureString (Read-Host -Prompt "Enter the compromised password to remove from the store" -AsSecureString)
```
