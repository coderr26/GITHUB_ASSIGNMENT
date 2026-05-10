# GITHUB_ASSIGNMENT
GITHUB_ASSIGNMENT

A complete hands-on guide to learning essential Git and GitHub operations including:

- Repository initialization
- Tracking changes
- Commit history management
- Branching and merging
- Stashing changes
- Resetting commits
- Reverting commits
- Working with remote repositories


# 1. Introduction

Git is a distributed version control system used to track changes in source code during software development.

GitHub is a cloud-based platform used to host Git repositories and collaborate with developers.

This project demonstrates practical Git workflows commonly used in real-world development environments.

---

# 2. Project Initialization & First Push

## Objective

Set up a new project using Git and upload it to a remote repository.

---

## Step 1: Create a Project Folder

Create a new directory for the project.

```bash
mkdir my-python-project
cd my-python-project
```

### Explanation
- `mkdir` creates a new folder
- `cd` moves into the project directory

---

## Step 2: Initialize Git Repository

```bash
git init
```

### Explanation
This command initializes an empty Git repository inside the project folder.

Git creates a hidden `.git` directory that stores version history and repository metadata.

---

## Step 3: Create Python File

```bash
touch app.py
```

Add sample Python code:

```python
print("Hello, Git!")
```

### Explanation
- `touch` creates a new file
- `app.py` contains the Python application code

---

## Step 4: Check Git Status

```bash
git status
```

### Explanation
Displays:
- Untracked files
- Modified files
- Staged files
- Current branch information

Example:
```bash
Untracked files:
  app.py
```

---

## Step 5: Stage File

```bash
git add app.py
```

### Explanation
Moves the file to the staging area so Git can include it in the next commit.

---

## Step 6: Commit Changes

```bash
git commit -m "Initial commit: add app.py with basic Python code"
```

### Explanation
Creates a snapshot of the project at the current state.

- `-m` adds a commit message
- Commit messages should clearly describe the changes

---

## Step 7: Create Remote Repository

Create a repository on GitHub:

1. Login to GitHub
2. Click **New Repository**
3. Enter repository name
4. Click **Create Repository**

---

## Step 8: Add Remote Repository

```bash
git remote add origin https://github.com/your-username/my-python-project.git
```

### Explanation
- `origin` is the default remote repository name
- Links local repository to GitHub repository

---

## Step 9: Verify Remote Configuration

```bash
git remote -v
```

### Explanation
Shows remote repository URLs for:
- Fetch
- Push

Example:
```bash
origin  https://github.com/your-username/my-python-project.git (fetch)
origin  https://github.com/your-username/my-python-project.git (push)
```

---

## Step 10: Push Code to GitHub

```bash
git branch -M main
git push -u origin main
```

### Explanation
- Renames branch to `main`
- Pushes code to GitHub
- `-u` sets upstream tracking

---

# 3. Working with Changes & History

## Objective

Track modifications and manage project history efficiently.

---

## Modify `app.py`

Example:

```python
print("Hello, Git!")

def greet(name):
    return f"Hello, {name}!"

print(greet("Bob"))
```

---

## Check Current Changes

```bash
git status
```

### Explanation
Displays modified files before staging.

---

## View Differences

```bash
git diff
```

### Explanation
Shows line-by-line differences between:
- Working directory
- Last committed version

Example:
```diff
+def greet(name):
+    return f"Hello, {name}!"
```

---

## Stage Specific Changes

```bash
git add -p app.py
```

### Explanation
Interactive staging:
- Stage only selected code sections
- Useful for clean commits

Options:
- `y` → stage
- `n` → skip
- `q` → quit

---

## Commit Changes

```bash
git commit -m "Add greet function to app.py"
```

---

## Add Another Feature

```python
def add(a, b):
    return a + b
```

---

## Stage All Changes

```bash
git add .
```

### Explanation
Stages all modified and new files.

---

## Commit Again

```bash
git commit -m "Add addition utility function"
```

---

## View Full Commit History

```bash
git log
```

### Explanation
Displays:
- Commit hash
- Author
- Date
- Commit message

---

## View Compact History

```bash
git log --oneline
```

### Explanation
Shows short commit history in one-line format.

Example:
```bash
a1b2c3d Add addition utility function
e4f5g6h Add greet function
```

---

# 4. Branching & Feature Development

## Objective

Develop features separately without affecting the main branch.

---

## Create New Branch

```bash
git branch feature-update
```

### Explanation
Creates a new branch named `feature-update`.

---

## Switch to Branch

```bash
git checkout feature-update
```

