+++
date = '2025-11-15T07:53:19-08:00'
draft = true
title = 'GitHub authentication with SSH'
summary = 'Command line access.'
+++

Once you have created a [GitHub account](/posts/creating-a-github-account), an [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh) key can help access your code repositories from your computer through the [command line](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line). Please note, these instructions for Mac users.

## Generate a new SSH key

Open a terminal and navigate to your home directory...

```sh
cd ~
```

Generate an SSH key (use the email associated with your GitHub account), e.g...

```sh
ssh-keygen -t ed25519 -C "your@email.com"
```

You should be prompted to save the `id_ed25519` key to a `.ssh` folder in your home directory `/Users/username`, e.g...

```plaintext
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/username/.ssh/id_ed25519):
```

Press “return” to create a `.ssh` folder (if it doesn’t already exist), e.g...

```plaintext
Created directory '/Users/username/.ssh'.
```

And enter a [passphrase](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)...

```plaintext
Enter passphrase (empty for no passphrase):
```

Then enter it again...

```plaintext
Enter same passphrase again:
```

Nice work! You should see several confirmations, starting with the location of your private and public SSH keys, e.g...

```plaintext
Your identification has been saved in /Users/username/.ssh/id_ed25519
Your public key has been saved in /Users/username/.ssh/id_ed25519.pub
```

The key’s [fingerprint](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints), e.g...

```plaintext
The key fingerprint is:
SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU your@email.com
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

## Managing your SSH key with ssh-agent

Let’s add your key to an SSH agent to avoid entering the passphrase every time you use the key. The SSH agent manages your SSH keys and remembers your passphrase.

We’ll get started by running the ssh-agent in the background...

```sh
eval "$(ssh-agent -s)"
```

The agent should return a Process Identifier, e.g...

```plaintext
Agent pid 6417
```

We’ll use that process ID to kill the ssh-agent running in the background, in the meantime, let’s create an SSH config file (if it doesn’t already exist)...

```sh
touch ~/.ssh/config
```

Edit `~/.ssh/config`...

```plaintext
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Finally, add your private SSH key to the SSH agent, and store your passphrase in the keychain...

```sh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

You’ll be prompted to enter the passphrase, e.g...

```plaintext
Enter passphrase for /Users/username/.ssh/id_ed25519:
```

After which a confirmation message should be returned, e.g...

```plaintext
Identity added: /Users/username/.ssh/id_ed25519 (your@email.com)
```

Review the running ssh-agent processes

```sh
pgrep ssh-agent
```

Should return a process ID, e.g...

```plaintext
6417
```

Kill the ssh-agent process

```sh
kill 6417
```

Verify the kill...

```sh
pgrep ssh-agent
```

Should return no process IDs.

## Copy SSH keys to GitHub

1. Open a terminal
2. Copy the SSH key to your clipboard `pbcopy < ~/.ssh/id_ed25519.pub`

yep...

1. Open a browser
2. Visit https://github.com/
3. Click on profile photo, and select "Settings" from the menu (top right corner of the screen)
4. On the settings-page, click on the "SSH and GPG keys" link (right side of the screen)
5. On the ssh-and-gpg-keys page, click on the "New SSH key" button (right side of the screen)

On the "Add new SSH Key" page fill in the

1. "Title", e.g. "Home"
2. "Key type", select "Authentication Key" from the dropdown-menu
3. "Key", see clipboard instructions

## Resources

- [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
