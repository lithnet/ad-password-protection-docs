# Installation

Download the latest version of the installer from the [downloads](downloads.md) page.

## Installation options

The installer presents several options for you to choose from

* Enable password filtering on this computer
* PowerShell module
* Group policy templates (ADMX)

### Enable password filtering on this computer

When you select this option, the installer will register the password filter with the local security authority subsystem (LSASS) on the local computer. After a reboot, Windows will pass all password changes to the filter for validation. Note that you still need an appropriate [group policy](configure-group-policy.md) configured before the filter will be configured to reject any passwords.

When you select this option on a domain controller, this means that the password filter will process any password change or set operations for any user.

{% hint style="info" %}
Note that as any writable domain controller in a domain can process a password change, the module must be installed on every domain controller.
{% endhint %}

When you select this option a member server or workstation, enabling this option will mean that password changes for local accounts are checked by the filter for approval. Password changes for domain accounts are always processed by the domain controller, so this setting has no effect for domain account password changes performed on member servers and workstations.

### PowerShell module

The PowerShell module allows you to build your store, add passwords and banned words and test passwords against the policy. For managing the password store, the PowerShell module can be installed on any machine that has access to the store folder. For testing passwords, the PowerShell module should be installed on a machine that has the domain's group policy applied to it. In order to audit existing user's passwords against the compromised password store, we recommend installing this module on the domain controller and running the appropriate cmdlet from there.

### Group policy templates

The group policy templates should be installed on any machine that you need to configure the password settings group policy on. We recommend copying the ADMX files to a [central policy store](https://support.microsoft.com/en-au/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), which will enable you to see and manage the group policy settings from any machine in the domain.

### Choosing a store path

If you are going to use the compromised password and banned word functionality, you'll need to create a password store. The store is a file-based data structure containing the NTLM hashes of the compromised passwords and banned words.

See the guide on [Creating a store](create-a-new-store.md) for instructions on how to setup and configure your store.