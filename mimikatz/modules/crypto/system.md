# system

`crypto::system` it describes a Windows System Certificate. It as the following command line arguments:

* `/file:` the path of the certificate
* `/export:` export to a _**.der**_ file

The following output was taken from [this](https://tinyapps.org/docs/decrypt-efs-without-cert-backup.html) guide:

```
mimikatz # crypto::system /file:"SystemCertificates\My\Certificates\096BA4D021B50F5E78F2B9854A7461678EDAA006" /export
...
        Key Container  : d209e940-6952-4c9d-b906-372d5a3dbd50
        Provider       : Microsoft Enhanced Cryptographic Provider v1.0
...
  Saved to file: 096BA4D021B50F5E78F2B9854A7461678EDAA006.der
```
