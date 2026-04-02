# Collaborative git exercise

## Push access to same repository.

In this exercise, we will work on a Github workflow, where both users have push access to the same repository. Be sure to create a new Github repository and use a different local directory compared to the exercise last week.

The basic idea of this workflow is that:

- *User B* will host a GitHub repository
- *User A* __and__ *User B* will have push access to the repository
- the `main` branch of the GitHub repo is the "stable" version of the code
	- neither user will ever push directly to the `main` branch
- each user will use their own `main` branch to track the stable version of the code
- in order for e.g., *User A* to update the stable code base, they will take the following steps:
	- make sure that the local `main` branch is up to date with the remote `main` branch
	- create a local `devel` branch from the local `main` branch
	- make changes to the code on the local `devel` branch
	- push the `devel` branch to GitHub
	- submit a pull request on GitHub to merge `devel` into `main` and request a code review from *User B*
	- *User B* then `fetch`es the remote `devel` branch and tests it out locally
	- when they are satisfied that it works, *User B* merges into `main` 
	- *User B* pushes `main` back to the remote to close the PR
	- Both users update their local `main` branches

## Determine users

Assign one partner to be *User A* and one partner to be *User B*.

## User B: confirm code base is stable

*User B* should download and unzip the project files from Canvas. *User A* __does not__ need to download and unzip the project folder because they will download it in a later step from *User B*'s GitHub.

*User B* should move the files/directory to a desired location on *User B*'s computer either using the command line or a file browser.

- Do not use the same directory as last week. We will be setting up entirely new git  and GitHub repositories for this week.

	- E.g., you could have a directory `git_exercises` that contains two directories called `first_folder` and `second_folder`, where `first_folder` is the git repository used in the exercise last week and `second_folder` is the folder that contains the files that you just downloaded and unzipped.

Once the files are in their desired location, *User B* should confirm that they can build the report (e.g., by executing `make`).

- If the report does not build, correct code until it builds correctly


### User B: Initialize git repository

*User B* should initialize a local git repository.

1. Use `git init` to initialize a git repository in your project directory folder
2. Appropriately use `git status`, `git add`, and `git commit` to create your first commit. The commit should include: 
- all contents of the `code` directory
- `report.Rmd`
- `README.md`
- `Makefile`
- `.gitignore`
- the `output` directory (i.e., the `output/.gitkeep` file)

### User B: Create a GitHub repository

*User B* should create a GitHub repository using the following steps.

1. Log in to GitHub and create an empty GitHub repository.

- be sure to select the option not to add a README nor a license.
- choose any name for the repository you like

2. *User B* uses `git remote add origin git@github.com:<user_b_github_name>/<user_b_repo_name>` to add *User B*'s GitHub repository as a remote of *User B*'s local repository named `origin`.

- replace `<user_b_github_name>` and `<user_b_repo_name>` with *User B*'s GitHub user name and GitHub repository name, repsectively
- be sure to use the "ssh" style syntax for adding a remote and not "https". I.e., your command should be `git remote add origin git@github.com:...` and __not__ `git remote add origin https://github.com/...`.
- You can confirm what web address was used to add the remote by executing `git remote -v`. 
- If the output of `git remote -v` shows that `origin` points to `https://github.com/<user_b_github_name>/<user_b_repo_name>`, then *User B* should remove the origin `remote` using `git remote remove origin` try Step 2 again.

3. Use `git push origin <your_branch_name>` to push *User B*'s local repository to GitHub.
- `<your_branch_name>` is probably `main`, but it may be `master` for some of you.
4. Refresh the web page for *User B*'s GitHub repository's to confirm that the push was successful.

### User B: Add *User A* as a collaborator on the GitHub repository

1. *User B* should navigate to the `Settings` tab of their repository on GitHub.
2. On the left side bar menu, select `Collaborators`.
3. Under `Manage Access` select `Add people` and add *User A* by typing in their GitHub user name.

------------------------------------------------------------------------

### User A: Accept invitation to *User B*'s GitHub

1. *User A* should check for an email from GitHub inviting them to join *User B*'s repository as a collaborator.

2. Accept the invitation.

### User A: Clone the repository

1. *User A* should use `cd` in their terminal to navigate to a directory where they wish to download *User B*'s (shared) repository.

