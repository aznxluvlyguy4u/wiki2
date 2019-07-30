## Apache

### Installation

```shell
$ sudo apt-get install apache2
```

Verify that apache is properly started

```shell
$ sudo systemctl status apache2
```

### Output

```shell
● apache2.service - LSB: Apache2 web server
   Loaded: loaded (/etc/init.d/apache2; bad; vendor preset: enabled)
  Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
   Active: active (running) since Thu 2018-08-09 16:59:04 CEST; 17min ago
     Docs: man:systemd-sysv-generator(8)
  Process: 1542 ExecStop=/etc/init.d/apache2 stop (code=exited, status=0/SUCCESS)
  Process: 1575 ExecStart=/etc/init.d/apache2 start (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/apache2.service
           ├─1593 /usr/sbin/apache2 -k start
           ├─1596 /usr/sbin/apache2 -k start
           ├─1597 /usr/sbin/apache2 -k start
           ├─1598 /usr/sbin/apache2 -k start
           ├─1599 /usr/sbin/apache2 -k start
           └─1600 /usr/sbin/apache2 -k start

Aug 09 16:59:03 ubuntu systemd[1]: Starting LSB: Apache2 web server...
Aug 09 16:59:03 ubuntu apache2[1575]:  * Starting Apache httpd web server apache2
Aug 09 16:59:03 ubuntu apache2[1575]: AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this m
Aug 09 16:59:04 ubuntu apache2[1575]:  *
Aug 09 16:59:04 ubuntu systemd[1]: Started LSB: Apache2 web server.
```

### Version checking

```shell
$ apache2 -v
```

```shell
Server version: Apache/2.4.18 (Ubuntu)
Server built:   2018-06-07T19:43:03
```

### Virtual host

```shell
$ sudo touch /etc/apache2/sites-available/<service>.<domain>.com.conf
$ sudo nano /etc/apache2/sites-available/<service>.<domain>.com.conf
```

### Proxy requests

In order to proxy all incoming requests to the nodeJs application, enable proxy:

```
$ a2enmod proxy && a2enmod proxy_http
```

#### Production

Paste and fit changes to your needs, this example is configured for Ocean Premium - ***Production without SSL*** environment:

```conf
<VirtualHost *:80>
    ServerAdmin admin@oceanpremium.com
    ServerName rental.oceanpremium.com

    ProxyRequests off

    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>

    <Location />
        ProxyPass http://localhost:3000/
        ProxyPassReverse http://localhost:3000/
    </Location>

    # Redirect ip address call to dns
    RewriteCond %{HTTP_HOST} ^34\.255\.133\.117$
    RewriteRule ^(.*)$ https//rental.oceanpremium.com$1 [L,R=301]
</VirtualHost>
```

- Where _http://localhost:3000/_ is the host and port the NodeJS express server is listening for incoming requests.

- Where _{HTTP_HOST}_ points to the IP address of the server

### With SSL

See [these](SSL%20certificate) instructions for SSL certificate.

The following configuration *redirects all HTTP to HTTPS* and uses an SSL certificate generated with letsencrypt.

Paste and fit changes to your needs, this example is configured for Ocean Premium - ***Production with SSL*** environment:

```
<VirtualHost *:80>
    ServerAdmin admin@oceanpremium.com
    ServerName rental.oceanpremium.com

    ProxyRequests off

    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>

    <Location />
        ProxyPass http://localhost:3000/
        ProxyPassReverse http://localhost:3000/
    </Location>
    
    # Redirect all http requests to https
    RewriteEngine on
    RewriteCond %{SERVER_NAME} =rental.oceanpremium.com
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
    
    # Redirect ip address call to dns
    RewriteCond %{HTTP_HOST} ^34\.255\.133\.117$
    RewriteRule ^(.*)$ https://rental.oceanpremium.com$1 [L,R=301]
</VirtualHost>
```

- Where _http://localhost:3000/_ is the host and port the NodeJS express server is listening for incoming requests.

- Where _{HTTP_HOST}_ points to the IP address of the server

- Where _{SERVER_NAME}_ points to the DNS, that points to IP address of server

Disable default apache config:

```shell
$ a2dissite 000-default
```

Enable custom api config:

```shell
$ sudo a2ensite <service>.<domain>.com
$ apachectl configtest
$ sudo a2enmod rewrite
$ sudo systemctl restart apache2
```