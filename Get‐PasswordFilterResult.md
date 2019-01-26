## Description
The ```Get-PasswordFilterResult``` cmdlet allows you to programatically test passwords against your password policy. 

This cmdlet does not attempt to change the user's password, nor does it contact the domain controller. Use of this cmdlet requires that the [[group policy|configure group policy]] for the password filter is configured and applied to the computer you are running the cmdlet on. The password filter does not need to be configured to filter passwords on the local computer, but the policy needs to be in place. 

## Syntax
```
Get-PasswordFilterResult -Password <string> -Username <string> -Fullname <string> -IsSetOperation <bool>
```
## Parameters
##### `Password`
Required. The password to test
##### `Username`
Required. The username of the user who would be changing their password
##### `Fullname`
Required. The full name of the user who would be changing their password
##### `IsSetOperation`
Optional. A boolean value indicating whether this should simulate a password set operation. The default value is false if not specified, which indicates that a password change operation should be simulated.

## Return value
The cmdlet will return one of the following values

| String value | Numeric value | Description |
| --- | --- | --- |
| Approved | 0 | The password was approved by the filter |
| LengthRequirementsNotMet | 1 | The password did not meet the minimum length requirements |
| ComplexityThresholdNotMet | 2 | The password did not meet the complexity requirements for a password of the given length |
| ComplexityPointsNotMet | 3 | The password did not meet the minimum number of complexity points |
| DidNotMatchApprovalRegex | 4 | The password did not match the regular expression required for approval |
| MatchedRejectRegex | 5 | The password did matched the rejection regular expression |
| ContainsAccountName | 6 | The password contained the user's account name |
| ContainsFullName | 7 | The password contained all or part of the user's full name |
| Banned | 8 | The password was found in the breached password store |
| BannedNormalizedPassword | 9 | The password was found in the breached password store after the [[normalization rules]] were applied |
| BannedNormalizedWord | 10 | The password was found in the banned word store after the [[normalization rules]] were applied |
| PasswordWasBlank | 11 | The password was an empty string |
| FilterError | 100 | An exception occurred in the filter engine and the password could not be processed |

## Examples
```powershell
PS> Get-PasswordFilterResult -Password "password" -Username "test-user" -Fullname "John Test"
Banned


PS> Get-PasswordFilterResult -Password "John" -Username "test-user" -Fullname "John Test"
ContainsFullName
```