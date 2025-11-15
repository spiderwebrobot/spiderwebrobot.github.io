+++
date = '2025-11-15T07:53:19-08:00'
draft = true
title = 'GitHub authentication with SSH'
summary = 'Command line access.'
+++

Once you have created a GitHub account, an [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh) key can help access your code repositories from your computer on the [command line](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line). Please note, these instructions for Mac users.

## Generating a new SSH key

Open up a terminal and navigate to your home directory

```sh
cd ~
```

Generate an SSH key (use the email associated with your GitHub account), e.g...
   ```sh
   ssh-keygen -t ed25519 -C "your@email.com"
   ```

You should be prompted to save the `id_ed25519` key to an `.ssh` folder in your home directory `/Users/username`, e.g...

```sh
> Generating public/private ed25519 key pair.
> Enter file in which to save the key (/Users/username/.ssh/id_ed25519):
```

Press the “return” key to accept this location, after which you should be prompted to enter a [passphrase](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases), e.g.

```sh
> Created directory '/Users/username/.ssh'.
> Enter passphrase (empty for no passphrase):
```

When you are done entering your passphrase, you'll be prompted to enter it again, e.g.

```sh
> Enter same passphrase again:
```

You’ll then receive a series of confirmations, starting with the location of your SSH keys (private and public), e.g.

```sh
> Your identification has been saved in /Users/username/.ssh/id_ed25519
> Your public key has been saved in /Users/username/.ssh/id_ed25519.pub
```

The key’s [fingerprint](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints), e.g.

```sh
The key fingerprint is:
```

And finally the key’s randomart image, e.g.

```sh
The key's randomart image is:
```

## Managing your SSH key with ssh-agent

Let’s add your key to an SSH agent to avoid entering the passphrase every time you use the key. The SSH agent manages your SSH keys and remembers your passphrase.

We’ll get started by running the ssh-agent in the background...

```sh
eval "$(ssh-agent -s)"
```

The agent should return a Process Identifier, e.g.

```sh
> Agent pid 6417
```

We’ll use that PID number later on to kill the ssh-agent running in the background, in the meantime you’ll need to create an SSH config file (if it doesn’t already exist)...

```sh
touch ~/.ssh/config
```

Then edit `~/.ssh/config`...

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Finally, add your SSH key to the SSH agent and store your passphrase in the keychain...

```sh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

You’ll be prompted to enter the passphrase, e.g...

```sh
Enter passphrase for /Users/username/.ssh/id_ed25519:
```

After which a confirmation message should be returned, e.g...

```ssh
Identity added: /Users/username/.ssh/id_ed25519 (your@email.com)
```


1. Review the running ssh-agent processes
   ```sh
   pgrep ssh-agent
   6417 # the PID
   ```
2. Kill the ssh-agent process
   ```sh
   kill 6417
   ```
3. Verify the kill
   ```sh
   pgrep ssh-agent
   ```

## Copy SSH keys to GitHub

1. Open a terminal
2. Copy the SSH key to your clipboard `pbcopy < ~/.ssh/id_ed25519.pub`


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
