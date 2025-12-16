+++
date = '2025-12-15T07:53:19-08:00'
draft = false
title = 'GitHub authentication with SSH'
summary = 'Command line access.'
+++

[SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh) keys give you access to your code repositories through the command line. The command line can be executed in the [terminal](/posts/local-development-tools-for-mac-users/#terminal) for Mac users.

## Generating new SSH keys

Open a terminal and navigate into your home directory...

```sh
cd ~
```

Run the `ssh-keygen` command (with your [GitHub](/posts/creating-a-github-account/) account’s email address), e.g...

```sh
ssh-keygen -t ed25519 -C "your@email.com"
```

The terminal should prompt you to save the generated keys, e.g...

```plaintext
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/username/.ssh/id_ed25519):
```

Press “return” to accept the default file location, e.g...

```plaintext
Created directory '/Users/username/.ssh'.
```

Then enter a [passphrase](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)...

```plaintext
Enter passphrase (empty for no passphrase): 
```

After you’ve entered a passphrase, the terminal will prompt you to enter it again...

```plaintext
Enter same passphrase again:
```

The terminal should then return the location of your keys, e.g...

```plaintext
Your identification has been saved in /Users/username/.ssh/id_ed25519
Your public key has been saved in /Users/username/.ssh/id_ed25519.pub
```

The key’s [fingerprint](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints), e.g...

```plaintext
The key fingerprint is:
ssh-ed25519 +DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU your@email.com
```

And finally the key’s randomart image, e.g...

```plaintext
The key's randomart image is:
+--[ED25519 256]--+
|         .o o..  |
|          o +Eo  |
|          + .    |
|         . + o.  |
|        S o =    |
|       o         |
|        . o @.   |
|       .= o      |
|       . o      *|
+----[SHA256]-----+
```

## Managing your private key with ssh-agent

Now that you’ve created a pair of public/private keys, we’ll use an agent to remember your passphrase. Let’s start by creating a config file (if it doesn’t already exist)...

```sh
touch ~/.ssh/config
```

Next we’ll edit the `~/.ssh/config` file to automatically load keys into the agent, and store passphrases in your keychain...

```plaintext
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

### Running the agent

You’ve configured access to your private key, now let’s hand the key over to the agent. Let’s start by running the `ssh-agent` in the background...

```sh
eval "$(ssh-agent -s)"
```

The terminal should return the agent’s Process ID, e.g...

```plaintext
Agent pid 6417
```

We’ll use that ID later to kill the `ssh-agent` running in the background, in the meantime, let’s add your private key to your keychain...

```sh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

The terminal should prompt you to enter the passphrase you created earlier, e.g...

```plaintext
Enter passphrase for /Users/username/.ssh/id_ed25519:
```

And then return a confirmation message after you’ve entered your passphrase, e.g...

```plaintext
Identity added: /Users/username/.ssh/id_ed25519 (your@email.com)
```

### Killing the agent

Now that you have securely stored your private key’s password, let's do some clean up. First let’s find all of `ssh-agent` processes currently running...

```sh
pgrep ssh-agent
```

The terminal should return the ID of the `ssh-agent` you started earlier, e.g...

```plaintext
6417
```

Since we’re done with that process, let’s kill it, e.g...

```sh
kill 6417
```

To verify the kill run...

```sh
pgrep ssh-agent
```

The terminal should NOT return the ID.

## Adding your public key to GitHub

We’ve created, saved, and configured SSH keys on your local machine, now let’s use them. Start by logging into [GitHub](https://github.com/login), and then...

1. Click on your profile photo, and select “Settings” from the menu
2. On the [Settings](https://github.com/settings/profile) page, click on the “SSH and GPG keys” link
3. On the [Keys](https://github.com/settings/keys) page, click on the “New SSH key” button

### Pasting your public key

On the [Add new SSH key](https://github.com/settings/ssh/new) page...

1. Enter a **Title** for your public key, e.g. “My personal laptop key”
2. Select “Authentication Key” from the **Key type** dropdown-menu
3. Copy your public key (see [instructions](#copying-your-public-key))
4. Then paste (⌘ + v) your public key into the **Key** textarea
5. Finally, click on the **Add SSH key** button

### Copying your public key

Open a terminal and run the `pbcopy` command to add your public key to your clipboard...

```sh
pbcopy < ~/.ssh/id_ed25519.pub
```

Then get back to [pasting](#pasting-your-public-key) your public key.

## Known hosts

Awesome work! All that’s left is to [test your SSH connection](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection). Once that’s done, you should see a `known_hosts` file inside of your `.ssh` directory. Open a terminal and run...

```sh
ls ~/.ssh/
```

The terminal should return something like...

```plaintext
config		id_ed25519	id_ed25519.pub	known_hosts
```

## Resources

- [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [ssh-agent and ssh-add](https://cylab.be/blog/230/ssh-agent-and-ssh-add#ssh-agent-and-ssh-add)
