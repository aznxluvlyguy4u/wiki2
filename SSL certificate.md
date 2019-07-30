# SSL Certificate

The production frontend (https://rental.oceanpremium.com) is configured with an SSL certificate generated via: letsencrypt.org

*Note: the **SSL certificate expires every 90 days**, therefore we setup an auto-renewal certbot, see [here](markdown-header-auto-renewal--certbot)*

### SSL report

https://www.ssllabs.com/ssltest/analyze.html?d=rental.oceanpremium.com


### Installing certbot

- Install certbot:

```
$ sudo add-apt-repository ppa:certbot/certbot
```

```
$ sudo apt install python-certbot-apache
```

### Configure virtual host

- See [here](https://bitbucket.org/jvt/ocean-premium-frontend/wiki/Apache#markdown-header-virtual-host) for instructions.

- Make sure to set the _serverName_ to the **correct** domain (i.e.: rental.oceanpremium.com)

- More information: https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04

* _note:_ **Again**: the _serverName_ in the virtualhost conf file, needs to match the domain for which the SSL certificate is generated.

```
$ sudo certbot --apache -d rental.oceanpremium.com
```

#### Output
```
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel): steven@jongensvantechniek.nl

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v02.api.letsencrypt.org/directory
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(A)gree/(C)ancel: A

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: N
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for rental.oceanpremium.com
Waiting for verification...
Cleaning up challenges
Created an SSL vhost at /etc/apache2/sites-available/rental.oceanpremium.com-le-ssl.conf
Enabled Apache socache_shmcb module
Enabled Apache ssl module
Deploying Certificate to VirtualHost /etc/apache2/sites-available/rental.oceanpremium.com-le-ssl.conf
Enabling available site: /etc/apache2/sites-available/rental.oceanpremium.com-le-ssl.conf

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
Redirecting vhost in /etc/apache2/sites-enabled/rental.oceanpremium.com.conf to ssl vhost in /etc/apache2/sites-available/rental.oceanpremium.com-le-ssl.conf

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations! You have successfully enabled https://rental.oceanpremium.com

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=rental.oceanpremium.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/rental.oceanpremium.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/rental.oceanpremium.com/privkey.pem
   Your cert will expire on 2019-10-28. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
 - Your account credentials have been saved in your Certbot
   configuration directory at /etc/letsencrypt. You should make a
   secure backup of this folder now. This configuration directory will
   also contain certificates and private keys obtained by Certbot so
   making regular backups of this folder is ideal.
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

## EC2 Security Group settings 

- Make sure to add an _inbound rule_ for port 443 (https)

See here: https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#SecurityGroups:sort=groupId

The concerning security group is: _JVT EC2_

## Auto-renewal certbot

Because letsencrypt **generated SSL certificates expire every 90 days**, we need to setup auto-renewal.