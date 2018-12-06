## Description
The ```Test-BreachedPassword``` cmdlet checks to see if a specified string matches a value in the banned password store. 

## Syntax
```
Test-BreachedPassword -Value <string> -Normalize

Test-BreachedPassword -Hash <byte[]>
```

## Parameters
##### `Value`
Required. The string to test. 

##### `Normalized`
Optional. If specified, [[normalization rules]] are applied to the password before being checked against the breached password store. To test against the banned word store, use the [[Test‐BannedWord]] cmdlet instead.

##### Hash
Required. A binary hash to test.

## Return value
The cmdlet returns a boolean value indicating whether the input string or hash matches a value in the breached password store.

## Examples
```powershell
# Add a password to the store
PS> Add-BreachedPassword -Value password!!!

# Test the password and ensure it is found
PS> Test-BreachedPassword -Value password!!!
True
```