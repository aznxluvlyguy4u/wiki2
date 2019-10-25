# Tmux

See [here](https://tmuxcheatsheet.com/) for a tmux cheatsheet.

### Find or create tmux session

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

### Detach from current tmux session

- Hit **CTRL**, *keep it pressed*, and hit also **b**, *then release all keys*, and then hit **d**

*DO not copy paste below, that does not work... type it in.
*

```shell
CTRL b 
d
```

### Kill a tmux session (if needed)

Assume you want to kill to session named: _node_

```shell
$ tmux kill-session -t node     
```