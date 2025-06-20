### Show available NFS Shares 
```shell-session
showmount -e 10.129.14.128
```

### Mount NFS Share 
```
mkdir target-NFS
sudo mount -t nfs ip.addr:/ ./target-NFS/ -o nolock 
cd target-NFS 
tree . 
```
If the `root_squash` option is set, we cannot edit the files that are owned by root even as `root`.

### Unmounting 
```
sudo umount ./target-NFS
```

