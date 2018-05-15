# Mac OS X Dev Setup

<div align="center">
  <a href="https://github.com/rohankvats/mac-setup">
    <img src="https://user-images.githubusercontent.com/35331661/37242209-c5d740cc-2465-11e8-92b3-e6d786e98dda.jpg" width="125px">
  </a>
  <br>
  <h1> Mac Setup</h1>
  <p>
    <em>Front End Web Development Setup for  macOS</em>
  </p>
  <p>
    <a href="https://github.com/rohankvats/mac-setup/stargazers">
      <img src="https://img.shields.io/github/stars/rohankvats/mac-setup.svg" /> 
    </a>
    <a href="https://github.com/rohankvats/mac-setup/network/members">
      <img src="https://img.shields.io/github/forks/rohankvats/mac-setup.svg" /> 
    </a>
    <a href="https://github.com/rohankvats/mac-setup">
      <img src="https://img.shields.io/badge/macOS-10.13.4-blue.svg" /> 
    </a>
    <a href="https://github.com/rohankvats/mac-setup/commits/master">
      <img src="https://img.shields.io/github/last-commit/rohankvats/mac-setup.svg" />
    </a>
  </p>
  <br>
  <br>
</div>

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up the terminal, Node (JavaScript) environments, mainly for JavaScript development. As you read  and follow these steps, feel free to send me any feedback or comments you may have. The document assumes you are new to Mac. The steps below were tested on OS X Mountain Lion.

---
## Table of Contents

