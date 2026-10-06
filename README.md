# Data-Science-Club-FA26

This repository is meant to serve as a collective codebase for exploration of the three Kaggle datasets found in the `data` folder. Those datasets are:

- Spaceship Titanic
- 281K Patient Dataset for Multi-Disease Prediction
- NBA games data

Feel free to clone this repo to poke around with the data. Use any code language you want, but it might take me some time to review any pull requests made in a language other than R or Python.

Some suggestions:
- Keep code in the `src` folder
- Clone the repo, *then create a new branch to work on*; don't work in the main branch
- If you are going to save modified versions of the datasets, don't overwrite the existing dataset files
  - Doing so will make it almost impossible to incorporate your code

If you're looking for something to do, check the [TODO List](docs/TODO.md).

---

The following guide for using Git through RStudio was generated with Claude Sonnet 5.5:

# Clone, Branch, Commit, and Open a Pull Request with RStudio and GitHub

A walkthrough for working on a GitHub repository from RStudio, from first-time setup through a merged pull request.

---

## 0. One-time setup: install and configure Git

You only need to do this once per computer. Everything here happens outside of R, in a terminal. Afterward, RStudio will pick Git up automatically.

### Step 1: Check whether Git is already installed

Open a terminal:
- **Windows:** open the Start menu and search for **Command Prompt** or **PowerShell**
- **Mac:** open **Terminal** (Applications → Utilities)

Then run:
```bash
git --version
```
If you see a version number, skip to Step 3.

### Step 2: Install Git

