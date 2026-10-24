# GitHub Follow-Back Manager

A Python command-line tool for managing your GitHub follow network. Identify accounts that do not follow you back, discover potentially relevant developers, review bulk-unfollow candidates, and maintain an ignore list.

## Features

- **Find non-followers:** Compare your followers and following lists.
- **Discover potential follows:** Evaluate candidate accounts using public profile and activity signals.
- **Bulk unfollow:** Review non-followers or high-follower-ratio accounts before taking action.
- **Ignore list:** Exclude selected usernames from follow/unfollow workflows.
- **Token setup:** Configure a GitHub Personal Access Token locally.
- **Rate-limit information:** Check remaining API calls when available.

> **Note:** Auto-follow recommendations are heuristic and cannot guarantee that someone will follow you back. Review every preview before confirming follow or unfollow actions.

## Requirements

- Python 3.8 or newer
- A GitHub account
- A GitHub Personal Access Token for follow/unfollow actions

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/Sahil002620Q/Who-is-not-following-back-git.git
cd Who-is-not-following-back-git
```

### 2. Create and activate a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt:

```bat
venv\Scripts\activate.bat
```

**Linux or macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the application

```bash
python script.py
```

On the first run, select **Option 5 — Setup Account & Token** and follow the prompts.

## GitHub token setup

1. Open [GitHub token settings](https://github.com/settings/tokens/new).
2. Create a token with the permission required to follow and unfollow users. For a classic token, select the `user:follow` scope.
3. Generate the token and copy it.
4. Run the application and select **Option 5 — Setup Account & Token**.
5. Paste the token when prompted.

The application stores the token in a local `.env` file. Never share your token or commit `.env` to the repository. If a token is exposed, revoke it in GitHub settings. Without a token, some read-only requests may still work, but follow/unfollow actions require authentication.

## Menu options

```text
1. View Non-Followers
2. Auto-Follow Smart Users
3. Bulk Unfollow
4. Manage Ignore List
5. Setup Account & Token
6. Exit
```

- **View Non-Followers:** Lists accounts you follow that do not follow you back, excluding usernames on your ignore list.
- **Auto-Follow Smart Users:** Evaluates candidate accounts using public profile and recent-activity signals, then displays a preview for confirmation.
- **Bulk Unfollow:** Lets you review and unfollow non-followers or accounts whose follower count exceeds their following count.
- **Manage Ignore List:** Add or remove usernames that should be excluded from follow/unfollow workflows.
- **Setup Account & Token:** Change your configured GitHub username or update your token.

## Project structure

```text
.
├── script.py
├── api_handler.py
├── utils.py
├── requirements.txt
├── config.json
├── .env
└── .gitignore
```

The `.env` file stores your local token. The `config.json` file stores local configuration, including the username and ignore list. These files may be created or updated when you use the application.

## Troubleshooting

- **Python command not found:** Install Python 3.8+ and ensure it is available on your PATH. On some systems, use `python3`.
- **Missing module:** Activate your virtual environment and run `pip install -r requirements.txt`.
- **Token rejected:** Create a token with the required follow permission and update it through Option 5.
- **Rate limit reached:** Wait for GitHub's API limit to reset.
- **No candidates found:** The selection criteria may not find suitable accounts for your network at that time.

## Security

- Keep your token in the local `.env` file.
- Ensure `.env` is included in `.gitignore` before committing changes.
- Review the candidate list before confirming follow/unfollow operations.
- Use the tool responsibly and follow GitHub's terms and policies.

## Contributing

Bug reports, suggestions, and pull requests are welcome. Do not include access tokens or other secrets in issues.

## License

This project is licensed under the MIT License if the repository's MIT license file is present.
