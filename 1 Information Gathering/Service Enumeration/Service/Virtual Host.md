
|Tool|Description|Features|
|---|---|---|
|[gobuster](https://github.com/OJ/gobuster)|A multi-purpose tool often used for directory/file brute-forcing, but also effective for virtual host discovery.|Fast, supports multiple HTTP methods, can use custom wordlists.|
|[Feroxbuster](https://github.com/epi052/feroxbuster)|Similar to Gobuster, but with a Rust-based implementation, known for its speed and flexibility.|Supports recursion, wildcard discovery, and various filters.|
|[ffuf](https://github.com/ffuf/ffuf)|Another fast web fuzzer that can be used for virtual host discovery by fuzzing the `Host` header.|Customizable wordlist input and filtering options.|

### gobuster

add the domain name and the ip address to the /etc/host file first 

```shell-session
gobuster vhost -u http://<target_IP_address> -w <wordlist_file> --append-domain
```

```shell-session
gobuster vhost -u http://inlanefreight.htb:32023 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain
```


- Consider using the `-t` flag to increase the number of threads for faster scanning.
- The `-k` flag can ignore SSL/TLS certificate errors.
- You can use the `-o` flag to save the output to a file for later analysis.