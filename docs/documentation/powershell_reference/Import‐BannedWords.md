# Description
The ```Import-BannedWords``` cmdlet will import a file containing new line-separated words into the banned word store. Each line read from the file will have the [normalization rules](../Normalization-rules.md) applied to it before being committed to the store.

## Syntax
```
Import-BannedWords -Filename <string> -BatchSize <int>
```

### Parameters
##### `Filename`
Required. The name of the file containing the words to add to the store. 

##### `BatchSize`
Optional. Specifies how many lines to read from the file before committing them to disk. 

In order to minimize the impact of memory usage when importing words, the words are read from the file and committed to the store in batches of this size. The larger the batch size, the faster the import, but the more memory is used. If left unspecified, the default value of 5,000,000 is used which provides an adequate balance of memory usage and speed.

### Examples
The following example shows how to import a file of words
```powershell
Import-BannedWords -Filename "D:\password-protection\english-dictionary.txt"
```

To increase speed when importing a large file when additional memory is available, you can specify a larger batch size
```powershell
Import-BannedWords -Filename "D:\password-protection\english-dictionary.txt" -BatchSize 50000000
```


