# Examples

## Sync -S
Download and install the "gpm" package including its dependencies:\
`pacman -S gpm`

Update package list and upgrade all packages afterwards:\
`pacman -Syu`

Search for a package:\
`pacman -Ss`

## Query -Q
list all files owned by package\
`pacman -Ql <package>`

view package info\
`pacman -Qi <package>`  

## Upgrade -U
Install ceofhack-0.6-1 package from a local file:\
`pacman -U /home/user/ceofhack-0.6-1-x86_64.pkg.tar.gz`

## Remove -R
Remove a package:\
`pacman -R <package>`

Remove a package and its dependencies:\
`pacman -Rs`

Remove orphaned packages:\
`pacman -Rns $(pacman -Qtdq)`
