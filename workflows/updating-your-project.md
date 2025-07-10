# Updating Your Project

This scenario assumes you already have an existing project both locally and on GitHub, and you want to make changes, incorporate any remote updates, and keep everything in sync. If you didn't do it already, you should do **Creating a New Project** scenario before this one.

1. Make your changes locally

   * Open your project in your editor (VS Code, Sublime, Vim, etc.)
   * Edit, add, or delete files as needed for your update

2. Check the status of your working directory and the staging area with `git status`.  You’ll see which files are modified, added, or deleted.

For me, I have two changes that are not staged for a commit: 
    modified:   README.md
    modified:   workflows/creating-new-project.md

And one untracked file:
    workflows/updating-your-project.md

3. To add **all** changes in the current directory to the staging area we can use `git add .` However, sice I've modified one scneario and added a new one, it makes more sense for me to actually do two separete commits, so that's what I'm going to do.
`git add README.md workflows/creating-new-project.md`

4. Now let's create a **commit** with a descriptive message:
`git commit -m "docs: modify creating-new-project.md"`

**Note**: We can use prefixes like `feat:`, `fix:`, `docs:`, or `chore:` to keep commit messages consistent. You can see the full proposed list here: https://www.conventionalcommits.org/en/v1.0.0-beta.2/#summary

5. Now let's make another commit for the new scenario we added. But first, we add it to the staging area. We can do `git add .` for the whole directory, since it's the only uncommited change anyways. And then we do:
`git commit -m "docs: add new scenario updating-your-project.md"`

5. Now before we `push` our updates to the remote repo, it's good practice to `pull` first. We do this so we don't overwrite others' work, and to have the latest version locally.

Pull from the remote repo won't overwrite the changes we've made locally, it will only pull all the commits that maybe happened in the meantime. However, if somebody else was working on the same files in the same place, we will get a **merge coflict**, but more on that later.

For now, let's just pull the updates from remote to the local. 

We can do `git pull origin main`, or, since we've already set the upstream in the previous scenario **Creating a New Project**, we can simply do `git pull`.

In my case, I'm getting `Already up to date.` messages, so there's nothing to worry or think about.

6. Now we're ready to `push`. Again, we can do `git push origin main`, or simply `git push`, since the upstream is already set.

   * If there are merge conflicts, resolve them in your editor, then stage and commit the resolutions:

     ```bash
     git add .
     git commit -m "fix: resolve merge conflicts"
     ```

6. Push your local commits to GitHub:

   ```bash
   git push
   ```

   * Because you previously set the upstream with `-u`, you can omit `origin main`

7. Verify on GitHub.com that your new commit appears and your project is up to date.

**Side‑note:**

* Always pull (`git pull`) regularly when collaborating to minimize conflicts.
* Consider using branches for larger updates: create a branch (`git checkout -b my-feature`), work there, then merge via a pull request.
* Keep commit messages clear and concise to make your project history easy to read.






# Updating Your Project

This scenario assumes you already have an existing project both locally and on GitHub, and you want to make changes, incorporate any remote updates safely, and keep everything in sync.

1. Make your changes locally

   * Open your project in your editor (VS Code, Sublime, Vim, etc.)
   * Edit, add, or delete files as needed for your update

2. Check the status of your working directory:

   ```bash
   git status
   ```

   * You’ll see which files are modified, added, or deleted

3. Stage your changes:

   * To stage all changes in the current directory:

     ```bash
     git add .
     ```
   * Or to stage individual files:

     ```bash
     git add path/to/changed-file.js
     ```

4. Create a commit with a descriptive message:

   ```bash
   git commit -m "feat: describe your update here"
   ```

   * Use prefixes like `feat:`, `fix:`, `docs:`, or `chore:` to keep commit messages consistent

5. Fetch remote updates without merging immediately:

   ```bash
   git fetch origin
   ```

   * This downloads new commits from the remote `origin` but does **not** change your local files or branches.
   * To see what’s new on the remote before merging:

     ```bash
     git log HEAD..origin/main
     git diff origin/main..HEAD
     ```

6. Merge remote changes into your branch (safe integration):

   ```bash
   git merge origin/main
   ```

   * This combines the fetched commits from `origin/main` into your current branch.
   * If there are conflicts, Git will pause, and you’ll need to resolve the conflicting files, then:

     ```bash
     git add .
     git commit -m "fix: resolve merge conflicts"
     ```

   **Why use `fetch` + `merge` instead of `pull`?**

   * `git pull` is shorthand for `git fetch` + `git merge` in one step. It won’t overwrite your local commits, but doing it separately gives you a chance to review changes before merging.

7. Push your local commits (including the merge) to GitHub:

   ```bash
   git push
   ```

   * Since you set the upstream branch before, you can omit `origin main`.

8. Verify on GitHub.com that your new commit and merged updates appear.

**Side‑notes:**

* `git fetch` never overwrites your working files; it only updates remote-tracking branches.
* A plain `git pull` also won’t overwrite committed work, but may automatically merge and create a merge commit.
* For larger features or experiments, consider creating a new branch (`git checkout -b my-feature`) and later merging via a Pull Request on GitHub.
