1. Run subdomin/vhost fuzzing
	1. Add all of the new domains into /etc/hosts
2. Run extension fuzzing scan on all found domains
3. Then do directory recursion
4. Run page fuzzing scan on all domains, on all extensions
5. Once you get a page, do get and post request parameter fuzzing