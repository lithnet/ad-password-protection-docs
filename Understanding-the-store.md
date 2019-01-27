Lithnet Password Protection can (optionally) test incoming passwords against a compromised password store, as well as a banned word store. The stores are a collection of files that represent a database containing the NTLM hashes. The stores are kept locally, and therefore the filter does not require any internet access to perform compromised password checking.

The stores are created and maintained using [[PowerShell|PowerShell reference]].

## Compromised password store
The compromised password store contains the NTLM hashes of exact passwords that you want to prevent your users from using. The most commmon usage of this store, is to populate it with hashes from the [haveibeenpwned.com](https://haveibeenpwned.com) compromised password lists (see the [[Import‐CompromisedPasswordHashes]] PowerShell cmdlet for more details). However, you can also add hashes from other sources such as the cracked password lists on [hashes.org](https://hashes.org), or even your own list of known bad passwords. 

You can add passwords to the store using the [[Add‐CompromisedPassword]], [[Import‐CompromisedPasswords]] and [[Import‐CompromisedPasswordHashes]] cmdlets.

## Banned word store
While the breach password store provides an effective way of making sure known compromised passwords are not used, it doesn't protect against bad passwords that have not yet been compromised. For example, a very common password is `WinterXXXX` where XXXX is the year the user set the password. While `Winter2018` may be in the compromised password store, `Winter2020` may not be, until it's detected in password breach. The banned word store allow you to specify words that a password should never be based on. It does this by applying [[normalization rules]] against the incoming password, and then looking for a match in the banned word store. By applying the normalization rules against `Winter2020`, it would be converted to `winter`, which would then be checked against the store.

Another common pattern that users employ when selecting passwords, is to base it on the company name. If you were to add `lithnet` to the banned word store, you could prevent the usage of passwords based on that such as `L!thnet`, `Lithnet123`, etc. 

You can add passwords to the store using the [[Add‐BannedWord]], [[Import‐BannedWords]] and [[Import‐BannedWordHashes]] cmdlets.