# Creating a New Project

This scenario assumes you're starting a brand new project on your local machine and want to use Git and GitHub for version control and collaboration.

1. Create a new folder for your project. In your terminal (Git Bash, Terminal, or similar), run:
`mkdir github-workflows`

This makes a directory named `github-workflows` where all your project files will live.

2. Move into your project folder:
`cd github-workflows`

Now your terminal is 'inside' that folder, ready to work there.

3. Initialize a Git repository:
`git init`

This creates a hidden `.git` directory (file) inside your folder. That directory holds all the metadata Git needs to track changes in your project. From this point on, Git will monitor everything inside this folder.

**Note**: To align with most GitHub defaults, you s rename the initial branch to `main`: `git branch -M main`. We will be covering branches in another workflow.

4. Create your documentation file and a folder for scenarios:

   ```
   touch README.md
   mkdir workflows
   touch workflows/creating-new-project.md
   ```

   * `README.md` is where you’ll describe your project.
   * `workflows/` will hold each scenario as its own Markdown file.
   * Files ending in `.md` are Markdown files - similar plain tex but with simple formatting, ideal for documentation and READMEs.

5. Open and edit your files in your preferred editor (Visual Studio Code, Notepad++ etc.).

6. Use `git status` to check what Git sees right now.

You’ll see your two new items `README.md` and the `workflows/` folder listed as untracked.

`git status` reports:

   * what’s changed in your working directory (everything in your project folder)
   * which changes you’ve flagged for the next snapshot (the **staging area**)

The **staging area** is an area where you stage changes (new, modified, or deleted files) that you want in your next save - a **commit**. Think of **commit** as a 'save point', like hitting Save in your editor - it captures a snapshot of your project at that point in time.

7. To 'flag' all the files for your next snapshot (or **commit**) (i.e. move them into the staging area), run;:
`git add .`

This tells Git: “Include all files from the current folder in the upcoming snapshot.”

**Note**: To flag only a specific file, replace `.` with the file name, e.g.
`git add README.md`

8. You may run `git status` again, to confirm your files are staged for commit:
`git status`

9. Now let's create our first **commit** (snapshot) by running: 
`git commit -m "chore: initialize project structure"`

* `-m` lets you add a commit message inline. Standard is to use concise messages,  in imperative form - like "add feature" or "fix bug."

10. Now let's publish our project on GitHub:

    1. On GitHub.com, click **New repository**.
    2. Name it `github-workflows` (matching your folder name is recommended, altough not required).
    3. Do **not** initialize with a README, .gitignore, or license. (more on .gitignore and licence later)
    4. Click **Create repository**.
	
This is now our **remote repository**.

11. To 'connect' your local repository to the remote repository you just created, we're going to add a remote repository by using the command `git remote add`.

This command will take two arguments:
   - A name of your choosing, by which you'll refer to the remote repository (usually we use `origin`)
   - An URL to the remote repository (found on the repository page), something like: https://github.com/YourUsername/github-workflows.git

So, for me, the full command is:
`git remote add origin https://github.com/VladimirVuletic/github-workflows.git`

12. Now we have two repos — one locally, and one on GitHub. Our local repo has commits (it’s an actual project now), while the remote GitHub repo is still empty. We need to sync them up.

What we’ll do is `push` our changes (remember: we started with an empty local repo via git init, then **committed** changes) to the remote repo named origin.

Command is as follows:
`git push -u origin main`

Let’s break this down:
   - `git push origin main` will upload all commits (snapshots) on your local main branch that aren’t yet on the remote origin.
   - The flag `-u` (short for `--set-upstream`) tells Git to remember origin/main as the default for future pushes and pulls. After this, you can simply run `git push` (or `git pull`, more on that later) without specifying `origin main`.

13. Verify on GitHub.com that your files and commit message appear in the repository.

Congratulations - you're done! (But really only started!)
   - You’ve created a new project locally
   - Initialized a Git repo
   - Created a corresponding GitHub repo
   - And synced them. 
   
 Ready for the next core workflow: Making changes to your project?
