Here's a cleaned-up and professional version of your Git workflow documentation suitable for a GitHub `.md` file:

---

# Git Workflow Documentation

## Initial Setup

1. **Install Git** on your local machine.
2. **Configure Git and GitLab credentials**:
   ```bash
   git config --global user.name "mdsajid786"
   git config --global user.email "mdsajid020@gmail.com"
   ```

3. **Clone the repository**:
   ```bash
   git clone https://github.com/Sagar2366/LearnWithSagar.git
   ```

---

## Working with Branches

1. **Create and switch to a new branch**:
   ```bash
   git checkout -b feature/day3-challenge
   ```

2. **Verify current branch**:
   ```bash
   git branch
   # * feature/day3-challenge
   #   main
   ```

3. **Make changes and stage them**:
   ```bash
   git add .
   git commit -m "Added new features in the new branch"
   ```

4. **Check current HEAD position**:
   ```bash
   git rev-parse --abbrev-ref HEAD
   # feature/day3-challenge
   ```

---

## Push and Pull Request

1. **Push the changes to the remote repository**:
   ```bash
   git push origin feature/day3-challenge
   ```

2. **Create a Pull Request** on GitHub and **merge** it into the `main` branch.

   ![PR Screenshot](image.png)  
   ![Merged Screenshot](image-1.png)

---

## Merging Updates and Conflict Resolution

1. **Switch to the main branch and pull latest changes**:
   ```bash
   git checkout main
   git pull origin main
   ```

2. **Merge updates into the feature branch**:
   ```bash
   git checkout feature/day3-challenge
   git merge main
   ```

---

## Cleaning Up

1. **Delete the feature branch locally and remotely**:
   ```bash
   git branch -d feature/day3-challenge
   git push origin --delete feature/day3-challenge
   ```

---

## Commit History

### One-line Log
```bash
git log --oneline
```
```
b756798 Merge pull request #1 from mdsajid786/feature/day3-challenge
6c2f6db Updated commit message with additional changes
...
```

### Detailed Log
```bash
git log --pretty=format:"%h - %an, %ar : %s"
```
```
b756798 - Sajid Mohammad, 37 minutes ago : Merge pull request #1 from mdsajid786/feature/day3-challenge
6c2f6db - mdsajid786, 40 minutes ago : Updated commit message with additional changes
...
```

### Log with Stats
```bash
git log --stat
```

---

## Summary of Git Commands Used

| Command | Description |
|--------|-------------|
| `git init` | Initializes a new Git repository |
| `git clone` | Copies a remote repository to your local machine |
| `git config` | Sets user name and email |
| `git checkout -b` | Creates and switches to a new branch |
| `git add .` | Stages all changes |
| `git commit -m` | Commits staged changes with a message |
| `git push origin <branch>` | Pushes local branch to remote |
| `git pull origin main` | Pulls latest changes from main branch |
| `git merge` | Merges another branch into the current one |
| `git branch -d` | Deletes a local branch |
| `git push origin --delete <branch>` | Deletes a remote branch |
| `git log` | Shows commit history |
| `git diff` | Displays differences between commits or branches |
| `HEAD` | Represents the current checked-out commit or branch |
| `origin` | Default name of the remote repository |

---

Let me know if you’d like this as a downloadable `.md` file or want to include it directly in a repository README.
