# packages

`lsadump::packages` lists the available Windows authentication mechanisms.

```
mimikatz # lsadump::packages
Name        : Negotiate
Description : Microsoft Package Negotiator
Capabilities: 00883bb3 ( INTEGRITY ; PRIVACY ; CONNECTION ; MULTI_REQUIRED ; EXTENDED_ERROR ; IMPERSONATION ; ACCEPT_WIN32_NAME ; NEGOTIABLE ; GSS_COMPATIBLE ; LOGON ; RESTRICTED_TOKENS ; APPCONTAINER_CHECKS ; )
MaxToken    : 48256
RPCID       : 0x0009 (9)
Version     : 1

Name        : NegoExtender
Description : NegoExtender Security Package
Capabilities: 00913913 ( INTEGRITY ; PRIVACY ; CONNECTION ; IMPERSONATION ; NEGOTIABLE ; GSS_COMPATIBLE ; LOGON ; MUTUAL_AUTH ; NEGO_EXTENDER ; APPCONTAINER_CHECKS ; )
MaxToken    : 12000
RPCID       : 0x001e (30)
Version     : 1

Name        : Kerberos
Description : Microsoft Kerberos V1.0
Capabilities: 028f3bbf ( INTEGRITY ; PRIVACY ; TOKEN_ONLY ; DATAGRAM ; CONNECTION ; MULTI_REQUIRED ; EXTENDED_ERROR ; IMPERSONATION ; ACCEPT_WIN32_NAME ; NEGOTIABLE ; GSS_COMPATIBLE ; LOGON ; MUTUAL_AUTH ; DELEGATION ; READONLY_WITH_CHECKSUM ; RESTRICTED_TOKENS ; APPCONTAINER_CHECKS ; ? ; )
MaxToken    : 48000
RPCID       : 0x0010 (16)
Version     : 1

Name        : NTLM
Description : NTLM Security Package
Capabilities: 02882b37 ( INTEGRITY ; PRIVACY ; TOKEN_ONLY ; CONNECTION ; MULTI_REQUIRED ; IMPERSONATION ; ACCEPT_WIN32_NAME ; NEGOTIABLE ; LOGON ; RESTRICTED_TOKENS ; APPCONTAINER_CHECKS ; ? ; )
MaxToken    : 2888
RPCID       : 0x000a (10)
Version     : 1

Name        : TSSSP
Description : TS Service Security Package
Capabilities: 00810230 ( CONNECTION ; MULTI_REQUIRED ; ACCEPT_WIN32_NAME ; MUTUAL_AUTH ; APPCONTAINER_CHECKS ; )
MaxToken    : 13000
RPCID       : 0x0016 (22)
Version     : 1

Name        : pku2u
Description : PKU2U Security Package
Capabilities: 00a11113 ( INTEGRITY ; PRIVACY ; CONNECTION ; IMPERSONATION ; GSS_COMPATIBLE ; MUTUAL_AUTH ; NEGOTIABLE2 ; APPCONTAINER_CHECKS ; )
MaxToken    : 12000
RPCID       : 0x001f (31)
Version     : 1

Name        : CloudAP
Description : Cloud AP Security Package
Capabilities: 00202000 ( LOGON ; NEGOTIABLE2 ; )
MaxToken    : 0
RPCID       : 0x0024 (36)
Version     : 1

Name        : WDigest
Description : Digest Authentication for Windows
Capabilities: 00800304 ( TOKEN_ONLY ; IMPERSONATION ; ACCEPT_WIN32_NAME ; APPCONTAINER_CHECKS ; )
MaxToken    : 4096
RPCID       : 0x0015 (21)
Version     : 1

Name        : Schannel
Description : Schannel Security Package
Capabilities: 004107b3 ( INTEGRITY ; PRIVACY ; CONNECTION ; MULTI_REQUIRED ; EXTENDED_ERROR ; IMPERSONATION ; ACCEPT_WIN32_NAME ; STREAM ; MUTUAL_AUTH ; APPCONTAINER_PASSTHROUGH ; )
MaxToken    : 24576
RPCID       : 0x000e (14)
Version     : 1

Name        : Microsoft Unified Security Protocol Provider
Description : Schannel Security Package
Capabilities: 004107b3 ( INTEGRITY ; PRIVACY ; CONNECTION ; MULTI_REQUIRED ; EXTENDED_ERROR ; IMPERSONATION ; ACCEPT_WIN32_NAME ; STREAM ; MUTUAL_AUTH ; APPCONTAINER_PASSTHROUGH ; )
MaxToken    : 24576
RPCID       : 0x000e (14)
Version     : 1

Name        : Default TLS SSP
Description : Schannel Security Package
Capabilities: 004107b3 ( INTEGRITY ; PRIVACY ; CONNECTION ; MULTI_REQUIRED ; EXTENDED_ERROR ; IMPERSONATION ; ACCEPT_WIN32_NAME ; STREAM ; MUTUAL_AUTH ; APPCONTAINER_PASSTHROUGH ; )
MaxToken    : 24576
RPCID       : 0x000e (14)
Version     : 1

Name        : CREDSSP
Description : Microsoft CredSSP Security Provider
Capabilities: 00810733 ( INTEGRITY ; PRIVACY ; CONNECTION ; MULTI_REQUIRED ; IMPERSONATION ; ACCEPT_WIN32_NAME ; STREAM ; MUTUAL_AUTH ; APPCONTAINER_CHECKS ; )
MaxToken    : 73032
RPCID       : 0xffff (65535)
Version     : 1
```
