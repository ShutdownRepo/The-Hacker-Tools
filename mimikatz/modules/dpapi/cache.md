# cache

`dpapi::cache` displays the credential cache of the DPAPI module. It has the following command line argument:

* `/save`: save the output to a `.ndr` file
* `/load`: load the `.ndr` file. By default it will search on the current path

```
mimikatz # dpapi::cache

CREDENTIALS cache
=================

MASTERKEYS cache
================
GUID:{0686f7cf-76f3-413b-a51e-28d0d0531013};KeyHash:c5049248822679fdb3e60ba37531ae3e805f7122;Key:available
GUID:{b3f80f3d-c0e3-49bf-b625-138f351e58fe};KeyHash:4d7a99f0704d8d9a470c1520a6ae8a5088074d9e;Key:available
GUID:{04ba5c5c-7ae8-4a09-8cf6-d623558cdfec};KeyHash:5d45c4d426c247354968963aacdcccc439112c6c;Key:available
GUID:{58636dcf-f23d-4461-9579-23d032b65a93};KeyHash:9dcc466c6bb5b0772fe5650386cf33fc1a1f00fc;Key:available
GUID:{436352c3-01c5-49b1-a5f7-148f86203b4c};KeyHash:ff82db201aff8a92df65ac8d5e3649b919a02a55;Key:available
GUID:{ad426236-788d-4fe6-a1c7-04a21440f493};KeyHash:7752ff93b8cc9bc275ebedf84115f59e347578e8;Key:available
GUID:{612eeb99-0f2b-42e3-be2d-d65046fb2738};KeyHash:d6ef42907dcc8e100f03e4f971bada865ee90ad0;Key:available
GUID:{f150d358-fc03-427a-9707-8e14fa82c9e2};KeyHash:f9e649f84edde57d8d84c4f8b33ea18dd4e8e0c4;Key:available

DOMAINKEYS cache
================
GUID:{e3364acb-379c-4775-bef7-c3c1e1992589};TYPE:RSA
GUID:{b799ff33-a573-444f-bc86-b8aeb36fcb3f};TYPE:LEGACY
```
