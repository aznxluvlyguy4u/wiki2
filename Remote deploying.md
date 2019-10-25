# Remote deploying

| Table of Content                                                             |
|------------------------------------------------------------------------------|
| 0. [Prerequisites](#markdown-header-prerequisites)           |
| 1. [SSH-ing into server](#markdown-header-1-ssh-ing-into-server)     |
| 2. [Attach or create new Tmux session](#markdown-header-2-attach-or-create-new-tmux-session)|                   
| 3. [Navigate to the web app](#markdown-header-3-navigate-to-the-web-app)|
| 4. [Deploy frontend](#markdown-header-4-get-latest-changes)
| 5. [Detach from Tmux session](#markdown-header-5-detach-from-tmux-session)|
| 6. [Verification](#markdown-header-verification)|

## Prerequisites

We currently use an EC2 instance to host the frontend app.

You will need SSH access to the server to which you want to deploy. This is managed via Opworks, see [here](https://stackoverflow.com/c/jongens-van-techniek/questions/98) for instructions, 
and ask Steve to setup an IAM user for you, if not already done so, that _allows SSH access to the concerning EC2 instance via IAM user configuration._

If you already have an IAM user, with the mandatory configurations as described [here](https://stackoverflow.com/c/jongens-van-techniek/questions/98), you can continue.

- [Register your SSH key](Register%20SSH%20key) 

- Make sure to be on the _whitelisted JVT office IP address_ **before** SSH-ing into instance, see [here](https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#SecurityGroups) on to view and / or update the _inbound_ Security Group rules

- See [here](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) on more information about _AWS Security Groups_

#### 1 SSH-ing into server

```shell
$ ssh username@instance.ip.address
```

Currently two instances are setup:

- Frontend PRODUCTION

```
 34.255.133.117
```

- Frontend STAGING: 

```
99.80.168.39
```

- See [here](https://bitbucket.org/jvt/ocean-premium-frontend/wiki/Register%20SSH%20key#markdown-header-determine-ip-of-target-host) to find the IP address of the target host
You can find the IP address of the instance on the OP AWS under the [EC2 section](https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Instances:sort=instanceId).

- Switch to sudo user:

```shell
$ sudo -i
```

#### Attach or create new Tmux session

#####  Find or create tmux session


We use [tmux](https://en.wikipedia.org/wiki/Tmux) to support detachable SSH sessions to run long running jobs, like running the node server. 

- Follow the [tmux](tmux) instructions to create or attach to tmux session

- See [here](https://tmuxcheatsheet.com) for a tmux cheatsheet

- See [here](https://leimao.github.io/blog/Tmux-Tutorial/) for a Tmux tutorial

First check if there already exists a tmux session:

```shell
$ tmux ls
```

#### Output

In case of existing tmux sessions (for example called: node):

```shell
node: 1 windows (created Tue Apr 16 16:22:53 2019) [204x55]
```

In case of *no* tmux sessions:

```shell
no server running on /private/tmp/tmux-501/default
```

### Create a tmux session (if none exists)

Assume you want to create a session named: _node_

```shell
$ tmux new -s node
```
This will create a new tmux session with the name: _node_ and you will automatically be attached to it.

### Attach to tmux session

Assume you want to attach to session named: _node_

```shell
$ tmux a -t node
```

### 3 Navigate to the web app

First navigate to where the app is installed:

#### Staging

```shell
$ cd /var/www/op-dev.jongensvantechniek.nl
```

- Hosted on: https://op-dev.jongensvantechniek.nl
- SSL via: https://cloudflare.com

#### Production

```shell
$ cd /var/www/rental.oceanpremium.com
```

- Hosted on: https://rental.oceanpremium.com
- SSL via: https://letsencrypt.org
- See here _how_ SSL is setup: [SSL Certificate](SSL%20certificate)

##### Obsolete

```shell
$ cd /var/www/op-prod.jongensvantechniek.nl
```

- Hosted on: https://op-prod.jongensvantechniek.nl
- SSL via: https://cloudflare.com

### 4 Deploy frontend

First, pull the latest changes (determine if you are on the correct branch):

```shell
$ git pull
```

#### Install packages

If needed, install packages:

```shell
$ (sudo) npm install
```

#### Create a production build 

```shell
$ npm run build
```

#### Spin up node server

```shell
$ npm run start
```

Which will starts a node server on [http://localhost:3000](http://localhost:3000), for which Apache is configured to proxy request to when server request are coming in.

**Don't forget** to [detach](tmux#markdown-header-detach-from-current-tmux-session) from the tmux session.

#### 5 Detach from Tmux session

**Click** the following button combination (do not copy paste, that won't work): 

```
Hit **CTRL**, *keep it pressed*, and hit also **b**, *then release all keys*, and then hit **d**
```

```shell
CTRL b
and without CTRL
d
```

```
CTRL + b
d
```

```
- while CTRL button is pressed, press b
- then release all keys 
- then press d
```

#### Exit sudo session
```shell
$ exit
```

#### Exit ssh connection

```shell
$ exit
```

## 6 Verification

Now you are done deploying, either go to the staging or production environment to verify that the deployment is successful.

### Staging

- https://op-dev.jongensvantechniek.nl

### Production

- https://rental.oceanpremium.com 

or

- https://op-prod.jongensvantechniek.nl