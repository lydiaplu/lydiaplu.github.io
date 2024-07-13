---
title: Common Git Commands  
date: 2017-01-15 21:10:23  
toc: true  
categories:  
- Uncategorized  
---

#Common Git Commands  

### Git Workflow

1. **Downloading Code**

   - Assign a Git account or generate your own public and private keys, then submit the public key to the Git administrator.
   - Clone the remote repository with `git clone`.
   - Develop based on the downloaded code and then commit your changes.

2. **Creating a New Project**

   - Create a new repository on the server.
   - Generate a local repository with `git init`, develop in this repository, and commit the code after development.
   - Then push the code to the empty repository on the server.

### Three Important Areas in Git

1. **Working Directory**

   The content extracted independently from a particular version of the project. These files are extracted from the compressed database of the Git repository and placed on the disk for you to use or modify.

2. **Staging Area**

   A file that stores the list of information about files to be committed next. It is usually located in the Git repository directory and is sometimes referred to as the index, but it is generally called the staging area.

3. **Local Repository**

   The place where Git stores the project's metadata and object database. This is the most important part of Git. When you clone a repository from another computer, you are copying this data.

### Four States of Git Files

1. **Untracked**

   Files just created in the working directory.

2. **Staged**

   Files that have been moved from the working directory to the staging area.

3. **Committed**

   Files that have been committed from the staging area to the local repository.

4. **Modified**

   Files that have been modified in the staging area.

### Git Commands

1. Initialize a Repository

   ```shell
   git init
   ```

2. Configure User Information

   ```shell
   git config --global user.name "Name"
   git config --global user.email "Email"
   ```

3. Check File Status

   ```shell
   git status
   ```

4. Add Untracked Files to the Staging Area

   ```shell
   git add file (Separate multiple files with spaces)
   git add -A (Add all files)
   git add *  (Also add all files)
   ```

5. Remove Files from the Staging Area

   ```shell
   git rm --cached file (Separate multiple files with spaces)
   ```

6. Commit the Staging Area to the Local Repository

   ```shell
   git commit -m 'Description'
   ```

7. View Local Repository Commit Records

   ```shell
   git log
   ```

8. Discard Changes in the Staging Area

   ```shell
   git checkout -- files
   ```

   Discard all changes in the staging area

   ```shell
   git checkout .
   ```

9. Overwrite the Working Directory and Staging Area with a Snapshot from the Local Repository, Discarding Commits After a Specific Commit ID

   ```shell
   git reset --hard <commitID>
   ```

10. Overwrite the Staging Area with the Latest Version from the Local Repository Without Overwriting the Working Directory

    Essentially cancels the `git add` operation

    ```shell
    git reset HEAD
    ```

### Branch Commands

1. Create a Branch

   If no branch name is provided, it lists the current branches. `*` indicates the current branch.

   ```shell
   git branch branch_name
   ```

2. View Remote Branches

   ```shell
   git branch -r
   ```

3. View Local and Remote Branches

   ```shell
   git branch -a
   ```

4. Delete a Branch

   ```shell
   git branch -d branch_name
   ```

5. Switch Branches

   ```shell
   git checkout branch_name
   ```

6. Merge Branches

   ```shell
   git merge branch_name (Source branch)
   ```

7. Create and Switch to a Branch

   Equivalent to running `git branch` and `git checkout` simultaneously

   ```shell
   git checkout -b branch_name
   ```

8. Fetch from Remote Repository Without Merging

   ```shell
   git fetch
   ```

9. Merge Fetched Code

   ```shell
   git merge
   ```

10. Delete Remote Branch

    ```shell
    git push origin --delete branch_name
    git push origin:branch_name
    ```

### Shared Repository

Create a folder ending with `.git` locally, then run the following command in this `.git` folder:

```shell
git init --bare
```

### Push Code

1. Push Code to a Remote Repository

   ```shell
   git push remote_repo_url local_branch:remote_branch
   ```

   If the local and remote branch names are the same, you can omit the remote branch name.

   ```shell
   git push remote_repo_url local_branch
   ```

2. Pull Code from a Remote Repository

   ```shell
   git pull remote_repo_url remote_branch:local_branch
   ```

   If the local and remote branch names are the same, you can omit the local branch name.

   ```shell
   git pull remote_repo_url remote_branch
   ```

3. Clone a Remote Repository

   When cloning, an alias `origin` is automatically generated for the remote repository.

   ```shell
   git clone remote_repo_url directory_name (Optional, defaults to the remote repository name)
   ```

4. Add an Alias for a Remote Repository

   ```shell
   git remote add alias_name remote_repo_url
   ```

5. View Remote Repository Aliases

   ```shell
   git remote
   ```

6. View the Specific URL of a Remote Repository Alias

   ```shell
   git remote show origin
   ```

7. Push Code Using an Alias

   ```shell
   git push origin master:master
   ```

8. Push Code Using an Alias

   ```shell
   git push
   ```

9. Pull Code Using an Alias

   `git pull` is equivalent to running `git fetch` and `git merge` simultaneously.

   ```shell
   git pull
   ```

10. Set Upstream Branch for Tracking After Pulling Code

    ```shell
    git branch --set-upstream-to=origin/master master
    ```

    - `origin/master` indicates the remote branch.
    - `master` indicates the local branch.

11. Save Work Scene to Temporarily Switch to Other Work

    ```shell
    git stash
    ```

12. Resume Work Scene After Other Work is Done

    ```shell
    git stash pop
    ```

**Difference Between `git pull` and `git clone`**

1. `git clone` automatically creates an alias `origin` for the remote repository URL.
2. `git clone` automatically tracks remote branches, so you can directly use `git pull` to update code.

### Other Git Operations

#### Ignoring Files with `.gitignore`

Create a `.gitignore` file in the project's root directory to list files that should not be committed, such as project configuration files and `node_modules`.

#### Comparing Differences

When content is modified and you are unsure what has changed, you can use `git diff` to compare differences.

1. Compare differences between the working directory and the staging area.

   ```shell
   git difftool
   ```

2. Compare differences with a specific commit.

   ```shell
   git difftool "SHA"
   ```

3. Compare differences between two commits.

   ```shell
   git difftool "SHA1" "SHA2"
   ```

4. Compare differences with a branch.

   ```shell
   git difftool branch_name
   ```