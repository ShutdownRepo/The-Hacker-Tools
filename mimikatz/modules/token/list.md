# list

`token::list` lists all tokens on the system.

It has the following command line arguments:

* `/id`: The token to list by its ID
* `/user`: The user token to list
* `/system`: List only system tokens
* `/admin`: List a token of builtin local administrators
* `/domainadmin`: List tokens with Domain Admin privileges
* `/enterpriseadmin`: List tokens with Enterprise Admin privileges
* `/localservice`: List local service accounts tokens
* `/networkservice`: List network service accounts tokens

A low-privileged user can list only own tokens:

```
mimikatz # token::list
Token Id  : 0
User name :
SID name  :

3844    {0;0008d895} 2 L 588473         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)        Primary
964     {0;0008d895} 2 L 651175         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)        Primary
760     {0;0008d895} 2 L 659720         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)        Primary
1456    {0;0008d895} 2 L 664286         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)        Primary
5200    {0;0008d895} 2 L 676578         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)        Primary
6164    {0;0008d895} 2 L 5603039        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,01p)        Impersonation (Impersonation)
```

Every line shows one token:

```
6164    {0;0008d895} 2 L 5603039        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,01p)        Impersonation (Impersonation)
```

Displayed information (source: [kuhl_m_token.c](https://github.com/gentilkiwi/mimikatz/blob/master/mimikatz/modules/kuhl_m_token.c#L181)):

- `6164`: Process ID
  - To which process the token belongs.
  - Every process has one primary token and can have multiple impersonation tokens.
  - This ID can be seen in Taskmanager, or Get-Process
- `{0;0008d895}`: Logon Session ID (64 bit)
  - higher 32 bit and lower 32 bit
- `2`: Session ID
- `L`: Token Elevation Type
  - `D`: Default
  - `F`: Full
  - `L`: Limited
- `5603039`: Token ID
- `SERVER01\tmassie`: Username
  - Domain Accounts: `domain\username`
  - Local Accounts: `hostname\username` or `NT AUTHORITY\USERNAME`
- `S-1-5-21-755659916-1915924768-2761631771-1001`: SID
- `(15g,01p)`: Groups and privileges
  - `g`: Number of groups
  - `p`: Number of privileges
- `Impersonation`: Token Type
  - Unknown
  - Primary
  - Impersonation
- `(Impersonation)`: Impersonation Level (Only for impersonation tokens)
  - `Anonymous`: Server cannot impersonate the client
  - `Identification`: Server can identify client but not impersonate
  - `Impersonation`: Server can impersonate client’s security context on local system
  - `Delegation`: Server can impersonate client’s security context on remote systems using cached credentials

As a local admin but without the `SeDebugPrivilege` privilege, you can see the tokens of other user's as well but not of system users like `SYSTEM` or `NETWORK SERVICE`:

```
mimikatz # token::list
Token Id  : 0
User name :
SID name  :

3844    {0;0008d895} 2 L 588473         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
4376    {0;0008d895} 2 L 601368         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
964     {0;0008d895} 2 L 651175         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
760     {0;0008d895} 2 L 659720         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
3768    {0;0008d7f5} 2 F 661766         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
1456    {0;0008d895} 2 L 664286         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
5200    {0;0008d895} 2 L 676578         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
7156    {0;000f0ac5} 3 F 1075487        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
5508    {0;0008d7f5} 2 F 5127728        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
7224    {0;0008d7f5} 2 F 5870190        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
6164    {0;0008d895} 2 L 5603039        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,01p)       Impersonation (Impersonation)
```

With the `SeDebugPrivilege` privilege enabled, you can see all tokens on the system:

```
mimikatz # privilege::debug
Privilege '20' OK

mimikatz # token::list
Token Id  : 0
User name :
SID name  :

[...]
1916    {0;000003e7} 2 D 556559         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
3844    {0;0008d895} 2 L 588473         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
3428    {0;000003e7} 0 D 593863         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,05p)       Primary
4376    {0;0008d895} 2 L 601368         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
964     {0;0008d895} 2 L 651175         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
3992    {0;000003e7} 0 D 655073         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,11p)       Primary
760     {0;0008d895} 2 L 659720         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
3768    {0;0008d7f5} 2 F 661766         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
1456    {0;0008d895} 2 L 664286         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
5200    {0;0008d895} 2 L 676578         SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,02p)       Primary
5268    {0;000003e7} 3 D 973825         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
7156    {0;000f0ac5} 3 F 1075487        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Primary
4428    {0;000003e7} 0 D 2267524        NT AUTHORITY\SYSTEM     S-1-5-18        (04g,28p)       Primary
5508    {0;0008d7f5} 2 F 5127728        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
7224    {0;0008d7f5} 2 F 5870190        SERVER01\tmassie    S-1-5-21-755659916-1915924768-2761631771-1001   (15g,24p)       Primary
676     {0;000003e7} 0 D 28607          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Impersonation (Impersonation)
676     {0;000003e4} 0 D 555174         NT AUTHORITY\NETWORK SERVICE    S-1-5-20        (11g,06p)       Impersonation (Impersonation)
676     {0;003e1c50} 0 D 4070487        winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (12g,24p)       Impersonation (Impersonation)
676     {0;0000756e} 0 D 30076          Font Driver Host\UMFD-0 S-1-5-96-0-0    (09g,02p)       Impersonation (Impersonation)
676     {0;000003e7} 0 D 46009          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Impersonation (Impersonation)
[...]
2096    {0;000003e5} 0 D 75329          NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (16g,03p)       Primary
2812    {0;000003e6} 0 D 109047         NT AUTHORITY\ANONYMOUS LOGON    S-1-5-7 (01g,00p)       Impersonation (Impersonation)
2956    {0;000003e7} 0 D 326793         NT AUTHORITY\SYSTEM     S-1-5-18        (12g,07p)       Impersonation (Impersonation)
1916    {0;000003e7} 2 D 559210         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,10p)       Primary
5268    {0;000003e7} 3 D 976221         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,10p)       Primary
```

List token of specific user:

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
920     {0;000563e4} 2 L 443911         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
920     {0;000563e4} 2 L 432114         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,02p)       Impersonation (Impersonation)
920     {0;000563b2} 2 F 460527         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,24p)       Impersonation (Impersonation)
1816    {0;000563e4} 2 L 424793         winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (15g,01p)       Impersonation (Impersonation)
```

List token with specific token id:

```
mimikatz # token::list /id:27044241
Token Id  : 27044241
User name :
SID name  :

