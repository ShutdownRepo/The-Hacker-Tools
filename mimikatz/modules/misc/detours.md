# detours

`misc::detours` is experimental and it tries to enumerate all modules with [Detours-like hooks](https://www.codeproject.com/Articles/30140/API-Hooking-with-MS-Detours).

```
mimikatz # misc::detours
Registry (92)
ERROR kuhl_m_misc_detours_callback_process ; OpenProcess (0x00000005)
smss.exe (404)
ERROR kuhl_m_misc_detours_callback_process ; OpenProcess (0x00000005)
csrss.exe (500)
ERROR kuhl_m_misc_detours_callback_process ; OpenProcess (0x00000005)
csrss.exe (620)
ERROR kuhl_m_misc_detours_callback_process ; OpenProcess (0x00000005)
wininit.exe (632)
ERROR kuhl_m_misc_detours_callback_process ; OpenProcess (0x00000005)
winlogon.exe (688)
services.exe (764)
ERROR kuhl_m_misc_detours_callback_process ; OpenProcess (0x00000005)
lsass.exe (784)
svchost.exe (896)
fontdrvhost.exe (920)
fontdrvhost.exe (928)
svchost.exe (1012)
svchost.exe (280)
LogonUI.exe (448)
dwm.exe (860)
svchost.exe (1048)
svchost.exe (1092)
svchost.exe (1100)
svchost.exe (1108)
svchost.exe (1216)

...Output Omitted...
```
