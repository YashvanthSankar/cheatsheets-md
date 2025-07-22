# 📝 Git Cheatsheet

---

## 1. What is Git?

Git is a distributed version control system.  
It tracks changes in your code and helps you collaborate with others.

---

## 2. Basic Workflow

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

## 3. Remote Repositories

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

## 4. Undoing Changes

| Task                   | Command                        | Explanation             |
|------------------------|-------------------------------|-------------------------|
| Unstage file           | `git reset HEAD filename.txt`  | Take out of staging     |
| Discard changes        | `git checkout -- filename.txt` | Undo edits              |
| Amend last commit      | `git commit --amend`           | Edit last commit        |
| Revert a commit        | `git revert <commit>`          | Make undoing commit     |

---

## 5. Stashing (Temporary Changes)

```bash
git stash           # Save changes for later
git stash pop       # Reapply stashed changes
git stash list      # Show stashes
```

---

## 6. Tagging

```bash
git tag v1.0        # Create tag
git tag             # List tags
git push origin v1.0   # Push tag
```

---

## 7. Viewing Differences

```bash
git diff            # See unstaged changes
git diff --staged   # See staged changes
git diff branchA..branchB # Compare branches
```

---

## 8. Ignoring Files

- Create a `.gitignore` file:
  ```
  node_modules/
  *.log
  .env
  ```

---

## 9. Useful Shortcuts

| Shortcut            | Command                    | Description          |
|---------------------|---------------------------|----------------------|
| Show last commit    | `git show`                | Commit details       |
| See short log       | `git log --oneline`       | Compact history      |
| See branches graph  | `git log --graph --all`   | Visual history       |
| List files tracked  | `git ls-files`            | Tracked files        |

---

## 10. Help

```bash
git help <command>
# Example:
git help log
```

---

## 11. Common GitHub Tasks

- **Fork:** Copy someone’s repo to your account.
- **Pull Request:** Propose your changes to a project.
- **Clone:** Download a repo to your computer.
- **Push:** Upload your changes to GitHub.

---

## 12. Tips

- Commit often with meaningful messages.
- Pull before you push, to avoid conflicts.
- Use branches for new features/fixes.

---

## 13. Resources

- [Git Official Docs](https://git-scm.com/doc)
- [GitHub Learning Lab](https://lab.github.com/)
- [Learn Git Branching](https://learngitbranching.js.org/)
- [Oh My Git!](https://ohmygit.org/)

---

**Happy coding and collaborating! 🚀**