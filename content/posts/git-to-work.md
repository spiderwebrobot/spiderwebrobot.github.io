+++
date = '2025-12-24T06:32:20-08:00'
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

## Syncing with the main

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

## Pushing your commits

After syncing with `main`, push your changes...

```sh
git push
```

## Create a pull-request

1. Open a browser
2. Navigate to the "Your branches" page, e.g. `https://github.com/spiderwebrobot/spiderwebrobot.github.io/branches`
3. On the "Your branches" page, click on the "..." associated with your branch to expand the menu.
4. Click on the "New pull request" option from in the expanded menu
4. On the "Comparing changes" page, click on the "Create pull request" button

## Deployment

1. Open a browser
2. Navigate to the "Pull requests" page, e.g. `https://github.com/spiderwebrobot/spiderwebrobot.github.io/pulls`
3. On the "Pull requests" page, click on the feature-branch to be merged
4. Select "Squash and merge" from the "Merge pull request" dropdown menu (if it is not already selected)
5. Click on the "Squash and merge" button
6. Click on the "Confirm squash and merge" button
7. Click on the "Delete branch" button

## Resources

* [GitHub Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet/)
* [Conventional Branch](https://conventional-branch.github.io)
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
