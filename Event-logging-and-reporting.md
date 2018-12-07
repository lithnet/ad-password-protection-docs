The password filter logs events to the `Application` log on the domain controllers using the event source `LithnetPasswordFilter`. Reporting is easily performing using a logging and analytics service such as Microsoft OMS or splunk. The following table lists the event log messages that are logged by the module, and their descriptions

| Code | Severity | Message | Notes |
| --- | --- | --- | --- |
| 1 | Error | An unexpected error occurred | The filter encountered an unexpected error and could not process the request |
| 2 | Warning | The Lithnet AD Password Filter is currently disabled and has not evaluated the password change request | This message appears when the filter is installed and registered with LSASS, but has been disabled and is not evaluating password changes |
| 4 | Success | Processing a password %1 request for %2 (%3). | Each password set/change attempt will cause this event to be logged |
| 5 | Success | The password %1 request for %2 (%3) was approved. | This event is logged when a password is appoved by the filter |
| 8 | Error | An unexpected error occurred | The filter encountered an unexpected win32 error and could not process the request | |
| 9 | Error | There was a problem opening the store file. Check that the store folder exists and is accessible | The store could not be accessed by the filter. Make sure that `SYSTEM` has permission to read the folder and files if the store is local, if its on a remote share, ensure that the machines computer account has read access to the share |
| 8193 | Warning | The password %1 request was rejected. The module is configured to deny password requests when an error occurs. |  | 
| 8194 | Warning | The password %1 request for %2 (%3) was rejected because its length (%4) did not meet the minimum configured length (%5). |
| 8195 | Warning | The password %1 request for %2 (%3) was rejected because it matched a password in the banned password store. | | 
| 8196 | Warning | The password %1 request for %2 (%3) was rejected after being normalized because it matched a password in the banned password store. | |
| 8197 | Warning | The password %1 request for %2 (%3) was rejected because it did not match the approval regular expression. | | 
| 8198 | Warning | The password %1 request for %2 (%3) was rejected because it matched the rejection regular expression. | |
| 8199 | Warning | The password %1 request for %2 (%3) was rejected because it achieved only %4 of the required %5 complexity points. | | 
| 8200 | Warning | The password %1 request for %2 (%3) was rejected because it did not meet the complexity requirements of a password below the specified threshold. | | 
| 8201 | Warning | The password %1 request for %2 (%3) was rejected because it did not meet the complexity requirements of a password above the specified threshold. | | 
| 8202 | Warning | The password %1 request for %2 (%3) was rejected because it contained the account name | |
| 8203 | Warning | The password %1 request for %2 (%3) was rejected because it contained at least part of the display name | |
| 8204 | Warning | The password %1 request for %2 (%3) was rejected because it did not meet the complexity requirements of a password of %4 characters. | | 
| 8205 | Warning | The password %1 request for %2 (%3) was rejected after being normalized because it matched a password in the banned word store. | |


