## Description
The ```Test-BannedWord``` cmdlet checks to see if a specified string matches a value in the banned word store. The [[normalization rules]] are applied to the string and the resulting value is checked against the store.

## Syntax
```
Test-BannedWord -Value <string>

Test-BannedWord -Hash <byte[]>

Test-BannedWord -SecureString <SecureString>
```

## Parameters
##### `Value`
Required. The string to test. [[Normalization rules]] are applied to this string before it is checked against the store

##### `Hash`
Required. A binary hash to test. A hash cannot be normalized, so it is tested as-is.

##### `SecureString`
Required. The string to test as a SecureString. [[Normalization rules]] are applied to this string before it is checked against the store

## Return value
The cmdlet returns a boolean value indicating whether the input string or hash matches a value in the banned word store.

## Examples
```powershell
# Add a word to the store
PS> Add-BannedWord -Value password

# Test the exact word and ensure it is found
PS> Test-BannedWord -Value password
True

# Test a modification of the banned word, and ensure it is found
PS> Test-BannedWord -Value P@ssw0rd!
True

# Prompt for a banned word to test
PS> Test-BannedWord -SecureString (Read-Host -Prompt "Enter the banned word to test" -AsSecureString)
```