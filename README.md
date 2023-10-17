
# My bash profile

Here's my terminal profile for a couple of MacBooks. Has yet to be fully implemented on a Raspberry Pi, but that would be cool.


<br>

## Usage
---

```
# Go home
cd ~

# Clone mine or your own fork
git clone git://github.com/nat5142/profile.git .profile.d

# All *.conf files are loaded alphabetically, so this will retain your original settings
mv .profile .profile.d/z_myoldsettings.conf

# .profile.d/init kicks off the whole thing
ln -s .profile.d/init .profile

# Make sure you don't have any .bash_profile or .bashrc hanging out which might override .profile
# and reload your profile
source .profile
```

From here you can now put any `.profile.d/*.conf` file in your `uname` folder. I've also added `local/` to the `.gitignore`, so any files/variables that are specific to one machine and shouldn't be tracked by git should be placed here. The load order is:

1. `.profile.d/` (the top-level directory)
2. `.profile.d/${PLATFORM}` ("Darwin" for MacOS)
3. `.profile.d/local/` (gitignored)

Note that this means local settings will override repository globals.

<br>

## Features

- Reactive prompt - includes date and exit code of last command and git branch.
- Tab Completion for Git and Subversion
- Tab completion for ssh hosts on OS X.
- Git aliases
- 'safeedit' function that makes a timestamped backup copy of a file before editing
- 'profile_push' function for pushing these files out to other servers
- 'link_dotfiles' command that will create symlinks for all the files listed in the dotfiles directory
- Auto setup of .foward file on Linux and Solaris
- Local overriding

<br>  

## Desired features

- .zsh compliance on Darwin systems
- Raspberry Pi implementation

<br>

## Known issues

- When you open a terminal in vscode on mac, you'll get `bash: update_terminal_cwd: command not found`. Not sure how to fix that yet.
  - Fixed by adding the following code snippet to your `/etc/bashrc` file (source [here](https://apple.stackexchange.com/a/139808)):

```shell
update_terminal_cwd() {
    # Identify the directory using a "file:" scheme URL,
    # including the host name to disambiguate local vs.
    # remote connections. Percent-escape spaces.
    local SEARCH=' '
    local REPLACE='%20'
    local PWD_URL="file://$HOSTNAME${PWD//$SEARCH/$REPLACE}"
    printf '\e]7;%s\a' "$PWD_URL"
}
```


## TODO: 

- Add script to install all brew packages (traverse down tree just like with .conf files)
