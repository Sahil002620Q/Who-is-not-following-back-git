# GitHub Follow-Back Manager

A Python command-line tool to manage your GitHub follow network. Find accounts that do not follow you back, discover potentially relevant developers to follow, bulk-unfollow selected accounts, and protect important users with an ignore list.

## Features

| Feature | Description |
| --- | --- |
| **View non-followers** | Compare your followers and following lists to find accounts that do not follow you back. |
| **Smart auto-follow** | Find candidate developers using public profile and recent activity signals. Review the list before following. |
| **Bulk unfollow** | Review and unfollow non-followers or accounts with more followers than following. |
| **Ignore list** | Exclude selected usernames from follow and unfollow actions. |
| **Token setup** | Configure your GitHub username and token from the interactive menu. |
| **Rate-limit information** | Display remaining API calls when GitHub provides the information. |

> **Important:** Follow and unfollow actions change your GitHub account. Review the preview and confirm carefully. Candidate scoring is heuristic and cannot guarantee that someone will follow you back.

## Requirements

- Python 3.8 or newer
- A GitHub account
- A GitHub Personal Access Token for follow/unfollow actions

## Installation

Clone the repository, install the dependencies, and run the script:

```bash
git clone https://github.com/Sahil002620Q/Who-is-not-following-back-git.git
cd Who-is-not-following-back-git
python -m pip install -r requirements.txt
python script.py
```

If your system uses `python3`, replace `python` with `python3` in the commands above. A virtual environment is optional; if you use one, activate it before installing dependencies.

On the first launch, choose **Option 5 — Setup Account & Token** to configure your account.

## Menu overview

```text
1. View Non-Followers
2. Auto-Follow Smart Users
3. Bulk Unfollow
4. Manage Ignore List
5. Setup Account & Token
6. Exit
```

## How to use

### 1. View Non-Followers

Fetches your followers and following lists, then displays accounts you follow that do not follow you back. Usernames on your ignore list are excluded.

### 2. Auto-Follow Smart Users

Finds potential accounts by scanning the following lists of some of your followers. It excludes accounts you already follow, ignored usernames, and your own account, then evaluates public profile details and recent activity.

- Candidates are filtered using follower/following signals and recent public activity.
- The tool scores candidates and shows a preview before taking action.
- Choose how many accounts to consider for the session.
- Confirm with `y` to proceed, or press Enter to cancel.

This is a heuristic based on public signals, not a guarantee of a follow-back.

### 3. Bulk Unfollow

Choose one of the available categories:

- **Non-followers:** accounts you follow that do not follow you back.
- **High-ratio accounts:** accounts whose follower count is greater than their following count.

Choose a batch size, review the preview, and confirm before unfollowing. Accounts on your ignore list are excluded.

### 4. Manage Ignore List

Add usernames you want to protect or remove usernames from the list. Ignored accounts are skipped by the tool's follow/unfollow workflows.

### 5. Setup Account & Token

Use this option to configure or update your GitHub username and Personal Access Token. Follow the prompts in the application.

## GitHub token setup

1. Open [GitHub token settings](https://github.com/settings/tokens/new).
2. Create a token and select an expiration period.
3. Grant the **`user:follow`** permission required for follow/unfollow actions.
4. Generate the token and copy it immediately; GitHub will not show it again.
5. Run the script and choose **Option 5 — Setup Account & Token** to enter the token.

The token is stored locally in a `.env` file and loaded by the application. Without a token, some read-only requests may still work, but they have a lower unauthenticated API limit and follow/unfollow actions are unavailable.

**Keep your token private.** Never paste it into an issue, message, or commit. If it is exposed, revoke it in GitHub settings and create a replacement. Make sure `.env` is listed in `.gitignore`.

## API rate limits

GitHub applies API rate limits. Unauthenticated requests generally have a lower limit than authenticated requests, and the exact remaining quota can vary. The application displays rate-limit information when available. If you reach a limit, wait for it to reset before trying again.

## Project structure

```text
Who-is-not-following-back-git/
├── script.py          # CLI menu and workflows
├── api_handler.py     # GitHub API requests and follow operations
├── utils.py           # Configuration, scoring, and display helpers
├── requirements.txt   # Python dependencies
├── config.json        # Local username and ignore-list settings
├── .env               # Local GitHub token; do not commit
└── .gitignore         # Git exclusions
```

The `.env` and `config.json` files may be created or updated locally while using the tool.

## Troubleshooting

- **Python command not found:** Install Python 3.8+ and ensure it is on your PATH; try `python3` if needed.
- **Missing module:** Run `python -m pip install -r requirements.txt`.
- **Token rejected:** Create a token with the required follow permission and update it through Option 5.
- **Rate limit reached:** Wait for the limit to reset before retrying.
- **No candidates found:** The current account network or activity signals may not produce suitable candidates. Try again later.

## Security and responsible use

- Keep your token in the local `.env` file and ensure it is ignored by Git.
- Review every preview before confirming follow/unfollow actions.
- Use the tool responsibly and respect GitHub's rules and other users.

## Contributing

Bug reports, suggestions, and pull requests are welcome. When reporting a problem, include the steps to reproduce it and remove any tokens or other private information first.
