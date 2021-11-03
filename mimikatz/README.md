# 🛠️ Mimikatz 🥝

What is Mimikatz?

## Modules

### ts

placeholder: what is the purpose of ts

* ``[`ts::mstsc`](modules/ts/mstsc.md) can be used to extract cleartext credentials from the mstsc process (client side)
* ``[`ts::remote`](modules/ts/remote.md) can be used to perform RDP takeover/hijacking of active sessions
* ``[`ts::multirdp`](modules/ts/multirdp.md) can be used to enable multiple RDP connections on the target server
* ``[`ts::sessions`](modules/ts/sessions.md) can be used to list the current RDP sessions. It comes in handy for RDP hijacking
* ``[`ts::logonpasswords`](modules/ts/logonpasswords.md) module extracts clear text credentials from RDP running sessions (server side)

### sid

placeholder: what is the purpose of sid

* ``[`sid::add`](modules/sid/add.md) can be used to add a SID to `sIDHistory` of an object
* ``[`sid::clear`](modules/sid/clear.md) can be used to clear the `sIDHistory` of a target object
* ``[`sid::patch`](modules/sid/patch.md) can be used to patch the NTDS (NT Directory Services). It's useful when running [`sid::modify`](modules/sid/modify.md) or [`sid::add`](modules/sid/add.md)
* ``[`sid::query`](modules/sid/query.md) can be used to query an object by its SID or name
* ``[`sid::lookup`](modules/sid/lookup.md) can be used to lookup an object by its SID or name
* ``[`sid::modify`](modules/sid/modify.md) can be used to modify an object's SID

### rpc

placeholder: what is the purpose&#x20;

* ``[`rpc::close`](modules/rpc/close.md)` `can be used to close remote RPC sessions
* ``[`rpc::enum`](modules/rpc/enum.md) can be used to enumerate RPC endpoints on a system
* ``[`rpc::server`](modules/rpc/server.md) can be used to start an RPC server
* ``[`rpc::connect`](modules/rpc/connect.md) be used to connect to an RPC endpoint

### net

placeholder: what is the purpose&#x20;

* ``[`net::if`](modules/net/if.md) displays the available local IP addresses and the hostname
* ``[`net::tod`](modules/net/tod.md) displays the current time
* ``[`net::user`](modules/net/user.md) displays the local users
* ``[`net::alias`](modules/net/alias.md) displays more information about the local group memberships including Remote Desktop Users, Distributed COM Users, etc.
* ``[`net::trust`](modules/net/trust.md) displays information for the active directory forest trust(s)
* ``[`net::stats`](modules/net/stats.md) displays when the target was booted
* ``[`net::deleg`](modules/net/deleg.md) checks for the following types of [Kerberos delegations](https://www.thehacker.recipes/ad-ds/movement/kerberos/delegations)
* ``[`net::share`](modules/net/share.md) displays the available shares
* ``[`net::group`](modules/net/group.md) displays the local groups
* ``[`net::session`](modules/net/session.md) displays the active sessions through [NetSessionEnum()](https://web.archive.org/web/20201201223201/https://docs.microsoft.com/en-us/windows/win32/api/lmshare/nf-lmshare-netsessionenum) Win32 API function
* ``[`net::wsession`](modules/net/wsession.md) displays the active sessions through [NetWkstaUserEnum()](https://web.archive.org/web/20190909155552/https://docs.microsoft.com/en-us/windows/win32/api/lmwksta/nf-lmwksta-netwkstauserenum) Win32 API function
* ``[`net::serverinfo`](modules/net/serverinfo.md) displays information about the logged in server

### misc

placeholder: what is the purpose&#x20;

*

### event

placeholder: what is the purpose&#x20;

* ``[`event::drop`](modules/event/drop.md) can be used to patch event services to avoid new events ( :warning: experimental)
* ``[`event::clear`](modules/event/clear.md) clears a specified event log

### token

The Mimikatz Token module enables Mimikatz to interact with Windows authentication tokens, including grabbing and impersonating existing tokens.

*

### dpapi

placeholder: what is the purpose&#x20;

*
