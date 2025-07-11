## Extension Fuzzing
before we start, we must find out what types of pages the website uses, like `.html`, `.aspx`, `.php`, or something else.
```shell-session
ffuf -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://83.136.255.218:50935/indexFUZZ -ic
```


## Recursive Scanning 
```shell-session
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://academy.htb:39395/FUZZ -recursion -recursion-depth 1 -e .php -v -ic
```
you can add multiple extensions at the back also, but its a bit unreliable so might have to just manually use the add in the extensions

## Directory Fuzzing
```shell-session
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -ic
```


## Page Fuzzing
```shell-session
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://academy.htb/FUZZ.php -ic
```
