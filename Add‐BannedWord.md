## Description
The ```Add-BannedWord``` cmdlet takes a string of text, applies the [[normalization rules]] to it, and adds it to the banned word store. 

## Syntax
```
Add-BannedWord -Value <string>
```
## Parameters
##### Value
Required. The string of text to add to the store. [[Normalization rules]] will be applied to the string before it is committed to the store 

## Examples
The following example adds a single banned word to the store
```powershell
Add-BannedWord -Value "password"
```

To import a file of breached passwords, use the [[Import‐BannedWords]] or [[Import‐BannedWordHashes]] cmdlets