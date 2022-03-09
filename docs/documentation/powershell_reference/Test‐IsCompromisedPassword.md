# Description
The ```Test-IsCompromisedPassword``` cmdlet checks to see if a specified string matches a value in the compromised password store. 

## Syntax
```
Test-IsCompromisedPassword -Value <string> -Normalize

Test-IsCompromisedPassword -Hash <byte[]>

Test-IsCompromisedPassword -SecureString <SecureString> -Normalize
```

### Parameters
##### `Value`
Required. The string to test. 

##### `Normalize`
Optional. If specified, [normalization rules](../Normalization-rules.md) are applied to the password before being checked against the compromised password store. To test against the banned word store, use the [Test‐IsBannedWord](Test‐IsBannedWord) cmdlet instead.

##### `Hash`
Required. A binary hash to test.

##### `SecureString`
Required. The string to test as a SecureString. 

### Return value
The cmdlet returns a boolean value indicating whether the input string or hash matches a value in the compromised password store.

### Examples
```powershell
# Add a password to the store
PS> Add-CompromisedPassword -Value password!!!

# Test the password and ensure it is found
PS> Test-IsCompromisedPassword -Value password!!!
True

# Prompt for a compromised password to test
PS> Test-IsCompromisedPassword -SecureString (Read-Host -Prompt "Enter the password to test" -AsSecureString)
```