9196    {0;019c935c} 2 F 27044241       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Primary
```

List tokens of local admins:

```
mimikatz # token::list /admin
Token Id  : 0
User name :
SID name  : BUILTIN\Administrators

660     {0;000003e7} 1 D 22777          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
676     {0;000003e7} 0 D 23261          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
1356    {0;000003e7} 0 D 69077          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,07p)       Primary
1392    {0;000003e7} 0 D 69588          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,07p)       Primary
1428    {0;000003e7} 0 D 69888          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,04p)       Primary
[...]
```

List tokens of domain admins:
```
mimikatz # token::list /domainadmin
Token Id  : 0
User name :
SID name  : winattacklab\Domain Admins

6260    {0;019c935c} 2 F 30080881       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Primary
676     {0;019c935c} 2 F 27038624       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Impersonation (Impersonation)
9196    {0;019c935c} 2 F 27044241       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Primary
```

List tokens of enterprise admins:

```
mimikatz # token::list /enterpriseadmin
Token Id  : 0
User name :
SID name  : winattacklab\Domain Admins

6260    {0;019c935c} 2 F 30080881       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Primary
676     {0;019c935c} 2 F 27038624       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Impersonation (Impersonation)
9196    {0;019c935c} 2 F 27044241       winattacklab\ffast     S-1-5-21-1345929560-157546789-2569868433-1123   (14g,24p)       Primary
```

List tokens of local service accounts:

```
mimikatz # token::list /localservice
Token Id  : 0
User name :
SID name  : NT AUTHORITY\LOCAL SERVICE

676     {0;000003e5} 0 D 540433         NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (17g,02p)       Impersonation (Impersonation)
676     {0;000003e5} 0 D 61742          NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (17g,11p)       Impersonation (Impersonation)
[...]
3816    {0;000003e5} 0 D 20547077       NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (17g,03p)       Primary
```

List tokens of local `SYSTEM` account:

```
mimikatz # token::list /system
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

660     {0;000003e7} 1 D 22777          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
676     {0;000003e7} 0 D 23261          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
[...]
2236    {0;000003e7} 0 D 118305         NT AUTHORITY\SYSTEM     S-1-5-18        (12g,04p)       Impersonation (Identification)
3272    {0;000003e7} 0 D 31384213       NT AUTHORITY\SYSTEM     S-1-5-18        (12g,07p)       Impersonation (Impersonation)
5568    {0;000003e7} 2 D 594642         NT AUTHORITY\SYSTEM     S-1-5-18        (04g,10p)       Primary
```
