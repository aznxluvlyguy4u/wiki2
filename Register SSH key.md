# Register SSH key

### Login credentials AWS - Ocean premium (OP)

 - See Lastpass, for the shared AWS credentials of your AWS account

 - OP - AWS login console: https://oceanpremium.signin.aws.amazon.com/console

After logging in, _register your public SSH key_, in OP - _AWS code commit & OpsWorks_:

- AWS code commit:

https://console.aws.amazon.com/iam/home?region=eu-west-1#/security_credentials?credentials=codecommit

- AWS Opsworks:

https://console.aws.amazon.com/opsworks/home?region=eu-west-1#/users/arn%3Aaws%3Aiam%3A%3A469374438605%3Auser%2Fpeter.verkooijen/edit

After registration of your public SSH key, you can SSH into the EC2 instances.

_Note: Make sure to SSH from the whitelisted IP address (JVT Office)_

More information about EC2 SSH key registration process: 
https://stackoverflow.com/c/jongens-van-techniek/questions/98

### Determine IP of target host

Go to AWS EC2 overview, to see the corresponding elastic ip associated to the instance:

https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Instances:sort=instanceId 

or 

https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Addresses:sort=PublicIp

Currently two instances are setup:

- Frontend PRODUCTION
- Frontend STAGING

### SSH 

Finally you can SSH into instance:

```shell
$ ssh iam-username@ip.address
```