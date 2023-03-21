# Setup requirements
In order to protect the passwords of users in a domain, Lithnet Password Protection must be installed on all writable domain controllers in a domain. This is because a user's password change request may be processed by any domain controller in their domain. 

You can install Lithnet Password Protection on any x64 Windows workstation or server operating system, where the password filter will work against local accounts on that computer. This can be useful for testing and performing proof-of-concepts, without requiring an entire test domain. The feature set is exactly the same between password filtering on local accounts and domain accounts.

## Prerequisites
Lithnet Password Protection is only supported on x64 editions of Windows. The installer will present three components that can be installed together or independently.

### Password Filter
This is the component that actually performs the password filtering. It has the following requirements.
* Windows Server 2012 R2 or higher
* [Microsoft Visual C++ Redistributable package 2015-2022](https://aka.ms/vs/17/release/vc_redist.x64.exe)

### PowerShell module
The PowerShell module is used for managing the store, and can be used to configure parts of the filter and test it.
* .NET Framework 4.7.2
* Windows PowerShell 5
* [Microsoft Visual C++ Redistributable package 2015-2022](https://aka.ms/vs/17/release/vc_redist.x64.exe)

### Group policy templates
The group policy templates should be installed on any machine that you need to configure the password settings group policy on. We recommend copying the ADMX files to a [central policy store](https://support.microsoft.com/en-au/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), which will enable you to see and manage the group policy settings from any machine in the domain.

