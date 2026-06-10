# git-follow-booster - GitHub Follower Manager CLI

A lightweight command-line tool to manage your GitHub followers and following — intelligently.  
Auto-follow users who are likely to follow back, bulk unfollow those who won't, and keep full control over your network.

---

## Requirements

- Python 3.8+
- A GitHub account
- A GitHub Personal Access Token *(required for follow/unfollow actions)*

---

## Installation

```bash
# 1. Clone the repository
git clone https://github.com/Sahil002620Q/git-follow-booster.git
cd git-follow-booster 

# 2. Create and activate a virtual environment
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the tool
python script.py
```

> **Note:** On first launch, use **Option 5 → Setup Account & Token** to configure your username and GitHub token. The tool will guide you through every step.

---

## Menu Overview

```
╔══════════════════════════════════════╗
║      GITHUB FOLLOWER MANAGER CLI            ║
╠══════════════════════════════════════╣
║  User  : your-username                      ║
║  Token : [OK] Token loaded                  ║
╠══════════════════════════════════════╣
║  1.  View Non-Followers                     ║
║  2.  Auto-Follow Smart Users                ║
║  3.  Bulk Unfollow                          ║
║  4.  Manage Ignore List                     ║
║  5.  Setup Account & Token                  ║
║  6.  Exit                                   ║
╚══════════════════════════════════════╝
```

---

## Options

### 1 · View Non-Followers

Lists every GitHub account you follow that is **not following you back**.

**What it does:**
- Fetches your complete following and followers lists via the GitHub API
- Computes the difference: *you follow them, they do not follow you*
- Excludes anyone on your **Ignore List**
- Displays the results as a clean numbered list

**Usage:**
1. Select `1` from the main menu
2. The tool fetches your data and displays the list
3. Press **Enter** to return to the menu

**Example output:**
```
=== USERS NOT FOLLOWING YOU BACK (12) ===
  001. alice
  002. bob-dev
  003. some-org
  ...
```

---

### 2 · Auto-Follow Smart Users

Automatically finds and follows GitHub users who have a **high probability of following you back**.

**How candidates are selected:**
- Scans the following lists of your followers *(warm leads — people your audience already follows)*
- Removes anyone you already follow, anyone on your Ignore List, and yourself
- Applies two hard filters:
  - **Active in the last 7 days** — only users with recent public activity
  - **Generous follow ratio** — `following ≥ followers` *(they follow back generously)*

**Scoring system** *(only candidates scoring ≥ 3 are shown)*:

| Criteria | Points |
|---|---|
| `following ≥ followers` | +3 |
| `following > followers × 1.5` | +2 bonus |
| Active within last 3 days | +2 |
| Active within last 4–7 days | +1 |

**Usage:**
1. Select `2` from the main menu
2. Enter how many accounts to follow in this session *(default: 10)*
3. The tool scans and scores candidates automatically — this may take a few minutes
4. Review the preview table showing each candidate's username, follower/following counts, and score
5. Type `y` to confirm and follow, or press Enter to cancel

**Example preview:**
```
=== AUTO-FOLLOW PREVIEW  (8 candidates) ===

+---+--------------+-----------+-----------+-------+-------------------------------+
| # | Username     | Followers | Following | Score | Why                           |
+---+--------------+-----------+-----------+-------+-------------------------------+
| 1 | dev-user-x   | 42        | 130       | 7     | following ≥ followers (+3)... |
| 2 | coder-99     | 18        | 60        | 5     | following ≥ followers (+3)... |
+---+--------------+-----------+-----------+-------+-------------------------------+

  Follow these 8 accounts? [y/N]:
```

> **Tip:** Accounts are followed with a 0.6-second delay between each to respect GitHub's API rate limits.

---

### 3 · Bulk Unfollow

Unfollow multiple accounts at once using smart category filters.

**Sub-menu options:**

#### 3.1 — Non-followers
Unfollows accounts that **you follow but who are not following you back**.

- Same logic as Option 1, but instead of just listing, it takes action
- You choose how many to unfollow per session (or unfollow all at once)
- Shows a numbered preview list before any action is taken