- [System preferences](#system-preferences)
- [Google Chrome](#google-chrome)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Consolas](#consolas)
- [Beautiful terminal](#beautiful-terminal)
- [iTerm2](#iterm2)
- [Git](#git)
- [Editors](#editors)
- [Vim](#vim)
- [Node.js](#nodejs)
- [Apps](#apps)
    - [Note-taking](#Note-taking)
    - [IDEs](IDEs)
    - [Developer Utilities](#Developer-Utilities)
    - [Regular Expression Editors](#Regular-Expression-Editors)
    - API Development and Analysis
    - Virtualization
    - Remote Login Software
    - Quality of Life Improvements
    - System Related Tools
    - Gaming Software
---
 

If you have any comments or suggestions, feel free to give me a shout on [Twitter](https://twitter.com/rohankvats)!

## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In *Apple Icon > System Preferences*:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

## Google Chrome

Install your favourite browser, mine happens to be Chrome.

## iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

In *Finder*, drag and drop the *iTerm* Application file into the *Applications* folder.

You can now launch iTerm, through the *Launchpad* for instance.

Let's just quickly change some preferences. In *iTerm > Preferences...*, under the tab *General*, uncheck *Confirm closing multiple sessions* and *Confirm "Quit iTerm2 (Cmd+Q)" command* under the section *Closing*.

In the tab *Profiles*, create a new one with the "+" icon, and rename it to your first name for example. Then, select *Other Actions... > Set as Default*. Finally, under the section *Window*, change the size to something better, like *Columns: 125* and *Rows: 35*.

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the *Command Line Tools* for *Xcode*. These include compilers that will allow you to build things from source.

Now, Xcode weights something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode. To do this you need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

Once you reach the downloads page, search for "command line tools", and download the latest *Command Line Tools (OS X Mountain Lion) for Xcode*. Open the *.dmg* file once it's done downloading, and double-click on the *.mpkg* installer to launch the installation. When it's done, you can unmount the disk in Finder.

*Note*: If you are running *OS X 10.9 Mavericks*, then you can install the Xcode Command Line Tools directly from the command line with `$ xcode-select --install`, and you don't have to go through the download page and the questionnaire.

Finally, we can install Hombrew! In the terminal paste the following line (without the `$`), hit *Enter*, and follow the steps on the screen:

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Open a new terminal tab with *Cmd+T* (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
### Usage

To install a package (or *Formula* in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
*Note*: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

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

## Consolas

I really like the Consolas font for coding. Being a Microsoft (!) font, it is not installed by default. Since we're going to be looking at a lot of terminal output and code, let's install it now.

There are two ways we can install it. If you bought *Microsoft Office for Mac*, install that and Consolas will be installed as well.

If you don't have Office, follow these steps:

    $ brew install cabextract
    $ cd ~/Downloads
    $ mkdir consolas
    $ cd consolas
    $ curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
    $ cabextract PowerPointViewer.exe
    $ cabextract ppviewer.cab
    $ open CONSOLA*.TTF

And click *Install Font*. Thanks to Alexander Zhuravlev for his [post](http://blog.ikato.com/post/15675823000/how-to-install-consolas-font-on-mac-os-x).

## Beautiful terminal
Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

Let's go ahead and start by changing the font. In *iTerm > Preferences...*, under the tab *Profiles*, section *Text*, change both fonts to *Consolas 13pt*.

Now let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

Scroll down the page and download the latest version. Unzip the archive. In it you will find the `iterm2-colors-solarized` folder with a `README.md` file, but I will just walk you through it here:

- In *iTerm2 Preferences*, under *Profiles* and *Colors*, go to *Load Presets... > Import...*, find and open the two *.itermcolors* files we downloaded.
- Go back to *Load Presets...* and select *Solarized Dark* to activate it. Voila!

*Note*: You don't have to do this, but there is one color in the *Solarized Dark* preset I don't agree with, which is *Bright Black*. You'll notice it's too close to *Black*. So I change it to be the same as *Bright Yellow*, i.e. *R 83 G 104 B 112*.

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/rohankvats/mac-dev-setup/master/.bash_profile
    $ curl -O https://raw.githubusercontent.com/rohankvats/mac-dev-setup/master/.bash_prompt
    $ curl -O https://raw.githubusercontent.com/rohankvats/mac-setup/master/.aliases
    
With that, open a new terminal tab (Cmd+T) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to *System Preferences* > *Sharing*. For example, I changed mine from "Nicolas's MacBook Air" to just "MacBook Air", so it shows up as `MacBook-Air` in the terminal.

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
    
*Note*: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/nicolashery/mac-dev-setup/blob/master/.gitignore) file for inspiration.

## Editors
+ **[Sublime Text](https://www.sublimetext.com/)**: the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.
    - [Must Have Plugins for Sublime Text](https://github.com/rohankvats/mac-setup/blob/master/editor-plugin.md#sublime-text-plugin)
+ **[Atom](https://atom.io/)**: Atom is a text editor that's modern, approachable, yet hackable to the core—a tool you can customize to do anything but also use productively without ever touching a config file.
    - [Must Have Plugins for Atom](https://github.com/rohankvats/mac-setup/blob/master/editor-plugin.md#atom-plugin)
+ **[Brackets](http://brackets.io/)**: An open source code editor for the web, written in JavaScript, HTML and CSS.
+ **[Visual Studio Code](https://code.visualstudio.com/)**: Build and debug modern web and cloud applications. VS Code is free and available on your favorite platform - Linux, Mac OSX, and Windows.

## Sublime Text
With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

Go ahead and [download](http://www.sublimetext.com/) it. Open the *.dmg* file, drag-and-drop in the *Applications* folder, you know the drill now. Launch the application.

*Note*: At this point I'm going to create a shortcut on the OS X Dock for both for Sublime Text and iTerm. To do so, right-click on the running application and select *Options > Keep in Dock*.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $70 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool. :)

Just like the terminal, let's configure our editor a little. Go to *Sublime Text 2 > Preferences > Settings - User* and paste the following in the file that just opened:

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

I use tab size 2 for everything except Python and Markdown files, where I use tab size 4. If you have a Python and Markdown file handy (or create dummy ones with `$ touch dummy.py`), for each one, open it and go to *Sublime Text 2 > Preferences > Settings - More > Syntax Specific - User* to paste in:

```json
{
    "tab_size": 4
}
```

Now for the color. I'm going to change two things: the *Theme* (which is how the tabs, the file explorer on the left, etc. look) and the *Color Scheme* (the colors of the code). Again, feel free to pick different ones, or stick with the default.

A popular Theme is the [Soda Theme](https://github.com/buymeasoda/soda-theme). To install it, run:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages/
    $ git clone https://github.com/buymeasoda/soda-theme/ "Theme - Soda"
    
Then go to *Sublime Text 2 > Preferences > Settings - User* and add the following two lines:

    "theme": "Soda Dark.sublime-theme",
    "soda_classic_tabs": true

Restart Sublime Text for all changes to take effect (Note: on the Mac, closing all windows doesn't close the application, you need to hit *Cmd+Q*).

The Soda Theme page also offers some [extra color schemes](https://github.com/buymeasoda/soda-theme#syntax-highlighting-colour-schemes) you can download and try. But to be consistent with my terminal, I like to use the *Solarized* Color Scheme, which already ships with Sublime Text. To use it, just go to *Sublime Text 2 > Preferences > Color Scheme > Solarized (Dark)*. Again, this is really according to personal flavors, so pick what you want.

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

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, *Insert* (by pressing `i`) and *Normal* (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. After that it's just remembering a few important keys.

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

## Node.js

Install [Node.js](http://nodejs.org/) with Homebrew:

    $ brew update
    $ brew install node
    
The formula also installs the [npm](https://npmjs.org/) package manager. However, as suggested by the Homebrew output, we need to add `/usr/local/share/npm/bin` to our path so that npm-installed modules with executables will have them picked up.

To do so, add this line to your `~/.path` file, before the `export PATH` line:

```bash
PATH=/usr/local/share/npm/bin:$PATH
```
        
Open a new terminal for the `$PATH` changes to take effect.

We also need to tell npm where to find the Xcode Command Line Tools, by running:

    $ sudo xcode-select -switch /usr/bin

(If Xcode Command Line Tools were installed by Xcode, try instead:)

    $ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

Node modules are installed locally in the `node_modules` folder of each project by default, but there are at least two that are worth installing globally. Those are [CoffeeScript](http://coffeescript.org/) and [Grunt](http://gruntjs.com/):

    $ npm install -g coffee-script
    $ npm install -g grunt-cli

### Npm usage

To install a package:

    $ npm install <package> # Install locally
    $ npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    $ npm install <package> --save

To see what's installed:

    $ npm list # Local
    $ npm list -g # Global

To find outdated packages (locally or globally):

    $ npm outdated [-g]

To upgrade all or a particular package:

    $ npm update [<package>]

To uninstall a package:

    $ npm uninstall <package>

## JSHint

JSHint is a JavaScript developer's best friend. 

If the extra credit assignment to install Sublime Package Manager was completed, JSHint can be run as part of Sublime Text. 

Install JSHint via npm (global install preferred)

    $ npm install -g jshint

Follow additional instructions on the [JSHint Package Manager page](https://sublime.wbond.net/packages/JSHint) or [build it manually](https://github.com/jshint/jshint).

## Projects folder
This really depends on how you want to organize your files, but I like to put all my personal version-controlled projects in `~/Projects` an d Other organisation projects I may have, or things not yet under version control in `~/<Company-name>`.

## Apps
Here is a quick list of some apps I use, and that you might find useful as well:

![Open-Source Software][OSS Icon] means **open source**, click to open **open source** repo;  
![Freeware][Freeware Icon] means **free** to use, or **free** personal license;  
![hot][hot Icon] means **hot** app;  
![Recommend][tuijian Icon] means **recommended** app;  
![Must Have][bibei Icon] means **must have** app;  
![App Store][app-store Icon] means **App store** hyperlink;  
![1 star][red Icon] means highly recommended, must-have app. The number of stars represents how strongly I recommend it;


#### Note-taking
* [Bear Writer](http://www.bear-writer.com/) - Beautiful, flexible writing app for crafting notes and prose. [![App Store][app-store Icon]](https://itunes.apple.com/us/app/bear-beautiful-writing-app/id1091189122?ls=1&mt=12)
* [Boostnote](https://boostnote.io/) - Note-taking app made for programmers. [![Open-Source Software][OSS Icon]](https://github.com/BoostIO/Boostnote) ![Recommend][tuijian Icon]
* [Evernote](https://evernote.com/) - Infamous note-taking app, available on many platforms. ![Freeware][Freeware Icon] ![hot][hot Icon] ![Recommend][tuijian Icon] ![Must Have][bibei Icon]

#### IDEs

- [Atom](https://atom.io/): Hackable text editor for the 21st century made by GitHub. Atom Plugins. star 4 Open-Source Software Freeware hot Recommend must-have
* [Visual Studio Code](https://code.visualstudio.com/) - Microsoft's free & open-source editor, TypeScript friendly, [VSCode Plugins](editor-plugin.md#vscode-plugin). [![Open-Source Software][OSS Icon]](https://github.com/Microsoft/vscode) ![Freeware][Freeware Icon] ![hot][hot Icon]
* [WebStorm](http://www.jetbrains.com/webstorm/) - The smartest JavaScript IDE by JetBrains. **FREE** for Students, check [here](https://www.jetbrains.com/student/) for more info. ![hot][hot Icon] ![Recommend][tuijian Icon]
    * [NodeJS Plugin](https://plugins.jetbrains.com/plugin/6098-nodejs) - `Node.js` integration. You definitely need this, quite a few features require it.
    * [EditorConfig Plugin](https://plugins.jetbrains.com/plugin/7294-editorconfig) - JetBrains IDE plugin supporting the EditorConfig standard.
    * [Material Theme UI Plugin](https://plugins.jetbrains.com/plugin/8006-material-theme-ui) - Provides 3 modes, nice and clean.

#### Developer Utilities

* [BetterRename](http://www.publicspace.net/BetterRename/) - The most powerful and complete Mac file renaming application on the market. [![App Store][app-store Icon]](https://itunes.apple.com/us/app/better-rename-9/id414209656)
* [Dash](https://kapeli.com/dash) - Awesome API documentation browser and code snippet manager. ![Freeware][Freeware Icon] ![hot][hot Icon] ![Recommend][tuijian Icon] ![must-have][bibei Icon] ![star 5][star5 Icon]
* [DiffMerge](http://sourcegear.com/diffmerge/) - Application to visually compare and merge files. ![Freeware][Freeware Icon]
* [EnvPane](https://github.com/hschmidt/EnvPane) - OS X preference pane for environment variables. [![Open-Source Software][OSS Icon] ![Freeware][Freeware Icon]](https://github.com/hschmidt/EnvPane)
* [FinderGo](https://github.com/onmyway133/FinderGo) - Open terminal quickly from Finder. [![Freeware][Freeware Icon] ![Open-Source Software][OSS Icon]](https://github.com/onmyway133/FinderGo)
* [SnippetsLab](https://www.renfei.org/snippets-lab/) - Easy-to-use code snippets manager.
* [zeplin](https://www.zeplin.io/) - Collaboration tool for work between designers and developers. ![Freeware][Freeware Icon] ![hot][hot Icon]

#### Regular Expression Editors

* [Patterns](http://krillapps.com/patterns/) - Regular expression editor. ![Recommend][tuijian Icon]
* [RegExRX](http://www.mactechnologies.com/index.php?page=downloads#regexrx) - Development tool for regular expressions. ![hot][hot Icon]
* [Regex](https://motionobj.com/regex/) - Regular expression testing tool with an emphasis on simplicity.

#### API Development and Analysis

* [Cocoa Rest Client](https://mmattozzi.github.io/cocoa-rest-client/) - Free, open-source, native Apple OS X app for testing HTTP/REST endpoints. [![Open-Source Software][OSS Icon]](https://github.com/mmattozzi/cocoa-rest-client) ![Freeware][Freeware Icon]
* [Insomnia](https://insomnia.rest/) - The most intuitive cross-platform REST API Client. [![Open-Source Software][OSS Icon]](https://github.com/getinsomnia/insomnia) ![Freeware][Freeware Icon]
* [Postman](https://www.getpostman.com) - Powerful GUI platform to make your API development faster & easier, from building API requests through testing, documentation and sharing. ![star 4][star4 Icon]![Freeware][Freeware Icon] ![hot][hot Icon] ![must-have][bibei Icon]

#### Virtualization

* [Docker](https://www.docker.com/) - Powerful, performs operating-system-level virtualization. [![Open-Source Software][OSS Icon]](https://github.com/github/hub) ![Freeware][Freeware Icon] ![Recommend][tuijian Icon]
* [Virtual Box](http://www.virtualbox.org) - Powerful x86 and AMD64/Intel64 virtualization product. ![star 4][star4 Icon] ![Freeware][Freeware Icon] ![Recommend][tuijian Icon]
* [Vagrant](https://www.vagrantup.com) - Tool for building and distributing development environments. [![Open-Source Software][OSS Icon]](https://github.com/mitchellh/vagrant) ![Freeware][Freeware Icon] ![star 5][star5 Icon]
* [Vagrant Manager](http://vagrantmanager.com) - Manage your vagrant machines in one place. [![Open-Source Software][OSS Icon] ![Freeware][Freeware Icon]](https://github.com/lanayotech/vagrant-manager/)

#### Remote Login Software

* [TeamViewer](https://www.teamviewer.com/en) - Proprietary computer software package for remote control, desktop sharing, online meetings, web conferencing and file transfer between computers. ![Freeware][Freeware Icon] ![Recommend][tuijian Icon] ![must-have][bibei Icon] ![star 4][star4 Icon]

#### Quality of Life Improvements

* [CheatSheet](https://www.mediaatelier.com/CheatSheet/) -  Hold the ⌘-Key to get a list of all active shortcuts of the current application. It's as simple as that. ![star 4][star4 Icon] ![Freeware][Freeware Icon]
* [f.lux](https://justgetflux.com/) - Makes the color of your computer's display adapt to the time of day. ![Freeware][Freeware Icon]
* [KeyCastr](https://github.com/keycastr/keycastr) - Open-source keystroke visualizer.  [![Open-Source Software][OSS Icon]](https://github.com/keycastr/keycastr) ![Freeware][Freeware Icon]
* [Shifty](http://shifty.natethompson.io) - A macOS menu bar app that gives you more control over Night Shift. [![Open-Source Software][OSS Icon]](https://github.com/thompsonate/Shifty)
* [Snap](http://indragie.com/snap) - Launch an app in a snap. Ridiculously easy shortcut management. ![Freeware][Freeware Icon] [![App Store][app-store Icon]](https://itunes.apple.com/cn/app/id418073146)

#### System Related Tools

* [AppCleaner](http://freemacsoft.net/appcleaner/) - Small application which allows you to thoroughly uninstall unwanted apps. ![Freeware][Freeware Icon] ![Recommend][tuijian Icon]
* [Caffeine](http://lightheadsw.com/caffeine/) - Don't let your Mac fall asleep!
* [Cleaner for Xcode](https://github.com/waylybaye/XcodeCleaner) - Helps make your Xcode faster by removing unwanted and deprecated files. [![Open-Source Software][OSS Icon]](https://github.com/waylybaye/XcodeCleaner) ![Freeware][Freeware Icon] ![tuijian][tuijian Icon]
* [Coolant](https://coolantformac.com) - Menubar app that lets you know when an app is consuming 100% CPU or more than a gigabyte of memory (or any arbitrary limits you choose).
* [DaisyDisk](https://daisydiskapp.com/) - Gives a great overview of disk usage. Can also make more disk-space available by cleaning up your disk.
* [gfxCardStatus](https://gfx.io/) - Unobtrusive menu bar app for OS X that allows MacBook Pro users to see which apps are affecting their battery life by using the more power-hungry graphics. ![Freeware][Freeware Icon] ![Recommend][tuijian Icon]
* [HandShaker](http://www.smartisan.com/apps/handshaker) -  Mac on the management of Android mobile phone content. ![Freeware][Freeware Icon]
* [HTML5 Player](http://zythum.sinaapp.com/youkuhtml5playerbookmark/) - HTML 5 video player. Keep your Mac from "burning".
* [InsomniaX](https://www.macupdate.com/app/mac/22211/insomniax) - Disable either lid and/or idle sleep (so you can play music with your lid closed, for example).
* [iStat Menus](https://bjango.com/mac/istatmenus/) - Advanced Mac system monitor on the menubar. ![Recommend][tuijian Icon]
* [iStats](https://github.com/Chris911/iStats) - Command-line tool that allows you to easily grab the CPU temperature, fan speeds and battery information on OSX. [![Open-Source Software][OSS Icon] ![Freeware][Freeware Icon]](https://github.com/Chris911/iStats)
* [Juice](https://github.com/brianmichel/Juice) - Make your battery information a bit more interesting. [![Open-Source Software][OSS Icon]](https://github.com/brianmichel/Juice) ![Freeware][Freeware Icon]
* [KeepingYouAwake](https://github.com/newmarcel/KeepingYouAwake) - Alternative to Caffeine with better support for dark mode in Mac. [![Open-Source Software][OSS Icon]](https://github.com/newmarcel/KeepingYouAwake)
* [Monity](http://www.monityapp.com/) - System monitoring widget for OS X. ![star 3][star3 Icon]
* [Mounty](http://enjoygineering.com/mounty/) - Tiny tool to re-mount write-protected NTFS volumes under Mac OS X 10.9+ in read-write mode. ![Freeware][Freeware Icon]
* [NitroShare](https://nitroshare.net/) - Cross-platform network file transfer utility. [![Open-Source Software][OSS Icon]](https://github.com/nitroshare/nitroshare-desktop) ![Freeware][Freeware Icon]
* [OmniDiskSweeper](https://www.omnigroup.com/more) - Shows you the files on your drive, ordered by size. It can be used to find and remove unused files.  ![Freeware][Freeware Icon] ![Recommend][tuijian Icon]
* [Paragon NTFS](https://www.paragon-software.com/home/ntfs-mac/) - Read/write access to NTFS in macOS Sierra.
* [Porting Kit](http://portingkit.com/) - Install Windows® Games inside your Mac. ![Freeware][Freeware Icon]
* [SSH Tunnel](https://codinn.com/products/ssh-tunnel/) - Application for managing SSH connections.
* [Tuxera NTFS](http://www.tuxera.com/products/tuxera-ntfs-for-mac/) - Full read-write compatibility with NTFS-formatted drives on a Mac.


#### Gaming Software

* [OpenEmu](http://openemu.org/) - A great video game console emulator, supports many different emulators in a single application. (e.g. Sony PSP, GameBoy, NDS and so on) [![Open-Source Software][OSS Icon] ![Freeware][Freeware Icon] ![Recommend][tuijian Icon]](https://github.com/OpenEmu/OpenEmu)



[OSS Icon]: https://jaywcjlove.github.io/sb/ico/min-oss.svg
[Freeware Icon]: https://jaywcjlove.github.io/sb/ico/min-free.svg
[hot Icon]: https://jaywcjlove.github.io/sb/ico/min-hot.svg
[tuijian Icon]: https://jaywcjlove.github.io/sb/ico/min-tuijian.svg
[bibei Icon]: https://jaywcjlove.github.io/sb/ico/min-bibei.svg
[red Icon]: https://jaywcjlove.github.io/sb/star/red.svg
[app-store Icon]: https://jaywcjlove.github.io/sb/ico/min-app-store.svg
[star0 Icon]: https://jaywcjlove.github.io/sb/star/red0.svg
[star1 Icon]: https://jaywcjlove.github.io/sb/star/red1.svg
[star2 Icon]: https://jaywcjlove.github.io/sb/star/red2.svg
[star3 Icon]: https://jaywcjlove.github.io/sb/star/red3.svg
[star4 Icon]: https://jaywcjlove.github.io/sb/star/red4.svg
[star5 Icon]: https://jaywcjlove.github.io/sb/star/red5.svg