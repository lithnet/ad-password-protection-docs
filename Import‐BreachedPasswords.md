## Description
The ```Import-BreachedPasswords``` cmdlet will import a file containing new line-separated plain-text passwords into the breached password store. 

## Syntax
```
Import-BreachedPasswords-Filename <string> -BatchSize <int>
```

## Parameters
##### Filename
Required. The name of the file containing the plain text passwords. 

#### BatchSize
Optional. Specifies how many passwords to read from the file before committing them to disk. 

In order to minimize the impact of memory usage when importing passwords, the passwords are read from the file and committed to the store in batches of this size. The larger the batch size, the faster the import, but the more memory is used. If left unspecified, the default value of 5,000,000 is used which provides an adequate balance of memory usage and speed.

## Examples
The following example shows how to import a file of passwords
```powershell
Import-BreachedPasswords -Filename "D:\password-filter\plain-text-passwords.txt"
```

To increase speed when importing a large file when additional memory is available, you can specify a larger batch size
```powershell
Import-BreachedPasswords -Filename "D:\password-filter\plain-text-passwords.txt" -BatchSize 50000000
```


