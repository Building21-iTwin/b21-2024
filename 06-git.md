# Getting started with GitHub

## What is Git?

A Git repository is a place to store source code that stores the current and all previous versions of each file. Once you save a change it can never be accidentally deleted.

## What is GitHub?

A website that hosts Git Repositories and has other services that developers use to build and maintain their code.

## How to get started?

Go to https://github.com and create an account, it's free!

Share user name so you can be added to the team.

## How to use GitHub

[GitHub Cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf)

Use 'Setup' instructions to configure.

Configuring user information used across all local repositories.  Use private email found here: http://github.com/settings/emails

1. set a name that is identifiable for credit when review version history
```bash
git config --global user.name “[firstname lastname]”
```
2. set an email address that will be associated with each history marker
```bash
git config --global user.email “[valid-email]”
```
3. set automatic command line coloring for Git for easy reviewing
```bash
git config --global color.ui auto
```

List all configs to make sure these settings wer applied correctly
```bash
git config --list
```

## Cleaning up your local repository

Before you can push your code online you need to be sure there are no secrets in it.  If there are someone will steal them.  The `.env` file in your repository has secrets in it.  

The `IMJS_AUTH_CLIENT_CLIENT_ID`, `IMJS_ITWIN_ID` and `IMJS_IMODEL_ID` variables are secret.  Create a new file `.env.local` and copy those three variables to that file.  Once copied blank them out in the `.env` file like below.

```bash
# ---- Authorization Client Settings ----
IMJS_AUTH_CLIENT_CLIENT_ID = ""
IMJS_AUTH_CLIENT_REDIRECT_URI = "http://localhost:3000/signin-oidc"
IMJS_AUTH_CLIENT_LOGOUT_URI = ""
IMJS_AUTH_CLIENT_SCOPES ="imodelaccess:read imodels:read realitydata:read"
IMJS_AUTH_AUTHORITY="https://ims.bentley.com"

# ---- Test ids ----
IMJS_ITWIN_ID = ""
IMJS_IMODEL_ID = ""
```

Make sure both files are saved before you move on.

## Check in your local changes

Changes must be committed before they can be pushed to GitHub.

Findout what changes are uncommitted using

```bash
git status
```

The result should look something like this

```bash
admin@pcf:~/src/phila-city$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .env
        modified:   package-lock.json
        modified:   src/App.tsx

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .devcontainer/
        src/providers/

no changes added to commit (use "git add" and/or "git commit -a")
```

Notice that the `.env.local` file is not listed.  That is intentional because it contains our secrets and should have been set to be ignored.

We must add the untracked files using `git add`

```bash
git add .devcontainer/*
git add src/providers/*
```

Run `git status` again, you should see the files in `.devcontainer` and `src/providers` are now listed as `new
`

Now we can commit the new and the modified files

```bash
git commit -m"First Commit" -a
```

Run `git status` again, you should see that there is nothing left to commit.

```bash
admin@pcf:~/src/phila-city$ git status
On branch master
nothing to commit, working tree clean
```

## Creating a repository on Github

1. Go to https://github.com and login with the account info you created above.
2. Click on the green "New Repository" button to start creating a new repo.
3. Enter a name for your repository. The name you used to create your app is a good idea.
4. Click "Create Repository" at the bottom of the page.

Now you can push your local repository to the one you just created on GitHub.  Replace `[URL TO GITHUB REPO]` with the url of your repository.

```bash
git remote add origin [URL TO GITHUB REPO]
git branch -M main
git push -u origin main
```

Refresh the github website, you should see your changes.