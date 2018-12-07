The password filter logs events to the `Application` log on the domain controllers using the event source `LithnetPasswordFilter`. Reporting is easily performing using a logging and analytics service such as Microsoft OMS or splunk. The following table lists the event log messages that are logged by the module, and their descriptions

| Code | Severity | Message | Notes |
| --- | --- | --- | --- |
| 1 | Error | An unexpected error occurred | The filter encountered an unexpected error and could not process the request |
| 2 | Warning | The Lithnet AD Password Filter is currently disabled and has not evaluated the password change request | |
| 4 | Success | Processing a password %1 request for %2 (%3). | |
| 5 | Success | The password %1 request for %2 (%3) was approved. | |
| 8 | Error | An unexpected error occurred | The filter encountered an unexpected win32 error and could not process the request | |
| 9 | Error | There was a problem opening the store file. Check that the store folder exists and is accessible | |
| 8193 | Warning | The password %1 request was rejected. The module is configured to deny password requests when an error occurs. | | 
| 8194 | Warning | The password %1 request for %2 (%3) was rejected because its length (%4) did not meet the minimum configured length (%5). |
| 8195 | | | | 

