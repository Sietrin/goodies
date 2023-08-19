The main config for Apache is located  ^fb0895
```php
/etc/httpd/conf/httpd.conf
```


**Directory and File Locations**: This part defines the default locations for server files, logs, and error documents. For example:

```php
DocumentRoot "/var/www/html"
ErrorLog "/var/log/httpd/error_log"
```

**AddType** directive in Apache's configuration is used to define custom MIME [[Terminology and misc#^b1248b]] types or to override existing ones. In this case, AddType  adds a new MIME type "application/x-x509-ca-cert" for files with the ".crt" extension.

```php
AddType application/x-x509-ca-cert .crt
```
#### Virtual Hosts 

Allow the server to host multiple websites on the same IP address by responding differently based on the domain name or IP address requested. Each virtual host has its own set of configurations. Virtual Hosts are typically defined inside a **VirtualHost** block, such as:

```php
<VirtualHost *:80>
   ServerName example.com
   DocumentRoot /var/www/example
</VirtualHost>
```


The httpd.conf file might be split into multiple files using the Include directive. For instance, you may see lines like:
```php
Include conf.modules.d/*.conf
IncludeOptional conf.d/*.conf
```

These lines include additional configuration files from the specified directories. The last line of these included files would typically be the closing tag **IfModule** or the closing tag for the respective section, ensuring that everything is correctly encapsulated.

#### Logging levels

In Apache, there are several levels of logging that allow you to control the amount of detail recorded in the log files. The available log levels are (from least verbose to most verbose):

- emerg: Emergencies - System is unusable (highest severity level).
- alert: Alerts - Action must be taken immediately.
- crit: Critical - Critical conditions.
- error: Errors - Error conditions.
- warn: Warnings - Warning conditions.
- notice: Notices - Normal but significant conditions.
- info: Informational - Informational messages.
- debug: Debug - Debug-level messages (most verbose).

To setup logging levels level add to the main config file [[#^fb0895]]:
```php
LogLevel warn
```