Or:

```bash
git switch feature-update
```

### Explanation
Moves from current branch to the feature branch.

---

## Add New Feature

Example:

```python
def multiply(a, b):
    return a * b
```

---

## Stage & Commit

```bash
git add app.py
git commit -m "Add multiply function feature"
```

---

## Switch Back to Main Branch

```bash
git checkout main
```

---

## Merge Feature Branch

```bash
git merge feature-update
```

### Explanation
Combines feature branch changes into `main`.

---

## Verify Merge

```bash
git log --oneline
```

or

```bash
cat app.py
```

---

## Delete Branch Safely

```bash
git branch -d feature-update
```

### Explanation
Deletes branch only if merged successfully.

---

## Force Delete Branch

Create dummy branch:

```bash
git branch dummy-branch
git checkout dummy-branch
```

Make changes and commit:

```bash
git add app.py
git commit -m "Dummy branch test commit"
```

Switch back:

```bash
git checkout main
```

Safe delete may fail:

```bash
git branch -d dummy-branch
```

Force delete:

```bash
git branch -D dummy-branch
```

### Explanation
- `-D` forcefully deletes branch
- Removes unmerged branch permanently

---

# 5. Handling Errors (Stash, Reset, Revert)

## Objective

Learn how to manage unfinished work and fix mistakes safely.

---

# Git Stash

## Make Temporary Changes

Example:

```python
def subtract(a, b):
    return a - b
```

Create untracked file:

```bash
touch notes.txt
```

---

## Stash Changes Including Untracked Files

```bash
git stash push -u -m "WIP: subtract feature"
```

### Explanation
- Saves unfinished changes temporarily
- `-u` includes untracked files
- Useful when switching tasks quickly

---

## View Stash List

```bash
git stash list
```

Example:
```bash
stash@{0}: On main: WIP: subtract feature
```

---

## Apply Stashed Changes

```bash
git stash apply
```

### Explanation
Restores stashed changes back to working directory.

---

## Commit Restored Changes

```bash
git add .
git commit -m "Add subtract function"
```

---

# Git Reset

## Add Incorrect Code

```python
def divide(a, b):
    return a / 0
```

Commit changes:

```bash
git add app.py
git commit -m "Add broken divide function"
```

---

## Undo Last Commit

### Soft Reset

```bash
git reset --soft HEAD~1
```

### Explanation
Removes commit but keeps changes staged.

---

### Mixed Reset

```bash
git reset --mixed HEAD~1
```

### Explanation
Removes commit and unstages changes.

---

### Hard Reset

```bash
git reset --hard HEAD~1
```

### Explanation
Deletes:
- Commit
- Staged changes
- Working directory changes

⚠ Warning:
This permanently removes changes.

---

# Git Revert

## Add Correct Code

```python
def divide(a, b):
    if b == 0:
        return "Cannot divide by zero"
    return a / b
```

Commit:

```bash
git add app.py
git commit -m "Add safe divide function"
```

---

## Revert Commit

```bash
git revert HEAD
```

### Explanation
Creates a new commit that reverses previous changes.

Unlike reset:
- History remains preserved
- Safe for shared repositories

---

# Verify Commit History

## Compact View

```bash
git log --oneline
```

## Detailed View

```bash
git log
```

---

# 6. Important Git Commands Summary

| Task | Command |
|------|---------|
| Initialize repository | `git init` |
| Check status | `git status` |
| Stage file | `git add file_name` |
| Stage all files | `git add .` |
| Commit changes | `git commit -m "message"` |
| View differences | `git diff` |
| Full commit history | `git log` |
| Compact history | `git log --oneline` |
| Create branch | `git branch branch-name` |
| Switch branch | `git checkout branch-name` |
| Merge branch | `git merge branch-name` |
| Delete branch | `git branch -d branch-name` |
| Force delete branch | `git branch -D branch-name` |
| Stash changes | `git stash push -u` |
| View stashes | `git stash list` |
| Apply stash | `git stash apply` |
| Reset commit | `git reset HEAD~1` |
| Revert commit | `git revert HEAD` |

---

# 7. Conclusion

This project demonstrates essential Git workflows used in professional software development.

Topics covered include:

- Creating and managing repositories
- Tracking and committing code changes
- Working with branches
- Merging features
- Managing unfinished work using stash
- Undoing mistakes safely with reset and revert
- Viewing and understanding commit history

Mastering these concepts is fundamental for:
- Team collaboration
- Version control
- Safe software development
- Continuous integration workflows

---

# Author

Rashmi Rajput 

---
