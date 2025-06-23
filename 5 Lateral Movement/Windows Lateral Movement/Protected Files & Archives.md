# finding ssh key
```
grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"
```

can use ssh2john [[John The Ripper]] which generates the corresponding hashes for the encrypted key which we can then crack with johnnie again

```
john ssh.hash --show
```
that will show the ssh password

# Microsoft Office Documents
use `office2john` then john then `--show`

# PDF 
`pdf2john`

# GZIP 
```shell-session
for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null| tar xz;done
```

# VHD
most likely they are encrypted with bitlocker
bitlocker -> john 


the smb share was mounted
```
sudo mkdir -p /mnt/David

sudo mount -t cifs //10.129.202.222/david /mnt/David -o username=david,password=gRzX7YbeTcDG7
```

```
bitlocker2john -i Backup.vhd > backup.hashes
grep "bitlocker\$0" backup.hashes > backup.hash
cat backup.hash
```
the comments above will crack the hash
don't do the bitlocker2john in the /mnt/David


mounting the vhd
```
sudo mkdir /media/backup_bitlocker /media/mount

sudo losetup -P /dev/loop100 /mnt/david/backup.vhd

sudo dislocker -v -V /dev/loop100p2 -u — /media/backup_bitlocker

sudo mount -o loop,rw /media/backup_bitlocker/dislocker-file /media/mount
```


try to hashcat that
```shell-session
hashcat -m 22100 backup.hash /usr/share/wordlists/rockyou.txt -o backup.cracked
```

