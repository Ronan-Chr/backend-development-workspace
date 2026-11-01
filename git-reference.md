# Git Reference

My personal Git command cheat sheet. Based on the [official Git cheat sheet](https://git-scm.com/cheat-sheet).
![GitHub-Cheat-Sheet](PDFs\GitCheatSheet01.png)
![GitHub-Cheat-Sheet02](PDFs\GitCheatSheet02.png)

## Table of Contents
- [Getting Started](#getting-started)
- [Prepare to Commit](#prepare-to-commit)
- [Make Commits](#make-commits)
- [Branches](#branches)
- [Diffs](#diffs)
- [Ways to Refer to a Commit](#ways-to-refer-to-a-commit)
- [Discard Changes](#discard-changes)
- [Edit History](#edit-history)
- [Code Archaeology](#code-archaeology)
- [Combine Branches](#combine-branches)
- [Restore an Old File](#restore-an-old-file)
- [Remotes, Push & Pull](#remotes-push--pull)
- [Configure Git](#configure-git)
- [Important Files](#important-files)

---

## Getting Started
| Task | Command |
|---|---|
| Start a new repo | `git init` |
| Clone an existing repo | `git clone <url>` |

## Prepare to Commit
| Task | Command |
|---|---|
| Stage a file (untracked or changed) | `git add <file>` |
| Stage everything | `git add .` |
| Choose which parts of a file to stage | `git add -p` |
| Move / rename a file | `git mv <old> <new>` |
| Delete a file | `git rm <file>` |
| Stop tracking a file (keep it on disk) | `git rm --cached <file>` |
| Unstage one file | `git restore --staged <file>` *or* `git reset <file>` |
| Unstage everything | `git restore --staged .` *or* `git reset` |
| Check what's staged | `git status` |

## Make Commits
| Task | Command |
|---|---|
| Commit (opens editor for message) | `git commit` |
| Commit with a message | `git commit -m "message"` |
| Stage all tracked changes + commit | `git commit -am "message"` |

## Branches
| Task | Command |
|---|---|
| List branches | `git branch` |
| List by most recent commit | `git branch --sort=-committerdate` |
| Switch branches | `git switch <name>` *or* `git checkout <name>` |
| Create + switch to a branch | `git switch -c <name>` *or* `git checkout -b <name>` |
| Delete a branch | `git branch -d <name>` |
| Force delete a branch | `git branch -D <name>` |

## Diffs
### Staged / Unstaged Changes
| Task | Command |
|---|---|
| All staged + unstaged changes | `git diff HEAD` |
| Only staged changes | `git diff --staged` |
| Only unstaged changes | `git diff` |

### Between Commits
| Task | Command |
|---|---|
| Commit vs. its parent | `git show <commit>` |
| Two commits | `git diff <commit> <commit>` |
| One file since a commit | `git diff <commit> <file>` |
| Summary of a diff | `git diff <commit> --stat` *or* `git show <commit> --stat` |

## Ways to Refer to a Commit
Anywhere you see `<commit>`, you can use:

| Reference | Example |
|---|---|
| A branch | `main` |
| A tag | `v0.1` |
| A commit ID | `3e887ab` |
| A remote branch | `origin/main` |
| Current commit | `HEAD` |
| 3 commits ago | `HEAD~3` *or* `HEAD^^^` |

## Discard Changes
> ⚠️ These delete work. Double-check before running.

| Task | Command |
|---|---|
| Discard unstaged changes to one file | `git restore <file>` *or* `git checkout <file>` |
| Discard all changes to one file | `git restore --staged --worktree <file>` *or* `git checkout HEAD <file>` |
| Discard ALL staged + unstaged changes | `git reset --hard` *or* `git restore --staged --worktree .` |
| Delete untracked files | `git clean` |
| Stash all changes for later | `git stash` |

## Edit History
| Task | Command |
|---|---|
| Undo last commit (keep files as-is) | `git reset HEAD^` |
| Fix last commit message / add forgotten file | `git commit --amend` |
| Squash last 5 commits | `git rebase -i HEAD~5` → change `pick` to `fixup` on commits to combine |
| Undo a failed rebase | `git reflog <branch>` → find the right ID → `git reset --hard <commit>` |

## Code Archaeology
| Task | Command |
|---|---|
| Branch history | `git log main` |
| History as a graph | `git log --graph main` |
| Compact history | `git log --oneline` |
| Every commit that touched a file | `git log <file>` |
| Same, including before renames | `git log --follow <file>` |
| Commits that added/removed some text | `git log -G <text>` |
| Who last changed each line | `git blame <file>` |

## Combine Branches
| Method | Commands |
|---|---|
| Rebase | `git switch <feature>` → `git rebase main` |
| Merge | `git switch main` → `git merge <feature>` |
| Squash merge | `git switch main` → `git merge --squash <feature>` → `git commit` |
| Fast-forward (bring up to date) | `git switch main` → `git merge <feature>` |
| Copy one commit onto current branch | `git cherry-pick <commit>` |

## Restore an Old File
| Task | Command |
|---|---|
| Get a file's version from another commit | `git restore <file> --source <commit>` *or* `git checkout <commit> <file>` |

## Remotes, Push & Pull
### Remotes
| Task | Command |
|---|---|
| Add a remote | `git remote add <name> <url>` |

### Push
| Task | Command |
|---|---|
| Push main to origin | `git push origin main` |
| Push current branch to its tracking branch | `git push` |
| Push a new branch for the first time | `git push -u origin <name>` |
| Force push (safely) | `git push --force-with-lease` |
| Push tags | `git push --tags` |

### Pull
| Task | Command |
|---|---|
| Fetch without changing local branches | `git fetch origin main` |
| Fetch + rebase current branch | `git pull --rebase` |
| Fetch + merge into current branch | `git pull` *or* `git pull origin main` |

## Configure Git
| Task | Command |
|---|---|
| Set an option (this repo) | `git config user.name "Your Name"` |
| Set an option globally | `git config --global ...` |
| Add an alias | `git config alias.st status` |
| See all config options | `man git-config` |

## Important Files
| File | Purpose |
|---|---|
| `.git/config` | Local (repo) config |
| `~/.gitconfig` | Global config |
| `.gitignore` | Files Git should ignore |
