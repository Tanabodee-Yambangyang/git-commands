# Quick Guide to Git


***By Tanabodee Yambangyang***

## Using Git

---
### Table of contents
| No. | Contents |
|--------|--------|
| 1 | [Basics](#basics)|
| 2 | [Adding and Changing Things](#adding-and-changing-things)  |
| 3 | [Undo Changes and Recover Files](#undo-changes-and-recover-files)   |
| 4 | [Viewing Commits](#viewing-commits)  |
| 5 | [Branch and Merge](#branch-and-merge) |
| 6 | [Commands for Remotes](remote-commands.md) |
| 7 | [Favorites](#favorites) |
| 8 | [Resources](#resources) |


#### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.    

## Basics

1. When using Git locally, what are these?  Define each one in a sentence
   * Staging area - Space where you can add, remove or preview files before committing. 
   * Working copy - A feature of Git which allows you to clone your Git repositories onto your devices.
   * master - The default branch name of Git.
   * HEAD - Is a pointer that points to the latest commit you are viewing on a current branch.

2. When you install git on a new machine (or in a new user account) you should perform these 2 git commands to tell git your name and email.  These values are used in commits that you make:
   ```
   # Git configuration commands for a new account
   
   1.Tell git your name
   git config --global user.name "your_username"
   
   2.Tell git your email
   git config --global user.email "your_email_address"
   ```

3. There are 2 ways to create a local Git repository.  What are they?
   
   > ***1.Initializing a Repository in an Existing Directory:*** If you want to get controlling your project with Git. You can create a new empty Git repository by going to your project’s directory and then type `git init` command. You can then add your files by typing `git add` and finally using `git commit` to commit all your files.   
   
   > ***2.Cloning an Existing Repository:*** If you want to get a copy of an existing Git repository. You can use `git clone <url>` that'll create a directory initializes a `.git` directory inside it and pulls down all the data for that repository.
   

4. When you create a git repository by entering `git init`, Git will create a "hidden" directory for the local repository.  Where is the directory for this local repository (relative to the directory where you typed "git init")?
   
   > ***Answer:*** When you type `git init`. Git will create a hidden directory in the project root folder.


## Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:
```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```

1. Add README.md and *everything* in the `src` directory to the git staging area.
   ```
   git add README.md
   git add src/
   ```

2. Add `test/test_a.py` to the staging area (but not any other files).
   ```
   git add test/test_a.py
   ```

3. List the files in the staging area.
   ```
   README.md
   src/a.py
   src/b.py
   src/c.py
   test_a.py
   ```
4. Remove `README.md` from the staging area. (Useful if you accidentally add something you don't want to commit.)
   ```
   git rm README.md
   ```
5. Commit everything in the staging area to the repository.
   ```
   git commit
   ```
6. Describe 2 steps to configure the repository so git will ignore all files in the `out/` directory:
   >***step one:*** Create a file name `.gitignore` in your directory
   
   > ***step two:*** Type `out/` in `.gitignore` file, and git will ignore all files that have been typed in `.gitignore`. So, git will ignore `out/`
7. Command to move all the .py files from `src` to the top-level directory of this repository, so they are also moved in the Git repo.
   ```
   git mv src/a.py
   git mv src/b.py
   git mv src/c.py
   ```
8. Commit this change with the message "moved src directory":
   ```
   git commit -m "moved src directory"
   ```
9. Command to add **all changed files** (but not untracked files) to the staging area using a single command.
   ```
   git add -u
   ```
10. **Delete** the file `c.py` from your working copy **and** the repository:
    ```
    git rm c.py
    ```
## Undo Changes and Recover Files

1. Display the differences between your *working copy* of `a.py` and the `a.py` in the *local repository* (HEAD revision):
   ```
   git diff a.py
   ```
2. Display the differences between your *working copy* of `a.py` and the version in the *staging area*. (But, if a.py is not in the staging area this will compare working copy to HEAD revision):
   ```
   git diff --cached a.py
   ```
3. **View changes to be committed:** Display the differences between files in the staging area and the versions in the repository. (You can also specify a file name to compare just one file.) 
   ```
   git diff --cached
   ```
4. **Undo "git add":** If `main.py` has been added to the staging area (`git add main.py`), remove it from the staging area:
   ```
   git rm --cached main.py
   ```
5. **Recover a file:** Command to replace your working copy of `a.py` with the most recent (HEAD) version in the repository.  This also works if you have deleted your working copy of this file.
   ```
   git restore a.py
   ```
6. **Undo a commit:** Suppose you want to discard some commit(s) and move both HEAD and "master" to an earlier revision (an earlier commit)  Suppose the git commit graph looks like this (`aaaa`, etc, are the commit ids)
   ```
   aaaa ---> bbbb ---> cccc ---> dddd [HEAD -> master]
   ``` 
   The command to reset HEAD and master to the commit id `bbbb`:
   ```
   git reset --hard bbbb
   ```
7. **Checkout old code:** Using the above example, the command to replace your working copy with the files from commit with id `aaaa`:
   ```
   git checkout aaa
   ```
   
    Note:
    - Git won't let you do this if you have uncommitted changes to any "tracked" files.
    - Untracked files are ignored, so after doing this command they will still be in your working copy.
 

## Viewing Commits

1. Show the history of commits, using one line per commit:
   ```
   git log --oneline
   ```
* Some versions of git have an *alias* "log1" for this (`git log1`).
2. Show the history (as above) including *all* branches in the repository and include a graph connecting the commits:
   ```
   git log --oneline --decorate --graph
   ```

3. List all the files in the current branch of the repository:
   ```
   git ls-files
   ```
   example output:
   ```
   .gitignore
   README.md
   a.py
   b.py
   test/test_a.py
   test/test_b.py
   ```
   
## Branch and Merge

1. Create a new branch named `dev-foo`:
   ```
   git branch dev-foo
   ```
2. Display the name of your current branch:
   ```
   git branch –show-current
   ```
3. List the names of **all** branches, including remote branches:
   ```
   git show-branch -r
   ```
4. Switch your working copy to the branch named `dev-foo`:
   ```
   git checkout dev-foo
   ```

5. **Merge:** To merge the work from `dev-foo` into the master branch, perform these steps:
   1. step one
      ```
      Type git checkout master to change the branch to master branch
      ```
   2. step two
      ```
      Type the command git merge dev-foo to merge the work from `dev-foo` into the master branch
      ```
   
6. Describe under what conditions a merge may fail.
   >`git merge` may fail because the user has committed changes that conflict with the committed 
   > changes other users have made.
     
## Favorites
> ***(a) Git task I would like to remember or think is really useful:*** I think the most useful git task for me is the </br>task for correcting mistakes on the repository such as, removing data or changing file names.
   
> ***(b) Git commands of that task:*** To remove data on repository use `git rm <file_name>`, to move or rename </br>files on repository use `git mv <file_name> <other_file>`



---
## Resources

#### My favorite Git resources.

   * [Atlassian Git Tutorial](https://www.atlassian.com/git)
   * [Git Tower](https://www.git-tower.com/learn/git/ebook/)
   * [Pro Git](https://git-scm.com/book/en/v2)
   * [Learn Git Branching](https://learngitbranching.js.org/)

[Pro Git Online Book][ProGit] Chapters 2 & 3 contain the essentials. Downloadable PDF is also available.     
[Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.

Try Git:

[Learn Git Interactive Tutorial][LearnGitInteractive] excellent visual tutorial.   
[Git Visualizer][VisualizeGit] execute Git commands in a web browser and see the results as a graph.    

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
[markdown-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[github-markdown]: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
[vscode-markdown-preview-enhanced]: https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced
