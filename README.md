# Comprehensive Git Configuration and Cheat Sheet

This guide provides you with an in-depth explanation on how to properly configure your Git environment, from user information and tool setups to creating aliases for faster Git operations. Additionally, we cover essential Git operations in a cheat sheet format, with examples to help you understand how to use Git more efficiently.

## 1. Properly Configure Your `~/.gitconfig`

The `~/.gitconfig` file stores global Git configurations such as your name, email, and preferred tools for diff and merge operations. Here's how to configure it properly:

### 1.1 Configure User Information

Git uses your name and email address for commit tracking. These configurations ensure that commits you make are correctly attributed to you, especially when working with GitHub or any other remote repository.

In your `~/.gitconfig`, you can add your user information as follows:

```ini
[user]
    name = Guilherme M. Trein
    email = valid@email.com
```

- **`name`**: This is your full name, which will appear in your commit history.
- **`email`**: This is your email address, which is used by platforms like GitHub to associate your commits with your account.

> **Note**: If you work on multiple machines or repositories with different email addresses, you can configure a different email for each repository using `git config user.email "new-email@example.com"` inside the repository.

### 1.2 Configure Diff and Merge Tools

Git allows you to configure external tools for handling diffs and merges. This is helpful for reviewing changes or resolving merge conflicts with more user-friendly interfaces.

To set `opendiff` (a macOS tool) as your difftool and mergetool, add the following to your `~/.gitconfig`:

```ini
[difftool "opendiff"]
    cmd = /usr/bin/opendiff \"$LOCAL\" \"$REMOTE\" -merge \"$MERGED\" | cat

[diff]
    tool = opendiff

[merge]
    tool = opendiff
```

- **`difftool`**: Specifies the tool to use for showing differences between file versions.
- **`merge tool`**: Specifies the tool to use for resolving merge conflicts.

> **Note**: Replace `/usr/bin/opendiff` with the path to your preferred diff/merge tool if you're using another one (e.g., `meld`, `vimdiff`, etc.).

### 1.3 Create Aliases for Common Git Commands

Git aliases are shortcuts for frequently used Git commands. By adding these aliases to your `~/.gitconfig`, you can save time and reduce typing. Below is a list of some useful Git aliases.

```ini
[alias]
    st = status
    ci = commit
    br = branch
    co = checkout
    ds = diff --staged
    changes = log -n1 -p --format=fuller
    amend = commit --amend -C HEAD
    undo = clean -f -d
    undoci = reset HEAD~1
    unstage = reset HEAD --
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
    ls = log --pretty=format:"%C(yellow)%h %C(blue)%ad%C(red)%d %C(reset)%s%C(green) [%cn]" --decorate --date=short
    lg-full = log --name-status --pretty=fuller
```

- **`st`**: Shortcut for `git status`.
- **`ci`**: Shortcut for `git commit`.
- **`br`**: Shortcut for `git branch`.
- **`co`**: Shortcut for `git checkout`.
- **`lg`**: A more detailed log with graph visualization and color highlighting.
- **`lg-full`**: Full commit logs, including file changes.

> **Example**: Instead of typing `git status`, you can now simply type `git st`.

## 2. Git Cheat Sheet

Here’s a comprehensive list of common Git operations, categorized for easy reference. Each section provides the command and a brief explanation.

### 2.1 Create

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| Clone an existing repository               | `$ git clone ssh://user@domain.com/repo.git`                 |
| Create a new local repository              | `$ git init`                                                |

**Example**: To clone a repository:
```bash
git clone ssh://user@domain.com/repo.git
```

### 2.2 Local Changes

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| Changed files in your working directory    | `$ git status`                                              |
| Changes to tracked files                   | `$ git diff`                                                |
| Add all current changes to the next commit | `$ git add .`                                               |
| Add some changes to the next commit        | `$ git add -p <file>`                                       |
| Commit all local changes                   | `$ git commit -a`                                           |
| Commit staged changes                      | `$ git commit`                                              |
| Amend the last commit                      | `$ git commit --amend`                                      |

**Example**: After editing files, you can check which files have been modified:
```bash
git status
```

### 2.3 Commit History

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| Show all commits, starting with newest     | `$ git log`                                                 |
| Show changes for a specific file           | `$ git log -p <file>`                                       |
| Who changed what and when                  | `$ git blame <file>`                                        |

**Example**: To see all commits:
```bash
git log
```

### 2.4 Branches and Tags

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| List all existing branches                 | `$ git branch`                                              |
| Switch to a branch                         | `$ git checkout <branch>`                                   |
| Create a new branch                        | `$ git branch <new-branch>`                                 |
| Create a new tracking branch               | `$ git checkout --track <remote/branch>`                    |
| Delete a local branch                      | `$ git branch -d <branch>`                                  |
| Mark the current commit with a tag         | `$ git tag <tag-name>`                                      |

**Example**: To list branches:
```bash
git branch
```

### 2.5 Update and Publish

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| List all currently configured remotes      | `$ git remote -v`                                            |
| Add new remote repository                  | `$ git remote add <remote> <url>`                            |
| Fetch changes from a remote                | `$ git fetch <remote>`                                       |
| Pull changes from a remote branch          | `$ git pull <remote> <branch>`                               |
| Push local changes to a remote             | `$ git push <remote> <branch>`                               |
| Delete a branch on the remote              | `$ git branch -dr <remote/branch>`                           |
| Publish tags                               | `$ git push --tags`                                         |

**Example**: To push changes:
```bash
git push origin main
```

### 2.6 Merge and Rebase

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| Merge a branch into the current branch     | `$ git merge <branch>`                                      |
| Rebase the current branch onto another     | `$ git rebase <branch>`                                     |
| Abort a rebase                             | `$ git rebase --abort`                                      |
| Continue a rebase after conflict resolution| `$ git rebase --continue`                                   |
| Use the configured merge tool for conflicts| `$ git mergetool`                                           |

**Example**: To merge `feature` branch into `main`:
```bash
git merge feature
```

### 2.7 Undo Changes

| Operation                                  | Command                                                     |
| ------------------------------------------ | ----------------------------------------------------------- |
| Discard all local changes                  | `$ git reset --hard HEAD`                                   |
| Discard changes in a specific file         | `$ git checkout HEAD <file>`                                |
| Revert a commit (creates a new commit)     | `$ git revert <commit>`                                     |
| Reset to a previous commit and discard changes | `$ git reset --hard <commit>`                              |

**Example**: To discard all changes:
```bash
git reset --hard HEAD
```

---

## Conclusion

Properly configuring your `~/.gitconfig` and understanding Git commands can make your workflow significantly more efficient. With user information, difftools, mergetools, and aliases, you can streamline everyday Git tasks and work more effectively, whether you're collaborating on a team or managing your personal repositories. The cheat sheet provided also helps you easily access common Git operations, ensuring you spend more time coding and less time managing version control.
