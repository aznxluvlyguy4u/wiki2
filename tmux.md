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

```shell
$ tmux new -s node
```
This will create a new tmux session with the name: _node_ and you will automatically be attached to it.

### Attach to tmux session

```shell
$ tmux a -t node
```

### Detach from current tmux session

```shell
$ ctrl b d
```