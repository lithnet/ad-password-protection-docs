## Description
The ```Add-BannedWord``` cmdlet takes a string of text, normalizes it, and adds it to the banned word store. 

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

You can import a file of newline-separated words using the PowerShell pipeline
```powershell
Get-Content -Path C:\words\english-dictionary.txt | Add-BannedWord
```