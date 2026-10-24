# GitHub Follow-Back Manager

<p align="center">
  <strong>Find who doesn't follow you back. Discover active developers. Clean up your following list — from your terminal.</strong>
</p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white">
  <img alt="GitHub API" src="https://img.shields.io/badge/GitHub-REST%20API-181717?logo=github">
  <img alt="CLI" src="https://img.shields.io/badge/Interface-CLI-2ea44f">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-blue.svg">
</p>

A Python command-line tool for understanding and managing your GitHub follow network. See accounts that don't follow you back, preview potential developers to follow, bulk-unfollow selected accounts, and protect important users with an ignore list.

**No web dashboard. No database setup. Just Python and the GitHub API.**

> **Important:** This tool can follow and unfollow accounts on your behalf. Review the preview carefully before confirming an action. It does not guarantee that another user will follow you back.

## ✨ What can it do?

| Feature | What it does |
| --- | --- |
| 🔎 **Find non-followers** | Compare your followers and following lists to identify accounts that don't follow you back. |
| 🤝 **Discover potential follows** | Score candidate accounts using public activity and follower/following signals, then show a preview before following. |
| 🧹 **Bulk unfollow** | Preview and unfollow selected non-followers or accounts with more followers than following. |
| 🛡️ **Ignore list** | Protect specific usernames from the tool's follow/unfollow workflows. |
| 📊 **Rate-limit awareness** | Show remaining GitHub API calls when available. |
| 🔐 **Local token setup** | Configure a GitHub token through the interactive menu; the token is saved locally in `.env`. |

## 🚀 Quick start

### 1. Requirements

- Python **3.8 or newer**
- A GitHub account
- A GitHub Personal Access Token for follow/unfollow actions

### 2. Clone the repository

```bash
git clone https://github.com/Sahil002620Q/Who-is-not-following-back-git.git
cd Who-is-not-following-back-git
```

### 3. Create a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can run `venv\Scripts\python.exe` directly or use Command Prompt:

```bat
venv\Scripts\activate.bat
```

**Linux / macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 4. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 5. Launch

```bash
python script.py
```

On first launch, choose **Option 5 — Setup Account & Token**. Enter your GitHub username and follow the prompts to configure a token.

## 🔑 Set up your GitHub token

1. Open [GitHub token settings](https://github.com/settings/tokens/new).
2. Create a token and choose an expiration that works for you.
3. Grant only the permissions required for following/unfollowing users (the classic token flow labels this `user:follow`).
4. Generate the token and copy it immediately.
5. In the application, choose **5 — Setup Account & Token** and paste it when prompted.

The application saves the token in a local `.env` file. **Never share your token or commit `.env` to Git.** If a token is exposed, revoke it in GitHub settings immediately. Without a token, read-only requests may still work within GitHub's lower unauthenticated rate limit, but follow/unfollow actions are unavailable.

## 🧭 Menu guide

```text
1. View Non-Followers
2. Auto-Follow Smart Users
3. Bulk Unfollow
4. Manage Ignore List
5. Setup Account & Token
6. Exit
```

### 1 — View Non-Followers
Fetches your followers and following lists, then displays accounts you follow that do not follow you back. Accounts on your ignore list are excluded.

### 2 — Auto-Follow Smart Users
Builds a candidate list from accounts followed by some of your followers, filters out accounts you already follow or have ignored, and evaluates public profile/activity signals. It shows a ranked preview and asks for confirmation before following. **This is a heuristic, not a prediction or guarantee.**

### 3 — Bulk Unfollow
Choose one of the available categories:
- **Non-followers:** accounts you follow that don't follow you back.
- **High-ratio accounts:** accounts whose follower count is greater than their following count.

The tool displays a preview and asks for confirmation before unfollowing. Use this carefully; bulk actions may be difficult to reverse manually.

### 4 — Manage Ignore List
Add usernames you want the tool to skip or remove usernames from the list. Use this to protect accounts you always want to keep following.

### 5 — Setup Account & Token
Change your configured GitHub username and set or update your token.

## 📁 Project structure

```text
Who-is-not-following-back-git/
├── script.py          # Interactive CLI and menu
├── api_handler.py     # GitHub API operations
├── utils.py            # Configuration, scoring, and display helpers
├── requirements.txt    # Python dependencies
├── config.json         # User settings / ignore list (created or updated locally)
├── .env                # Local token (created locally; do not commit)
└── .gitignore          # Files excluded from Git, if configured
```

The `.env` and `config.json` files may be created or updated while you use the tool. Keep local secrets out of version control.

## 🧰 Troubleshooting

- **`python` not found:** install Python 3.8+ and ensure it is on your PATH; on some systems use `python3`.
- **Missing module error:** activate your virtual environment and run `pip install -r requirements.txt`.
- **Token rejected:** create a new token with the needed follow permission and update it through Option 5.
- **Rate limit reached:** wait until GitHub's limit resets. Authenticated limits depend on the API and token.
- **No candidates found:** the heuristic may not find suitable accounts for your current network or activity window. Try again later.

## 🔒 Security notes

- Keep your token in the local `.env` file; never paste it into an issue, public chat, or commit.
- Verify that `.env` is listed in `.gitignore` before making commits.
- Review each preview before confirming follow/unfollow operations.
- Use this project responsibly and respect GitHub's rules and other users.

## 🤝 Contributing

Suggestions, bug reports, and pull requests are welcome. If you find a bug, open an issue with the steps to reproduce it. **Never include access tokens or other secrets in issues.**

## 📄 License

MIT License. See the [LICENSE](LICENSE) file if included in this repository.

---

<p align="center">
  If this tool is useful to you, consider giving the repository a ⭐ and sharing feedback.
</p>
