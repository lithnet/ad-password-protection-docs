# Change log
## v1.1.53 8th May 2023
### Password Protection service
- \[FIX\] Fixes an issue where a NullReferenceException occurs using the PowerShell module to change the store path

## v1.1.51 30th April 2023
### Password Protection service
- \[FIX\] Fixes an issue where some of the PowerShell scripts in the installer were not signed

## v1.1.48 19th March 2023
### Password Protection service
- \[FIX\] Fixes an issue where some of the PowerShell scripts in the installer were not signed
- \[FEATURE\] Add several new cmdlets
  - Sync-HashesFromHibp - Allows you to sync hashes from the Have I Been Pwned API directly into your compromised password store. This replaces the previous flat-file import process.
  - Get-PasswordFilterConfig - Allows you to get the registration and enabled/disabled status of the password filter, as well as the password store location
  - Get-PasswordFilterPolicy - Allows you to see the filter policy settings currently in place
  - Set-PasswordFilterConfig - Allows you to set the store location and enabled/disabled status of the filter
