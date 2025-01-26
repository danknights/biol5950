# Logging in to MSI
To connect to an MSI supercomputer, please follow these steps:

### Accept the MSI User Agreement
* You will have received an email invitation to accept the user agreement.
* You can also fill it out here: [https://www.msi.umn.edu/user-agreement](https://www-archive.msi.umn.edu/user-agreement).
  
### Connect to MSI login node:
* You can connect using "Open On Demand" in your web browser:
    * Control-click (Windows) or Command-click (Mac) here to open the MSI OnDemand dashboard in a new tab: [https://ood.msi.umn.edu](https://ood.msi.umn.edu)
    * Click Clusters > Agate Shell Access to open a terminal with command-line access to a login node.
    * Click Files > Home Directory to view your files
        * One cool aspect of "Open On Demand" is that you can easily upload/download files by dragging and dropping without needing a separate FTP client.
* Alternatively, if you are comfortable with the command line, you can SSH to MSI from a terminal with `ssh username@login.msi.umn.edu`

### Switch to the BIOL 5950 "group" _if_ you also have another group
If you are in a lab group or another class group, you can run this to switch to our class group account:
```bash
newgrp biol5950
```

You can check if you're in other groups with this:
```bash
groups
```

### Launch and connect to an interactive computing node
- When you first log in to MSI, you will be on a "login" node. You are not allowed to run computations on this node. Instead, you can launch an interactive node for running computations with this command:

 ```bash
# Note: --ntasks-per-node is the number of cores you want
# and --mem-per-cpu is the RAM _per_ core, multiple these to get total memory
# -t is the time you want allowed
# Only request what you need
srun -N 1 --ntasks-per-node=4 --mem-per-cpu=4gb -t 02:00:00 -p agsmall --pty bash
 ```

This may take a while to finish running. It will log you directly in to the interactive node. Often you can see that this has happened because the start of the line in the terminal will say something like "yourusername@cn0077" or "yourusename@acn001" and it will be different from what it was on the previous line. If in doubt, you can run `hostname` to print out the name of the node. Login nodes usually start with `ahl` or `login` or `ln`. 

Note: if this fails to connect, please try logging back in and running this instead (requesting the `interactive` partition instead of the `agsmall` partition):
 ```bash
srun -N 1 --ntasks-per-node=4 --mem-per-cpu=4gb -t 02:00:00 -p interactive --pty bash
 ```

### Create a new folder in your home folder (the very first time only!)
This will be a place to store all of your work in the class. You only need to create this folder once at the start of the semester.
```bash
# Do this only the very first time you log in!
mkdir biol5950
```

### Enter the course folder that you created
You will do this every time you log in.
```bash
cd biol5950
```

### Troubleshooting
  * If you cannot connect to ood.msi.umn.edu or cannot SSH from a terminal, make sure you are on campus, connected to the the UofM network or eduroam network. Otherwise, MSI will block your computer from connecting. To work from home, you can use a [University of Minnesota VPN](https://it.umn.edu/services-technologies/virtual-private-network-vpn). 
