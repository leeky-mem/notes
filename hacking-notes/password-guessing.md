# Hydra (Authentication)
`hydry -l username -P wordlist.txt TARGET_IP SERVICE` \
More options:\
`-s PORT` if not default port for the service \
`-t N` where `N` is the number of parallel connections

# ncrack (Authentication)
password guessing engine of nmap

# Hash Cracking
## Hash identifying
Online [here](https://hashes.com/en/tools/hash_identifier) -- so far more reliable \
`wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py` - gets a python script

## John the Ripper(hash cracking)[wiki](https://www.openwall.com/john/)
Install with pacman or apt if on debian systems \
Get wordlists on [SecLists](https://github.com/danielmiessler/SecLists/tree/master/Passwords) \
`john <options> <path-to-hash-file.txt>` - basic syntax
>`--format=<format>` - foramt of the hash e.g `raw-md5` \
>`--list=formats | gerp <format>` - lists formats \
>`--wordlist=<path/to/wordlist>` - path to wordlist \
>`--single` - uses single crack mode (uses word mangling on username) hash must be in form: `<username>:<hash>`

### Custom Rules for Word Mangling
Check out the [wiki](https://www.openwall.com/john/doc/RULES.shtml)\
`--rule=<rulename>` - adds a custom rule to the wordlist

#### Custom Rule file
`[List.Rules:<rulename>]` - must be the first line of the rule, decales the rulename \
Rule then use a regex style syntax `<modifiers>"[<pattern1>] [<pattern2>]"` \
**Common modifiers**\
`Az` - appends character to word\
`A0` - prepends character to word\
`c` - Captitalizes the chars positionaly\
**Common Patterns**\
`[0-9]` - numbers\
`[0]` - number 0 \
`[a-z][A-Z]` - all lowercase and uppercase letters\
`[°$%@]` - the caracters °$%@\
**example rule**\
`cAz"[0-9][~!?=]"` - capitalizes the first letter and appends a number between 0 and 9 followed by one of the characters ~!?= \
more examples can be found in `/etc/john/john.conf`

### unshadow
For hashes of linux systems John need the /etc/passwd and /etc/shadow file and we must unshadow it first before John can use it\
`unshadow <path/to/passwd> <path/to/shadow> > <outputfile.txt>` - format should be automatically detected by John, if not it is: `--format=sha256crypt`

### zip2john/rar2john/ssh2john
zip2john/rar2john are a different tool from the Jumbo John suite. It generates hashes from password protected zip files which John can work with\
`zip2john <intut-file.zip> > <output-hash.txt>` - basic syntaxt 

## hashcat (hash cracking)
