# bootkey

It sets the SecureKernel Boot Key and attempts to decrypt LSA Isolated credentials. It has the following command line arguments:

* `/new`: the new Boot key value
* `/raw`: RAW memory search for candidate keys in cache
* `/flush`: it flushes cache

```
mimikatz # sekurlsa::bootkey

Candidate keys in cache:

Current IumMkPerBoot: <none>
```
