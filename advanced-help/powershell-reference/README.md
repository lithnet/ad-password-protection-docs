# PowerShell reference

The PowerShell module contains the following cmdlets

| Cmdlet                                                                  | Description                                                                                                       |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [Add‐BannedWord](add-bannedword.md)                                     | Adds a new word to the banned word store                                                                          |
| [Add‐CompromisedPassword](add-compromisedpassword.md)                   | Adds a new password to the compromised password store                                                             |
| [Get‐PasswordFilterConfig](get-passwordfilterconfig.md)                 | Tests the result of the full password policy set against a specified password                                     |
| [Get‐PasswordFilterPolicy](get-passwordfilterpolicy.md)                 | Gets the current configuration of the password filter                                     |
| [Get‐PasswordFilterResult](get-passwordfilterresult.md)                 | Gets the effective policy applied by the password filter |
| [Import‐BannedWordHashes](import-bannedwordhashes.md)                   | Imports a file contained hashes of banned words                                                                   |
| [Import‐BannedWords](import-bannedwords.md)                             | Imports a file containing banned words                                                                            |
| [Import‐CompromisedPasswordHashes](import-compromisedpasswordhashes.md) | Imports a file containing hashes of compromised passwords                                                         |
| [Import‐CompromisedPasswords](import-compromisedpasswords.md)           | Imports a file containing compromised plain-text passwords                                                        |
| [Open‐Store](open-store.md)                                             | Opens a store                                                                                                     |
| [Remove‐BannedWord](remove-bannedword.md)                               | Removes a word from the banned word store                                                                         |
| [Remove‐CompromisedPassword](remove-compromisedpassword.md)             | Removes a password from the compromised password store                                                            |
| [Set-PasswordFilterConfig](set-passwordfilterconfig.md)                 | Sets configuration of the password filter |
| [Sync-HashesFromHibp](sync-hashesfromhibp.md)                           | Synchronizes compromised passwords hashes from the Have I Been Pwned API |
| [Test‐IsADUserPasswordCompromised](test-isaduserpasswordcompromised.md) | Extracts the hash of an AD user's password from the directory and tests it against the compromised password store |
| [Test‐IsBannedWord](test-isbannedword.md)                               | Tests to see if the specified string matches an item in banned word store                                         |
| [Test‐IsCompromisedPassword](test-iscompromisedpassword.md)             | Tests to see if the specified string is in the compromised password store                                         |
