# Modules

## Modules

* [`crypto`](./#crypto): _placeholder_
* [`dpapi`](./#dpapi): _placeholder_
* [`event`](./#event): _placeholder_
* [`kerberos`](./#kerberos): _placeholder_
* [`lsadump`](./#lsadump): _placeholder_
* [`misc`](./#misc): _placeholder_
* [`net`](./#net): _placeholder_
* [`privilege`](./#privilege): _placeholder_
* [`process`](./#process): _placeholder_
* [`rpc`](./#rpc): _placeholder_
* [`sekurlsa`](./#sekurlsa): _placeholder_
* [`service`](./#service): _placeholder_
* [`sid`](./#sid): _placeholder_
* [`standard`](./#standard): _placeholder_
* [`token`](./#token): _placeholder_
* [`ts`](./#ts): _placeholder_
* [`vault`](./#vault): _placeholder_

## Commands

### crypto

* ``[`crypto::capi`](crypto/capi.md) patches CryptoAPI layer for easy export (Experimental :warning:)
* [`crypto::certificates`](modules/crypto/certificates.md) lists or exports certificates
* [`crypto::certtohw`](modules/crypto/certtohw.md) tries to export a software CA to a crypto (virtual) hardware
* [`crypto::cng`](modules/crypto/cng.md) patches the CNG (Cryptography API: Next Generation) service for easy export (Experimental :warning:)
* [`crypto::extract`](modules/crypto/extract.md) extracts keys from the CAPI RSA/AES provider (Experimental :warning:)
* [`crypto::hash`](modules/crypto/hash.md) hashes a password in the main formats (NT, DCC1, DCC2, LM, MD5, SHA1, SHA2) with the username being an optional value
* [`crypto::keys`](modules/crypto/keys.md) lists or exports key containers
* [`crypto::providers`](modules/crypto/providers.md) lists cryptographic providers
* [`crypto::sc`](modules/crypto/sc.md) lists smartcard/token reader(s) on, or deported to, the system. When the CSP (Cryptographic Service Provider) is available, it tries to list keys on the smartcard
* [`crypto::scauth`](modules/crypto/scauth.md) it creates a authentication certificate (smartcard like) from a CA
* [`crypto::stores`](modules/crypto/stores.md) lists cryptographic stores
* [`crypto::system`](modules/crypto/system.md) it describes a Windows System Certificate
* [`crypto::tpminfo`](modules/crypto/tpminfo.md) displays information for the Microsoft's TPM Platform Crypto Provider

### dpapi

* [`dpapi::blob`](modules/dpapi/blob.md) describes a DPAPI blob and unprotects/decrypts it with API or Masterkey
* [`dpapi::cache`](modules/dpapi/cache.md) displays the credential cache of the DPAPI module
* [`dpapi::capi`](modules/dpapi/capi.md) decrypts a CryptoAPI private key file
* [`dpapi::chrome`](modules/dpapi/chrome.md) dumps stored credentials and cookies from Chrome
* [`dpapi::cloudapkd`](modules/dpapi/cloudapkd.md) is undocumented at the moment
* [`dpapi::cloudapreg`](modules/dpapi/cloudapreg.md) dumps azure credentials by querying the following registry location
* [`dpapi::cng`](modules/dpapi/cng.md) decrypts a given CNG private key file
* [`dpapi::create`](modules/dpapi/create.md) creates a DPAPI Masterkey file from raw key and metadata
* [`dpapi::cred`](modules/dpapi/cred.md) decrypts DPAPI saved credential such as RDP, Scheduled tasks, etc (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad-ds/movement/credentials/dumping/dpapi-protected-secrets))
* [`dpapi::credhist`](modules/dpapi/credhist.md) describes a Credhist file
* [`dpapi::luna`](modules/dpapi/luna.md) decrypts Safenet LunaHSM KSP
* [`dpapi::masterkey`](modules/dpapi/masterkey.md) describes a Masterkey file and unprotects each Masterkey (key depending). In other words, it can decrypt and request masterkeys from active directory
* [`dpapi::protect`](modules/dpapi/protect.md) protects data via a DPAPI call
* [`dpapi::ps`](modules/dpapi/ps.md) decrypts PowerShell credentials (PSCredentials or SecureString)
* [`dpapi::rdg`](modules/dpapi/rdg.md) decrypts Remote Desktop Gateway saved passwords
* [`dpapi::sccm`](modules/dpapi/sccm.md) is used to decrypt saved SCCM credentials
* [`dpapi::ssh`](modules/dpapi/ssh.md) extracts OpenSSH private keys
* [`dpapi::tpm`](modules/dpapi/tpm.md) decrypts TPM PCP key file ([Microsoft's TPM Platform Crypto Provider](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/setting-up-tpm-protected-certificates-using-a-microsoft/ba-p/1129055) (PCP))
* [`dpapi::vault`](modules/dpapi/vault.md) decrypts DPAPI vault credentials from the [Credential Store](https://support.microsoft.com/en-us/windows/accessing-credential-manager-1b5c916a-6a16-889f-8581-fc16e8165ac0)
* [`dpapi::wifi`](modules/dpapi/wifi.md) decrypts saved Wi-Fi passwords
* [`dpapi::wwman`](modules/dpapi/wwan.md) decrypts Wwan credentials

### event

* [`event::clear`](modules/event/clear.md) clears a specified event log
* [`event::drop`](modules/event/drop.md) patches event services to avoid new events ( :warning: experimental)

### kerberos

* [`kerberos::ask`](modules/kerberos/ask.md) can be used to obtain Service Tickets. The Windows native command is [`klist get`](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/klist)
* [`kerberos::clist`](modules/kerberos/clist.md) lists tickets in [MIT](https://web.mit.edu/kerberos/)/[Heimdall](https://github.com/heimdal/heimdal) ccache format. It can be useful with other tools (i.e. ones that support [Pass the Cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc))
* [`kerberos::golden`](modules/kerberos/golden.md) can be used to [forge golden and silver tickets](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets). It can also be used for forging inter-realm trust keys
* [`kerberos::hash`](modules/kerberos/hash.md) computes the different types of Kerberos keys for a given password
* [`kerberos::list`](modules/kerberos/list.md) has a similar functionality to [`klist`](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/klist) command without requiring elevated privileges. Unlike [`sekurlsa::tickets`](modules/sekurlsa/tickets.md), this module does not interact with LSASS
* [`kerberos::ptc`](modules/kerberos/ptc.md) can be used to [pass the cache](https://www.thehacker.recipes/ad/movement/kerberos/ptc). This is similar to [`kerberos::ptt`](ptt.md) that does pass the ticket but is different in the sense that the ticket used is a `.ccache` ticket instead of a `.kirbi` one
* [`kerberos::ptt`](modules/kerberos/ptt.md) is used for [passing the ticket](https://www.thehacker.recipes/ad/movement/kerberos/ptt) by injecting one or may Kerberos tickets in the current session. The ticket can either be a TGT (Ticket-Granting Ticket) or an ST (Service Ticket)
* [`kerberos::purge`](modules/kerberos/purge.md) purges all kerberos tickets similar to [`klist purge`](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/klist)
* [`kerberos::tgt`](modules/kerberos/tgt.md) retrieves a TGT (Ticket-Granting Ticket) for the current user

### lsadump

* [`lsadump::backupkeys`](modules/lsadump/backupkeys.md) dumps the DPAPI backup keys from the Domain Controller (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad/movement/credentials/dumping/dpapi-protected-secrets))
* [`lsadump::cache`](modules/lsadump/cache.md) can be used to enumerate Domain Cached Credentials from registry. It does so by acquiring the `SysKey` to decrypt `NL$KM` (binary protected value) and then `MSCache(v1/v2)`
* [`lsadump::changentlm`](modules/lsadump/changentlm.md) can be used to change the password of a user
* [`lsadump::dcshadow`](modules/lsadump/dcshadow.md) TODO
* [`lsadump::dcsync`](modules/lsadump/dcsync.md) can be used to do a [DCSync](https://www.thehacker.recipes/ad/movement/credentials/dumping/dcsync) and retrieve domain secrets. This command uses the Directory Replication Service Remote protocol ([MS-DRSR](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-drsr/f977faaa-673e-4f66-b9bf-48c640241d47?redirectedfrom=MSDN)) to request from a domain controller to synchronize a specified entry
* [`lsadump::lsa`](modules/lsadump/lsa.md) extracts hashes from memory by asking the LSA server. The `patch` or `inject` takes place on the fly
* [`lsadump::mbc`](modules/lsadump/mbc.md) dumps the Machine Bound Certificate. Devices on which Credential Guard is enabled are using Machine Bound Certificates
* [`lsadump::netsync`](modules/lsadump/netsync.md) can be used to act as a Domain Controller on a target by doing a [Silver Ticket](https://www.thehacker.recipes/ad/movement/kerberos/forged-tickets#silver-ticket). It then leverages the [Netlogon](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f) to request the RC4 key (i.e. NT hash) of the target computer account
* [`lsadump::packages`](modules/lsadump/packages.md) lists the available Windows authentication mechanisms
* [`lsadump::postzerologon`](modules/lsadump/postzerologon.md) is a procedure to update AD domain password and its local stored password remotely mimic `netdom resetpwd`
* [`lsadump::RpData`](modules/lsadump/rpdata.md) can retrieve private data (_at the time of writing, Nov 1st 2021, we have no idea what this does or refers to_ :man\_shrugging:)
* [`lsadump::sam`](modules/lsadump/sam.md) dumps the local Security Account Manager (SAM) NT hashes (cf. [SAM secrets dump](https://www.thehacker.recipes/ad/movement/credentials/dumping/sam-and-lsa-secrets))
* [`lsadump::secrets`](modules/lsadump/secrets.md) can be used to [dump LSA secrets](https://www.thehacker.recipes/ad/movement/credentials/dumping/sam-and-lsa-secrets) from the registries. It retrieves the `SysKey` to decrypt `Secrets` entries
* [`lsadump::setntlm`](modules/lsadump/setntlm.md) can be used to perform a password reset without knowing the user's current password. It can be useful during an active directory [Access Control (ACL) abuse](https://www.thehacker.recipes/ad/movement/access-controls) scenario
* [`lsadump::trust`](modules/lsadump/trust.md) can be used for dumping the forest trust keys. Forest trust keys can be leveraged for forging inter-realm trust tickets. Since most of the EDRs are paying attention to the KRBTGT hash, this is a stealthy way to compromise forest trusts
* [`lsadump::zerologon`](modules/lsadump/zerologon.md) detects and exploits the [ZeroLogon](https://www.thehacker.recipes/ad/movement/netlogon/zerologon) vulnerability

### misc

* [`misc::aadcookie`](modules/misc/aadcookie.md) can be used to dump the Azure Panel's session cookie from `login.microsoftonline.com`
* [`misc::clip`](modules/misc/clip.md) monitors clipboard. `CTRL+C` stops the monitoring
* [`misc::cmd`](modules/misc/cmd.md) launches the command prompt
* [`misc::compress`](modules/misc/compress.md) performs a self compression of mimikatz
* [`misc::detours`](modules/misc/detours.md) is experimental and it tries to enumerate all modules with [Detours-like hooks](https://www.codeproject.com/Articles/30140/API-Hooking-with-MS-Detours)
* [`misc::efs`](modules/misc/efs.md) is Mimikatz's implementation of the [MS-EFSR abuse (PetitPotam)](https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-efsr), an authentication coercion technique
* [`misc::lock`](modules/misc/lock.md) locks the screen. It can come in handy with [`misc::memssp`](memssp.md)
* [`misc::memssp`](modules/misc/memssp.md) patches LSASS by injecting a new Security Support Provider (a DLL is registered)
* [`misc::mflt`](modules/misc/mflt.md) identifies Windows minifilters inside mimikatz, without using **fltmc.exe**. It can also assist in fingerprinting security products, by altitude too (Gathers details on loaded drivers, including driver altitude)
* [`misc::ncroutemon`](modules/misc/ncroutemon.md) displays Juniper network connect (without route monitoring)
* [`misc::ngcsign`](modules/misc/ngcsign.md) can be used to dump the NGC key (Windows Hello keys) signed with the symmetric pop key.
* [`misc::printnightmare`](modules/misc/printnightmare.md) can be used to exploit the [PrintNightMare](https://adamsvoboda.net/breaking-down-printnightmare-cve-2021-1675/) vulnerability in both \[[MS-RPRN RpcAddPrinterDriverEx](https://docs.microsoft.com/en-us/openspecs/windows\_protocols/ms-rprn/b96cc497-59e5-4510-ab04-5484993b259b)] and \[[MS-PAR AddPrinterDriverEx](https://docs.microsoft.com/en-us/windows/win32/printdocs/addprinterdriverex)]. The bug was discovered by Zhiniang Peng ([@edwardzpeng](https://twitter.com/edwardzpeng?lang=en)) & Xuefeng Li ([@lxf02942370](https://twitter.com/lxf02942370?lang=en))
* [`misc::regedit`](modules/misc/regedit.md) launches the registry editor
* [`misc::sccm`](modules/misc/sccm.md) decrypts the password field in the `SC_UserAccount` table in the SCCM database
* [`misc::shadowcopies`](modules/misc/shadowcopies.md) is used to list the available shadow copies on the system
* [`misc::skeleton`](modules/misc/skeleton.md) injects a "[Skeleton Key](https://www.thehacker.recipes/ad/persistence/skeleton-key)" into the LSASS process on the domain controller
* [`misc::spooler`](modules/misc/spooler.md) is Mimikat's implementation of the [MS-RPRN abuse (PrinterBug)](https://www.thehacker.recipes/ad/movement/mitm-and-coerced-authentications/ms-rprn), an authentication coercion technique
* [`misc::taskmgr`](modules/misc/taskmgr.md) launches the task manager
* [`misc::wp`](modules/misc/wp.md) sets up a wallpaper
* [`misc::xor`](modules/misc/xor.md) performs XOR decoding/encoding on a provided file with `0x42` default key

### net

* [`net::alias`](modules/net/alias.md) displays more information about the local group memberships including Remote Desktop Users, Distributed COM Users, etc
* [`net::deleg`](modules/net/deleg.md) checks for the following types of [Kerberos delegations](https://www.thehacker.recipes/ad-ds/movement/kerberos/delegations)
* [`net::group`](modules/net/group.md) displays the local groups
* [`net::if`](modules/net/if.md) displays the available local IP addresses and the hostname
* [`net::serverinfo`](modules/net/serverinfo.md) displays information about the logged in server
* [`net::session`](modules/net/session.md) displays the active sessions through [NetSessionEnum()](https://web.archive.org/web/20201201223201/https://docs.microsoft.com/en-us/windows/win32/api/lmshare/nf-lmshare-netsessionenum) Win32 API function
* [`net::share`](modules/net/share.md) displays the available shares
* [`net::stats`](modules/net/stats.md) displays when the target was booted
* [`net::tod`](modules/net/tod.md) displays the current time
* [`net::trust`](modules/net/trust.md) displays information for the active directory forest trust(s)
* [`net::user`](modules/net/user.md) displays the local users
* [`net::wsession`](modules/net/wsession.md) displays the active sessions through [NetWkstaUserEnum()](https://web.archive.org/web/20190909155552/https://docs.microsoft.com/en-us/windows/win32/api/lmwksta/nf-lmwksta-netwkstauserenum) Win32 API function

### privilege

* [`privilege::backup`](modules/privilege/backup.md) requests the backup privilege (`SeBackupPrivilege`)
* [`privilege::debug`](modules/privilege/debug.md) requests the debug privilege (`SeDebugPrivilege`)
* [`privilege::driver`](modules/privilege/driver.md) requests the load driver privilege (`SeLoadDriverPrivilege`)
* [`privilege::id`](modules/privilege/id.md) requests a privilege by its `id`
* [`privilege::name`](modules/privilege/name.md) requests a privilege by its name
* [`privilege::restore`](modules/privilege/restore.md) requests the restore privilege (`SeRestorePrivilege`)
* [`privilege::security`](modules/privilege/security.md) requests the security privilege (`SeSecurityPrivilege`)
* [`privilege::sysenv`](modules/privilege/sysenv.md) requests the system environment privilege (`SeSystemEnvironmentPrivilege`)
* [`privilege::tcb`](modules/privilege/tcb.md) requests the tcb privilege (`SeTcbPrivilege`)

### process

* [`process::exports`](modules/process/exports.md) lists all the exported functions from the DLLs each running process is using. If a\*\* \*\*`/pid` is not specified, then exports for `mimikatz.exe` will be displayed
* [`process::imports`](modules/process/imports.md) lists all the imported functions from the DLLs each running process is using. If a\*\* \*\*`/pid` is not specified, then imports for `mimikatz.exe` will be displayed
* [`process::list`](modules/process/list.md) lists all the running processes. It uses the [NtQuerySystemInformation](https://docs.microsoft.com/en-us/windows/win32/api/winternl/nf-winternl-ntquerysysteminformation) Windows Native API function
* [`process::resume`](modules/process/resume.md) resumes a suspended process by using the [NtResumeProcess](https://www.geoffchappell.com/studies/windows/win32/ntdll/api/native.htm) Windows Native API function
* [`process::run`](modules/process/run.md) creates a process by using the [CreateProcessAsUser](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessasusera) Win32 API function. The [CreateEnvironmentBlock](https://docs.microsoft.com/en-us/windows/win32/api/userenv/nf-userenv-createenvironmentblock) is also utilized
* [`process::runp`](modules/process/runp.md) runs a subprocess under a parent process (Default parent process is `LSASS.exe`). It can also be used for lateral movement and process spoofing
* [`process::start`](modules/process/start.md) starts a process by using the [CreateProcess](https://web.archive.org/web/20170713150625/https://msdn.microsoft.com/en-us/library/windows/desktop/ms682425.aspx) Win32 API function. The `PID` of the process is also displayed
* [`process::stop`](modules/process/stop.md) terminates a process by using the [NtTerminateProcess](https://www.geoffchappell.com/studies/windows/win32/ntdll/api/native.htm) Windows Native API function. The Win32 API equal one is [TerminateProcess](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-terminateprocess)
* [`process::suspend`](modules/process/suspend.md) suspends a process by using the [NtSuspendProcess](https://ntopcode.wordpress.com/tag/ntsuspendprocess/) Windows Native API function

### rpc

* [`rpc::close`](modules/rpc/close.md) closes remote RPC sessions
* [`rpc::connect`](modules/rpc/connect.md) connects to an RPC endpoint
* [`rpc::enum`](modules/rpc/enum.md) enumerates RPC endpoints on a system
* [`rpc::server`](modules/rpc/server.md) starts an RPC server

### sekurlsa

* [`sekurlsa::backupkeys`](modules/sekurlsa/backupkeys.md) lists the preferred Backup Master keys
* [`sekurlsa::bootkey`](modules/sekurlsa/bootkey.md) sets the SecureKernel Boot Key and attempts to decrypt LSA Isolated credentials
* [`sekurlsa::cloudap`](modules/sekurlsa/cloudap.md) lists Azure (Primary Refresh Token) credentials based on the following research: [Digging further into the Primary Refresh Token](https://dirkjanm.io/digging-further-into-the-primary-refresh-token/). [According to Benjamin](https://twitter.com/gentilkiwi/status/1291102498099527682?s=20):
* [`sekurlsa::credman`](modules/sekurlsa/credman.md) lists Credentials Manager by targeting the Microsoft Local Security Authority Server DLL ([lsasrv.dll](https://windows10dll.nirsoft.net/lsasrv\_dll.html))
* [`sekurlsa::dpapi`](modules/sekurlsa/dpapi.md) lists DPAPI cached masterkeys
* [`sekurlsa::dpapisystem`](modules/sekurlsa/dpapisystem.md) lists the `DPAPI_SYSTEM` secret key
* [`sekurlsa::ekeys`](modules/sekurlsa/ekeys.md) lists Kerberos encryption keys
* [`sekurlsa::kerberos`](modules/sekurlsa/kerberos.md) lists Kerberos credentials
* [`sekurlsa::krbtgt`](modules/sekurlsa/krbtgt.md) retrieves the krbtgt RC4 (i.e. NT hash), AES128 and AES256 hashes
* [`sekurlsa::livessp`](modules/sekurlsa/livessp.md) lists LiveSSP credentials. According to Microsoft, the LiveSSP provider is included by default in Windows 8 and later and is included in the Office 365 Sign-in Assistant
* [`sekurlsa::logonpasswords`](modules/sekurlsa/logonpasswords.md) lists all available provider credentials. This usually shows recently logged on user and computer credentials
* [`sekurlsa::minidump`](modules/sekurlsa/minidump.md) can be used against a dumped LSASS process file and it does not require administrative privileges. It's considered as an "offline" dump
* [`sekurlsa::msv`](modules/sekurlsa/msv.md) dumps and lists the NT hash (and other secrets) by targeting the [MSV1\_0 Authentication Package](https://docs.microsoft.com/en-us/windows/win32/secauthn/msv1-0-authentication-package)
* [`sekurlsa::process`](modules/sekurlsa/process.md) switches (or reinits) to LSASS process context. It can be used after [`sekurlsa::minidump`](minidump.md)
* [`sekurlsa::pth`](modules/sekurlsa/pth.md) performs [Pass-the-Hash](https://www.thehacker.recipes/ad/movement/ntlm/pth), [Pass-the-Key](https://www.thehacker.recipes/ad/movement/kerberos/ptk) and [Over-Pass-the-Hash](https://www.thehacker.recipes/ad/movement/kerberos/opth). Upon successful authentication, a program is run (n.b. defaulted to `cme.exe`)
* [`sekurlsa::ssp`](modules/sekurlsa/ssp.md) lists [Security Support Provider](https://docs.microsoft.com/en-us/windows-server/security/windows-authentication/security-support-provider-interface-architecture) (SSP) credentials
* [`sekurlsa::tickets`](modules/sekurlsa/tickets.md) lists Kerberos tickets belonging to all authenticated users on the target server/workstation. Unlike [`kerberos::list`](../process/list.md), sekurlsa uses memory reading and is not subject to key export restrictions. Sekurlsa can also access tickets of others sessions (users)
* [`sekurlsa::trust`](modules/sekurlsa/trust.md) retrieves the forest trust keys
* [`sekurlsa::tspkg`](modules/sekurlsa/tspkg.md) lists TsPkg credentials. This credentials provider is used for Terminal Server Authentication
* [`sekurlsa::wdigest`](modules/sekurlsa/wdigest.md) lists WDigest credentials. According to Microsoft, [WDigest.dll](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc778868\(v%3dws.10\)) was introduced in the Windows XP operating system

### service

* [`service::-`](modules/service/undefined.md) removes the `mimikatzsvc` service
* [`service::+`](modules/service/+.md) installs the `mimikatzsvc` service by issuing `rpc::server service::me exit`
* [`service::preshutdown`](modules/service/preshutdown.md) pre-shuts down a specified service by sending a `SERVICE_CONTROL_PRESHUTDOWN` signal
* [`service::remove`](modules/service/remove.md) removes the specified service (It must be used with caution)
* [`service::resume`](modules/service/resume.md) resumes a specified service, after successful suspending, by sending a `SERVICE_CONTROL_CONTINUE` signal
* [`service::shutdown`](modules/service/shutdown.md) shuts down a specified service by sending a `SERVICE_CONTROL_SHUTDOWN` signal
* [`service::start`](modules/service/start.md) starts a service
* [`service::stop`](modules/service/stop.md) stops a specified service by sending a `SERVICE_CONTROL_STOP` signal
* [`service::suspend`](modules/service/suspend.md) suspends the specified service. It sends a `SERVICE_CONTROL_PAUSE` signal

### sid

* [`sid::add`](modules/sid/add.md) adds a SID to `sIDHistory` of an object
* [`sid::clear`](modules/sid/clear.md) clears the `sIDHistory` of a target object
* [`sid::lookup`](modules/sid/lookup.md) looks up an object by its SID or name
* [`sid::modify`](modules/sid/modify.md) modifies an object's SID
* [`sid::patch`](modules/sid/patch.md) patchs the NTDS (NT Directory Services). It's useful when running [`id::modify`](modules/sid/modify.md) or [`sid::add`](modules/sid/add.md)
* [`sid::query`](modules/sid/query.md) queries an object by its SID or name

### standard

* [`standard::answer`](modules/standard/answer.md) or `answer` provides an answer to [The Ultimate Question of Life, the Universe, and Everything!](https://hitchhikers.fandom.com/wiki/Ultimate\_Question) :stars:
* [`standard::base64`](modules/standard/base64.md) or `base64` switches file input/output to base64
* [`standard::cd`](modules/standard/cd.md) or `cd` can change or display the current directory. The changed directory is used for saving files
* [`standard::cls`](modules/standard/cls.md) or `cls` clears the screen
* [`standard::coffee`](modules/standard/coffee.md) or `coffee` is the most important command of all
* [`standard::exit`](modules/standard/exit.md) or `exit` quits Mimikatz after clearing routines
* [`standard::hostname`](modules/standard/hostname.md) or `hostname` displays system local hostname
* [`standard::localtime`](modules/standard/localtime.md) or `localtime` displays system local date and time
* [`standard::log`](modules/standard/log.md) or `log` logs mimikatz input/output to a file
* [`standard::sleep`](modules/standard/sleep.md) or `sleep` make Mimikatz sleep an amount of milliseconds
* [`standard::version`](modules/standard/version.md) or `version` displays the version in use of Mimikatz

### token

The Mimikatz Token module enables Mimikatz to interact with Windows authentication tokens, including grabbing and impersonating existing tokens

* [`token::elevate`](modules/token/elevate.md) can be used to impersonate a token. By default it will elevate permissions to `NT AUTHORITY\SYSTEM`
* [`token::list`](modules/token/list.md) lists all tokens on the system
* [`token::revert`](modules/token/revert.md) reverts to the previous token
* [`token::run`](modules/token/run.md) executes a process with its token
* [`token::whoami`](modules/token/whoami.md) displays the current token

### ts

* [`ts::logonpasswords`](modules/ts/logonpasswords.md) extracts clear text credentials from RDP running sessions (server side)
* [`ts::mstsc`](modules/ts/mstsc.md) extracts cleartext credentials from the mstsc process (client side)
* [`ts::multirdp`](modules/ts/multirdp.md) enables multiple RDP connections on the target server
* [`ts::remote`](modules/ts/remote.md) performs RDP takeover/hijacking of active sessions
* [`ts::sessions`](modules/ts/sessions.md) lists the current RDP sessions. It comes in handy for RDP hijacking

### vault

* [`vault::cred`](modules/vault/cred.md) enumerates vault credentials. More information can be found at Benjamin's guide [howto-\~-scheduled-tasks-credentials](https://github.com/gentilkiwi/mimikatz/wiki/howto-\~-scheduled-tasks-credentials)
* [`vault::list`](modules/vault/list.md) lists saved credentials in the Windows Vault such as scheduled tasks, RDP, Internet Explorer for the current user. More information can be found at Benjamin's guide [howto-\~-scheduled-tasks-credentials](https://github.com/gentilkiwi/mimikatz/wiki/howto-\~-scheduled-tasks-credentials)
