# Mac OS X Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up [Node](http://nodejs.org/) (JavaScript), [Python](http://www.python.org/), and [Ruby](http://www.ruby-lang.org/) environments, mainly for JavaScript and Python development. Even if you don't program in all three, it is good to have them as many command-line tools use one of them. As you read  and follow these steps, feel free to send me any feedback or comments you may have.

The document assumes you are new to Mac. The steps below were tested on **OS 11.2.2 Big Sur**.

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

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > Software Update...**

## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Trackpad > Tracking speed > Fast (all the way to the right)
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Keyboard > Use F1, F2, etc. keys as standard function keys
- Keyboard > Shortcuts > Move right / left a space => replace ctrl + arrows with ctrl + alt + arrows (Ctrl + arrows is super useful to jump when editing text or if you ever use Excel in a Windows VM so we better free this up again)
- Keyboard > Press 🌐 to Show Emojis
- Dock > Size > Small (all the way to the left)
- Dock > Magnification (checked) > Max (all the way to the right)
- Dock > Automatically hide and show the Dock
- Accessibility > Mouse & Trackpad > Trackpad Options > Enable dragging (This allows you to double tap without releasing the second tap and drag)
- Sound > Show volume in menu bar

**If you don't have a US Keyboard**

Repare "Move focus to next windows" (equivalent to cmd+tab but between open windows of the current application) by mapping it to cmd+whatever, whatever key being just next to your tab key.

**Finder**

Show hidden files by typing the following in the terminal:

    $ defaults write com.apple.finder AppleShowAllFiles YES
    $ killall Finder


**Dock**

I remove all apps from the dock because:

- I always open my apps through Spotlight (cmd + space bar)
- This way, every app in the dock is a running app

## Finder

- View > Show path bar
- View > Show status bar
- Go > Go to folder > "/" and then drag the root (Macintosh HD) on top of the favourites
- Also add your home folder and your desktop to your favourites

## Google Chrome

Install your favorite browser, mine happens to be Chrome.

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

In the tab **Terminal**, change the scrollback lines from 1'000 to something more reasonable like 1'000'000.

In the tab **Colors** > Colors presets > Solarized Dark.

Download and install the consolas font, then in the tab **Text** > Font > Change Font chose Consolas with size 16.

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source.

Now, Xcode weights something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode.

You can install the Xcode Command Line Tools directly from the command line with `$ xcode-select --install`, and you don't have to go through the download page and the questionnaire.

Finally, we can install Hombrew! In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

    $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Open a new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated
    
To update a package:

    $ brew upgrade <formula>
        
Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

## Z

Amazing tool to jump around folders.

Grab a copy of the code:

    $ mkdir ~/tools
    $ cd ~/tools
    $ git clone https://github.com/rupa/z

Add it to your path by editing `~/.bash_profile` and adding this in the end:

    . ~/tools/z/z.sh


## Consolas

I really like the Consolas font for coding. Being a Microsoft (!) font, it is not installed by default. Since we're going to be looking at a lot of terminal output and code, let's install it now.

There are two ways we can install it. If you bought **Microsoft Office for Mac**, install that and Consolas will be installed as well.

If you don't have Office, follow these steps:

    $ brew install cabextract
    $ cd ~/Downloads
    $ mkdir consolas
    $ cd consolas
    $ curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
    $ cabextract PowerPointViewer.exe
    $ cabextract ppviewer.cab
    $ open CONSOLA*.TTF

