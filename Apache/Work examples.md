# Virtual Hosts setup

To set up a VirtualHost with the domain name vh1.my that uses a separate document root and handles all HTTP requests from all network interfaces, you'll need to follow these steps:

### Create the VirtualHost Configuration

```
sudo vi /etc/httpd/conf/httpd.conf
```

At the end of the file or within the VirtualHost section, add the following configuration for vh1.my:
```
<VirtualHost *:80>
	ServerName vh1.my
	DocumentRoot /var/www/vh1.my

	# Additional directives, if needed

	# Log files
	ErrorLog /var/log/httpd/vh1.my_error.log
	CustomLog /var/log/httpd/vh1.my_access.log combined
</VirtualHost>

```

This sets up a VirtualHost that listens on port 80 (*:80) for all network interfaces and points the DocumentRoot to /var/www/vh1.my. You can modify the DocumentRoot to the directory where you want to host the website content.

### Create the Document Root Directory

Create the directory specified as DocumentRoot in the configuration:

```
sudo mkdir -p /var/www/vh1.my
```

Set appropriate permissions so that the Apache process can access the files:

```
sudo chown -R apache:apache /var/www/vh1.my
```

### Enable the VirtualHost and Restart Apache

Enable the VirtualHost configuration using a2ensite (RHEL uses the a2ensite command for enabling VirtualHosts):
```
sudo a2ensite vh1.my
```

Restart Apache to apply the changes:

```
sudo systemctl restart httpd
```
