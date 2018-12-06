## Description
The ```Import-BreachedPasswordHashes``` cmdlet will import a file containing newline-separated NTLM hashes into the breached password store. 

The NTLM password files from [haveibeenpwned.com](https://haveibeenpwned.com/passwords) can be imported directly without modification using this cmdlet. Ensure you download the "sorted-by-hash" version of the file for the best import performance.

## Syntax
```
Import-BreachedPasswordHashes -Filename <string> -Sorted <boolean> -BatchSize <int>
```
## Parameters
##### Filename
Required. The of the file containing the NTLM hashes. Each hash should be in hex format, be 32 characters in length, and each record must appear on a new line. The hash can optionally end with a colon and anything after the colon character is ignored. 

The following list shows the allowed formats. The hashes are not case sensitive.
```
8846f7eaee8fb117ad06bdd830b7586c
5835048ce94ad0564e29a924a03510ef:123
e22e04519aa757d12f1219c4f31252f4:3
e22e04519aa757d12f1219c4f31252f4:
```

#### Sorted
Optional. A boolean value indicating if the hashes in the file are sorted in ascending order or not. The cmdlet will optimize the type of import it performs based on this parameter. A sorted file will allow a much faster import of data into the store. However, there is a significant penalty if you specify that the file is sorted when it is not. If this parameter is omitted, the cmdlet will guess which algorithm to use by reading the first 1000 lines of the file. If those first 1000 lines are all in order, a sorted import will be performed.

#### BatchSize
Optional. Specifies how many hashes to read from an unsorted file before committing to disk. This parameter has no effect on a sorted file. 

In order to minimize the impact of memory usage when importing unsorted hashes, the hashes are read from the file and committed to the store in batches of this size. The larger the batch size, the faster the import, but the more memory is used. If left unspecified, the default value of 5,000,000 is used which provides an adequate balance of memory usage and speed.

## Examples
The following example shows how to import a file of hashes, while allowing the cmdlet to determine the sort status and batch size
```powershell
Import-BreachedPasswordHashes -Filename "D:\password-filter\pwned-passwords-ntlm-ordered-by-hash.txt"
```

To increase speed when importing an unsorted file when additional memory is available, you can specify a larger batch size
```powershell
Import-BreachedPasswordHashes -Filename "D:\password-filter\pwned-passwords-ntlm-ordered-by-count.txt" -Sorted $false -BatchSize 50000000
```


