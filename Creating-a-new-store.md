The store contains the list of breached passwords and banned words you want to prevent from being used in your environment. You need to use the PowerShell module to build your store. 

# Creating a new store
First, create a new empty folder for the store
```powershell
mkdir D:\password-filter\store
```

Next, import the PowerShell module and open the store folder
```powershell
Import-Module PasswordFilterPS
Open-Store -Path "D:\password-filter\store"
```
# Add breached passwords to the store
The PowerShell module is now ready to use the new store folder. First, import your breached passwords. We recommend starting with the [Have I Been Pwned](https://haveibeenpwned.com/Passwords) NTLM password list. Download the version that says `(ordered by hash)` for the best performance. Once you have the download, import them into your new store.

```powershell
Import-BreachedPasswordHashes -Filename "D:\password-filter\pwned-passwords-ntlm-ordered-by-hash.txt"
```

If you have other NTLM hash sets you want to import, you can do so. Just make sure they are in a text file, each separated by a new line.

You can also choose to import any plain-text password lists that you have access to. Hashes.org has a large list of [cracked plain-text passwords](https://hashes.org/left.php) that you can download and import.

```powershell
Import-BreachedPasswords -Filename "D:\password-filter\hashes.org-2018.txt"
```

If you have individual passwords you want to add, you can use the [[Add‐BreachedPassword]] cmdlet

```powershell
Add-BreachedPassword -Password p@ssw0rd
```

To test to see if a password is in the breached password store, use the [[Test‐BreachedPassword]] cmdlet. The cmdlet will return `true` if the password was found in the breached store.
```
Test-BreachedPassword -Password p@ssw0rd
```

# Add banned words to the store
The password filter can also protect against common substitutions by normalizing incoming passwords, and checking them against the banned word store. For example, adding the word `lithnet` to the banned word store, will prevent common variations such as `lithnet2018` `l1thn3t` `Lithnet!` from being used. You can read more about the [[normalization rules]] to understand how this works in more detail. The banned word store contains the list of these words you want to prevent passwords being based on. You can load in common names in your organization, or load in the entire dictionary. The [[Import-BannedWords]] cmdlet is used to import a file of new-line separated words.

```powershell
Import-BannedWords -Filename "D:\password-filter\english-dictionary-words.txt"
```

To add individual words use the [[Add‐BannedWord]] cmdlet

```powershell
Add-BannedWord -Value "lithnet"
```

Once you have completed creating your store, you need to decide how your servers are going to access the store. We recommend using DFS-R to replicate the store to each domain controller, so they each have am up-to-date local copy. Alternatively, you can manually copy it to each domain controller, or share it from a highly-available file server. See the guide on [[distributing the store]] for more information.

