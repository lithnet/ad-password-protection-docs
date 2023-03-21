# Populate the store

Now that we have [created a store](create-a-new-store.md), we can populate it with compromised passwords and banned words.

Import the PowerShell module and open the store folder

```powershell
Import-Module LithnetPasswordProtection
Open-Store -Path "D:\password-protection\store"
```

## Add compromised passwords to the store

We recommend you synchronize your password store with the [Have I Been Pwned API](https://haveibeenpwned.com/API/v3) using the [Sync-HashesFromHibp](../advanced-help/powershell-reference/sync-hashesfromhibp.md) cmdlet. 

```powershell
Sync-HashesFromHibp
```

{% hint style="info" %}
If you are replicating the store with DFS-R, pause replication before you start populating the store. Wait until you have completed the import process before resuming replication.
{% endhint %}

If you don't have internet access from the server where the LPP store is being created, you can use the [HIBP downloader](https://github.com/HaveIBeenPwned/PwnedPasswordsDownloader) to download the dataset.

{% hint style="info" %}
When using the HIBP downloader tool, make sure you download the NTLM hashes, not the SHA1 hashes, and download them into a single file

```
haveibeenpwned-downloader.exe -n pwnedpasswords_ntlm
```
{% endhint %}

If you have other NTLM hash sets you want to import, you can do so. Just make sure they are in a text file, each separated by a new line. Use the [Import-CompromisedPasswordHashes ](../advanced-help/powershell-reference/import-compromisedpasswordhashes.md) cmdlet to import them.

You can also choose to import any plain-text password lists that you have access to. These are imported using the [Import-CompromisedPasswords](../advanced-help/powershell-reference/import-compromisedpasswords.md) cmdlet.

```powershell
Import-CompromisedPasswords -Filename "D:\password-protection\hashes.org-2018.txt"
```

If you have individual passwords you want to add, you can use the [Add-CompromisedPassword](../advanced-help/powershell-reference/add-compromisedpassword.md) cmdlet

```powershell
Add-CompromisedPassword -Value p@ssw0rd
```

To test to see if a password is in the compromised password store, use the [Test‐IsCompromisedPassword](../advanced-help/powershell-reference/test-iscompromisedpassword.md) cmdlet. The cmdlet will return `true` if the password was found in the compromised store.

```powershell
Test-IsCompromisedPassword -Value p@ssw0rd
```

### Add banned words to the store

The password filter can also protect against common substitutions by normalizing incoming passwords, and checking them against the banned word store. For example, adding the word `lithnet` to the banned word store, will prevent common variations such as `lithnet2018` `l1thn3t` `Lithnet!` from being used. You can read more about the [normalization rules](../advanced-help/normalization-rules.md) to understand how this works in more detail. The banned word store contains the list of these words you want to prevent passwords being based on. You can load in common names in your organization, or load in the entire dictionary. The [Import‐BannedWords](../advanced-help/powershell-reference/import-bannedwords.md) cmdlet is used to import a file of new-line separated words.

```powershell
Import-BannedWords -Filename "D:\password-protection\english-dictionary-words.txt"
```

To add individual words use the [Add‐BannedWord](../advanced-help/powershell-reference/add-bannedword.md) cmdlet

```powershell
Add-BannedWord -Value "lithnet"
```
