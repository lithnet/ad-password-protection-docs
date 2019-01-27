## Description
The ```Test-IsADUserPasswordCompromised``` cmdlet will extract the current password hash from Active Directory for the specified user, and check to see if it exists in the compromised password store. 

This cmdlet must be executed by a user in the `Domain Admins` group, or by a user who holds the `Replicate Directory Changes All` permission on the domain containing the user to test. 

Performing this action is a security-sensitive operation, and should only be performed from trusted devices within the domain. 

This cmdlet does not require the password filter to be registered with LSASS, but it does require direct access to the store. The cmdlet will not check the password against other password policy settings. It only checks to see if the password hash is located in the compromised password store.

## Syntax
```powershell
# Test a user's password using their username and domain name
Test-IsADUserPasswordCompromised -AccountName <string> -DomainName <string> -Server <string> -Credential <PSCredential> -OutBadHashOnMatch

# Test a user's password using their UPN
Test-IsADUserPasswordCompromised -Upn <string> -Server <string> -Credential <PSCredential> -OutBadHashOnMatch

# Test a user's password using the string representation of their SID
Test-IsADUserPasswordCompromised -Sid <string> -Server <string> -Credential <PSCredential> -OutBadHashOnMatch
```

## Parameters
##### `AccountName`
Required. The samAccountName of the user who's password should be tested.

##### `Domain`
Required. The domain of the user who's password should be tested.

##### `Upn`
Required. The userPrincipalName attribute of the user who's password should be tested.

##### `Sid`
Required. The string-representation of the SID of the user who's password should be tested.

##### `Server`
Optional. The server to retrieve the password hash from. If omitted, the cmdlet will use the value of the logged on-user's `UserDNSDomain` environment variable.

##### `Credential`
Optional. The credentials to use to retrieve the password has from the directory. If omitted, the credentials of the currently logged on user are used.

##### `OutBadHashOnMatch`
The cmdlet ordinarily returns a `$true` `$false` value to indicate if the password is in the store. If this switch is specified, the cmdlet will output the raw NTLM hash when a match is found in the store, and nothing if there was no match.

## Return value
The cmdlet returns a boolean value indicating whether the user's password was found in the compromised password store. 
However, if the `OutBadHashOnMatch` switch is specified, and the user's password was found in the compromised password store, the cmdlet will return the compromised password hash in hex format.

## Examples
Test a user password using the default credentials against the default domain
```powershell
PS> Test-IsADUserPasswordCompromised -AccountName ryan -DomainName lithnet
True
```

Test a user password using the UPN of the user
```powershell
PS> Test-IsADUserPasswordCompromised -Upn ryan@lithnet.io
True
```

Test a user password using the SID of the user
```powershell
PS> Test-IsADUserPasswordCompromised -Sid S-1-5-23423432-2343243211-44423
True
```

Test a user password, specifying a server name and prompting for credentials for the operation
```powershell
PS> Test-IsADUserPasswordCompromised -Upn ryan@lithnet.io -Server dc1.lithnet.local -Credentials (Get-Credential)
False
```

Test a user password using the samAccountName of the user, and return the hash if a compromised password was detected
```powershell
# cmdlet returns the hash when a compromised password was found
PS> Test-IsADUserPasswordCompromised -AccountName ryan -Domain lithnet -OutBadHashOnMatch
8846f7eaee8fb117ad06bdd830b7586c

# cmdlet returns nothing if the password isn't compromised
PS> Test-IsADUserPasswordCompromised -AccountName bob -Domain lithnet -OutBadHashOnMatch
```






