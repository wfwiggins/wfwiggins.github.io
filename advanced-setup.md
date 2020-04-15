---
title: "Advanced Setup"
---
# Advanced Setup

These are optional steps for those interested in taking advantage of some
advanced tools for the CLI. I find these tools very useful, but it takes
a fair amount of time to get everything installed and running. There's also
the possibility that you'll spend a considerable amount of time tweaking things
to your liking...

Also, if you haven't yet installed the Xcode Developer Command Line Tools, return
to the [Basic Setup Guide](/setup.html#developer-tools) and do this first.

<hr>
## Zsh: the Z shell

Zsh is an alternative shell that offers some really nice features like
improved tab-completion (probably the most routinely useful one), syntax
highlighting, and extended "globbing" - I'll explain the last one in a separate
post under the [Command Line page](/command-line.html).

Let's start by installing iTerm2, Homebrew, the Z shell (Zsh), Oh My Zsh and
Powerline fonts to make sure everything runs smoothly once we actually start
to use Zsh.

1. Start by installing iTerm2 from the [website](https://iterm2.com/). iTerm2 is
a more customizable terminal emulator for MacOS.
2. Next, open iTerm2.
3. Then head over to this
[guide](https://gist.github.com/derhuerst/12a1558a4b408b3b2b6e#installing-zsh-on-a-mac)
to installing Homebrew (a really useful package manager) and Zsh on MacOS.
The commands are included here for your convenience (the first one is the
corrected version from the comments). They should be entered into `bash`
line-by-line and don't include the `$` - it's just there to tell you that
each command goes on it's own line.

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.zshhubusercontent.com/Homebrew/install/master/install)"
$ brew doctor
$ brew install zsh
$ sudo -s 'echo /usr/local/bin/zsh >> /etc/shells' && chsh -s /usr/local/bin/zsh
```

<hr>
## Oh My Zsh

Welcome to Zsh! Now on to installing Oh My Zsh, which is a collection of themes
for taking full advantage of Zsh and "beautifying your shell". Start by
installing `git`, a version management command line tool that you'll be using a
lot, if you continue to use this site.

```zsh
$ brew install git
```

Next, we'll install Oh-My-Zsh from Robby Russell's GitHub [repository](https://github.com/robbyrussell/oh-my-zsh)
(or 'repo').

```zsh
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Once this is is done, you'll be running your fancy new Zsh with Oh My Zsh. The
default theme is `robbyrussell`. We'll change that shortly, though you can
certainly keep it if you like it.

<hr>
## Powerline Fonts

Many Oh My Zsh themes require a [Powerline](https://github.com/powerline/fonts#quick-installation)
font to be rendered properly in the terminal. So, naturally, we'll install
those here to keep things running smoothly as we proceed. (Note: In the code
block below, the `#` indicates a comment, not a command.) Back to our new
friend `git`...

```zsh
# clone the Powerline fonts repo to your machine
$ git clone https://github.com/powerline/fonts.git --depth=1

# run the install script
$ cd fonts
$ ./install.sh

# clean up the files you no longer need
$ cd ..
$ rm -rf fonts
```

Now, head to "Preferences" in iTerm2 by pressing `{CMD + ,}`. Then go to
"Profiles > Text" to set the "Regular" and non-ASCII fonts to one of your newly
installed Powerline fonts (I recommend SourceCodePro for starters). I also
recommend switching your color palette to "Solarized", as it plays nicely with
Oh My Zsh.

<hr>
## Configuring Zsh and Oh My Zsh with Nano

Most commonly, people configure Zsh in their .zshrc file. The first time you
install and run Zsh, you probably won't have one of these files in your home
directory `~`. However, installing OMZ will create one for you and prepopulate
it with some useful stuff. Running `ls` in `~` won't show you "Dotfiles" (e.g.
.zshrc) by default. For that, you should run `ls -a` (or `la` - an "alias" or
shortcut for the preceding command). You should see something similar to what
I've shown below, though everyone will probably have many other files and
folders that get printed to the standard output (or "stdout") when they run
this command.

```zsh
$ ls -a
-rw-------  1 walter walter  496 Oct  6 22:36 .bash_history
-rw-r--r--  1 walter walter  220 Oct  6 22:50 .bashrc
drwxr-xr-x 11 walter walter 4.0K Oct  6 22:46 .oh-my-zsh
-rw-------  1 walter walter  56K Nov 15 11:35 .zsh_history
-rw-r--r--  1 walter walter 3.8K Nov 15 11:25 .zshrc
# ... with other files mixed in
```

Now, on to configuring Zsh in `.zshrc`. The first thing you should do is decide
which text editor you want to use. Your options are a graphical text editor or
one of the built-in text editors that run in the shell itself. For simplicity,
we'll go with `nano` - one of the built-in options. It's far easier to use than
`vi` or `vim` and simpler than opening a separate window every time you want to
make a minor change to your config. Entering `nano ~/.zshrc` will launch `nano`
with your config file in the editor. At the bottom of the window, you should
see the commands available to you (FYI: `^G` is shorthand for `{CTRL + G}`).
After you make changes, you will need to press `^O` (letter O, not number) to
"write out" (i.e. save) your changes before you `^X` (exit). Also, you'll be
navigating with the keyboard as your mouse won't work.

Everything you see in your `.zshrc` has been added by OMZ. The first thing we'll
do is change the theme. Navigate to the line that says `ZSH_THEME="robbyrussell"`.
We're going to change the theme to "agnoster", so delete "robbyrussell" and
replace it with "agnoster" such that the line now looks like this
`ZSH_THEME="agnoster"`. Then `^O` and `^X`. Now you've saved your changes,
exited `nano` and are back in Zsh...but everything looks the same.

To see the effects of your changes to the config, you'll have to reload your
shell. The command for this is `source ~/.zshrc`. Over time, you may find
yourself tweaking your shell config regularly, adding or changing different
aliases, etc. Thus, I recommend you go ahead and add the following lines to your
`.zshrc` under `# Aliases`. You may wish to delete the existing ones.

```zsh
alias zshconfig="nano ~/.zshrc"
alias reload="source ~/.zshrc"
```

You will have to reload your shell profile with the full command before you can
use your new aliases. But after you do that, you'll be able to edit your config
in `nano` simply by entering `zshconfig`, then `reload` when you're done.
