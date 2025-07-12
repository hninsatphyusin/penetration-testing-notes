Identify it by going to /robots.txt
it will look like this: 
```shell-session
User-agent: *
Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php
Disallow: /wp-content/uploads/wpforms/

Sitemap: https://inlanefreight.local/wp-sitemap.xml
```
or do this: 
```shell-session
curl -s http://blog.inlanefreight.local | grep WordPress
```

check 
- wp-admin/
- wp-content/plugins
- wp-content/themes
- wp-sitemap.xml
for vulnerable stuff

```shell-session
curl -s http://blog.inlanefreight.local/ | grep themes
```


```shell-session
curl -s http://blog.inlanefreight.local/ | grep plugins
```

to get more information you can go to `/wp-content/plugins/plugin-name/readme.txt`
## WP Scan 
you have to create an account here and use the api token [WPVulnDB](https://wpvulndb.com/)

```shell-session
sudo wpscan --url http://blog.inlanefreight.local --enumerate --api-token dEOFB<SNIP>
```