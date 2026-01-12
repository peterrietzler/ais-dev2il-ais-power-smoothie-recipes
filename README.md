# 🥤 The AIS Survival Smoothie

In this tutorial, you will build a recipe for the "Ultimate AIS Survival Smoothie." 
You will learn how to use Git as a system to track your progress and navigate history using commits.

## Git Basics

### 🛠 Tools You'll Need
- **Terminal:** Command Prompt/PowerShell (Windows) or Terminal (Mac).
- **Text Editor:**
   - **Windows:** Notepad. Make sure that you are using plain text format
   - **Mac:** TextEdit. Make sure that you are using plain text format (_Format > Make Plain Text_)
   - **For the Brave:** `vi` or `vim`. Use this option only if you are comfortable with vi!


### Step 1: Tell Git Who You Are (Global Config)
Before we start, Git needs to know who is creating the commits. 
In Git, there are **system** settings (everyone on the PC), 
**global** settings (only for you), 
and **local** settings (just this repository). We will use the global settings.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Step 2: Create the Recipe Book
Create a new folder for your project and tell Git to start watching it.

```bash
mkdir survival-smoothie
cd survival-smoothie
git init
```

**👻 Where is my repository (the "Vault")?**

Git creates a hidden folder called `.git` to store your commits. To see the "invisible" magic, try this:

- Mac / Linux: `ls -la`
- Windows (PowerShell): `ls -Force`

⚠️ Note: **Never** delete or fiddle around with the `.git` folder manually. If you delete it, your entire project history (your time machine) is gone!

### Step 3: Create the Recipe

1. Create a file named `README.md` and add your first ingredient: `1. 2x Bananas`.
1. Go back to your terminal and check the status: `git status`.

🔍 Git sees the file but calls it **untracked**. It’s in the room, but not "on the stage" yet.

Move it to the Staging Area:
```bash
git add README.md
git status
```

📦 The file is now **staged**. It's ready for the commit.

### Step 4: Your First Version of the Recipe

A commit is a permanent save-point of your work. The message is the most important part because it tells your future self what you did.

🚫 **The "Wall of Shame"**

Do not use messages like these:
- _update_
- _fixed stuff_

✅ **The "Professional Way"**

A good message is short and describes the __intent__.

`git commit -m "Add base ingredient: bananas"`

**Our Timeline Now**

```
v1 (HEAD) Add base ingredient: bananas
```

❓ What is `HEAD`?

A pointer that says _"You are here"_. It points to the specific commit you are currently looking at.

### Step 5: Expand the Recipe

Add `2. 1x Scoop Protein Powder` to your `README.md`.

Now, let's see **WHAT** changed before we commit it:

```bash
git diff
```

🔍 Lines starting with `+` are the additions since your last commit.

Stage and commit again:

```bash
git add README.md
git commit -m "Add protein for brain power"
```

**Our Timeline Now**

```
v2 (HEAD) Add protein for brain power
v1 Add base ingredient: bananas
```

### Step 6: Quick History Check

Use a one-line view to see your current progress.

`git log --oneline`

Each commit is identified by a unique commit hash, aka a _Commit SHA_. It is a unique, 
40-character string that acts as a fingerprint for a specific snapshot of your project.
You rarely need to use all 40 characters. In most commands, you can just use the first 
7 characters. Git is smart enough to find the right commit as long as those 7 characters 
are unique within your repository.

### Step 7: Inspecting the History in More Detail

Now, let’s look at the full record to see the **Who**, **When**, and **Why**.

`git log`

If you also want to see the **What** use: `git log -p`.

⚠️ You might need to hit `q` to exit the log view.

### Step 8: Compare Two Points in Time

Sometimes you want to see exactly what changed between the very first version and the latest version.

Find the hashes for two versions and compare them using

```bash
git diff <hash-of-v1> <hash-of-v2>
```

### Step 9: The "Oops Moment"

**Scenario A: The Protein was a mistake (Revert)**

You want to remove the protein, but you want to keep the history of that mistake for the record. This creates a new commit.

```bash
git revert HEAD --no-edit
```

**Our Timeline Now**

Use what you've already learned to inspect the timeline starting from here!

**Scenario B: Emergency Stop (Reset)**

Your recipe is a mess. You want to **delete** everything and go back to an older version as if nothing else happened.

1. Find the real hash of your first commit
1. Reset the timeline

```bash
git reset --hard <hash-of-v1>
```

⚠️ Warning: Newer commits are now gone! Be very careful with this command!

### 🏆 Summary Cheat Sheet

