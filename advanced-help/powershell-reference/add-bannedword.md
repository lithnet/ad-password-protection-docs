# Add-BannedWord

The `Add-BannedWord` cmdlet takes a string of text, applies the [normalization rules](../../help-and-support/normalization-rules.md) to it, and adds it to the banned word store.

## Syntax

```
Add-BannedWord -Value <string>

Add-BannedWord -SecureString <SecureString>
```

### Parameters

**`Value`**

Required. The string of text to add to the store. [Normalization rules](../../help-and-support/normalization-rules.md) will be applied to the string before it is committed to the store

**`SecureString`**

Required. The string of text to add to the store as a secure string object.[ Normalization rules](../../help-and-support/normalization-rules.md) will be applied to the string before it is committed to the store

### Examples

The following example adds a single banned word to the store

```powershell
Add-BannedWord -Value "password"
```

The following example prompts for a word to be added to the store

```powershell
Add-BannedWord -SecureString (Read-Host -Prompt "Enter the banned word to add to the store" -AsSecureString)
```

To import a file of banned words, use the[ Import-BannedWords](import-bannedwords.md) or [Import‐BannedWordHashes](import-bannedwordhashes.md)
