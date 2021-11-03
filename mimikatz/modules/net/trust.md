# trust

`net::trust` displays information for the active directory forest trust(s). It has the following command line argument:

* `/server`: The domain controller to query. If not specified it will query the DC of the current domain

```
mimikatz # net::trust
RPC mode:
[ 0] Netbios   : hacklab
     DNS       : hacklab.local
     Flags     : 0x0000001d ( IN_FOREST ; TREE_ROOT ; PRIMARY ; NATIVE_MODE ; )
     Type      : 0x00000002 - UPLEVEL (DC >= 2000)
     Attributes: 0x00000000 ( )
     SID       : S-1-5-21-2725560159-1428537199-2260736313
     GUID      : {9901d757-a63d-478f-a96a-f8be1a8308ac}
```
