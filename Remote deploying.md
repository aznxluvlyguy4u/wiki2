### Remote deploying

#### Prerequisites

- SSH access to EC2 instance

We currently use an EC2 instance to host the frontend app.

You will need SSH access to the server to which you want to deploy. This is managed via Opworks, see [here](https://stackoverflow.com/c/jongens-van-techniek/questions/98) for instructions, 
and ask Steve to setup an IAM user for you, if not already done so, that _allows SSH access to the concerning EC2 instance via IAM user configuration._

If you already have an IAM user, with the mandatory configurations as described [here](https://stackoverflow.com/c/jongens-van-techniek/questions/98), you can continue.

#### SSH-ing into server

```shell
$ ssh iam-username@instance.ip.address
```

You can find the IP address of the instance on the OP AWS under the [EC2 section](https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Instances:sort=instanceId).

- Switch to sudo user:

```shell
$ sudo -i
```

We use [tmux](https://en.wikipedia.org/wiki/Tmux) to support detachable SSH sessions to run long running jobs, like running the node server. See [here](https://tmuxcheatsheet.com) for a tmux cheatsheet.

- Follow the [tmux](tmux) instructions to create or attach to tmux session


### Navigate to the web app

First navigate to where the app is installed:

```shell
$ cd /var/www/op-dev.jongensvantechniek.nl
```

### Get latest changes

Then pull the latest changes (determine if you are on the correct branch):

```shell
$ git pull
```

#### Install packages

```shell
$ sudo npm install
```

Notice the `sudo` command, this is needed otherwise you will get permission errors.

#### Create a production build 

```shell
$ npm run build
```

#### Spin up node server

```shell
$ npm run start
```

Which will starts a node server on [http://localhost:3000](http://localhost:3000), for which Apache is configured to proxy request to when server request are coming in.

**Don't forget** to [detach](https://bitbucket.org/jvt/ocean-premium-frontend/wiki/tmux#markdown-header-detach-from-current-tmux-session) from the tmux session.

```shell
$ CTRL b d
```