+++
date = '2025-12-20T08:23:12-08:00'
draft = false
title = 'Cloning a GitHub repository'
summary = 'Create a local copy.'
+++

You’ve set up your [SSH keys](/posts/github-authentication-with-ssh/), now let’s use the [terminal](/posts/local-development-for-mac-users/#terminal) to clone your GitHub repository.

## Finding a GitHub repository’s SSH URL

Open a browser and visit your GitHub repository, e.g. https://github.com/spiderwebrobot/spiderwebrobot.github.io.

Click on the **Code** dropdown-button. In the dropdown-panel, inside of the **Local** tab (under the **SSH** subnavigation), click on the ![Copy URL to clipboard](/copy.svg) icon.

Your repository’s SSH URL should have been copied to your clipboard, e.g. `git@github.com:spiderwebrobot/spiderwebrobot.github.io.git`

## Making a local copy of a repository

Open a terminal and create a workspace directory, e.g...

```sh
mkdir ~/workspace
```

Navigate into the workspace directory...

```sh
cd ~/workspace
```

Clone your repository, e.g...

```sh
git clone git@github.com:spiderwebrobot/spiderwebrobot.github.io.git
```

The terminal should respond with something like...

```plaintext
Cloning into 'spiderwebrobot.github.io'...
remote: Enumerating objects: 237, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 237 (delta 0), reused 0 (delta 0), pack-reused 232 (from 1)
Receiving objects: 100% (237/237), 4.98 MiB | 3.14 MiB/s, done.
Resolving deltas: 100% (80/80), done.
```

### Known hosts

If you are cloning a GitHub repository to your computer for the first time, you may run into an “authenticity” message. Not to worry, check out [Testing your SSH connection](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection) to store GitHub’s public key in your [known_hosts](/posts/github-authentication-with-ssh/#known-hosts) file.

## Configuring a GitHub repository

Open a terminal and navigate into your cloned repository, e.g...

```sh
cd ~/workspace/spiderwebrobot.github.io
```

Establish your identity (replacing `Your Name` and `your@email`), e.g...

```sh
git config user.name "Your Name" && git config user.email your@email.com
```

Specify `push` and `pull` behaviors...

```sh
git config pull.rebase false && git config push.default current
```

Verify your config changes...

```sh
git config --list
```

The terminal should return something like...

```plaintext
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=git@github.com:spiderwebrobot/spiderwebrobot.github.io.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
user.name=Your Name
user.email=your@email.com
pull.rebase=false
push.default=current
```

Including the `user.name`, `user.email`, `pull.rebase`, and `push.default` configs that you just added.

## Resources

- [Cloning with SSH URLs](https://docs.github.com/en/get-started/git-basics/about-remote-repositories#cloning-with-ssh-urls)
- [Git Guides - git pull](https://github.com/git-guides/git-pull)
- [Git Guides - git push](https://github.com/git-guides/git-push)
- [Octicons](https://primer.style/octicons/)
