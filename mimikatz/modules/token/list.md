# list

It lists all tokens on the system. It has the following command line arguments:

* `/user`: The user token to list
* `/system`: List only system tokens
* `/admin`: List a token of builtin local administrators
* `/domainadmin`: List tokens with Domain Admin privileges
* `/enterpriseadmin`: List tokens with Enterprise Admin privileges
* `/localservice`: List local service accounts tokens
* `/networkservice`: List network service accounts tokens

```text
mimikatz # token::list
Token Id  : 0
User name :
SID name  :

5328    {0;002cfe0a} 4 L 2956463        hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,05p)       Primary
1596    {0;002cfe0a} 4 L 3027920        hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,05p)       Primary
3232    {0;002cfe0a} 4 L 3069428        hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,02p)       Primary
6148    {0;002cfe0a} 4 L 3074556        hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,05p)       Primary
6200    {0;002cfe0a} 4 L 3080889        hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,02p)       Primary
2112    {0;002cfe0a} 4 L 51041168       hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,01p)       Impersonation (Impersonation)
5036    {0;002cfce0} 4 F 55140785       hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,24p)       Impersonation (Impersonation)
```

```text
mimikatz # token::list /admin
Token Id  : 0
User name :
SID name  : BUILTIN\Administrators

7040    {0;002cfce0} 4 F 32996383       hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,24p)       Primary
5036    {0;002cfce0} 4 F 55140785       hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,24p)       Impersonation (Impersonation)
```

```text
mimikatz # token::list /domainadmin
Token Id  : 0
User name :
SID name  : hacklab\Domain Admins

4512    {0;0007212c} 2 D 476947         hacklab\Administrator   S-1-5-21-2725560159-1428537199-2260736313-500   (29g,26p)       Primary
```

```text
mimikatz # token::list /localservice
Token Id  : 0
User name :
SID name  : NT AUTHORITY\LOCAL SERVICE

752     {0;000003e5} 0 D 77860          NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (16g,11p)       Impersonation (Impersonation)
752     {0;000003e5} 0 D 140955         NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (18g,06p)       Impersonation (Impersonation)
752     {0;000003e5} 0 D 300122         NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (16g,05p)       Impersonation (Impersonation)
752     {0;000003e5} 0 D 1128186        NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (16g,02p)       Impersonation (Impersonation)
952     {0;000003e5} 0 D 79148          NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (16g,02p)       Impersonation (Impersonation)
952     {0;000003e5} 0 D 79160          NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (16g,05p)       Impersonation (Impersonation)
1508    {0;000003e5} 0 D 128246         NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (17g,04p)       Impersonation (Identification)
1508    {0;000003e5} 0 D 138957         NT AUTHORITY\LOCAL SERVICE      S-1-5-19        (18g,04p)       Impersonation (Identification)
```

```text
mimikatz # token::list /networkservice
Token Id  : 0
User name :
SID name  : NT AUTHORITY\NETWORK SERVICE

752     {0;000003e4} 0 D 61263          NT AUTHORITY\NETWORK SERVICE    S-1-5-20        (10g,10p)       Impersonation (Impersonation)
752     {0;000003e4} 0 D 94253          NT AUTHORITY\NETWORK SERVICE    S-1-5-20        (10g,04p)       Impersonation (Impersonation)
752     {0;000003e4} 0 D 230166         NT AUTHORITY\NETWORK SERVICE    S-1-5-20        (10g,04p)       Impersonation (Impersonation)
1508    {0;000003e4} 0 D 127940         NT AUTHORITY\NETWORK SERVICE    S-1-5-20        (10g,03p)       Impersonation (Identification)
```

