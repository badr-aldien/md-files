---
marp: true
paginate: true
---

# GitHub and Remote Repositories - Day 2

### Badr Aldien Soliman

---

## Learning Objectives

- Understand the difference between **Git** and **GitHub**.
- Manage **Remote Repositories** (Create, Push, Pull).
- Work with **Branches** on GitHub.
- Master **Pull Requests** and **Merge Conflicts**.
- Collaborate effectively in teams.

---

## 1. What is GitHub?

GitHub is a cloud platform for hosting Git repositories.

- **Cloud Storage**: "Google Drive" for your code.
- **Collaboration**: Social network for developers to share/edit code.
- **Portfolio**: Showcase your projects to potential employers.

---

### Why Remote Repositories?

- **Safety**: Code is safe even if your hardware fails.
- **Teamwork**: Multiple people working on the same codebase.
- **Mobility**: Access and work on your code from any device.
- **Sync**: A central "Source of Truth" for the project.

---

## 2. Local vs Remote Repositories

| **Local Repository** (Your PC) | **Remote Repository** (GitHub) |
| :--- | :--- |
| Contains `.git` folder | Copy of `.git` folder |
| Your commits & history | Shared commits & history |


**The Connection:**
`git push` (Upload) ➔
`git pull` (Download) ⬅

---

## 3. Getting Started

### Step 1: Sign Up
- Go to [github.com](https://github.com).
- Choose a **professional username** (it's part of your portfolio!).

### Step 2: Create a Repository
1. Click **+** ➔ **New repository**.
2. Name it (e.g., `my-first-repo`).
3. Choose **Public** or **Private**.

---

### Public vs. Private Repositories

**Public**
- ✅ Visible to everyone (Great for portfolios).
- ✅ Required for open source contributions.
- ❌ Code is open to public.

**Private**
- ✅ Only you (and invited guests) can see it.
- ✅ Safe for experimentation/secret projects.
- ❌ Doesn't build public visibility.

---

## 4. Understanding "Origin"

### What is "Origin"?
It is just a **nickname** for your remote repository URL.

```bash
git remote add origin https://github.com/user/repo.git
```

- **Convention**: Everyone uses this name.
- **Efficiency**: Faster than typing the full URL every time.
- **Standard**: Git sets this as the default name.
> note: How git sets it automatically? 

---

## 5. Connecting Local to Remote

### Step 1: Add the Remote
```bash
git remote add origin https://github.com/user/repo.git
```

### Step 2: Push for the First Time
```bash
git push -u origin main
```
> Is -u origin main only for the first time?

---

**Breaking it down:**
- `push`: Send commits to GitHub.
- `-u`: Sets "Upstream" tracking (link local to remote).
- `origin`: The remote nickname.
- `main`: The branch name.

---

### What Does `-u` Do?

By setting a **Tracking Relationship**, you save time:

| **Without -u** (Every time) | **With -u** (One-time setup) |
| :--- | :--- |
| `git push origin main` | `git push` |
| `git pull origin main` | `git pull` |

*Git now "knows" exactly where to send and receive data for that branch.*

---

## 6. Working with Branches

### Workflow:
1. **Create locally**: `git checkout -b feature-login`
2. **Make changes**: `git add .` ➔ `git commit -m "..."`
3. **Push to GitHub**: `git push -u origin feature-login`

**After the first push:**
Simply use `git push` while on that branch.

---

## 7. Syncing Your Repo

### The Problem: Remote Changes
Others may have pushed code while you were working.

### The Solution: `git pull`
It performs two actions:
1. **Fetch**: Downloads new data.
2. **Merge**: Integrates it into your local files.

**Best Practice**: Always `git pull` before starting new work.

---

### Pulling a Specific Branch

```bash
# Pull main specifically
git pull origin main

# Pull a specific feature
git pull origin feature-login
```

---

## 8. Pull Requests (PR)

A **Pull Request** is a request to merge your changes into the main branch.

### The PR Workflow:
1. **Push** your branch to GitHub.
2. Click **"Compare & pull request"** on GitHub.
3. Review changes and add a description.
4. **Merge**: Once approved, the code is combined into `main`.
5. **Cleanup**: Delete the feature branch.

---

## 9. Handling Merge Conflicts

### Why do they happen?
- Two people edit the **same line**.
- Git can't decide which version is correct.

### Conflict Markers:
```markdown
<<<<<<< HEAD
Your local version (Hello World)
=======
The incoming version (Hello Universe)
>>>>>>> feature-branch
```

---

### Resolving Conflicts (Step-by-Step)

1. **Identify**: Run `git status` to see conflicted files.
2. **Choose**: Manually edit the file to keep the correct code.
3. **Clean**: Delete the `<<<<<`, `=====`, and `>>>>>` markers.
4. **Stage**: `git add file.html`
5. **Commit**: `git commit -m "Resolve conflict"`
6. **Push**: `git push`

---

## 10. Complete Team Workflow

1. `git pull` (Get latest code).
2. `git checkout -b feature-name` (Start work).
3. `git commit -am "Progress"` (Save work).
4. `git push -u origin feature-name` (Share branch).
5. **Open PR** on GitHub.
6. **Resolve Conflicts** if necessary.
7. **Merge** and `git pull` back on `main`.

---

# Every bug is a lesson

## **[badrsoliman.com](https://www.badrsoliman.com)**
