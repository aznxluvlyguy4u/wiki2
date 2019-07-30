# Remote deploying

## Table of Content

| Table of Content                                                             |
|------------------------------------------------------------------------------|
| 0. [Prerequisites](#markdown-header-prerequisites)           |
| 1. [SSH-ing into server](#markdown-header-1-ssh-ing-into-server)     |
| 2. [Attach or create new Tmux session](#markdown-header-2-attach-or-create-new-tmux-session)|                   
| 3. [Navigate to the web app](#markdown-header-3-navigate-to-the-web-app)|
| 4. [Get latest changes](#markdown-header-4a-get-latest-changes)
| 5. [Detach from Tmux session](#markdown-header-detach-from-tmux-session)|

## Prerequisites

- [Register SSH key](Register%20SSH%20key) 

We currently use an EC2 instance to host the frontend app.

You will need SSH access to the server to which you want to deploy. This is managed via Opworks, see [here](https://stackoverflow.com/c/jongens-van-techniek/questions/98) for instructions, 
and ask Steve to setup an IAM user for you, if not already done so, that _allows SSH access to the concerning EC2 instance via IAM user configuration._

If you already have an IAM user, with the mandatory configurations as described [here](https://stackoverflow.com/c/jongens-van-techniek/questions/98), you can continue.

#### 1 SSH-ing into server

```shell
$ ssh iam-username@instance.ip.address
```

You can find the IP address of the instance on the OP AWS under the [EC2 section](https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Instances:sort=instanceId).

- Switch to sudo user:

```shell
$ sudo -i
```

#### 2 Attach or create new Tmux session

We use [tmux](https://en.wikipedia.org/wiki/Tmux) to support detachable SSH sessions to run long running jobs, like running the node server. 

- Follow the [tmux](tmux) instructions to create or attach to tmux session

- See [here](https://tmuxcheatsheet.com) for a tmux cheatsheet

When attached or created a new tmux session, continue with below.

### 3 Navigate to the web app

First navigate to where the app is installed:

#### Staging

```shell
$ cd /var/www/op-dev.jongensvantechniek.nl
```

#### Production

```shell
$ cd /var/www/rental.oceanpremium.com
```

##### Obsolete

```shell
$ cd /var/www/op-prod.jongensvantechniek.nl
```

### 4a Get latest changes

Then pull the latest changes (determine if you are on the correct branch):

```shell
$ git pull
```

#### 4b Install packages

```shell
$ npm install
```

Possible, you need to execute with the `sudo` command, in case of permission errors:

```shell
$ sudo npm install
```

#### 4c Create a production build 

```shell
$ npm run build
```

#### 4d Spin up node server

```shell
$ npm run start
```

Which will starts a node server on [http://localhost:3000](http://localhost:3000), for which Apache is configured to proxy request to when server request are coming in.

**Don't forget** to [detach](https://bitbucket.org/jvt/ocean-premium-frontend/wiki/tmux#markdown-header-detach-from-current-tmux-session) from the tmux session.

#### 6 Detach from Tmux session

```shell
$ CTRL b d
```

#### Exit sudo session
```shell
$ exit
```

#### Exit ssh connection

```shell
$ exit
```

## Verification

Now you are done deploying, either go to the staging or production environment to verify that the deployment is successful.

### Staging

https://op-dev.jongensvantechniek.nl

### Production

http://rental.oceanpremium.com & https://op-prod.jongensvantechniek.nl