#### 3.2 — High-ratio accounts
Unfollows accounts where **followers >> following** — a pattern typical of celebrities, large organisations, and bots that almost never follow back.

- Fetches profile data for everyone you follow
- Filters to those with `followers > following`
- You choose the batch size and confirm before execution

**Usage:**
1. Select `3` from the main menu
2. Choose a filter category (`1` or `2`)
3. Enter how many accounts to unfollow — enter `0` to unfollow all found
4. Review the preview list
5. Type `y` to confirm — the tool unfollows each account with a short delay

**Example:**
```
=== BULK UNFOLLOW PREVIEW  (15 accounts | Non-followers) ===

  001. alice
  002. bob-dev
  003. some-org
  ...

  Unfollow these 15 accounts? [y/N]:
```

> **Note:** Accounts on your Ignore List are always excluded from unfollow operations.

---

### 4 · Manage Ignore List

Maintain a personal list of accounts that are **permanently protected** from any follow or unfollow action.

**What it does:**
- Accounts on the Ignore List are skipped by all other options
- Useful for protecting accounts you want to keep following regardless of whether they follow back (e.g. close friends, organisations you admire)

**Sub-menu options:**

| Option | Action |
|---|---|
| `1` | Add a username to the Ignore List |
| `2` | Remove a username from the Ignore List |
| `3` | Back to Main Menu |

**Usage:**
1. Select `4` from the main menu
2. Choose to add or remove a username
3. Type the exact GitHub username and press Enter

---

### 5 · Setup Account & Token

Configure your GitHub username and Personal Access Token in one guided flow.  
**This is the first thing you should do on a fresh install.**

#### Part A — Set Username
- Displays your currently configured username
- Press Enter to keep it unchanged, or type a new GitHub username

#### Part B — GitHub Personal Access Token (PAT)

The tool walks you through generating a token step by step:

```
Step 1. Open your browser and go to:
        https://github.com/settings/tokens/new

Step 2. Sign in if prompted.

Step 3. Fill in the form:
         Note      : GitHub Follower Manager
         Expiration: 90 days  (or No expiration)

Step 4. Under 'Select scopes', tick:
         [x]  user > follow

Step 5. Click 'Generate token'.

Step 6. COPY the token shown (starts with ghp_...)
        It will NOT be shown again!
```

- The tool offers to **open the GitHub token page in your browser automatically**
- After pasting the token, it validates the format (`ghp_` or `github_pat_`)
- The token is **saved to a `.env` file** in the project directory
- The token is **activated immediately** in the running session — no restart required

**Token status** is always visible in the main menu header:
```
║  Token : [OK] Token loaded    ║   ← token is set and active
║  Token : [!] No token (limited) ║  ← no token, read-only mode
```

> **Security:** Your token is stored only in the local `.env` file and is never transmitted anywhere other than the GitHub API.

---

## API Rate Limits

| Mode | Limit |
|---|---|
| No token (unauthenticated) | 60 requests / hour |
| With Personal Access Token | 5,000 requests / hour |

After each follow/unfollow operation, the tool displays how many API calls remain and when the limit resets.

> Running Auto-Follow or Bulk Unfollow on large accounts benefits greatly from a token.

---

## File Structure

```
git-tool-cli/
├── main.py          # CLI menu and all user-facing flows
├── api_handler.py   # All GitHub API calls (follow, unfollow, fetch, score)
├── utils.py         # Config helpers, scoring logic, display utilities
├── config.json      # Stores username and ignore list (auto-created)
├── .env             # Stores GITHUB_TOKEN (auto-created by Option 5)
└── venv/            # Python virtual environment
```

---

## Security & Privacy

- Your GitHub token is stored **locally only** in `.env`
- The `.env` file should **never be committed** to version control
- Add `.env` to your `.gitignore`:
  ```
  .env
  ```
- The tool only uses the `user` scope — it cannot access private repositories, delete content, or modify your profile beyond follow/unfollow actions

---

## License

MIT License — free to use, modify, and distribute.
