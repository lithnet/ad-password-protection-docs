# Change log

{% updates format="full" %}

{% update date="2026-06-25" tags="feature" %}
## v1.1.73

Minor servicing release with dependency updates and installer improvements

<mark style="color:green;"><i class="fa-sparkles">:sparkles:</i></mark> **Improved**
- Adds support services info to the installer
- Updates dependencies to the latest versions to ensure compatibility and security

### Downloads

- **Service** — [x64](https://packages.lithnet.io/win/password-protection/v1.1/x64/LithnetPasswordProtection-1.1.73.exe)

{% endupdate %}

{% update date="2026-03-01" tags="maintenance" %}
## v1.1.62

Fixes Test-IsAdPasswordCompromised on 2025 DCs and improves HIBP sync performance

### Service

<mark style="color:blue;"><i class="fa-wrench">:wrench:</i></mark> **Fixed**
- Fixes an issue with the Test-IsAdPasswordCompromised cmdlet when running on 2025 domain controllers with 32k page size enabled
- Improves performance of the Sync-HashesFromHibp cmdlet and allows increased hash counts

{% endupdate %}

{% update date="2024-12-13" tags="maintenance" %}
## v1.1.57

Fixes invalid access to memory location error when changing passwords via AD Users and Computers

### Service

<mark style="color:blue;"><i class="fa-wrench">:wrench:</i></mark> **Fixed**
- Fixes an issue where an "invalid access to memory location" error may occur when changing a password using the AD users and computers console

{% endupdate %}

{% update date="2024-11-19" tags="feature" %}
## v1.1.55

Adds HTTP proxy support for HIBP sync

### Service

<mark style="color:green;"><i class="fa-sparkles">:sparkles:</i></mark> **New**
- Adds support for specifying a HTTP proxy on the Sync-HashesFromHibp cmdlet with a new -ProxyAddress parameter

{% endupdate %}

{% update date="2023-05-07" tags="maintenance" %}
## v1.1.53

Fixes NullReferenceException when changing store path via PowerShell

### Service

<mark style="color:blue;"><i class="fa-wrench">:wrench:</i></mark> **Fixed**
- Fixes an issue where a NullReferenceException occurs using the PowerShell module to change the store path

{% endupdate %}

{% update date="2023-04-30" tags="maintenance" %}
## v1.1.51

Fixes unsigned PowerShell scripts in installer

### Service

<mark style="color:blue;"><i class="fa-wrench">:wrench:</i></mark> **Fixed**
- Fixes an issue where some of the PowerShell scripts in the installer were not signed

{% endupdate %}

{% update date="2023-03-18" tags="feature" %}
## v1.1.48

Fixes unsigned installer scripts and adds new PowerShell cmdlets for HIBP sync, config, and policy management

### Service

<mark style="color:green;"><i class="fa-sparkles">:sparkles:</i></mark> **New**
- Add several new cmdlets

<mark style="color:blue;"><i class="fa-wrench">:wrench:</i></mark> **Fixed**
- Fixes an issue where some of the PowerShell scripts in the installer were not signed

{% endupdate %}

{% endupdates %}