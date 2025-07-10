# Updating Your Project

This scenario assumes you already have an existing project both locally and on GitHub, and you want to make changes, incorporate any remote updates, and keep everything in sync. If you didn't do it already, you should do **Creating a New Project** scenario before this one.

Also, the following workflow will tell you about the easiest, however, arguably not the 'right' way to modify your project. After you've learned and understood the easiest way (without using **branches**), we'll talk about the right way.

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

And there we go! Your project is now updated and your local and remote repos are in sync. **However**, as we said in the beginning, this is not the right way to update your project, so let's talk about the branches.

When you first initialize a new repo, you only have one branch - the **main** branch. That's what the `git branch -M main` command is for, basically. If run immediately after `git init`, you will make sure that your one and only branch is called **main**, which is standard for GitHub. It used to be **master**, which is sometimes still the default, which is why we run that command.

**main** branch is where you want to keep your completely tested and approved code, the commits that passed with flying colors. **main** branch is supposed to be stable and is your best bet to be run on production.

Developers **DO NOT** push directly to **main**, and are usually not allowed to (you can forbid pushing directly to **main** in your remote repo settings).

The workflow to, for example, add a feature to the **main** branch is usually as follows:

1. First, make sure your local **main** is up to date by doing a `git pull`

2. Create a new branch called whatever you want by doing `branch new-feature` (new-feature is the name we chose here). This new branch, at this moment in time is the exact copy of your main branch. But from now on, changes done on each branch won't affect the state on the other branch, they are independant. 

3. 'Move' to the newly created branch. (You actually move the cursor called **HEAD**, but that's not that important right now) by doing:
`git checkout new‑feature`

4. If you're using *git bash*, you'll see that your branch is changed now. Also, if you're using Visual Studio Code, you can see your current branch.

5. Make the changes that you want to make to the files. Then do the same old staging and committing: 
`git add .`
`git commit -m "docs: modify updating-your-project.md via pull request`

6. Now we will push **the new branch** to our remote repo with: 
`git push origin new-feature`

7. Now if we go to the GitHub repo in our browser, we can see that the remote repo also has a new branch called new-feature. We now open what we is called a **pull request**. A pull request, or **PR**, is a request we will make to the main branch owner to pull the changes we made into the main branch. 

We're the main branch owner here, so we're playing the both roles in this case.

8. We click on the **Pull requests** tab, then **New pull requst**. We pick the main as the *base*, and the new-feature branch as the *compare*. 

Then we click on **Create pull request**, add more description if needed and finally click on **Create pull request**.

And finally (and this would be done by somebody else if it wasn't our repo) we click on **Merge pull request** and **Confirm merge**.

We get this message: 
> Pull request successfully merged and closed
> You're all set — the new-feature branch can be safely deleted.

And an option to delete the branch by clicking **Delete branch**, which we'll do.

After we've done that, we can delete that branch locally as well.

