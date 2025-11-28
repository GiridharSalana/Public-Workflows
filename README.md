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

## Secrets Management

### Syncing Secrets from Blogger-Automation

Since GitHub doesn't allow reading secrets from other repositories via API, I've created a sync workflow that runs in the **Blogger-Automation** repository and pushes its secrets to **Public_Workflows**.

#### How to Sync Secrets:

1. Go to the [Blogger-Automation repository](https://github.com/GiridharSalana/Blogger-Automation)
2. Navigate to **Actions** tab
3. Select the **"Sync Secrets to Public_Workflows"** workflow
4. Click **"Run workflow"** button
5. The workflow will automatically copy all secrets from Blogger-Automation to Public_Workflows

#### Required Secrets

The following secrets will be synced:
- `GOOGLE_API_KEY` - Google API key
- `COHERE_API_KEY` - Cohere API key
- `CEREBRAS_API_KEY` - Cerebras API key
- `BLOG_ID` - Blogger blog ID
- `LINKEDIN_ACCESS_TOKEN` - LinkedIn access token
- `IMGBB_CLIENT_ID` - ImgBB client ID
- `TELEGRAM_BOT_TOKEN` - Telegram bot token for notifications
- `TELEGRAM_CHAT_ID` - Telegram chat ID for notifications
- `BLOGGER_BOT_GITHUB_TOKEN` - GitHub token with repo access

**Note**: The `BLOGGER_BOT_GITHUB_TOKEN` must have the `repo` and `secrets` scope to write secrets to this repository.

### Manual Trigger Options

When running the "Run Blogger Automation" workflow manually, you can provide:
- **link**: Article URL for link mode
- **text**: Topic/prompt for text mode
- **config**: Configuration JSON (optional)

## Adding More Workflows

To add more external repository workflows:
1. Create a new workflow file in `.github/workflows/`
2. Use `actions/checkout@v4` with the `repository` and `path` parameters
3. Configure the necessary secrets and environment variables
4. Run the workflow steps in the cloned repository directory

## Repository Variables

Some configuration options can be set as repository variables instead of secrets:
- `MAX_BLOGS_POSTS` - Maximum number of blog posts to generate
- `BLOG_UPLOAD` - Whether to upload to blog (true/false)
- `USER_APPROVAL` - Whether to require user approval (true/false)
- `BLOG_GENERATE` - Whether to generate blog content (true/false)
- `IMAGE_UPLOAD` - Whether to upload images (true/false)
- `SCHEDULE_INTERVAL` - Schedule interval for automation
- `LINKEDIN_UPLOAD` - Whether to upload to LinkedIn (true/false)
- `LLM_PROVIDER` - LLM provider to use (google/cohere/cerebras)
