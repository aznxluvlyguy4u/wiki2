# Register SSH key & deploy instructions - On boarding

###Login credentials AWS - Ocean premium (OP)

 - Zie Lastpass (invite aan: peter@peershaped.nl)

 - OP - AWS login console: https://oceanpremium.signin.aws.amazon.com/console

Na inloggen, _registreer je public SSH key_, in OP - _AWS code commit en Opsworks_:

- AWS code commit:

https://console.aws.amazon.com/iam/home?region=eu-west-1#/security_credentials?credentials=codecommit

- AWS Opsworks:

https://console.aws.amazon.com/opsworks/home?region=eu-west-1#/users/arn%3Aaws%3Aiam%3A%3A469374438605%3Auser%2Fpeter.verkooijen/edit

Na registratie van je public SSH key, kan je SSH-en naar de EC2 instances

_Note: Let wel op dat SSH gebeurt vanaf IP adres van JVT kantoor, mocht je een ander adres
willen whitelisten, laat dat dan even aan mij weten._

Achtergrond informatie: EC2 SSH key registratie: https://stackoverflow.com/c/jongens-van-techniek/questions/98

### Voorbeeld

```shell
$ ssh iam-username@ip.address
```

#### Staging

```shell
ssh peterverkooijen@99.80.168.39
```

#### Production

```shell
ssh peterverkooijen@34.255.133.117
```

_Note: Bovenstaande stappen zijn door mij getest en gevalideerd (met eigen SSH key onder jouw account) en heb de conclusie
dat bovenstaande stappen correct zijn en leiden tot succesvol SSH-en, mits je de stappen correct opvolgd en een valide SSH key 
registreert._

### Deployen frontend

Na succesvol SSH-en naar EC2 instance, volg de volgende procedure om de frontend te deployen:

https://bitbucket.org/jvt/ocean-premium-frontend/wiki/Remote%20deploying