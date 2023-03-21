## The group policy settings do not appear when I open the group policy editor

If you have installed the group policy templates on the computer, but they do not appear under `Computer Configuration\Policies\Administrative Templates\Lithnet\Password Filter` when you open the group policy editor, then your domain is likely using a [central policy store](https://support.microsoft.com/en-au/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra).

See the steps in [configuring the group policy](../installation/configure-group-policy.md) for instructions on how to copy the group policy template files to the central policy store.

## Password changes are not being rejected as expected

If the password change was not blocked as expected, run the [Get-PasswordFilterConfig](../advanced-help/powershell-reference/get-passwordfilterconfig.md) and [Get-PasswordFilterPolicy](../advanced-help/powershell-reference/get-passwordfilterpolicy.md) cmdlets on the server that processed the password change, and ensure the correct configuration and policy is applied.

## Passwords are being rejected, but no event log from LPP is present

If the password was rejected, but there was no event log entry from LithnetPasswordProtection explaining the reason for the password change, there are two likely reasons for this

1. It may be because another password filter, or Windows itself rejected the password.  If you use the built-in Windows password policy, those settings are always processed before LPP can review the password. In this case, LPP will never see the password to evaluate it.

2. The event log from LithnetPasswordProtection will only appear on the server that processed the password change. This could be any writable domain controller in the domain. Ensure that you check all domain controllers for the event log entry.