2. *User A* should execute `git clone git@github.com:<user_b_name>/<user_b_repo>` to clone the repository.

- Note the use of __*User B*'s user name__ in the above.
- be sure to use the `git@github.com:<user_b_name>/<user_b_repo>` syntax and __not__ `https://github.com/<user_b_name>/<user_b_repo>` syntax.

3. *User A* should confirm that a folder called `<user_b_repo>` was added to the current working directory of their terminal.
	
- E.g., use `cd <user_b_repo>` and `ls` to change working directory into the newly downloaded repository and list its contents.
- You can confirm what web address was used to add the remote by executing `git remote -v`.
- If the output of `git remote -v` shows that you accidentally used `https://` syntax in your `git clone` command then *User A* should remove the origin `remote` using `git remote remove origin` and then re-add the remote using "ssh"-style syntax: `git remote add origin git@github.com:<user_a_name>/<user_a_repo>`.
- If the output of `git remote -v` shows that you correctly used `git@github.com:...` syntax in your `git clone` command, then *User A* can move on.


------------------------------------------------------------------------

### User A and B: Confirm that both users have `origin` remote

Both *User A* and *User B* should execute `git remote -v` and confirm that both users have a remote called `origin` that points to `git@github.com:<user_b_name>/<user_b_repo>`.

- Recall that `origin` is an appropriate name for both remotes, because the code for both local repositories "originates" from the same GitHub repository.

------------------------------------------------------------------------

### User A: Update the repository and submit a pull request

*User A* will now make a new branch and make updates to the stable code base. *User A* should complete the following steps:

1. Create and checkout a new branch called `devel-titles` by executing `git checkout -b devel-titles`.

- recall that this simultaneously creates and checks out a new branch called `devel-titles`
- confirm that *User A* has switched to the new branch by executing `git branch`
- you should see `main` and `*devel-titles`

2. Change the section headers of the "Random numbers `x`" to read "Distribution `x`" (i.e., sections should be Distribution 1, Distribution 2, and Distribution 3).

3. Confirm that *User A* can build the report (e.g., by executing `make report.html`)

4. Once *User A* is confident that `report.html` is building properly and that the titles have been changed, they should appropriately use `git add` and `git commit` to make a new commit along the `devel-titles` branch that includes updates `report.Rmd`.

- include a meaningful commit message

5. Push the `devel-titles` branch to GitHub.
- `git push origin devel-titles`

6. Submit a pull request to the shared repository.

- the pull request should request that the `devel-titles` branch be merged into the `main` branch.
- *User A* should request a code review from *User B*

------------------------------------------------------------------------

### User B: Test out pull request code

*User B* will now `fetch` the code submitted by *User A*, test it out, and eventually merge it into their `main` branch, thereby closing the pull request.

1. First, *User B* should confirm that their local `main` branch is up to date with the remote `main` branch.

- E.g., check `git status`

2. *User B* should fetch new code from `origin` using `git fetch origin`.

