# Creating a store

The LPP *store* is essentially a flat-file database of password hashes and configuration, efficiently stored in a binary format to maximize speed, while conserving space. 

Each domain controller must have read access to this store in order to compare incoming password changes against the compromised password lists. 

## Choosing a store distribution strategy
You'll need to decide how you will keep the password store in sync between domain controllers. There are several ways to achieve this. Each has its own pros and cons, and you'll need to decide what is best for your environment.

### Option 1: Each server has its own copy of the store, automatically replicated with DFS-R
This is the configuration we recommend. 

Each server that has LPP installed, has its own local copy of the store, and [DFS-R is used](https://learn.microsoft.com/en-us/windows-server/storage/dfs-replication/dfsr-overview) to replicate and keep changes in sync. This means the store will always be available, and there will be no bandwidth or latency issues with accessing it. 

New passwords can be added to any server in the replication group, and DFS-R will replicate those changes to the other servers. 

{% hint style="warning" %}
Do NOT place the store in the SYSVOL folder. Create a dedicated replication group for the LPP store.
{% endhint %}

{% hint style="info" %}
You can create a DFS replication group, without having to create a share in a DFS namespace. DFS Replication and DFS Namespaces can be used separately or together.
{% endhint %}

### Option 2: Each server has its own copy of the store, updates are performed manually
In this configuration, each server with LPP installed has a local copy of the store. This means the store will always be available, and there will be no bandwidth or latency issues. The downside is that if you want to update the store with new passwords, you need to update it on each server manually. Updates to the store will be infrequent, so this may not be an issue. As the store is flat-file based, it is easy to copy with tools such as robocopy and xcopy.

{% hint style="info" %}
Make sure the local `SYSTEM` account has read access to the store
{% endhint %}

### Option 3: Each server accesses a single copy of the store via a file share
In this configuration, each server with LPP installed points to a network share that contains the single copy of the store. The benefits are that there is only one copy of the store to be managed, but the downside is that if the file server goes down, the password filter will be unable to perform compromised password checking. This might also be an issue for distributed environments, where bandwidth and latency between domain controllers and the file server is an issue. Remember, the agent must be installed on every writable domain controller in your environment, so they will all need read access to this store. 

{% hint style="info" %}
Assign read access to the `Domain Controllers` group, on both the share and the underlying file system, so that all DCs are able to read the store
{% endhint %}

### Strategy Summary 
| Strategy | Update synchronization | Availability | Latency |
| --- | --- | --- |--- | 
| 1. DFS-R | Automatic using DFS-R | Always available | Low | 
| 2. Each server has own copy | Manual | Always available | Low |
| 3. Network share | Not required | Depends on file server availability | Depends on file server round-trip-time | 

## Create the store folder

All that is needed to prepare the store location is to create an empty folder, and sure the appropriate permissions have been assigned.

For a local store, ensure that the `SYSTEM` account has read access to the folder
For a store on a network share, ensure that the `Domain Controllers` group has both read access to the share, and underlying file system.

You can create a new empty store using PowerShell 
```powershell
mkdir D:\password-protection\store
```

If you've already installed LPP, and want to reconfigure the store location, you can run the following command from an elevated PowerShell window

```powershell
Import-Module LithnetPasswordProtection
Set-PasswordFilterConfig -StorePath "D:\password-protection\store"
```
