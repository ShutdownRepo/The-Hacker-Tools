# hash

`crypto::hash` hashes a password in the main formats (NT, DCC1, DCC2, LM, MD5, SHA1, SHA2) with the username being an optional value. It has the following command line argument:

* `/count`: number of iterations for the salted hashes

{% hint style="info" %}
LM and NT hashes are used to authenticate accounts using the NTLM protocol. These hashes are often called NTLM hash and many documentations, resources, blogpost and tools mix terms. In this case, "NTLM" refers to the NT hash.

([more information](https://www.thehacker.recipes/ad/movement/ntlm))
{% endhint %}

```
mimikatz # crypto::hash /user:test /password:password
NTLM: 8846f7eaee8fb117ad06bdd830b7586c
DCC1: 1f34a7dfade9ddaa26746086ecbe77bf
DCC2: a86012faf7d88d1fc037a69764a92cac
LM  : e52cac67419a9a224a3b108f3fa6cb6d
MD5 : b081dbe85e1ec3ffc3d4e7d0227400cd
SHA1: e8f97fba9104d1ea5047948e6dfb67facd9f5b73
SHA2: e201065d0554652615c320c00a1d5bc8edca469d72c2790e24152d0c1e2b6189
```
