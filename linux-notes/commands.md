# Search
**find** \
`find . -name flag1.txt` - find the file named “flag1.txt” in the current directory and down \
`find /home -name flag1.txt` - find the file names “flag1.txt” in the /home directory and down \
`find . -name \*flag\*` - find file containing the word flag in the current directory and down \
`find / -type d -name config` - find the directory named config under “/” \
`find / -type f -perm 0777` - find files with the 777 permissions (files readable, writable, and executable by all users) \
`find / -perm a=x` - find executable files \
`find /home -user frank` - find all files for user “frank” under “/home” \
`find / -mtime 10` - find files that were modified in the last 10 days \
`find / -atime 10` - find files that were accessed in the last 10 day \
`find / -cmin -60` - find files changed within the last hour (60 minutes) \
`find / -amin -60` - find files accesses within the last hour (60 minutes) \
`find / -size 50M` - find files with a 50 MB size. use +/- to search for files larger or smaller than the threshold given \

It is important to note that the “find” command tends to generate errors which sometimes makes the output hard to read. This is why it would be wise to use the “find” command with “-type f 2>/dev/null” to redirect errors to “/dev/null” and have a cleaner output \
`find / -size +100M f 2>/dev/null`

**fd** fd is a better search command line tool than `find`

# Terminal emulators
`tio` - use `/dev/serial/by-id/<device-id>` as device for uniqueness `tio -b 115200 -d 8 -s 1 none /dev/serial/by-id/<device-id>`\
To get get device permission, add the user to the `uucp` group:\
`usermod -aG uucp <user>`\
Then restart the host(Log out Log in was not sufficient).

# Miscellaneous
**nohup**\
`nohup <application> > <outfile>` - detach process from terminal output of process will be appended to "nohup.out" if no output file is specified. \
`nohup python -u <app.py> > out.txt` - runs python app. the `-u` is used so python does not buffer its output
