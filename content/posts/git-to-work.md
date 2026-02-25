+++
date = '2026-02-18T06:32:20-08:00'
draft = true
title = 'Git to work'
summary = 'Version control.'
+++

Now that you’ve [cloned](/posts/cloning-a-github-repository/) a GitHub repository, let’s make some changes.

## The main branch

Open a terminal and navigate into your cloned repository, e.g...

```sh
cd ~/workspace/spiderwebrobot.github.io
```

Then list all branches...

```sh
git branch
```

The terminal should return something like...

```plaintext
* main
```

If `main` is NOT the active branch (`*`), check it out...

```sh
git checkout main
```

And pull in the latest changes...

```sh
git pull
```

The terminal should return something like...

```plaintext
Already up to date.
```

## Branching off of main

After `main` has been updated, start a new branch, e.g...

```sh
git checkout -b chore/update-readme
```

And verify its creation...

```sh
git branch
```

The terminal should return something like...

```plaintext
* chore/update-readme
  main
```

## Making changes

After creating a new branch, edit the `README.md` file, e.g...

```md
# Your dogs must be barking 🐶

Why don’t you come in and sit a spell?
```

When you’re done making changes, check the staging area...

```sh
git status -su
```

The terminal should return something like...

```plaintext
 M README.md
```

Where `M` indicates the file was modified.

## Adding and committing changes

When you’re ready, add your changes...

```sh
git add README.md
```

And then commit your changes...

```sh
git commit -m "Changes to README"
```

Your terminal should return something like...

```plaintext
[chore/update-readme 1e31fad] Changes to README
 1 file changed, 12 insertions(+), 1 deletion(-)
```

## Syncing with main

After committing your changes, check out `main`...

```sh
git checkout main
```

And pull in its latest changes...

```sh
git pull
```

Then switch back to your working branch, e.g...

```sh
git checkout chore/update-readme
```

And merge the latest changes from `main`...

```sh
git merge main
```

Your terminal should return something like...

```plaintext
Already up to date.
```

## Pushing commits

After syncing with `main`, push your changes...

```sh
git push
```

The terminal should return something like...

```plaintext
Enumerating objects: 15, done.
Counting objects: 100% (15/15), done.
Delta compression using up to 8 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (10/10), 2.20 KiB | 2.20 MiB/s, done.
Total 10 (delta 4), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (4/4), completed with 3 local objects.
remote: 
remote: Create a pull request for 'chore/update-readme' on GitHub by visiting:
remote:      https://github.com/spiderwebrobot/spiderwebrobot.github.io/pull/new/chore/update-readme
remote: 
To github.com:spiderwebrobot/spiderwebrobot.github.io.git
 * [new branch]      chore/update-readme -> chore/update-readme
```

## Creating a pull-request

Open a browser, [log into GitHub](https://github.com/login), and navigate to the “Branches” page, e.g...

```plaintext
https://github.com/spiderwebrobot/spiderwebrobot.github.io/branches
```

On the “Branches” page, click on the “...” button to expand your branch’s menu, and then click on the “New pull request” option, e.g...

```plaintext
https://github.com/spiderwebrobot/spiderwebrobot.github.io/pull/new/chore/update-readme
```

On the “Open a pull request” page, click on the “Create pull request” button.

## Merging a pull-request

Open a browser and navigate to the “Pull requests” page, e.g....

```plaintext
https://github.com/spiderwebrobot/spiderwebrobot.github.io/pulls
```

On the “Pull requests” page, click on the pull request to be merged, and then select “Squash and merge" from the “Merge pull request” dropdown menu.

Click on the “Squash and merge” button, then click on the “Confirm squash and merge” button, and finally, click on the “Delete branch” button.

## Resources

* [GitHub Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet/)
* [Conventional Branch](https://conventional-branch.github.io)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
