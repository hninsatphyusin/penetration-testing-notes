common web ports
```shell-session
nmap -p 80,443,8000,8080,8180,8888,10000 --open -oA web_discovery -iL scope_list
```

cat scope_list
```
app.inlanefreight.local
dev.inlanefreight.local
drupal-dev.inlanefreight.local
drupal-qa.inlanefreight.local
drupal-acc.inlanefreight.local
drupal.inlanefreight.local
blog-dev.inlanefreight.local
blog.inlanefreight.local
app-dev.inlanefreight.local
jenkins-dev.inlanefreight.local
jenkins.inlanefreight.local
web01.inlanefreight.local
gitlab-dev.inlanefreight.local
gitlab.inlanefreight.local
support-dev.inlanefreight.local
support.inlanefreight.local
inlanefreight.local
10.129.201.50
```

whenever we find new domain, we just add it into the scope_list

quickly adding them all to /etc/hosts
```shell-session
printf "%s\t%s\n\n" "$IP" "app.inlanefreight.local dev.inlanefreight.local blog.inlanefreight.local" | sudo tee -a /etc/hosts
```

## Getting screenshots of the web app
go to ~/PT/EyeWitness
```shell-session
EyeWitness.py --web -x web_discovery.xml -d inlanefreight_eyewitness
```

Running aquatone
```shell-session
cat web_discovery.xml | ./aquatone -nmap
```
web_discovery.xml is the output of nmap in xml

read the report.html in the EyeWitness