 The **apachectl** is a command-line utility that provides various management functions for the Apache HTTP Server. Syntax example:
 ```bash
 apachectl start/stop/restart
```

**Difference between restart and graceful**: The restart command stops and then starts the Apache server, which may result in some downtime during the restart process. On the other hand, graceful is a more controlled approach. It allows Apache to finish processing the current requests before restarting, resulting in smoother transitions with minimal or no downtime. 
```
apachectl graceful
```

**Syntax Check**: To check the syntax of your Apache configuration files, use the following command:
```
apachectl configtest
```


- **apachectl -M** Show Loaded Modules: To display a list of all loaded Apache modules, use the following command:
- **apachectl -V** Show Version: To display the Apache server version and build details, use the following command:
- **apachectl -S** list of all configured virtual hosts, their corresponding ports, and the configuration files where they are defined
