Download the latest version of the installer from the [releases](https://github.com/lithnet/ad-password-protection/releases) page.

In order to enable password filtering on your domain users, the application will need to be installed on all writable domain controllers in the domain. You can install the PowerShell module and group policy templates on any x64 machine.

You can install and test the module using _local_ accounts on any x64 Windows workstation or server. However, if you want to test against domain accounts, you will need to install the module on your domain controllers. 

## Installation options
The installer presents several options for you to choose from
* Lithnet Password Protection for Active Directory
  * Enable password filtering on this computer
  * PowerShell module
* Group policy templates (ADMX)

### Lithnet Password Protection for Active Directory
This is the component that contains the logic to test passwords against your policy. It is required to be installed to use any of the other functions

### Enable password filtering on this computer
When you select this option, the installer will register the password filter with the local security authority subsystem (LSASS) on the local computer. After a reboot, Windows will pass all password changes to the filter for validation. Note that you still need an appropriate [[group policy|configure group policy]] configured before the filter will be configured to reject any passwords.

When you select this option on a domain controller, this means that the password filter will process any password change or set operations for any user. 
> Note that as any writable domain controller in a domain can process a password change, the module must be installed on every domain controller. 

When you select this option a member server or workstation, enabling this option will mean that password changes for local accounts are checked by the filter for approval. Password changes for domain accounts are always processed by the domain controller, so this setting has no effect on domain account password changes.

### PowerShell module 
The PowerShell module allows you to build your store, add passwords and banned words and test passwords against the policy. 
For managing the password store, the PowerShell module can be install on any machine that has access to the store folder. 
For testing passwords, the PowerShell module should be installed on a machine that has the domain's group policy applied to it.
For existing checking domain account passwords against the store, we recommend installing this module on the domain controller and running the appropriate cmdlet from there.

### Group policy templates
The group policy templates should be installed on any machine that you need to configure the password settings group policy on. We recommend copying the ADMX files to a [central policy store](https://support.microsoft.com/en-au/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), which will enable you to see and manage the group policy settings from any machine in the domain.

## Choosing a store path
If you are going to use the breached password and banned word functionality, you'll need to create a [[password store|Understanding the store]]. The store is a file-based data structure containing the NTLM hashes of the breached passwords and banned words. 

We recommend creating a folder, and replicating it with DFS-R to all the machines that will be performing password filtering. This means all servers have the same copy of the password store, and by having a local copy, they are immune to network or connectivity problems. Otherwise, you can manually copy the store to all nodes, and just ensure that any updates you make are copied to each host as well. If you prefer, you can configure a network share to host the store. You'll just need to ensure that the machine accounts for all servers performing filtering have read access to the share.

See the guide on [[Creating a store]] for instructions on populating your store with breached passwords.

Next: [[Create a new store|Create a new store]]