# Examples

## Sync
Download and install gpm package including dependencies:\
`pacman -S gpm`

Update package list and upgrade all packages afterwards:\
`pacman -Syu`

Search for a package:\
`pacman -Ss`

## Upgrade
Install ceofhack-0.6-1 package from a local file:\
`pacman -U /home/user/ceofhack-0.6-1-x86_64.pkg.tar.gz`

## Remove
Remove a package:\
`pacman -R <package>`

Remove a package and its dependencies:\
`pacman -Rs`

Remove orphaned packages:\
`pacman -Rns $(pacman -Qtdq)`
