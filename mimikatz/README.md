# 🛠️ Mimikatz 🥝

What is Mimikatz?



## Modules

* ts: used for blablaba
* sid: /////
* rpc
* net
* misc
* event
* token
* ...

## Commands

### ts

* [`ts::mstsc`](modules/ts/mstsc.md) extracts cleartext credentials from the mstsc process (client side)
* [`ts::remote`](modules/ts/remote.md) performs RDP takeover/hijacking of active sessions
* [`ts::multirdp`](modules/ts/multirdp.md) enables multiple RDP connections on the target server
* [`ts::sessions`](modules/ts/sessions.md) lists the current RDP sessions. It comes in handy for RDP hijacking
* [`ts::logonpasswords`](modules/ts/logonpasswords.md) extracts clear text credentials from RDP running sessions (server side)

### sid

* [`sid::add`](modules/sid/add.md) adds a SID to `sIDHistory` of an object
* [`sid::clear`](modules/sid/clear.md) clears the `sIDHistory` of a target object
* [`sid::patch`](modules/sid/patch.md) patchs the NTDS (NT Directory Services). It's useful when running [`id::modify`](modules/sid/modify.md) or [`sid::add`](modules/sid/add.md)
* [`sid::query`](modules/sid/query.md) queries an object by its SID or name
* [`sid::lookup`](modules/sid/lookup.md) looks up an object by its SID or name
* [`sid::modify`](modules/sid/modify.md) modifies an object's SID

### rpc

* [`rpc::close`](modules/rpc/close.md) closes remote RPC sessions
* [`rpc::enum`](modules/rpc/enum.md) enumerates RPC endpoints on a system
* [`rpc::server`](modules/rpc/server.md) starts an RPC server
* [`rpc::connect`](modules/rpc/connect.md) connects to an RPC endpoint

### net

* [`net::if`](modules/net/if.md) displays the available local IP addresses and the hostname
* [`net::tod`](modules/net/tod.md) displays the current time
* [`net::user`](modules/net/user.md) displays the local users
* [`net::alias`](modules/net/alias.md) displays more information about the local group memberships including Remote Desktop Users, Distributed COM Users, etc.
* [`net::trust`](modules/net/trust.md) displays information for the active directory forest trust(s)
* [`net::stats`](modules/net/stats.md) displays when the target was booted
* [`net::deleg`](modules/net/deleg.md) checks for the following types of [Kerberos delegations](https://www.thehacker.recipes/ad-ds/movement/kerberos/delegations)
* [`net::share`](modules/net/share.md) displays the available shares
* [`net::group`](modules/net/group.md) displays the local groups
* [`net::session`](modules/net/session.md) displays the active sessions through [NetSessionEnum()](https://web.archive.org/web/20201201223201/https://docs.microsoft.com/en-us/windows/win32/api/lmshare/nf-lmshare-netsessionenum) Win32 API function
* [`net::wsession`](modules/net/wsession.md) displays the active sessions through [NetWkstaUserEnum()](https://web.archive.org/web/20190909155552/https://docs.microsoft.com/en-us/windows/win32/api/lmwksta/nf-lmwksta-netwkstauserenum) Win32 API function
* [`net::serverinfo`](modules/net/serverinfo.md) displays information about the logged in server

### misc



### event

* [`event::drop`](modules/event/drop.md) patches event services to avoid new events ( :warning: experimental)
* [`event::clear`](modules/event/clear.md) clears a specified event log

### token

The Mimikatz Token module enables Mimikatz to interact with Windows authentication tokens, including grabbing and impersonating existing tokens.

* `token::run` executes a process with its token
* `token::list` lists all tokens on the system.
* `token::revert` reverts to the previous token.
* `token::elevate` can be used to impersonate a token. By default it will elevate permissions to `NT AUTHORITY\SYSTEM`.
* `token::whoami` displays the current token.

### dpapi

### crypto



### service

* `service::-` removes the `mimikatzsvc` service
* `service::+` installs the `mimikatzsvc` service by issuing `rpc::server service::me exit`
* `service::stop` stops a specified service by sending a `SERVICE_CONTROL_STOP` signal
* `service::start` starts a service
* `service::resume` resumes a specified service, after successful suspending, by sending a `SERVICE_CONTROL_CONTINUE` signal
* `service::remove` removes the specified service (It must be used with caution)
* `service::suspend` suspends the specified service. It sends a `SERVICE_CONTROL_PAUSE` signal. It has the following command line argument:
* `service::shutdown` shuts down a specified service by sending a `SERVICE_CONTROL_SHUTDOWN` signal. It has the following command line argument:
* `service::preshutdown` pre-shuts down a specified service by sending a `SERVICE_CONTROL_PRESHUTDOWN` signal. It has the following command line argument:

### process

* `process::run` creates a process by using the [CreateProcessAsUser](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessasusera) Win32 API function. The [CreateEnvironmentBlock](https://docs.microsoft.com/en-us/windows/win32/api/userenv/nf-userenv-createenvironmentblock) is also utilized
* `process::list` lists all the running processes. It uses the [NtQuerySystemInformation](https://docs.microsoft.com/en-us/windows/win32/api/winternl/nf-winternl-ntquerysysteminformation) Windows Native API function.
* `process::runp` runs a subprocess under a parent process (Default parent process is `LSASS.exe`). It can also be used for lateral movement and process spoofing
* `process::stop` terminates a process by using the [NtTerminateProcess](https://www.geoffchappell.com/studies/windows/win32/ntdll/api/native.htm) Windows Native API function. The Win32 API equal one is [TerminateProcess](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-terminateprocess)
* `process::start` starts a process by using the [CreateProcess](https://web.archive.org/web/20170713150625/https://msdn.microsoft.com/en-us/library/windows/desktop/ms682425.aspx) Win32 API function. The `PID` of the process is also displayed
* `process::resume` resumes a suspended process by using the [NtResumeProcess](https://www.geoffchappell.com/studies/windows/win32/ntdll/api/native.htm) Windows Native API function
* `process::exports` lists all the exported functions from the DLLs each running process is using. If a\*\* \*\*`/pid` is not specified, then exports for `mimikatz.exe` will be displayed
* `process::imports` lists all the imported functions from the DLLs each running process is using. If a\*\* \*\*`/pid` is not specified, then imports for `mimikatz.exe` will be displayed
* `process::suspend` suspends a process by using the [NtSuspendProcess](https://ntopcode.wordpress.com/tag/ntsuspendprocess/) Windows Native API function

### privilege

* `privilege::id` requests a privilege by its `id`.
* `privilege::name` requests a privilege by its name
* `privilege::tcb` requests the tcb privilege (`SeTcbPrivilege`)
* `privilege::driver` requests the load driver privilege (`SeLoadDriverPrivilege`)
* `privilege::debug` requests the debug privilege (`SeDebugPrivilege`)
* `privilege::sysenv` requests the system environment privilege (`SeSystemEnvironmentPrivilege`)
* `privilege::restore` requests the restore privilege (`SeRestorePrivilege`)
* `privilege::backup` requests the backup privilege (`SeBackupPrivilege`)
* `privilege::security` requests the security privilege (`SeSecurityPrivilege`)

### sekurlsa