**Windows**
1. Download the installer from [git-scm.com/downloads](https://git-scm.com/downloads).
2. Run it. The default options are fine for most people.
3. Close and reopen your terminal, and (if it's open) restart RStudio.

Alternatively, if you use `winget`:
```powershell
winget install --id Git.Git -e
```

**Mac**
- Run `git --version` in Terminal. If Git isn't installed, macOS will offer to install the Xcode Command Line Tools. Click **Install** and wait for it to finish.
- Or, if you use [Homebrew](https://brew.sh/):
  ```bash
  brew install git
  ```

Run `git --version` again to confirm it worked.

### Step 3: Set your identity

Git attaches this name and email to every commit you make:
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
Use the email address tied to your GitHub account so your commits are linked to your profile.

*Optional:* name your default branch `main` for new repos:
```bash
git config --global init.defaultBranch main
```

Check your settings any time with:
```bash
git config --global --list
```

### Step 4: Authenticate with GitHub

Pick one method.

**Option A: GitHub CLI (easiest)**
1. Install [`gh`](https://cli.github.com/) (Windows: `winget install --id GitHub.cli`; Mac: `brew install gh`.
2. Run:
   ```bash
   gh auth login
   ```
3. Choose **GitHub.com**, then **HTTPS**, and log in through the browser when prompted. This also configures Git to use those credentials.

**Option B: SSH key**
1. Generate a key (press Enter to accept the defaults):
   ```bash
   ssh-keygen -t ed25519 -C "you@example.com"
   ```
2. Copy the public key:
   - **Mac:** `pbcopy < ~/.ssh/id_ed25519.pub`
   - **Windows (PowerShell):** `Get-Content ~\.ssh\id_ed25519.pub | Set-Clipboard`
3. On GitHub, go to **Settings → SSH and GPG keys → New SSH key** and paste it in.
4. Use the **SSH** URL (`git@github.com:...`) when cloning.

**Option C: Personal access token (HTTPS)**
1. On GitHub, go to **Settings → Developer settings → Personal access tokens** and generate a token with the `repo` scope.
2. The first time Git asks for a password (for example when cloning or pushing), paste the token instead. Your system's credential manager will remember it.

*Note:* if you already sign in through GitHub Desktop, HTTPS cloning from RStudio may work without extra setup, since the credential manager is often shared.

### Step 5: Confirm RStudio sees Git

1. Open RStudio and go to **Tools → Global Options → Git/SVN**.
2. Check that **Git executable** shows a path (for example `C:/Program Files/Git/bin/git.exe` on Windows or `/usr/bin/git` on Mac). If it's blank, click **Browse** and select it, then restart RStudio.

---

## 1. Clone the repository

1. On GitHub, click the green **Code** button and copy the HTTPS (or SSH) URL. Use the same type you set up in Section 0.
2. In RStudio: **File → New Project → Version Control → Git**.
3. Paste the URL, choose where to save the project, and click **Create Project**.

RStudio opens the project, and a **Git** tab appears in the top-right pane. That tab only shows up inside a project that is a Git repo.

*Terminal alternative:* `git clone <url>`, then open the folder in RStudio with **File → Open Project**.

---

## 2. Create a branch

1. In the **Git** tab, click the purple **New Branch** icon.
2. Name it something descriptive, like `fix-plot-labels`.
3. Leave "Sync branch with remote" checked, then click **Create**.

RStudio switches to the new branch automatically. You can confirm the current branch in the top-right of the Git pane.

*Terminal alternative:* `git checkout -b fix-plot-labels`

---

## 3. Make commits

1. Edit and save your files.
2. In the **Git** tab, check the **Staged** box next to each file you want to include.
3. Click **Commit**, write a short, clear message (e.g. "Fix axis labels in scatter plot"), and click **Commit** again.
4. Repeat as often as you like. Small, focused commits are easier to review.
5. Click **Pull** first (to pick up any upstream changes), then **Push** to send your commits to GitHub.

---

## 4. Open a pull request

RStudio can't open pull requests itself, so you'll do this from GitHub's website or GitHub Desktop. Either way, **push your branch first** (the **Push** button in RStudio's Git tab, or **Push origin** in Desktop).

### Option A: From the GitHub website
1. Go to the repo on GitHub. A yellow banner should appear: **"Compare & pull request"**. Click it. (If it's missing, open the **Pull requests** tab → **New pull request** and pick your branch.)
2. Confirm the **base** branch (usually `main`) and the **compare** branch (yours).
3. Add a clear title and a description of what changed and why.
4. Optionally, add reviewers, labels, or link an issue (e.g. "Closes #12").
5. Click **Create pull request**. Use the dropdown arrow to open it as a **draft** if it isn't ready for review.

### Option B: From GitHub Desktop
1. Install [GitHub Desktop](https://desktop.github.com/) and sign in (**File → Options → Accounts**).
2. Add your RStudio project with **File → Add Local Repository** and select the project folder.
3. Make sure your branch is selected and pushed (**Push origin**).
4. Click **Create Pull Request** on the prompt, or choose **Branch → Create Pull Request** (`Ctrl+R` / `Cmd+R`).
5. Desktop opens GitHub in your browser with the PR form prefilled. Add a title and description, then click **Create pull request**.

*Tip:* **Branch → Preview Pull Request** in Desktop shows a diff against the base branch before you open the PR, which is a handy self-review.

### After the PR is open
- **Review feedback:** commit and push more changes to the same branch. The PR updates automatically, so there's no need to open a new one.
- **Merging:** once approved, a maintainer (or you, if you have permission) clicks **Merge pull request** on GitHub.
- **Cleanup:** switch back to `main` in RStudio (or Desktop) and **Pull** to sync, then delete the finished branch.

---

## 5. Manage pull requests with GitHub Desktop

GitHub Desktop and RStudio use the same local Git repo, so you can switch between them freely. Desktop is handy for tracking PRs, checking them out, and keeping your branch current. Reviewing and merging still happen on GitHub.

### Track and check out PRs
- Click the **Current Branch** dropdown and open the **Pull Requests** tab to see all open PRs for the repo.
- A colored icon next to each PR shows its CI check status (running, passed, or failed).
- Click any PR to check out its branch locally, which is useful for testing a teammate's changes or a PR from a fork.

### Keep your branch current
If `main` has moved ahead, use **Branch → Update from main** to merge those changes into your branch. If Desktop reports conflicts, open them in your editor, resolve them, commit, and push.

### After the PR is merged
1. In Desktop, switch to `main` and click **Fetch origin**, then **Pull origin**.
2. Delete the finished branch with **Branch → Delete**. GitHub also offers a **Delete branch** button on the merged PR.
3. In RStudio, the Git tab will reflect the updated `main`.
