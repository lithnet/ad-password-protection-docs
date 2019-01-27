Once you have the application up and running, it can be useful to audit user's current passwords stored in the Active Directory, to see if any of them are in the compromised password store. 

This process involves using a PowerShell cmdlet to extract the users password hashes from the Active Directory, and checking to see if a match is found in the compromised password store. This procedure can only check for compromised passwords, and cannot perform length and complexity validation, as those processes rely on having access to the user's plain-text password, which is not stored in Active Directory.

In order to perform this operation, you need to have the `Replicate Directory Changes All` permission on the domain object, or be a member of the `Domain Admins` group, which has this permission by default. 

**This is a security-sensitive operation, and should only be performed from a trusted device, such as the domain controllers themselves**

You'll need the PowerShell module installed, and utilize the [[Test‐IsADUserPasswordCompromised]] cmdlet.

The following script will create a CSV file of each user with a compromised password

```powershell
Import-Module LithnetPasswordProtection

$file = "get-pwned-users.csv";

"accountName,UPN,pwdLastSet,lastLogin,accountDisabled" | out-file $file

$Searcher = New-Object System.DirectoryServices.DirectorySearcher
$Searcher.PageSize = 200
$Searcher.SearchScope = "subtree"

$Searcher.Filter = "(&(objectCategory=person)(objectClass=user))"
$Attributes = @("PwdLastSet","lastLogonTimeStamp", "userAccountControl", "userPrincipalName", "name")
ForEach($Attribute In $Attributes)
{
    $Searcher.PropertiesToLoad.Add($Attribute) > $Null
}

$Results = $null
$Total = 0
$NumChanged = 0

$Searcher.FindAll() | % {
    $user = $_.Properties["UserPrincipalName"][0]

    if ($user -eq $null)
    {
        write-warning "User $($_.Properties["Name"][0]) has a null UPN";
        return;
    }

    $result = Test-IsADUserPasswordCompromised -UPN $user -server localhost 
    
    $pwdLastSet = $null
    $lastLogin = $null
    $disabled = $false;

    if ($_.Properties["PwdLastSet"][0] -gt 0)
    {
        $pwdLastSet = [DateTime]::FromFileTimeUtc($_.Properties["pwdLastSet"][0]).ToLocalTime()
    }

    if ($_.Properties["lastLogonTimeStamp"][0] -gt 0)
    {
        $lastLogin = [DateTime]::FromFileTimeUtc($_.Properties["lastLogonTimeStamp"][0]).ToLocalTime()
    }

    if (($_.Properties["userAccountControl"][0] -band 2) -eq 2)
    {
        $disabled = $true;
    }

    if ($result -ne $true)
    {  
        return;
    }

    $message = "$($_.Properties["Name"][0]),$user,$pwdLastSet,$lastLogin,$disabled"
    Write-Output $message
    $message | out-file $file -Append
} 
```

Using the results of the script, you could contact the users and ask them to change their password, or force a password change at next logon.

Next: [[Event logging and reporting]]