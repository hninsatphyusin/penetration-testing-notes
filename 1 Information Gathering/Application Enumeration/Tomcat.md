Java? 

Identified by Server Header in HTTP response,

request an invalid page and it should reveal the server and version 

thru docs
```
curl -s http://web01.inlanefreight.local:8180/docs/ | grep Tomcat 
```

enumeration using dirbuster
```shell-session
gobuster dir -u http://web01.inlanefreight.local:8180/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt 
```

general folder structure of Tomcat Installation
```shell-session
├── bin
├── conf
│   ├── catalina.policy
│   ├── catalina.properties
│   ├── context.xml
│   ├── tomcat-users.xml
│   ├── tomcat-users.xsd
│   └── web.xml
├── lib
├── logs
├── temp
├── webapps
│   ├── manager
│   │   ├── images
│   │   ├── META-INF
│   │   └── WEB-INF
|   |       └── web.xml
│   └── ROOT
│       └── WEB-INF
└── work
    └── Catalina
        └── localhost
```
tomat-users.xml -> used to allow or disallow access to /manger and host-manager, can see passwords also -> try to login using tomcat:tomcat or admin:admin

each folder in webapps
```shell-session
webapps/customapp
├── images
├── index.jsp
├── META-INF
│   └── context.xml
├── status.xsd
└── WEB-INF
    ├── jsp
    |   └── admin.jsp
    └── web.xml
    └── lib
    |    └── jdbc_drivers.jar
    └── classes
        └── AdminServlet.class 
```

1. its important to see the web.xml file (esp if got LFI)
2. Check the classes folder for compiled vulnerable classes too

if the class name is `com.inlanefreight.api.AdminServlet` then the path would be `classes/com/inlanefreight/api/AdminServlet.class`