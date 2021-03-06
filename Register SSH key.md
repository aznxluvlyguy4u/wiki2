# Register SSH key

### Login credentials AWS - Ocean premium (OP)

 - See Lastpass, for the shared AWS credentials of your AWS account

 - OP - AWS login console: https://oceanpremium.signin.aws.amazon.com/console

After logging in, _register your public SSH key_, in OP - _AWS code commit & OpsWorks_:

- AWS code commit:

https://console.aws.amazon.com/iam/home?region=eu-west-1#/security_credentials?credentials=codecommit

- AWS Opsworks:

https://console.aws.amazon.com/opsworks/home?region=eu-west-1#/users

- Select _edit_ for your user name and paste in public SSH key

After registration of your public SSH key, you can SSH into the EC2 instances.

_Note: Make sure to SSH from the whitelisted IP address (JVT Office)_

More information about EC2 SSH key registration process: 
https://stackoverflow.com/c/jongens-van-techniek/questions/98

### Determine IP of target host

Currently two instances are setup:

- Frontend PRODUCTION

```
 34.255.133.117
```

- Frontend STAGING: 

```
99.80.168.39
```

If IP address are not working, go to AWS EC2 overview, to see the actual corresponding elastic ip associated to the instance:

https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Instances:sort=instanceId 

or 

https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Addresses:sort=PublicIp

### SSH 

Finally you can SSH into instance:

```shell
$ ssh username@ip.address
```

When successfully ssh'd into server, continue with [Deploying to remote instructions](Remote%20deploying)