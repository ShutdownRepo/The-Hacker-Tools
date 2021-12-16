# luna

`dpapi::luna` decrypts Safenet LunaHSM KSP. It has the following command line arguments:

* `/hive`: TODO
* `/client`: TODO
* `/password`: the password to decrypt the LunaHSM
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen
