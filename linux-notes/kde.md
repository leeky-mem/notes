# Stop desktop applications from autostarting
- Locate your autostart directory. This is given by $XDG_CONFIG_DIRS/autostart or if $XDG_CONFIG_DIRS is not set, defaults to /etc/xdg/autostart. Note that if $XDG_CONFIG_HOME is set and used, that takes precedence over $XDG_CONFIG_DIRS. This is useful if you don't have root access as you can just copy $XDG_CONFIG_DIRS into $XDG_CONFIG_HOME and edit the files in $XDG_CONFIG_HOME.
- Copy the .desktop file to the autostart directory and add `Hidden=true` as second line to the file.
