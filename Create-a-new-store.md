The store is the database that contains the compromised passwords and banned words you want to prevent from being used in your environment. An empty store is created when you install the module, so you'll need to use the PowerShell module to build your store. 

## Creating a new store
If you didn't specify your store path when running the installer, first create a new empty folder for the store
```powershell
mkdir D:\password-protection\store
```

It is recommended to exempt this folder from anti-virus scans, at least while you are building the store. It can add a considerable amount of time to the process if you do not.

Next, import the PowerShell module and open the store folder
```powershell
Import-Module LithnetPasswordProtection
Open-Store -Path "D:\password-protection\store"
```
## Add compromised passwords to the store
The PowerShell module is now ready to use the new store folder. First, import your compromised passwords. We recommend starting with the [Have I Been Pwned](https://haveibeenpwned.com/Passwords) NTLM password list. Download the version that says `(ordered by hash)` for the best performance. Once you have the download, import them into your new store using the [[Import-CompromisedPasswordHashes|Import‐CompromisedPasswordHashes]] cmdlet.

```powershell
Import-CompromisedPasswordHashes -Filename "D:\password-protection\pwned-passwords-ntlm-ordered-by-hash.txt"
```

> The raw NTLM hash list from HIBP requires about 17GB of disk space when uncompressed. However, once imported, these hashes only take up 6.75GB of space in the store. Populating the store takes approximately 40mins on a host with 1 x vCPU @ 2.4Ghz with 3.5Gb RAM.

If you have other NTLM hash sets you want to import, you can do so. Just make sure they are in a text file, each separated by a new line.

You can also choose to import any plain-text password lists that you have access to. These are imported using the [[Import-CompromisedPasswords|Import‐CompromisedPasswords]] cmdlet. Hashes.org has a large list of [cracked plain-text passwords](https://hashes.org/left.php) that you can download and import.

```powershell
Import-CompromisedPasswords -Filename "D:\password-protection\hashes.org-2018.txt"
```

If you have individual passwords you want to add, you can use the [[Add‐CompromisedPassword]] cmdlet

```powershell
Add-CompromisedPassword -Value p@ssw0rd
```

To test to see if a password is in the compromised password store, use the [[Test‐IsCompromisedPassword]] cmdlet. The cmdlet will return `true` if the password was found in the compromised store.
```powershell
Test-IsCompromisedPassword -Value p@ssw0rd
```

## Add banned words to the store
The password filter can also protect against common substitutions by normalizing incoming passwords, and checking them against the banned word store. For example, adding the word `lithnet` to the banned word store, will prevent common variations such as `lithnet2018` `l1thn3t` `Lithnet!` from being used. You can read more about the [[normalization rules]] to understand how this works in more detail. The banned word store contains the list of these words you want to prevent passwords being based on. You can load in common names in your organization, or load in the entire dictionary. The [[Import‐BannedWords]] cmdlet is used to import a file of new-line separated words.

```powershell
Import-BannedWords -Filename "D:\password-protection\english-dictionary-words.txt"
```

To add individual words use the [[Add‐BannedWord]] cmdlet

```powershell
Add-BannedWord -Value "lithnet"
```

Once you have completed creating your store, you need to decide how your servers are going to access the store. We recommend using DFS-R to replicate the store to each domain controller, so they each have an up-to-date local copy. Alternatively, you can manually copy it to each domain controller, or share it from a highly-available file server. 

Next: [[Configure the password group policy|Configure group policy]]