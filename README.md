# Remote Dev Machine Setup

This document describes how I set up my developer environment on a remote server to use with Visual Studio Code.

If you have any comments or suggestions, feel free to give me a shout [on Twitter](https://twitter.com/nicolahery)!

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Finder](#finder)
- [Google Chrome](#google-chrome)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Consolas](#consolas)
- [Beautiful terminal](#beautiful-terminal)
- [iTerm2](#iterm2)
- [Git](#git)
- [Sublime Text](#sublime-text)
- [Vim](#vim)
- [Heroku](#heroku)
- [Projects folder](#projects-folder)
- [Apps](#apps)
- [Remote Dev Machine](#remove-dev-machine)

## APT

If you are on Ubuntu, you'll use `apt` to install apps. Update it to make sure that you have all the packages needed:

`$ apt update`

## Git

Let's start by installing git with `$ sudo apt install git-all`

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

In order to ignore system files in all of your repositories without explicitely having to add them to your projects' gitignore, you can create a global gitignore and configure git to use it:

    $ echo data > ~/.gitignore
    $ git config --global core.excludesfile ~/.gitignore

## ZSH

My shell of choice is `zsh`, let's start by installing it: `$ apt install zsh`

## Oh My Zsh

As per themselves, Oh My Zsh will not make you a 10x developer...but you may feel like one.

Install with `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

Activate the following plugins by editing `~/.zshrc`:

```bash
plugins=(
    dotenv # Loads env files when in a project folder
    zsh-history-substring-search # Fish-like history navigation with up and down arrows
    zsh-autosuggestions # Fish-like autocomplete
    z # Jump into folders
)
```

History substring and Autocomplete will need to be installed, follow the instructions here https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/history-substring-search and here https://github.com/zsh-users/zsh-autosuggestions

## Remote Dev Machine

Visual Studio Code lets you connect to remote machines using ssh and use them as development environement. This is incredibly powerful and frankly quiet simple. Through SSH, you can edit the remote file system and run your code on the remote machine. Then, by binding to the ports, you can run your apps locally.

Steps:

### Set-up the remote machine
1. Create a VM, for instance an AWS Ec2 (no pun intended)
2. Copy your local public key to your newly created instance, either through some GUI or with `cat ~/.ssh/id_rsa.pub | ssh -i ~/Downloads/joan_m1.pem ec2-user@ec2-18-191-25-224.us-east-2.compute.amazonaws.com "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >>  ~/.ssh/authorized_keys"`
3. SSH into the instance
4. Install git on the remote machine `sudo apt update` `sudo apt install git-all` (don't forget to configure username and email as well as global gitignore)
5. Install nvm curl -o- `https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash`
6. Install node `nvm install node`
7. Install yarn `npm install --global yarn`
8. Install docker & docker compose

### Connect with VS Code
1. Install the "Remote Development" extension by Microsoft for VS Code
2. Go to the newly created icon on the left bar
3. Add a new SSH target
4. Connect to your remote machine and clone your git repository through the VS Code interface
5. You may also want to open an existing directory, for example the root of your server `/`. Now you can edit all the wonderful text files that configure your Linux box with the power and convenience of VS Code.
6. By default, the number of file watchers on some machines will be too low. This will manifest either by VS Code complaining "Visual Studio Code is unable to watch for file changes in this large workspace" or by your webpack/node/whatever applications not starting. Fix it by like that:

"Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)#
When you see this notification, it indicates that the VS Code file watcher is running out of handles because the workspace is large and contains many files. Before adjusting platform limits, make sure that potentially large folders, such as Python .venv, are added to the files.watcherExclude setting (more details below). The current limit can be viewed by running:

`cat /proc/sys/fs/inotify/max_user_watches`

The limit can be increased to its maximum by editing `/etc/sysctl.conf` (except on Arch Linux, read below) and adding this line to the end of the file:

`fs.inotify.max_user_watches=524288`

The new value can then be loaded in by running `sudo sysctl -p`.

While 524,288 is the maximum number of files that can be watched, if you're in an environment that is particularly memory constrained, you may wish to lower the number. Each file watch takes up 1080 bytes, so assuming that all 524,288 watches are consumed, that results in an upper bound of around 540 MiB.

7. Make sure that your docker containers can network between cross-platform them by following this tutorial: https://dev.to/natterstefan/docker-tip-how-to-get-host-s-ip-address-inside-a-docker-container-5anh
