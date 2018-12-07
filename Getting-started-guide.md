In order to get up and running with the Lithnet Password Filter, you'll need to complete the following steps

* [[Install the module|installing the module]]
You'll need to download and install the application on your writable domain controllers to enable password filtering. You can also install the application on other servers to allow you to use the PowerShell cmdlets and manage the password settings via group policy.

* [[Create a new store|Create a new store]]
If you plan on using the breached password functionality, then once the module is installed you'll need to create the database that contains the breached passwords. You can use PowerShell to import breached passwords from data sets such as the haveibeenpwned.com pwned password list.

* [[Configure the password group policy|Configure group policy]]
In order for the password filter to become active, you need to configure it via a group policy that applies to your domain controllers. 

* [[Test the filter]]
Once filter has been installed and configured, you can start testing the password filter.

* [[Audit existing passwords]]
As an optional step, you can test the passwords of all existing users in your domain, to see if any of them are in the breached password store. As these passwords have already been converted to a one-way hash in the Active Directory database, you cannot test other policies such as length and complexity against them.

* [[Event logging and reporting]]
Understand the events logged by the password filter, so you can audit and report on password change results.