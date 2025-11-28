# Public-Workflows

This repository runs GitHub Actions workflows from external repositories.

## Current Workflows

### Run Blogger Automation
- **File**: `.github/workflows/run-blogger-automation.yml`
- **Source**: [Blogger-Automation](https://github.com/GiridharSalana/Blogger-Automation)
- **Schedule**: Runs daily at 5:00 PM IST (11:30 UTC)
- **Manual Trigger**: Can be triggered manually with optional inputs

#### How it Works
1. Clones the Blogger-Automation repository
2. Sets up Python 3.12 and UV package manager
3. Runs the automation script with Telegram notifications
4. Commits changes back to the Blogger-Automation repository
5. Uploads logs to GitHub Gist and shares via Telegram

#### Required Secrets
You need to configure the following secrets in your repository settings:
- `BLOGGER_BOT_GITHUB_TOKEN` - GitHub token with repo access
- `TELEGRAM_BOT_TOKEN` - Telegram bot token for notifications
- `TELEGRAM_CHAT_ID` - Telegram chat ID for notifications
- `GOOGLE_API_KEY` - Google API key
- `COHERE_API_KEY` - Cohere API key
- `CEREBRAS_API_KEY` - Cerebras API key
- `BLOG_ID` - Blogger blog ID
- `LINKEDIN_ACCESS_TOKEN` - LinkedIn access token
- `IMGBB_CLIENT_ID` - ImgBB client ID

#### Manual Trigger Options
- **link**: Article URL for link mode
- **text**: Topic/prompt for text mode
- **config**: Configuration JSON (optional)

## Adding More Workflows

To add more external repository workflows:
1. Create a new workflow file in `.github/workflows/`
2. Use `actions/checkout@v4` with the `repository` and `path` parameters
3. Configure the necessary secrets and environment variables
4. Run the workflow steps in the cloned repository directory