| Command                | What it does                             | Metaphor                                        |
|:-----------------------|:-----------------------------------------|:------------------------------------------------|
| `git init`             | Creates a new repository                 | Build the vault                                 |
| `git status`           | Shows changed workspace and staged files | Check what's already in the box to be shipped   |
| `git add`              | Stages a file                            | Put something into the box to be shipped        |
| `git commit`           | Creates a commit                         | Put the box into the vault                      |
| `git log`              | Shows commits                            | Show all the boxes in the vault                 | 
| `git diff HASH1 HASH2` | Compares two commits                     | Show the difference of two boxes in the vault   |
| `git revert`           | Undoes changes                           | Duplicate a box and put it into the vault       |
| `git reset --hard`     | Destroys changes                         | Remove boxes from the vault and throw them away |


### 🚀 Level Up

Finished early? Put your Git skills to the test with these "Pro" moves.

**Challenge 1: The "Forgetful" (Amending)**

Imagine you committed v1, but realized you had a typo or forgot to add a 
`CONTRIBUTORS.txt` file. You don't want a new version; you want to fix the last one.

- Create a file `CONTRIBUTORS.txt` with your name
- Stage it
- Instead of a new commit, run `git commit --amend -m "Add bananas and contributor list"`

**Challenge 2: "Pick-and-Choose" (Selective Staging)**

Sometimes you change multiple files, but you only want one of them to be in the next commit.

- Create `strawberries.txt` and `blueberries.txt`
- Run `git status`. Both are untracked.
- Stage only the `strawberries.txt`

Run git status again. Notice how one is staged and the other isn't!

**Challenge 3: The "Deep Clean" (Cleaning)**

Your workspace is getting messy with "trash" files (like `test.txt`) that you never added to Git.

- Create a trash file `junk.txt` in your workspace 
- Check the status to verify that it's untracked
- To delete all untracked files in one go, run `git clean -f` 

⚠️ Warning: Your files will be gone! Be very careful with this command!

**Challenge 4: "Who added rotten bananas to my smoothie ?" (Blaming)**

Git can tell you exactly who wrote which line in a file.

`git blame README.md`

💡 In high-performing DevOps teams, they practice "Blameless Post-Mortems". 
The goal is never to punish the person who made the mistake, but to fix the process 
that allowed the mistake to happen. `git blame` is simply a map to find the person 
who can help explain what happened here.

## Branching and Merging (The Multiverse)

Up until now, we have been working on a single timeline called `main`.
In a team, multiple people work on different features at the same time. If everyone commits to
the same timeline, chaos ensues!

To solve this, we use **branches**. Think of them as parallel universes where you can experiment
safely without breaking the main recipe.

### Daily Workflow - Step 1: Start a Task (Create a Branch)

You pick a ticket to work on. You want to add a new ingredient: **Blueberries**.
Instead of adding it directly to the main recipe, you create a dedicated branch.

```bash
git branch feature/blueberries
git checkout feature/blueberries
```

Or simpler (create and switch in one go):

```bash
git checkout -b feature/blueberries
```

### Daily Workflow - Step 2: Work and Commit

Now you are in the `feature/blueberries` universe. Check `git status` to see that you are actually on the branch!

1. Edit `README.md` and add `3. Handful of Blueberries`.
2. Save the file.
3. Commit your changes to this branch.

```bash
git add README.md
git commit -m "Add antioxidants (blueberries)"
```

### Daily Workflow - Step 3: Bring it Back (Merge)

Your task is done and the blueberries look delicious. It's time to bring your changes back to the main timeline
so everyone can enjoy them.

1. Switch back to the main timeline (trunk).
```bash
git checkout main
```

2. Merge your feature branch into the main timeline.
```bash
git merge feature/blueberries
```

3. Delete the branch. The feature is now part of the product. You don't need the working branch anymore.
```bash
git branch -d feature/blueberries
```

### 🚀 Level Up

Finished early? Ready for the real world? Things don't always go this smoothly.

**Challenge 1: The "Clash of Ingredients" (Merge Conflicts)**

What happens if two people change the **same line** at the same time?

