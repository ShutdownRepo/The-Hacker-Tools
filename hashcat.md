# 🛠️ hashcat



* to show hash format to provide for a kind of hash

```
hashcat --example-hashes | grep md5 
```
or go to [hashcat example url](https://hashcat.net/wiki/doku.php?id=example_hashes)


* simple use for files /etc/shadow hash
```
hascat -m 7400 ./hashFiles ./WordlistFile.txt
```

* show results
```
haschat -m 20 hashes --show
```

* kdbx files 

```
keepass2john MyPasswordks.kdbx >> keypassHashes
hashcat -m 13400 -O keypass_hashes   rockyou.txt --user
```
user option to skip user identification in file.

* no GPU , no problem
```
./hashcat64.bin -m 0 ./test/sea_hashes.keep.hashes ./test/phpbb.txt -o ./test/wordlist_with2rules.txt --force
```

force options skip GPU usage

* with rules
```
hashcat -m 100 ./hashHugo /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force --user
```