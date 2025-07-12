identification
```shell-session
curl -s http://drupal.inlanefreight.local | grep Drupal
```

indexes are through nodes -> page URI `/node/<nodeid>`

Version Identification
```
curl -s http://drupal-acc.inlanefreight.local/CHANGELOG.txt | grep -m2 ""
```

can also do droopescan 
```
droopescan scan drupal -u http://drupal.inlanefreight.local
```
is in the venv