And click **Install Font**. Thanks to Alexander Zhuravlev for his [post](http://blog.ikato.com/post/15675823000/how-to-install-consolas-font-on-mac-os-x).

## Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

Let's go ahead and start by changing the font. In **iTerm > Preferences...**, under the tab **Profiles**, section **Text**, change both fonts to **Consolas 13pt**.

Now let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

Scroll down the page and download the latest version. Unzip the archive. In it you will find the `iterm2-colors-solarized` folder with a `README.md` file, but I will just walk you through it here:

- In **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Load Presets... > Import...**, find and open the two **.itermcolors** files we downloaded.
- Go back to **Load Presets...** and select **Solarized Dark** to activate it. Voila!

**Note**: You don't have to do this, but there is one color in the **Solarized Dark** preset I don't agree with, which is *Bright Black*. You'll notice it's too close to *Black*. So I change it to be the same as *Bright Yellow*, i.e. **R 83 G 104 B 112**.

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases
    
With that, open a new terminal tab (Cmd+T) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to **System Preferences** > **Sharing**. For example, I changed mine from "Nicolas's MacBook Air" to just "MacBook Air", so it shows up as `MacBook-Air` in the terminal.

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

    $ brew install git
    
When done, to test that it installed fine you can run:

    $ git --version
    
And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain
    
In order to ignore system files in all of your repositories without explicitely having to add them to your projects' gitignore, you can create a global gitignore and configure git to use it:

    $ echo .DS_Store > ~/.gitignore
    $ git config --global core.excludesfile ~/.gitignore

**Git LFS**

Also install git LFS for putting these large binary files under version control.

Simply follow the instructions:

https://help.github.com/articles/installing-git-large-file-storage/

## Sublime Text

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

Go ahead and [download](http://www.sublimetext.com/) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the OS X Dock for both for Sublime Text and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $70 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool. :)

Just like the terminal, let's configure our editor a little. Go to **Sublime Text 2 > Preferences > Settings - User** and paste the following in the file that just opened:

```json
{
    "font_face": "Consolas",
    "font_size": 13,
    "rulers":
    [
        79
    ],
    "highlight_line": true,
    "bold_folder_labels": true,
    "highlight_modified_tabs": true,
    "tab_size": 2,
    "translate_tabs_to_spaces": true,
    "word_wrap": false,
    "indent_to_bracket": true
}
```
    
Feel free to tweak these to your preference. When done, save the file and close it.

I use tab size 2 for everything except Python and Markdown files, where I use tab size 4. If you have a Python and Markdown file handy (or create dummy ones with `$ touch dummy.py`), for each one, open it and go to **Sublime Text 2 > Preferences > Settings - More > Syntax Specific - User** to paste in:

```json
{
    "tab_size": 4
}
```

Now for the color. I'm going to change two things: the **Theme** (which is how the tabs, the file explorer on the left, etc. look) and the **Color Scheme** (the colors of the code). Again, feel free to pick different ones, or stick with the default.

A popular Theme is the [Soda Theme](https://github.com/buymeasoda/soda-theme). To install it, run:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages/
    $ git clone https://github.com/buymeasoda/soda-theme/ "Theme - Soda"
    
Then go to **Sublime Text 2 > Preferences > Settings - User** and add the following two lines:

    "theme": "Soda Dark.sublime-theme",
    "soda_classic_tabs": true

Restart Sublime Text for all changes to take effect (Note: on the Mac, closing all windows doesn't close the application, you need to hit **Cmd+Q**).

The Soda Theme page also offers some [extra color schemes](https://github.com/buymeasoda/soda-theme#syntax-highlighting-colour-schemes) you can download and try. But to be consistent with my terminal, I like to use the **Solarized** Color Scheme, which already ships with Sublime Text. To use it, just go to **Sublime Text 2 > Preferences > Color Scheme > Solarized (Dark)**. Again, this is really according to personal flavors, so pick what you want.

Sublime Text 2 already supports syntax highlighting for a lot of languages. I'm going to install a couple that are missing:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages/
    $ git clone https://github.com/jashkenas/coffee-script-tmbundle CoffeeScript
    $ git clone https://github.com/miksago/jade-tmbundle Jade
    $ git clone https://github.com/danro/LESS-sublime.git LESS
    $ git clone -b SublimeText2 https://github.com/kuroir/SCSS.tmbundle.git SCSS
    $ git clone https://github.com/nrw/sublime-text-handlebars Handlebars

Let's create a shortcut so we can launch Sublime Text from the command-line:

    $ cd ~
    $ mkdir bin
    $ ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" ~/bin/subl

Now I can open a file with `$ subl myfile.py` or start a new project in the current directory with `$ subl .`. Pretty cool.

Sublime Text is very extensible. For now we'll leave it like that, we already have a solid installation. To add more in the future, a good place to start would be to install the [Sublime Package Control](http://wbond.net/sublime_packages/package_control/installation).

## Vim

Although Sublime Text will be our main editor, it is a good idea to learn some very basic usage of [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. After that it's just remembering a few important keys.

Vim's default settings aren't great, and you could spend a lot of time tweaking your configuration (the `.vimrc` file). But if you're like me and just use Vim occasionally, you'll be happy to know that [Tim Pope](https://github.com/tpope) has put together some sensible defaults to quickly get started.

First, install [pathogen.vim](https://github.com/tpope/vim-pathogen) by running:

    $ mkdir -p ~/.vim/autoload ~/.vim/bundle && \
        curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim

Then create a file `~/.vimrc` (you can use `$ subl ~/.vimrc`), and paste in the following:

    execute pathogen#infect()
    syntax on
    filetype plugin indent on

And finally, install the Vim "sensible defaults" by running:

    $ cd ~/.vim/bundle
    $ git clone git://github.com/tpope/vim-sensible.git

With that, Vim will look a lot better next time you open it!

## Heroku

[Heroku](http://www.heroku.com/), if you're not already familiar with it, is a [Platform-as-a-Service](http://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) that makes it really easy to deploy your apps online. There are other similar solutions out there, but Heroku was among the first and is currently the most popular. Not only does it make a developer's life easier, but I find that having Heroku deployment in mind when building an app forces you to follow modern app development [best practices](http://www.12factor.net/).

### Install

Assuming that you have an account (sign up if you don't), let's install the [Heroku Client](https://devcenter.heroku.com/articles/using-the-cli) for the command-line. Heroku offers a Mac OS X installer, the [Heroku Toolbelt](https://toolbelt.heroku.com/), that includes the client. But for these kind of tools, I prefer using Homebrew. It allows us to keep better track of what we have installed. Luckily for us, Homebrew includes a `heroku-toolbelt` formula:

    $ brew install heroku-toolbelt
    
The formula might not have the latest version of the Heroku Client, which is updated pretty often. Let's update it now:

    $ heroku update
    
Don't be afraid to run `heroku update` every now and then to always have the most recent version.

### Usage

Login to your Heroku account using your email and password:

    $ heroku login
    
If this is a new account, and since you don't already have a public **SSH key** in your `~/.ssh` directory, it will offer to create one for you. Say yes! It will also upload the key to your Heroku account, which will allow you to deploy apps from this computer.

If it didn't offer create the SSH key for you (i.e. your Heroku account already has SSH keys associated with it), you can do so manually by running:

     $ mkdir ~/.ssh
     $ ssh-keygen -t rsa
     
Keep the default file name and skip the passphrase by just hitting Enter both times. Then, add the key to your Heroku account:

    $ heroku keys:add
    
Once the key business is done, you're ready to deploy apps! Heroku has a great [Getting Started](https://devcenter.heroku.com/articles/python) guide, so I'll let you refer to that (the one linked here is for Python, but there is one for every popular language). Heroku uses Git to push code for deployment, so make sure your app is under Git version control. A quick cheat sheet (if you've used Heroku before):

    $ cd myapp/
    $ heroku create myapp
    $ git push heroku master
    $ heroku ps
    $ heroku logs -t
    
The [Heroku Dev Center](https://devcenter.heroku.com/) is full of great resources, so be sure to check it out!

## Projects folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/Projects`. Other documents I may have, or things not yet under version control, I like to put in `~/Dropbox` (if you have Dropbox installed), or `~/Documents`.

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Dropbox](https://www.dropbox.com/): File syncing to the cloud. I put all my documents in Dropbox. It syncs them to all my devices (laptop, mobile, tablet), and serves as a backup as well! **(Free for 2GB)**
- [Google Drive](https://drive.google.com/): File syncing to the cloud too! I use Google Docs a lot to collaborate with others (edit a document with multiple people in real-time!), and sometimes upload other non-Google documents (pictures, etc.), so the app comes in handy for that. **(Free for 5GB)**
- [1Password](https://agilebits.com/onepassword): Allows you to securely store your login and passwords. Even if you only use a few different passwords (they say you shouldn't!), this is really handy to keep track of all the accounts you sign up for! Also, they have a mobile app so you always have all your passwords with you (syncs with Dropbox). A little pricey though. There are free alternatives. **($50 for Mac app, $18 for iOS app)**
- Magnet
- Shift
- [Marked](http://markedapp.com/): As a developer, most of the stuff you write ends up being in [Markdown](http://daringfireball.net/projects/markdown/). In fact, this `README.md` file (possibly the most important file of a GitHub repo) is indeed in Markdown, written in Sublime Text, and I use Marked to preview the results everytime I save. **($4)**
- [Path Finder](http://cocoatech.com/pathfinder/): I love OSX, it's Unix so great for developers, and all of it just works and looks pretty! Only thing I "miss" from Windows (OMG what did he say?), is a decent file explorer. I think Finder is a pain to use. So I gladly paid for this alternative, but I understand others might find it expensive just to not have to use Finder. **($40)**
- [Evernote](https://evernote.com/): If I don't write something down, I'll forget it. As a developer, you learn so many new things every day, and technology keeps changing, it would be insane to want to keep it all in your head. So take notes, sync them to the cloud, and have them on all your devices. To be honest, I switched to [Simplenote](http://simplenote.com/) because I only take text notes, and I got tired of Evernote putting extra spaces between paragraphs when I copy & pasted into other applications. Simplenote is so much better for text notes (and it supports Markdown!). **(Both are free)**
- [Moom](http://manytricks.com/moom/): Don't waste time resizing and moving your windows. Moom makes this very easy. **($10)**

## Remote Dev Machine

Visual Studio Code lets you connect to remote machines using ssh and use them as development environement. This is incredibly powerful and frankly quiet simple. Through SSH, you can edit the remote file system and run your code on the remote machine. Then, by binding to the ports, you can run your apps locally.

Steps:

### Set-up the remote machine
1. Create a VM, for instance an AWS Ec2 (no pun intended)
2. Copy your local public key to your newly created instance, either through some GUI or with `cat ~/.ssh/id_rsa.pub | ssh -i ~/Downloads/joan_m1.pem ec2-user@ec2-18-191-25-224.us-east-2.compute.amazonaws.com "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >>  ~/.ssh/authorized_keys"`
3. SSH into the instance
4. Install git on the remote machine `sudo apt update` `sudo apt install git-all` (don't forget to configure username and email)
5. Install nvm curl -o- `https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash`
6. Install node `nvm install node`
7. Install yarn `npm install --global yarn`
8. Install docker & docker compose

### Connect with VS Code
1. Install the "Remote Development" extension by Microsoft for VS Code
2. Go to the newly created icon on the left bar
3. Add a new SSH target
4. Connect to your remote machine and clone your git repository through the VS Code interface
5. You may also want to open an existing directory, for example the root of your server `/`
6. By default, the number of file watchers on some machines will be too low. This will manifest either by VS Code complaining "Visual Studio Code is unable to watch for file changes in this large workspace" or by your webpack/node/whatever applications not starting. Fix it by like that:

"Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)#
When you see this notification, it indicates that the VS Code file watcher is running out of handles because the workspace is large and contains many files. Before adjusting platform limits, make sure that potentially large folders, such as Python .venv, are added to the files.watcherExclude setting (more details below). The current limit can be viewed by running:

`cat /proc/sys/fs/inotify/max_user_watches`

The limit can be increased to its maximum by editing `/etc/sysctl.conf` (except on Arch Linux, read below) and adding this line to the end of the file:

`fs.inotify.max_user_watches=524288`

The new value can then be loaded in by running `sudo sysctl -p`.

While 524,288 is the maximum number of files that can be watched, if you're in an environment that is particularly memory constrained, you may wish to lower the number. Each file watch takes up 1080 bytes, so assuming that all 524,288 watches are consumed, that results in an upper bound of around 540 MiB.
