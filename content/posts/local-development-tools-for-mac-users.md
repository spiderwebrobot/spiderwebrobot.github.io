+++
date = '2025-07-05T06:59:20-07:00'
draft = false
title = 'Local development tools for Mac users'
summary = 'A good place to start.'
+++

Macs are expensive. Check out [refurbished Macs](https://www.apple.com/shop/refurbished/mac) for affordable options. Otherwise, [financing](https://www.apple.com/shop/browse/financing), and [educational discounts](https://www.apple.com/us-edu/store) are available if you qualify.

## Terminal

[Terminal](https://support.apple.com/guide/terminal/welcome/mac) is a software application that lets you communicate with the Mac operating system using a [command line interface](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line) (CLI).

Terminal can be opened with a Spotlight Search...

1. Enter the `command + space` keys
2. Then search for “Terminal”
3. Finally press the `return` key

## Install Xcode Command Line Tools

[Xcode](https://developer.apple.com/xcode/resources/) Command Line Tools help you develop software on a Mac.

Open up your terminal and run...

```sh
sudo xcode-select --install
```

After typing in your password, your terminal should return...

```plaintext
xcode-select: note: install requested for command line developer tools
```

And an “install” dialog should pop open...

1. Click on the “Install” button
2. Then click on the “Agree” button in the “License Agreement”
3. Wait for the installation to complete

Verify the installation by running...

```sh
xcode-select -p
```

Your terminal should return...

```plaintext
/Library/Developer/CommandLineTools
```

## Install Homebrew

[Homebrew](https://brew.sh/) is a software package management system for your Mac.

Open up your terminal and run...

```sh
which brew
```

If `brew` is already installed, your terminal should return...

```plaintext
/usr/local/bin/brew
```

Otherwise follow the instructions at https://brew.sh/.

If you've had `brew` for a while, consider running the following commands to refresh your current installation...

```sh
brew update && brew upgrade && brew cleanup
```

Or check your system for potential problems by running...

```sh
brew doctor
```

## Install Git

[Git](https://git-scm.com/) is a distributed version control system that tracks changes made to files within a project over time.

Open your terminal and run...

```sh
which git
```

If `git` is already installed, your terminal should return…

```plaintext
/usr/local/bin/git
```

Otherwise run...

```sh
brew install git
```

And verify the install by running...

```sh
brew list
```

## Resources

- [How to Install Xcode Command Line Tools on a Mac](https://www.freecodecamp.org/news/install-xcode-command-line-tools)
- [The Missing Package Manager for macOS (or Linux)](https://docs.brew.sh/Manpage)
- [Git - Download for macOS](https://git-scm.com/downloads/mac)
