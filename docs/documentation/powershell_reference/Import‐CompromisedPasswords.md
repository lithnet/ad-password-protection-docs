# Description

The ```Import-CompromisedPasswords``` cmdlet will import a file containing new line-separated plain-text passwords into the compromised password store. 

## Syntax
```
Import-CompromisedPasswords -Filename <string> -BatchSize <int>
```

##### Parameters
##### `Filename`
Required. The name of the file containing the plain text passwords. 

##### `BatchSize`
Optional. Specifies how many passwords to read from the file before committing them to disk. 

In order to minimize the impact of memory usage when importing passwords, the passwords are read from the file and committed to the store in batches of this size. The larger the batch size, the faster the import, but the more memory is used. If left unspecified, the default value of 5,000,000 is used which provides an adequate balance of memory usage and speed.

### Examples
The following example shows how to import a file of passwords
```powershell
Import-CompromisedPasswords -Filename "D:\password-protection\plain-text-passwords.txt"
```

To increase speed when importing a large file when additional memory is available, you can specify a larger batch size
```powershell
Import-CompromisedPasswords -Filename "D:\password-protection\plain-text-passwords.txt" -BatchSize 50000000
```


