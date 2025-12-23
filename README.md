# Public-Workflows

This repository runs GitHub Actions workflows from external repositories.

## Current Workflows

### 📝 Run Blogger Automation
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

---

### 🎬 Run YouTube Automation
- **File**: `.github/workflows/run-youtube-automation.yml`
- **Source**: [Youtube-Automation](https://github.com/GiridharSalana/Youtube-Automation)
- **Schedule**: Runs daily at 11:30 AM IST (6:00 UTC)
- **Manual Trigger**: Can be triggered manually with customizable inputs

#### How it Works
1. Clones the Youtube-Automation repository
2. Sets up Python 3.12, UV package manager, and FFmpeg
3. Configures YouTube OAuth credentials from secrets
4. Generates news video with AI-powered script and TTS
5. Uploads video to YouTube (with optional Shorts)
6. Commits database updates back to the repository
7. Uploads logs to GitHub Gist and shares via Telegram

#### Manual Trigger Options
| Input | Description | Default |
|-------|-------------|---------|
| `news_duration` | Video duration in seconds | 120 |
| `news_style` | Script style (professional/casual/dramatic) | professional |
| `news_categories` | News categories (space-separated) | world technology |
| `upload_youtube` | Upload to YouTube | true |
| `generate_shorts` | Also generate YouTube Shorts | true |
| `youtube_privacy` | Video privacy (public/unlisted/private) | public |

#### Required Secrets for YouTube Automation
| Secret | Description |
|--------|-------------|
| `GOOGLE_API_KEY` | Google/Gemini API key for AI and TTS |
| `YOUTUBE_CREDENTIALS_JSON` | YouTube OAuth credentials (base64 encoded) |
| `YOUTUBE_TOKEN_PICKLE` | YouTube OAuth token (base64 encoded) |
| `YOUTUBE_BOT_GITHUB_TOKEN` | GitHub token with repo access |
| `PEXELS_API_KEY` | Pexels API key for media sourcing |
| `PIXABAY_API_KEY` | Pixabay API key for media sourcing |
| `TELEGRAM_BOT_TOKEN` | Telegram bot token (optional) |
| `TELEGRAM_CHAT_ID` | Telegram chat ID (optional) |

#### Setting Up YouTube OAuth Credentials
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create OAuth 2.0 credentials for Desktop App
3. Download the credentials JSON file
4. Base64 encode it: `base64 -w 0 youtube_credentials.json`
5. Add as `YOUTUBE_CREDENTIALS_JSON` secret

For the token pickle (after first authentication):
```bash
base64 -w 0 creds/youtube_token.pickle
```
Add as `YOUTUBE_TOKEN_PICKLE` secret. The workflow auto-updates this when refreshed.

## Secrets Management

### Syncing Secrets from Blogger-Automation

Since GitHub doesn't allow reading secrets from other repositories via API, I've created a sync workflow that runs in the **Blogger-Automation** repository and pushes its secrets to **Public_Workflows**.

#### How to Sync Blogger Secrets:

1. Go to the [Blogger-Automation repository](https://github.com/GiridharSalana/Blogger-Automation)
2. Navigate to **Actions** tab
3. Select the **"Sync Secrets to Public_Workflows"** workflow
4. Click **"Run workflow"** button
5. The workflow will automatically copy all secrets from Blogger-Automation to Public_Workflows

#### Blogger-Automation Secrets

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

---

### Syncing Secrets from Youtube-Automation

#### How to Sync YouTube Secrets:

1. Go to the [Youtube-Automation repository](https://github.com/GiridharSalana/Youtube-Automation)
2. Navigate to **Actions** tab
3. Select the **"Sync Secrets to Public_Workflows"** workflow
4. Click **"Run workflow"** button
5. The workflow will automatically copy all secrets from Youtube-Automation to Public_Workflows

#### Youtube-Automation Secrets

The following secrets will be synced:
- `GOOGLE_API_KEY` - Google/Gemini API key for AI and TTS
- `COHERE_API_KEY` - Cohere API key (optional)
- `CEREBRAS_API_KEY` - Cerebras API key (optional)
- `NEWSAPI_KEY` - NewsAPI key for news fetching
- `PEXELS_API_KEY` - Pexels API key for media sourcing
- `PIXABAY_API_KEY` - Pixabay API key for media sourcing
- `YOUTUBE_CREDENTIALS_JSON` - YouTube OAuth credentials (base64 encoded)
- `YOUTUBE_TOKEN_PICKLE` - YouTube OAuth token (base64 encoded)
- `TELEGRAM_BOT_TOKEN` - Telegram bot token for notifications
- `TELEGRAM_CHAT_ID` - Telegram chat ID for notifications
- `YOUTUBE_BOT_GITHUB_TOKEN` - GitHub token with repo access

**Note**: The `YOUTUBE_BOT_GITHUB_TOKEN` must have the `repo` and `secrets` scope to write secrets to this repository.

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
