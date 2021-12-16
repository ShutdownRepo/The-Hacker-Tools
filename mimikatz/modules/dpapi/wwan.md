# wwan

`dpapi::wwman` decrypts Wwan credentials. It has the following command line argument:

* `/in`: The Wwan XML profile. The XML file location is `C:\ProgramData\Microsoft\Wlansvc\Profiles{interface guid}\*.xml`
* `/password`: the password to decrypt the wwan credentials
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

```
mimikatz# dpapi::wwan /in:"C:\ProgramData\Microsoft\Wlansvc\Profiles{interface guid}\*.xml" /unprotect
```
