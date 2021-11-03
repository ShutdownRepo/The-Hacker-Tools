# 🛠️ Impacket

Impacket is a collection of Python classes for working with network protocols. Impacket is focused on providing low-level programmatic access to the packets and for some protocols (e.g. SMB1-3 and MSRPC) the protocol implementation itself.

Packets can be constructed from scratch, as well as parsed from raw data, and the object oriented API makes it simple to work with deep hierarchies of protocols. The library provides a set of tools as examples of what can be done within the context of this library.

## Library

///// placeholder

## PLACEHOLDER

* **Quick start**: Click the following link to obtain the latest version [gzip’d tarbal](https://github.com/SecureAuthCorp/impacket/releases/download/impacket\_0\_9\_22/impacket-0.9.22.tar.gz)
* **Requirements**: [Python](http://www.python.org) interpreter (version 2.7, 3.6, 3.7, 3.8 or 3.9). [Third-party](https://github.com/SecureAuthCorp/impacket/blob/master/requirements.txt) packages also needed.
* **Installing**: In order to install the code, execute `python setup.py install` or from the directory you placed it `python -m pip install`\*\* **\_**.\*\*\_

## PLACEHOLDER

#### The following protocols are featured in Impacket <a href="toc1" id="toc1"></a>

* Ethernet, Linux “Cooked” capture.
* IP, TCP, UDP, ICMP, IGMP, ARP.
* IPv4 and IPv6 Support.
* NMB and SMB1, SMB2 and SMB3 (high-level implementations).
* MSRPC version 5, over different transports: TCP, SMB/TCP, SMB/NetBIOS and HTTP.
* Plain, NTLM and Kerberos authentications, using password/hashes/tickets/keys.
* Portions/full implementation of the following MSRPC interfaces: EPM, DTYPES, LSAD, LSAT, NRPC, RRP, SAMR, SRVS, WKST, SCMR, DCOM, WMI
* Portions of TDS (MSSQL) and LDAP protocol implementations.

The following tools are featured in Impacket

## Script examples

### **Remote Execution**

* [psexec.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/psexec.py) PSEXEC like functionality example using RemComSvc ([https://github.com/kavika13/RemCom](https://github.com/kavika13/RemCom)).
* [smbexec.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/smbexec.py) A similar approach to PSEXEC w/o using RemComSvc. The technique is described [here](https://web.archive.org/web/20140625065218/http://blog.accuvant.com/rdavisaccuvant/owning-computers-without-shell-access/). Our implementation goes one step further, instantiating a local smbserver to receive the output of the commands. This is useful in the situation where the target machine does NOT have a writeable share available.
* [atexec.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/atexec.py) This example executes a command on the target machine through the Task Scheduler service and returns the output of the executed command.
* [wmiexec.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/wmiexec.py) A semi-interactive shell, used through Windows Management Instrumentation. It does not require to install any service/agent at the target server. Runs as Administrator. Highly stealthy.
* [dcomexec.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/dcomexec.py) A semi-interactive shell similar to wmiexec.py, but using different DCOM endpoints. Currently supports MMC20.Application, ShellWindows and ShellBrowserWindow objects.

### **Kerberos**

* [GetTGT.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/getTGT.py) Given a password, hash or aesKey, this script will request a TGT and save it as ccache.
* [GetST.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/getST.py) Given a password, hash, aesKey or TGT in ccache, this script will request a Service Ticket and save it as ccache. If the account has constrained delegation (with protocol transition) privileges you will be able to use the -impersonate switch to request the ticket on behalf another user.
* [GetPac.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/getPac.py) This script will get the PAC (Privilege Attribute Certificate) structure of the specified target user just having a normal authenticated user credentials. It does so by using a mix of \[MS-SFU]’s S4USelf + User to User Kerberos Authentication.
* [GetUserSPNs.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/GetUserSPNs.py) This example will try to find and fetch Service Principal Names that are associated with normal user accounts. Output is compatible with JtR and HashCat.
* [GetNPUsers.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/GetNPUsers.py) This example will attempt to list and get TGTs for those users that have the property ‘Do not require Kerberos preauthentication’ set (UF\_DONT\_REQUIRE\_PREAUTH). Output is compatible with JtR.
* [ticketConverter.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/ticketConverter.py): This script will convert kirbi files, commonly used by mimikatz, into ccache files used by Impacket, and vice versa.
* [ticketer.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/ticketer.py) This script will create Golden/Silver tickets from scratch or based on a template (legally requested from the KDC) allowing you to customize some of the parameters set inside the PAC\_LOGON\_INFO structure, in particular the groups, ExtraSids, duration, etc.
* [raiseChild.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/raiseChild.py) This script implements a child-domain to forest privilege escalation by (ab)using the concept of Golden Tickets and ExtraSids.

### **Windows Secrets**

* [secretsdump.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/secretsdump.py) Performs various techniques to dump secrets from the remote machine without executing any agent there. For SAM and LSA Secrets (including cached creds) we try to read as much as we can from the registry and then we save the hives in the target system (%SYSTEMROOT%\Temp directory) and read the rest of the data from there. For DIT files, we dump NTLM hashes, Plaintext credentials (if available) and Kerberos keys using the DL\_DRSGetNCChanges() method. It can also dump NTDS.dit via vssadmin executed with the smbexec/wmiexec approach. The script initiates the services required for its working if they are not available (e.g. Remote Registry, even if it is disabled). After the work is done, things are restored to the original state.
* [mimikatz.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/mimikatz.py) Mini shell to control a remote mimikatz RPC server developed by @gentilkiwi.

### **Server Tools/MiTM Attacks**

* [ntlmrelayx.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/ntlmrelayx.py) This script performs NTLM Relay Attacks, setting an SMB and HTTP Server and relaying credentials to many different protocols (SMB, HTTP, MSSQL, LDAP, IMAP, POP3, etc.). The script can be used with predefined attacks that can be triggered when a connection is relayed (e.g. create a user through LDAP) or can be executed in SOCKS mode. In this mode, for every connection relayed, it will be available to be used later on multiple times through a SOCKS proxy.
* [karmaSMB.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/karmaSMB.py) A SMB Server that answers specific file contents regardless of the SMB share and pathname specified.
* [smbserver.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/smbserver.py) A Python implementation of an SMB server. Allows to quickly set up shares and user accounts.

### **WMI**

* [wmiquery.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/wmiquery.py) It allows to issue WQL queries and get description of WMI objects at the target system (e.g. select name from win32\_account).
* [wmipersist.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/wmipersist.py) This script creates/removes a WMI Event Consumer/Filter and link between both to execute Visual Basic based on the WQL filter or timer specified.

### **Known Vulnerabilities**

* [goldenPac.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/goldenPac.py) Exploit for MS14-068. Saves the golden ticket and also launches a PSEXEC session at the target.
* [sambaPipe.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/sambaPipe.py) This script will exploit CVE-2017-7494, uploading and executing the shared library specified by the user through the -so parameter.
* [smbrelayx.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/smbrelayx.py) Exploit for CVE-2015-0005 using a SMB Relay Attack. If the target system is enforcing signing and a machine account was provided, the module will try to gather the SMB session key through NETLOGON.

### **SMB/MSRPC**

* [smbclient.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/smbclient.py) A generic SMB client that will let you list shares and files, rename, upload and download files and create and delete directories, all using either username and password or username and hashes combination. It’s an excellent example to see how to use impacket.smb in action.
* [addcomputer.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/addcomputer.py): Allows to add a computer to a domain using LDAP or SAMR (SMB).
* [getArch.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/getArch.py) This script will connect against a target (or list of targets) machine/s and gather the OS architecture type installed by (ab)using a documented MSRPC feature.
* [exchanger.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/exchanger.py): A tool for connecting to MS Exchange via RPC over HTTP v2.
* [lookupsid.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/lookupsid.py) A Windows SID brute forcer example through \[MS-LSAT] MSRPC Interface, aiming at finding remote users/groups.
* [netview.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/netview.py) Gets a list of the sessions opened at the remote hosts and keep track of them looping over the hosts found and keeping track of who logged in/out from remote servers
* [reg.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/reg.py) Remote registry manipulation tool through the \[MS-RRP] MSRPC Interface. The idea is to provide similar functionality as the REG.EXE Windows utility.
* [rpcdump.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/rpcdump.py) This script will dump the list of RPC endpoints and string bindings registered at the target. It will also try to match them with a list of well known endpoints.
* [rpcmap.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/rpcmap.py): Scan for listening DCE/RPC interfaces. This binds to the MGMT interface and gets a list of interface UUIDs. If the MGMT interface is not available, it takes a list of interface UUIDs seen in the wild and tries to bind to each interface.
* [samrdump.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/samrdump.py) An application that communicates with the Security Account Manager Remote interface from the MSRPC suite. It lists system user accounts, available resource shares and other sensitive information exported through this service.
* [services.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/services.py) This script can be used to manipulate Windows services through the \[MS-SCMR] MSRPC Interface. It supports start, stop, delete, status, config, list, create and change.
* [smbpasswd.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/smbpasswd.py): This script is an alternative to smbpasswd tool and intended to be used for changing expired passwords remotely over SMB (MSRPC-SAMR)

### **MSSQL / TDS**

* [mssqlinstance.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/mssqlinstance.py) Retrieves the MSSQL instances names from the target host.
* [mssqlclient.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/mssqlclient.py) An MSSQL client, supporting SQL and Windows Authentications (hashes too). It also supports TLS.

### **File Formats**

* [esentutl.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/esentutl.py) An Extensibe Storage Engine format implementation. Allows dumping catalog, pages and tables of ESE databases (e.g. NTDS.dit)
* [ntfs-read.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/ntfs-read.py) NTFS format implementation. This script provides a mini shell for browsing and extracting an NTFS volume, including hidden/locked contents.
* [registry-read.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/registry-read.py) A Windwows Registry file format implementation. It allows to parse offline registry hives.

### **Other**

* [findDelegation.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/findDelegation.py): Simple script to quickly list all delegation relationships (unconstrained, constrained, resource-based constrained) in an AD environment.
* [GetADUsers.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/GetADUsers.py) This script will gather data about the domain’s users and their corresponding email addresses. It will also include some extra information about last logon and last password set attributes.
* [Get-GPPPassword.py](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/Get-GPPPassword.py): This example extracts and decrypts Group Policy Preferences passwords using streams for treating files instead of mounting shares. Additionally, it can parse GPP XML files offline.
* [mqtt\_check.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/mqtt\_check.py) Simple MQTT example aimed at playing with different login options. Can be converted into a account/password brute forcer quite easily.
* [rdp\_check.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/rdp\_check.py) \[MS-RDPBCGR] and \[MS-CREDSSP] partial implementation just to reach CredSSP auth. This example tests whether an account is valid on the target host.
* [sniff.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/sniff.py) Simple packet sniffer that uses the pcapy library to listen for packets in # transit over the specified interface.
* [sniffer.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/sniffer.py) Simple packet sniffer that uses a raw socket to listen for packets in transit corresponding to the specified protocols.
* [ping.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/ping.py) Simple ICMP ping that uses the ICMP echo and echo-reply packets to check the status of a host. If the remote host is up, it should reply to the echo probe with an echo-reply packet.
* [ping6.py:](https://github.com/SecureAuthCorp/impacket/blob/impacket\_0\_9\_23/examples/ping6.py) Simple IPv6 ICMP ping that uses the ICMP echo and echo-reply packets to check the status of a host.

## Resource

{% embed url="https://www.secureauth.com/labs/open-source-tools/impacket/" %}
