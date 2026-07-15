## Getting Started

Welcome to the VS Code Java world. Here is a guideline to help you get started to write Java code in Visual Studio Code.

## Folder Structure

The workspace contains two folders by default, where:

- `src`: the folder to maintain sources
- `lib`: the folder to maintain dependencies

Meanwhile, the compiled output files will be generated in the `bin` folder by default.

> If you want to customize the folder structure, open `.vscode/settings.json` and update the related settings there.

## Dependency Management

The `JAVA PROJECTS` view allows you to manage your dependencies. More details can be found [here](https://github.com/microsoft/vscode-java-dependency#manage-dependencies).

---

# Project Configuration Files

This section explains the purpose and significance of key configuration files used in this project.

---

## 1. The `.vscode` Folder & `settings.json`

### What is the `.vscode` folder?

The `.vscode` folder is a **project-specific configuration folder** automatically created by Visual Studio Code when you customize settings for a particular workspace. It lives in the root of your project and contains settings that apply **only to this project**, overriding your global (user-level) VS Code preferences.

### Common files inside `.vscode`:

| File | Purpose |
|------|---------|
| `settings.json` | Project-specific VS Code settings |
| `tasks.json` | Build/run task definitions |
| `launch.json` | Debugger configuration |
| `extensions.json` | Recommended extensions for the project |

### What is `settings.json`?

The `settings.json` file inside `.vscode` allows you to define **workspace-level settings** that override the default or user-level settings. This is useful for ensuring every contributor to the project uses the same configuration.

### Common settings used in Java projects:

```json
{
    "java.project.sourcePaths": ["src"],
    "java.project.outputPath": "bin",
    "java.project.referencedLibraries": ["lib/**/*.jar"],
    "editor.fontSize": 14,
    "files.autoSave": "onFocusChange",
    "editor.tabSize": 4
}
```

| Setting | Description |
|---------|-------------|
| `java.project.sourcePaths` | Defines the source code directories |
| `java.project.outputPath` | Specifies where compiled `.class` files go (e.g., `bin/`) |
| `java.project.referencedLibraries` | Lists external JAR dependencies |
| `editor.fontSize` | Sets the font size in the editor for this project |
| `files.autoSave` | Controls auto-save behavior |
| `editor.tabSize` | Sets the number of spaces per tab |

### Why is `.vscode/settings.json` important?

- **Consistency** — Ensures all developers working on the project use the same settings.
- **Portability** — Settings travel with the project when shared via Git.
- **Team Standards** — Enforces coding conventions (e.g., tab size, formatting).
- **Build Configuration** — Configures Java project paths, output directories, and library references.

> ⚠️ **Note:** It is common practice to **include** `.vscode/settings.json` in version control (commit it) so the team shares the same configuration, but **exclude** user-specific files like `.vscode/launch.json` if they contain machine-specific paths.

---

## 2. The `.gitignore` File

### What is `.gitignore`?

A `.gitignore` file is a **plain text configuration file** that tells Git which files and folders to **ignore** — meaning they will not be tracked, staged, or committed to the repository. It must be placed in the root of your Git repository.

### Why is `.gitignore` needed?

Not all files in a project should be committed to version control. Some files are:

- **Generated automatically** (compiled code, build output)
- **System-specific** (IDE settings, OS files)
- **Sensitive** (passwords, API keys, environment variables)
- **Large dependencies** (node_modules, JARs that can be downloaded)

### How `.gitignore` works

Git reads the patterns in `.gitignore` and automatically excludes any file or folder matching those patterns from `git add`, `git status`, and `git commit`.

### Common `.gitignore` patterns explained:

```
# Java compiled files
*.class
```
- `*.class` — Ignores all files ending with `.class` (compiled Java bytecode).

```
# Java build output
bin/
```
- `bin/` — Ignores the entire `bin/` directory where compiled `.class` files are output.

```
# VS Code settings
.vscode/
```
- `.vscode/` — Ignores the entire `.vscode/` configuration folder (optional — some teams choose to commit `settings.json` but ignore other files).

### More useful `.gitignore` patterns:

```gitignore
# OS files
.DS_Store        # macOS folder metadata
Thumbs.db        # Windows thumbnail cache

# IDE files
*.swp            # Vim swap files
.idea/           # JetBrains IntelliJ IDEA folder
*.iml            # IntelliJ module files

# Logs and temporary files
*.log
*.tmp
*.bak

# Environment and secrets
.env             # Environment variables (may contain API keys)
*.key            # Private keys
```

### Sample `.gitignore` for a Java project:

```gitignore
# Java compiled files
*.class

# Build output directories
bin/
build/
target/
dist/
out/

# VS Code settings
.vscode/

# IDE files (other editors)
.idea/
*.iml
.settings/
.project
.classpath
*.class

# OS files
.DS_Store
Thumbs.db

# Logs
*.log

# JAR dependencies (download via build tools)
lib/**/*.jar
```

### Why is `.gitignore` important?

| Reason | Explanation |
|--------|-------------|
| **Keeps repo clean** | Prevents build artifacts, temp files, and OS files from cluttering the repository. |
| **Reduces repo size** | Excluding binaries and generated files keeps the repository lightweight. |
| **Prevents sensitive data leaks** | Stops accidental commits of passwords, keys, or environment variables. |
| **Avoids conflicts** | System-specific files (like IDE settings) vary per developer and cause unnecessary merge conflicts. |
| **Improves performance** | Git operations (clone, fetch, status) are faster with fewer files to track. |

### Rules to remember:

1. `.gitignore` should be **committed** to the repository so all team members benefit from it.
2. Patterns are evaluated **per line** — one pattern per line.
3. Use `#` for **comments** to document why certain files are ignored.
4. Once a file is **already tracked** by Git, adding it to `.gitignore` will **not** stop tracking it — you must first run `git rm --cached <file>` to untrack it.
5. Use `!` to **negate** a pattern (re-include a specific file that was excluded by a broader pattern).

---

# Git Command Notes

This section contains detailed notes and examples of various Git commands used throughout this project.

---

## 1. First Commit & Push to GitHub

Step-by-step guide to initialize a Git repository and push changes to GitHub.

**Step 1:** Install Git Bash from [here](https://git-scm.com/downloads/windows) and navigate to your project directory.

**Step 2:** Initialize a Git repository in the root of your project folder.

```bash
git init
```
*Example output:*
```
Initialized empty Git repository in c/Users/Shankar/Documents/Workspace/GitHubCourse/GitHubSession/.git
```

**Step 3:** A `.git` hidden folder is created. To view hidden files:

```bash
ls -alt
```

**Step 4:** Check if any remote repository is already associated:

```bash
git remote -v
```
If it shows empty, no remote repository is associated.

**Step 5:** Associate a remote repository to your local repo:

```bash
git remote add origin <repository-url>
```

**Step 6:** Check the status of your working directory:

```bash
git status
```

**Step 7:** Create a `.gitignore` file and add the following entries:

```gitignore
# Java compiled files
*.class

# Java build output
bin/

# VS Code settings
.vscode/
```

**Step 8:** Stage all changed/modified/newly created files:

```bash
git add .
```
This adds all working copy changes to the staging area.

**Step 9:** Commit the staged changes to the local repository:

```bash
git commit -m "commit message"
```
> ⚠️ This commits changes only to the local repository, **not** the remote repository.

**Step 10:** Push the committed changes to the remote repository on GitHub:

```bash
git push origin master
```

**Step 11:** Verify by visiting your GitHub repository — your changes should now be visible there.

---

## 2. Git Diff Commands

Compare changes between different states of your repository.

| Command | Description |
|---------|-------------|
| `git diff` | Compares your **Working Directory** with the **Staging Area (Index)** — shows what recent changes have been made in your IDE. |
| `git diff <commit-id1> <commit-id2>` | Shows the differences between two specific commits. |

**Example:**

```bash
git diff 9982254 12caef6
```
This displays all changes between commit `9982254` and commit `12caef6`.

---

## 3. Git Shortlog

Summarize commit history in a concise, author-wise format.

| Command | Description |
|---------|-------------|
| `git log` | Shows commit-by-commit history in detail. |
| `git shortlog` | Summarizes commit history grouped by author. |
| `git blame` | Finds who last changed each line of a file and in which commit. |

**Example:**

```bash
git shortlog
```
*Output might look like:*
```
Shankar (3): Add login page, Fix registration bug, Update README
```

---

## 4. Last Commit / Show Commands

View the most recent commit and inspect changes.

| Command | Description |
|---------|-------------|
| `git show` | Shows the changes made in the **last commit** (same as `git show HEAD`). |
| `git show HEAD` | Identical to `git show` — displays the latest commit details. |
| `git show HEAD~1` | Shows changes from the commit **before the last** commit (1 commit ago). |
| `git show HEAD~2` | Shows changes from the commit **2 commits ago**. |
| `git show <commit-id>` | Shows changes for a specific commit ID. |
| `git show HEAD:<file-path>` | Displays the full content of a specific file as it was in the latest commit. |

**Examples:**

```bash
# Show changes from the last commit
git show

# Show changes from 2 commits ago
git show HEAD~2

# Show changes for a specific commit
git show ed01147

# Show the full content of a file as it was in the HEAD commit
git show HEAD:src/test/MyTest.java
```

---

## 5. Git Log Commands

Explore the commit history with various filtering options.

### Basic Log Commands

| Command | Description |
|---------|-------------|
| `git log` | Shows the complete commit history with full details. |
| `git log --oneline` | Displays a short one-line summary of each commit. |
| `git log -5` | Shows only the latest **5** commits. |
| `git log --oneline -10` | Shows the latest **10** commits in short format. |

### Filtering by Author

```bash
git log --author="cheeras"
```
Filters the commit history to show only commits by the specified author.

### Filtering by Date

```bash
git log --before="2026-07-15"
git log --after="2026-07-10"
git log --after="one week ago"
```

### Searching Commit Messages

```bash
git log --grep="files"    # Search for commits containing "files"
git log --grep="us101"    # Search for commits referencing user story "us101"
```

### Commit Range

```bash
git log 4d7306d...27a184e
```
Shows all commits between the specified range.

### Detailed Change Analysis

```bash
# Shows a complete list of modified files (HOW MUCH changed)
git log --stat

# Shows exactly what changed in each file (WHAT changed)
git log --patch
```

> **Difference between `--stat` and `--patch`:**
> - `git log --stat` tells you **how much** changed (file names, additions, deletions).
> - `git log --patch` tells you **exactly what** changed (the actual line-by-line diff).

---

## Summary of Essential Git Commands

| Command | Purpose |
|---------|---------|
| `git init` | Initialize a new Git repository |
| `git remote add origin <url>` | Link local repo to a remote GitHub repository |
| `git status` | Check the current state of the working directory |
| `git add .` | Stage all changes for commit |
| `git commit -m "msg"` | Commit staged changes to the local repository |
| `git push origin master` | Push local commits to the remote repository |
| `git diff` | Show unstaged changes in the working directory |
| `git log` | View commit history |
| `git show` | View details of a specific commit |
| `git shortlog` | View author-wise summary of commits |
| `git blame` | Find who last modified each line of a file |