- Recall that this downloads the contents of the shared Github repository (including the `

3. *User B* should create and checkout a new branch named `devel-titles` from the `origin/devel-titles` branch.

- `git checkout -b devel-titles origin/devel-titles`
- Recall that this creates a new branch in *User B*'s local repository called `devel-titles` that looks exactly like the branch `fetch`'ed from the shared GitHub repository.

4. *User B* should test out the code on the `devel-titles` branch.

- E.g., confirm that the report builds properly when you execute `make` and that the section headers are appropriately changed.

__If the code does not build properly__:

- *User B* should leave comments on the GitHub pull request describing the errors that they are seeing.
- *User A* and *User B* should discuss to determine the source of the errors.
- *User A* should update the code on their local `devel-titles` branch, `add`, `commit`, and `push` to GitHub.
- Once new code has been pushed to GitHub *User B* should retrieve the updated code. There are several ways to do this. The easiest way to do this is probably:
	- *User B* deletes the local `devel-titles` branch, `git branch -d devel-titles`
	- *User B* fetches changes, `git fetch origin`
	- *User B* goes back to Step 3 above.

__If the code does build properly__:

5. When *User B* is satisfied that the code works as expected, they should merge the `devel-titles` branch into `main`.
- `git checkout main`
- `git merge devel-titles`

6. *User B* should then push the updated `main` branch to GitHub.
- `git push origin main`
- Both users should now see *User A*'s pull request as "merged" on GitHub.

------------------------------------------------------------------------

### User A and B: Make sure local `main` is up to date

Both *User A* and *User B* should now ensure their local main branch is up to date.

- E.g., both users could use `git fetch origin`, `git checkout main`, `git merge origin/main`
- Or more simply, both users could use `git pull origin main`
- These commands should not do anything for *User B*, since they had already merged `devel-titles` into `main` in the above steps.
- These commands __should do something__ for *User A*, since they had not updated their `main` branch with the changes on the `devel-titles` branch.

------------------------------------------------------------------------

### User B: Update the repository and submit a pull request

*User B* will now make a new branch and make updates to the stable code base. *User B* should complete the following steps:

1. Create and checkout a new branch called `devel-colors` by executing `git checkout -b devel-colors`.

- recall that this simultaneously creates and checks out a new branch called `devel-colors`
- confirm that *User B* has switched to the new branch by executing `git branch`
- you should see `main` and `*devel-colors`

2. Change the color of the histograms by modifying lines 35, 42, and 49. E.g., change line 35 to

```r
hist(random_numbers1, col = "gray25")
```

Similarly, add this `col = ` option to the other histograms.

3. Confirm that *User B* can build the report (e.g., by executing `make report.html`)
4. Once *User B* is confident that `report.html` is building properly and that the colors have been changed, they should appropriately use `git add` and `git commit` to make a new commit along the `devel-colors` branch that includes updates `report.Rmd`.

- include a meaningful commit message

5. Push the `devel-colors` branch to GitHub.

- `git push origin devel-colors`

6. Submit a pull request to the shared repository.

- the pull request should request that the `devel-colors` branch be merged into the `main` branch.
- request a code review from *User A*

------------------------------------------------------------------------

### User A: Test out pull request code

*User A* will now `fetch` the code submitted by *User B*, test it out, and eventually merge it into their `main` branch, thereby closing the pull request.

1. First, *User A* should confirm that their local `main` branch is up to date with the remote `main` branch.

- E.g., check `git status`

2. *User A* should fetch new code from `origin` using `git fetch origin`.

- Recall that this downloads the contents of the shared Github repository (including the `devel-colors` branch), but does not yet integrate them into *User A*'s local repository yet.

3. *User A* should create and checkout a new branch named `devel-colors` from the `origin/devel-colors` branch.

- `git checkout -b devel-colors origin/devel-colors`
- Recall that this creates a new branch in *User A*'s local repository called `devel-colors` that looks exactly like the branch `fetch`'ed from the shared GitHub repository.

4. *User A* should test out the code on the `devel-colors` branch.

- E.g., confirm that the report builds properly when you execute `make` and that the histogram colors are appropriately changed.

__If the code does not build properly__:

- *User A* should leave comments on the GitHub pull request describing the errors that they are seeing.
- *User A* and *User B* should discuss to determine the source of the errors.
- *User B* should update the code on their local `devel-colors` branch, `add`, `commit`, and `push` to GitHub.
- Once new code has been pushed to GitHub *User A* should retrieve the updated code. There are several ways to do this. The easiest way to do this is probably:
	- *User A* deletes the local `devel-colors` branch, `git branch -d devel-colors`
	- *User A* fetches changes, `git fetch origin`
	- *User A* goes back to Step 3 above.

__If the code does build properly__:

5. When *User A* is satisfied that the code works as expected, they should merge the `devel-colors` branch into `main`.
- `git checkout main`
- `git merge devel-colors`

6. *User A* should then push the updated `main` branch to GitHub.
- `git push origin main`
- Both users should now see *User B*'s pull request as "merged" on GitHub.

------------------------------------------------------------------------

### User A and B: Make sure local `main` is up to date

Both *User A* and *User B* should now ensure their local main branch is up to date.

- E.g., both users could use `git fetch origin`, `git checkout main`, `git merge origin/main`
- Or more simply, both users could use `git pull origin main`
- These commands should not do anything for *User A*, since they had already merged `devel-colors` into `main` in the above steps.
- These commands __should do something__ for *User B*, since they had not updated their `main` branch with the changes on the `devel-colors` branch.

------------------------------------------------------------------------

### Submit to canvas

The group should submit to canvas a link to User B's repository.

Example:

User B: https://github.com/userB/repo


