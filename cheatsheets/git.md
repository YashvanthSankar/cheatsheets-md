# Git

---

## 1. What is Git?

Git is a distributed version control system.  
It tracks changes in your code and helps you collaborate with others.

---
## 3. Basic Git Terms (for Beginners)

| Term           | Meaning                                                                                  |
|----------------|------------------------------------------------------------------------------------------|
| Repository (repo) | The project folder tracked by Git. Can be local (your computer) or remote (GitHub).   |
| Commit         | A snapshot of your changes, with a message describing what changed.                      |
| Branch         | A separate line of development for features or fixes.                                    |
| Merge          | Combining changes from one branch into another.                                          |
| Clone          | Copying a remote repository onto your computer.                                          |
| Push           | Uploading your commits from local to remote (e.g. GitHub).                               |
| Pull           | Downloading new commits from remote to local.                                            |
| Fork           | Creating your own copy of someone else’s repo (on GitHub).                               |
| Pull Request (PR) | Asking to merge your changes into another repo; often used for code review.           |
| Staging Area   | Where files go after `git add`—ready to be committed.                                    |
| .gitignore     | File listing things Git should NOT track (like temp files).                              |
| Conflict       | When Git can’t automatically combine changes—needs manual fixing.                        |
| Remote         | A version of the repo hosted on a server (like GitHub).                                  |
| Origin         | The default name for your main remote repo.                                              |
| Tag            | A label for specific commits, often used for releases (like `v1.0`).                     |
| Diff           | Shows differences between files, commits, or branches.                                   |
| Stash          | Temporarily saves changes you’re not ready to commit.                                    |
| Checkout/Switch| Change which branch or commit you’re working on.                                         |

---

## 3. Basic Workflow

```bash
# Set your name and email (first time only)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Create a new repo
git init

# Clone an existing repo
git clone https://github.com/user/repo.git

# See repo status (changed files)
git status

# Add files to staging
git add filename.txt         # Add one file
git add .                    # Add all files

# Commit changes
git commit -m "Your message"

# See commit history
git log

# Push changes to remote (GitHub)
git push origin main         # 'main' is the branch name

# Pull changes from remote
git pull origin main

# Check which branch you're on
git branch

# Create a new branch
git branch new-feature

# Switch to a branch
git checkout new-feature
# or (modern Git)
git switch new-feature

# Merge a branch into current
git merge new-feature

# Delete a branch
git branch -d new-feature
```

---

## 4. Remote Repositories

- Add a remote:
  ```bash
  git remote add origin https://github.com/user/repo.git
  ```
- List remotes:
  ```bash
  git remote -v
  ```
- Change remote URL:
  ```bash
  git remote set-url origin NEW_URL
  ```

---

## 5. Undoing Changes

| Task                   | Command                        | Explanation             |
|------------------------|-------------------------------|-------------------------|
| Unstage file           | `git reset HEAD filename.txt`  | Take out of staging     |
| Discard changes        | `git checkout -- filename.txt` | Undo edits              |
| Amend last commit      | `git commit --amend`           | Edit last commit        |
| Revert a commit        | `git revert <commit>`          | Make undoing commit     |

---

## 6. Stashing (Temporary Changes)

```bash
git stash           # Save changes for later
git stash pop       # Reapply stashed changes
git stash list      # Show stashes
```

---

## 7. Tagging

```bash
git tag v1.0        # Create tag
git tag             # List tags
git push origin v1.0   # Push tag
```

---

## 8. Viewing Differences

```bash
git diff            # See unstaged changes
git diff --staged   # See staged changes
git diff branchA..branchB # Compare branches
```

---

## 9. Ignoring Files

- Create a `.gitignore` file:
  ```
  node_modules/
  *.log
  .env
  ```

---

## 10. Useful Shortcuts

| Shortcut            | Command                    | Description          |
|---------------------|---------------------------|----------------------|
| Show last commit    | `git show`                | Commit details       |
| See short log       | `git log --oneline`       | Compact history      |
| See branches graph  | `git log --graph --all`   | Visual history       |
| List files tracked  | `git ls-files`            | Tracked files        |

---

## 11. Help

```bash
git help <command>
# Example:
git help log
```

---

## 12. Common GitHub Tasks

- **Fork:** Copy someone’s repo to your account.
- **Pull Request:** Propose your changes to a project.
- **Clone:** Download a repo to your computer.
- **Push:** Upload your changes to GitHub.

---

## 13. Tips

- Commit often with meaningful messages.
- Pull before you push, to avoid conflicts.
- Use branches for new features/fixes.

---

## 14. Resources

- [Git Official Docs](https://git-scm.com/doc)
- [GitHub Learning Lab](https://lab.github.com/)
- [Learn Git Branching](https://learngitbranching.js.org/)
- [Oh My Git!](https://ohmygit.org/)

---

**Happy coding and collaborating! 🚀**
