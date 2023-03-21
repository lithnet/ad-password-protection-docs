# Getting started with Lithnet Password Protection

 In this guide, we will look at how to set up Lithnet Password Protection for Active Directory (LPP) from scratch. We'll configure a basic password policy, and integrate the haveibeenpwned.com pwned password data set to prevent users from changing their password to one that is known to be compromised.

* [Setup requirements](setup-requirements.md) - First, read the pre-requistes and requirements for installation, and learn about the options for setting up a test environment or a production environment.
* [Install the module](installing-the-module.md) - You'll need to download and install the application on your writable domain controllers to enable password filtering. You can also install the application on other servers to allow you to use the PowerShell cmdlets and manage the password settings via group policy.
* [Create a new store](create-a-new-store.md) - If you plan on using the compromised password functionality, then once the module is installed you'll need to create the database that contains the compromised passwords. Each domain controller will need access to this store, so this guide will assist you in determining the best way to achieve this.
* [Populate the store](populate-the-store.md) - Use the PowerShell to import compromised passwords from data sets such as the haveibeenpwned.com pwned password list.
* [Configure the group policy](configure-group-policy.md) - Configure the group policy to enable the password filter and customize your password policy settings
* [Test the password filter](../help-and-support/testing-the-password-filter.md) - Once filter has been installed and configured, you can start testing the password filter.
* [Audit existing passwords](audit-existing-passwords.md) - As an optional step, you can test the passwords of all existing users in your domain, to see if any of them are in the compromised password store. As these passwords have already been converted to a one-way hash in the Active Directory database, you cannot test other policies such as length and complexity against them.

## Troubleshooting
* [Read the troubleshooting guide](../help-and-support/troubleshooting.md) for information on how to troubleshoot configuration errors. If you are still having trouble you can reach out to the community for [support via our GitHub issue tracker](../help-and-support/getting-support.md)