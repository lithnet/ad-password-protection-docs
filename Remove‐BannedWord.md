## Description
The ```Remove-BannedWord``` cmdlet takes a string of text, applies the [[normalization rules]] to it, and removes it from the banned word store. If the normalized word is not present in the store, this cmdlet does nothing.

## Syntax
```
Remove-BannedWord -Value <string>

Remove-BannedWord -SecureString <SecureString>
```

## Parameters
##### `Value`
Required. The string of text to remove from the store. [[Normalization rules]] will be applied to the string.

##### `SecureString`
Required. The string of text to remove from the store as a secure string object. [[Normalization rules]] will be applied to the string. 

## Examples
The following example removes a single banned word from the store
```powershell
Remove-BannedWord -Value "password"
```

The following example prompts for a word to be removed from the store
```powershell
Remove-BannedWord -SecureString (Read-Host -Prompt "Enter the banned word to remove from the store" -AsSecureString)
```