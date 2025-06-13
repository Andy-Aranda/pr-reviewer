# 🤖 PR Reviewer with Claude + Notion + GitHub

This project automates the analysis of Pull Requests (PRs) using a LLM (Claude) connected via the [MCP (Model Context Protocol)](https://www.datacamp.com/es/tutorial/mcp-model-context-protocol). 

The system receives a PR link, generates a technical summary, and stores it in a Notion page as documentation.

---

## 🧩 Architecture

```plaintext
GitHub PR → MCP Server (Python) → Claude Desktop → Analysis → Notion
```

---

## ✨ Features

- Automatically fetches PR changes via GitHub API.
- Uses Claude Desktop to generate a semantic analysis of the code.
- Creates a Notion entry with the generated summary.
- Modular and extensible: you can add more tools to the MCP server.

---

## 🚀 How It Works

1. **Claude Desktop** detects the MCP server when it runs locally.
2. The user sends a PR link to Claude.
3. Claude calls the MCP server and uses:
   - `fetch_pr` → fetches PR metadata and diffs from GitHub.
   - `create_notion_page` → saves the analysis in a new Notion page.
4. The whole process is triggered from Claude's interface with no manual steps.

---

## 🔧 Requirements

- Python 3.10+
- [Claude Desktop](https://claude.ai/)
- Account / API key from:
  - [GitHub](https://github.com/settings/tokens)
  - [Notion](https://www.notion.so/my-integrations)

---

## ⚙️ Setup

1. Install `uv` (lightweight Python environment manager):
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. Initialize project:
   ```bash
   uv init pr_reviewer
   cd pr_reviewer
   uv venv
   source .venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   uv add "mcp[cli]" requests python-dotenv notion-client
   ```

4. Create `.env` file:
   ```env
   GITHUB_TOKEN=ghp_***************
   NOTION_API_KEY=secret_**************
   NOTION_PAGE_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
   ```

5. Configure Claude Desktop with the `claude_desktop_config.json` file, e.g.:
   ```json
   {
     "mcpServers": {
       "pr-reviewer": {
         "command": "/path/to/python",
         "args": ["/path/to/pr_anayzer.py"],
         "cwd": "/path/to/project"
       }
     }
   }
   ```

---

## 🧪 Usage

1. Run the MCP server:
   ```bash
   python pr_anayzer.py
   ```

2. Open Claude Desktop and pass a PR link:
   ```
   https://github.com/your_username/your_repo/pull/1
   ```

3. Claude will analyze the PR and ask whether to save the result in Notion.

---

## 📌 Possible Improvements

- Full automation using `n8n` or GitHub Actions.
- PR validation with custom rules.
- Integration with other tools like Slack or ClickUp.
