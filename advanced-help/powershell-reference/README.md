# Powershell reference

The PowerShell module contains the following cmdlets

| Cmdlet                                                                  | Description                                                                                                       |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [Add‐BannedWord](Add-BannedWord.md)                                     | Adds a new word to the banned word store                                                                          |
| [Add‐CompromisedPassword](Add-CompromisedPassword.md)                   | Adds a new password to the compromised password store                                                             |
| [Get‐PasswordFilterConfig](Get-PasswordFilterConfig.md)                 | Tests the result of the full password policy set against a specified password                                     |
| [Get‐PasswordFilterPolicy](Get-PasswordFilterPolicy.md)                 | Gets the current configuration of the password filter                                     |
| [Get‐PasswordFilterResult](Get-PasswordFilterResult.md)                 | Gets the effective policy applied by the password filter |
| [Import‐BannedWordHashes](Import-BannedWordHashes.md)                   | Imports a file contained hashes of banned words                                                                   |
| [Import‐BannedWords](Import-BannedWords.md)                             | Imports a file containing banned words                                                                            |
| [Import‐CompromisedPasswordHashes](Import-CompromisedPasswordHashes.md) | Imports a file containing hashes of compromised passwords                                                         |
| [Import‐CompromisedPasswords](Import-CompromisedPasswords.md)           | Imports a file containing compromised plain-text passwords                                                        |
| [Open‐Store](Open-Store.md)                                             | Opens a store                                                                                                     |
| [Remove‐BannedWord](Remove-BannedWord.md)                               | Removes a word from the banned word store                                                                         |
| [Remove‐CompromisedPassword](Remove-CompromisedPassword.md)             | Removes a password from the compromised password store                                                            |
| [Set-PasswordFilterConfig](Set-PasswordFilterConfig.md) |  Sets configuration of the password filter |
| [Sync-HashesFromHibp](Sync-HashesFromHibp.md) | Synchronizes compromised passwords hashes from the Have I Been Pwned API |
| [Test‐IsADUserPasswordCompromised](Test-IsADUserPasswordCompromised.md) | Extracts the hash of an AD user's password from the directory and tests it against the compromised password store |
| [Test‐IsBannedWord](Test-IsBannedWord.md)                               | Tests to see if the specified string matches an item in banned word store                                         |
| [Test‐IsCompromisedPassword](Test-IsCompromisedPassword.md)             | Tests to see if the specified string is in the compromised password store                                         |