1. Create a new branch `feature/milk` and switch to it.
2. Change the line `2x Bananas` to `3x Bananas` in `README.md`.
3. Commit the change.
4. Switch back to `main` (don't merge yet!).
5. Change the line `2x Bananas` to `1x Banana` in `README.md` (directly on master).
6. Commit the change on `main`.
7. Now try to merge the branch: `git merge feature/milk`.

💥 **BOOM! Conflict!**

Git will tell you that there is a conflict. Open `README.md` in your text editor. You will see something like this:

```text
<<<<<<< HEAD
1x Banana
=======
3x Bananas
>>>>>>> feature/milk
```

- Decide which version is correct (or combine them).
- Remove the markers `<<<<<<<`, `=======`, `>>>>>>>`.
- Save the file.
- `git add README.md`
- `git commit` (no message needed, Git creates a default one)

💡After resolving the conflict and saving, type `:wq` in vi on Mac/Linux to exit and save. 
On Windows, use `Ctrl+X` then `Y` in Notepad or follow your editor's save/close instructions.

**Challenge 2: "Hold my beer" (Stashing)**

You are working on a new branch `feature/spinach` and have made some experimental changes (you modified the file but didn't commit yet).
Suddenly, your boss shouts: "STOP! We need to fix a bug on master immediately!"

You can't switch branches because you have uncommitted changes that would be overwritten. You don't want to commit half-finished work.

Solution: **The Stash** (a temporary clipboard for your files).

1. Make a change to `README.md` but **do not** commit it.
2. Run `git stash` to save your work on the side.
   - Your workspace is clean again (check with `git status`).
3. You can now switch branches, do other work, etc.
4. When you are ready to continue, run `git stash pop`.
  Your changes are back!

💡Git can stash multiple changes. Run `git stash --help` to get more information. 

**Challenge 3: "Ghost Writer" (Patches)**

Sometimes you want to send a change to a friend without committing it to the repository (e.g. via email or chat).

1. Make a change to `README.md` (e.g. Add "Secret Sauce"). **Do not** commit it.
2. Create the patch file:
   ```bash
   git diff > secret.patch
   ```
3. Check the content of the file:
   - Mac/Linux: `cat secret.patch`
   - Windows: `type secret.patch`
4. Undo your changes in the workspace so we can simulate receiving the patch
5. Apply the patch:
   ```bash
   git apply secret.patch
   ```
6. Check `git status` and `cat README.md`. Your changes are back!

## Making Your Life Easier in Day-to-Day _Gitting_

Git is "CLI-first". You can do everything using the CLI, which makes it the perfect candidate for 
automating tasks. This also means that you can use Git in any environment where a command line and 
the `git` tool is available. 

In daily work, most developers use an IDE (Integrated Development Environment), which tremendously 
increases UX. Just imagine having to analyze the output of `git diff` for many files and changes 😱.

- Start PyCharm
- Open the `survival-smoothie` folder as a project
- Open the _Commit Tool_ ![commit-tool-symbol.png](commit-tool-symbol.png)
- You will see something like this 
![changes.png](changes.png)

### 🙈 Ignoring Unwanted Files (.gitignore)

When you open the project in PyCharm, it creates a hidden folder called `.idea`. This contains your 
personal IDE settings. Accept for the moment that you don't want to share these with your team.

**Rule of Thumb:**
- **Commit:** Source code (recipes in our case), shared config.
- **Do not commit:** IDE settings (`.idea`, `.vscode`), temporary files, build results and secrets.

To stop Git from tracking these, use a `.gitignore` file.

1. Create a file named `.gitignore` in your project root.
2. Add the following line to it:
   ```text
   .idea
   ```
3. Commit the `.gitignore` file using the _Commit Tool_. Just follow your knowledge and intuition. 

### Using Your IDE "to git"

All IDEs usually have great support for Git! In PyCharm, you can, e.g. use the 
_Commit Tool_ ![commit-tool-symbol.png](commit-tool-symbol.png) or the _Git_ Tool
![git-tool-symbol.png](git-tool-symbol.png). Also the _Project Tool_ ![project-tool-symbol.png](project-tool-symbol.png)
is going to augment your project with Git information. 

You already know everything you need! Follow your intuition to complete the following tasks:
- Create a new file, stage it and commit
- Add a new ingredient to our smoothie recipe and commit it
- Find and inspect the history of your commits (who, what, when, why) 
- Compare two commits
- Revert a commit
- Reset your project to a previous state
- Create a feature branch, work on it and merge it back into the trunk
- Create a merge conflict and resolve it

💡Hints
- If you can't find a tool use _View > Tool Windows_
- If you are searching for an IDE action, try _Navigate > Search Everywhere > Actions_ 

### 🚀 Level Up

Finished early? Put your IDE skills to the test with these "Pro" moves.

- Try to amend your last commit
- Modify two files. Commit the two files individually
- Open the `README.md` file and try to achieve these tasks using the _Git_ actions in the context menu
  - Activate the _Blame_ (_Annotate_) mode
  - Show the history only for this file
  - Put the cursor in the first line and find only the changes done to exactly this line
- You've messed up something but have no commit? Check out the _Local History Tool_. 
  ⚠️ Warning: This is not a Git feature
- PyCharm can also "stash" changes for you. Check out _Shelve Changes_ in the _Commit Tool_.
  ⚠️ Warning: This is not a Git feature
- Try to create a patch file from the _Commit Tool_ and the history in the _Git_ tool
- Compare the contents of branches: 
  - Find out which commits exist on a branch but not on the trunk
  - Find out which files and lines are different between the latest version of a branch and the trunk
  
## Further Readings

- https://training.github.com/downloads/github-git-cheat-sheet/
- https://skills.github.com/

