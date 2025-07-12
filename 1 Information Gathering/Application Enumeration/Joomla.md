identification
```shell-session
curl -s http://dev.inlanefreight.local/ | grep Joomla
```
check robots.txt

check for version in README.txt
```shell-session
curl -s http://dev.inlanefreight.local/README.txt | head -n 5
```
or through media/system/js or administrator/manifests/files/joomla.xml or plugins/system/cache/cache.xml

```shell-session
curl -s http://dev.inlanefreight.local/administrator/manifests/files/joomla.xml | xmllint --format -
```

## droopescan 
```shell-session
droopescan scan joomla --url http://dev.inlanefreight.local/
```

## Joomlascan
```shell-session
python2.7 joomlascan.py -u http://dev.inlanefreight.local
```