# providers

`crypto::providers` lists cryptographic providers. This module, one of the oldest, plays with `CryptoAPI` functions. Basically it's a little `certutil` that features token impersonation, patches legacy `CryptoAPI` functions and patches `CNG` key isolation service.

```
mimikatz # crypto::providers

CryptoAPI providers :
 0. RSA_FULL      ( 1)   - Microsoft Base Cryptographic Provider v1.0
 1. DSS_DH        (13)   - Microsoft Base DSS and Diffie-Hellman Cryptographic Provider
 2. DSS           ( 3)   - Microsoft Base DSS Cryptographic Provider
 3. RSA_FULL      ( 1) H - Microsoft Base Smart Card Crypto Provider
 4. DH_SCHANNEL   (18)   - Microsoft DH SChannel Cryptographic Provider
 5. RSA_FULL      ( 1)   - Microsoft Enhanced Cryptographic Provider v1.0
 6. DSS_DH        (13)   - Microsoft Enhanced DSS and Diffie-Hellman Cryptographic Provider
 7. RSA_AES       (24)   - Microsoft Enhanced RSA and AES Cryptographic Provider
 8. RSA_SCHANNEL  (12)   - Microsoft RSA SChannel Cryptographic Provider
 9. RSA_FULL      ( 1)   - Microsoft Strong Cryptographic Provider

CryptoAPI provider types:
 0. RSA_FULL      ( 1) - RSA Full (Signature and Key Exchange)
 1. DSS           ( 3) - DSS Signature
 2. RSA_SCHANNEL  (12) - RSA SChannel
 3. DSS_DH        (13) - DSS Signature with Diffie-Hellman Key Exchange
 4. DH_SCHANNEL   (18) - Diffie-Hellman SChannel
 5. RSA_AES       (24) - RSA Full and AES

CNG providers :
 0. Kiwi Random TPM Provider
 1. Microsoft Key Protection Provider
 2. Microsoft Passport Key Storage Provider
 3. Microsoft Platform Crypto Provider
 4. Microsoft Primitive Provider
 5. Microsoft Smart Card Key Storage Provider
 6. Microsoft Software Key Storage Provider
 7. Microsoft SSL Protocol Provider
 8. Windows Client Key Protection Provider
```
