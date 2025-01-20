# Maintaining your interactive session using `screen`

If you log back in to the same login node each time, you can maintain an interactive computing session.
This will be important if you are running tasks for a long period of time (like downloading a large file, 
or running genome assembly).

### Log in to a specific login node
```bash
ssh username@ahl01.msi.umn.edu # or ahl02, ahl03, ahl04
```

### Launch a screen session
Launch a `screen` session _before_ requesting a compute node
```bash
screen
```

### Request a compute node
For example, let us assume we need to download a large file. This may take a long time, but it will
not require a lot of cores or RAM, so we will only request 1 core and 4gb RAM, but we will
request 8 hours:
```bash
srun -N 1 --ntasks-per-node=1 --mem-per-cpu=4gb -t 08:00:00 -p agsmall --pty bash
```

After this command completes, we will be on a compute node.

### Detach from the `screen` session
To log out from MSI but leave the compute node running, we "detach" the screen session with _ctrl-a d_ (hold control key down, press the "a" key, then let go of the control key and press the "d" key).

### Exit from MSI
Log off from the login node using _ctrl-d_ or `exit`.

### Log back in and re-attach to the screen session
To lock back in and re-attach to the same screen session (with the interactive node still running), log in to that specific login node:
```bash
ssh username@ahl01.msi.umn.edu # or ahl02, ahl03, ahl04
```

And then re-attach with:
```bash
screen -Dr
```

Read more about screen on any of the many online tutorials, such as [this one](https://thelinuxcode.com/linux-screen-command-tutorial/).
