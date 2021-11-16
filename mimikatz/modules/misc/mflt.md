# mflt

`misc::mflt` identifies Windows minifilters inside mimikatz, without using **fltmc.exe**. It can also assist in fingerprinting security products, by altitude too (Gathers details on loaded drivers, including driver altitude).

{% hint style="info" %}
This command requires elevated privileges (by previously running [`privilege::debug`](../privilege/debug.md) or by executing Mimikatz as the `NT-AUTHORITY\SYSTEM` account).
{% endhint %}

```
mimikatz # misc::mflt
0 1     409800 bindflt
0 7     328010 WdFilter
0 0     244000 storqosflt
0 0     189900 wcifs
0 0     180451 CldFlt
0 0     141100 FileCrypt
0 1     135000 luafv
0 1      46000 npsvctrig
0 6      40700 Wof
0 7      40500 FileInfo
```
