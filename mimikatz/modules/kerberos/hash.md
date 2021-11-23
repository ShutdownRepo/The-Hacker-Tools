# hash

`kerberos::hash` computes the different types of Kerberos keys for a given password. It has the following command line arguments:

* `/user`: the `sAMAccountName` of the user
* `/password`: the plaintext password
* `/domain`: the active directory domain
* `/count`: number of iterations

```
mimikatz # kerberos::hash /user:m3g9tr0n /domain:hacklab.local /password:Super_SecretPass1!
        * rc4_hmac_nt       b09a14d2d325026f8986d4a874fbcbc7
        * aes128_hmac       f99e642fe29c8aa84e047876d29fc4f7
        * aes256_hmac       f5b77681af657ccec49e707c2e2f8fc1dc958088f8dc99f09ce3818183cf2392
        * des_cbc_md5       d3f89befcb43ce52
```
