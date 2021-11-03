# version

`standard::version` or `version` displays the version in use of Mimikatz. It has the following command line arguments:

* `/full`: it displays all the DLLs used by Mimikatz
* `/cab`: it creates a **.cab** file for troubleshooting purposes

```
mimikatz # version

mimikatz 2.2.0 (arch x64)
Windows NT 10.0 build 19042 (arch x64)
msvc 150030729 207
```

Benjamin has provided the following values:

* `150030729 207` is the WinDDK compiler
* `150030729 1` is the vc90 compiler (Visual Studio 2008)
* `160040219 1` is the vc100 compiler (Visual Studio 2010)
* `170061030 0` is the vc110(\_xp) compiler (Visual Studio 2012)
* `180040629 0` is the vc120(\_xp) compiler (Visual Studio 2013)
* `190023026 0` is the vc140(\_xp) compiler (Visual Studio 2015)

```
mimikatz # version /full

mimikatz 2.2.0 (arch x64)
Windows NT 10.0 build 19042 (arch x64)
msvc 150030729 207

lsasrv.dll      : 10.0.19041.1288
msv1_0.dll      : 10.0.19041.1023
tspkg.dll       : 10.0.19041.264
wdigest.dll     : 10.0.19041.388
kerberos.dll    : 10.0.19041.1288
dpapisrv.dll    : 10.0.19041.746
cryptdll.dll    : 10.0.19041.546
samsrv.dll      : 10.0.19041.1202
rsaenh.dll      : 10.0.19041.1052
ncrypt.dll      : 10.0.19041.662
ncryptprov.dll  : 10.0.19041.1202
wevtsvc.dll     : 10.0.19041.1266
termsrv.dll     : 10.0.19041.1202
```

```
mimikatz # version /cab

mimikatz 2.2.0 (arch x64)
Windows NT 10.0 build 19042 (arch x64)
msvc 150030729 207

CAB: mimikatz_x64_sysfiles_19042
 -> lsasrv.dll
 -> msv1_0.dll
 -> tspkg.dll
 -> wdigest.dll
 -> kerberos.dll
 -> dpapisrv.dll
 -> cryptdll.dll
 -> samsrv.dll
 -> rsaenh.dll
 -> ncrypt.dll
 -> ncryptprov.dll
 -> wevtsvc.dll
 -> termsrv.dll
```

![Cab file](<../../../.gitbook/assets/2 (1) (1).png>)
