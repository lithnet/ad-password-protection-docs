# Description
The ```Open-Store``` cmdlet connects the PowerShell module to a new or existing password store. The use of the ```Open-Store``` cmdlet is required when connecting to a store that is not the default store for the current machine. If the Open-Store cmdlet is not run, other cmdlets will try to connect to the machines default store, and throw an error if the default store does not exist.

## Syntax
```
Open-Store -Path <path>
```
### Parameters
##### `Path`
Required. The full path to the store you want to open. 

### Examples
```powershell
Import-Module LithnetPasswordProtection
# Open the non-default store
Open-Store -Path "D:\password-protection\test-store"
```