# Public Workflows

Centralized GitHub Actions workflows for triggering automation bots via dispatch.

## Automation Bots

| Bot | Description | Blog/Channel |
|-----|-------------|--------------|
| **Blogger Automation** | Tech blog automation | [giridharsalana.blogspot.com](https://giridharsalana.blogspot.com) |
| **YouTube Automation** | News video generation | [GeoPulse News](https://www.youtube.com/@GeoPulseNews) |
| **Semiconzone Bot** | VLSI/Semiconductor blog | [semiconzone.blogspot.com](https://semiconzone.blogspot.com) |

## Environment Variables

### Common Variables (All Bots)

| Variable | Description | Default | Values |
|----------|-------------|---------|--------|
| `USER_APPROVAL` | Enable Telegram approval before publishing | `false` | `true`, `false` |
| `REJECTED_STATE` | What to do with rejected content | `delete` | `delete`, `keep` |
| `LLM_PROVIDER` | LLM provider for content generation | `cohere` | `google`, `cohere`, `cerebras` |
| `TELEGRAM_BOT_TOKEN` | Telegram bot token (secret) | - | - |
| `TELEGRAM_CHAT_ID` | Telegram chat ID (secret) | - | - |

### Blogger Automation & Semiconzone Bot

| Variable | Description | Default |
|----------|-------------|---------|
| `MAX_BLOGS_POSTS` | Maximum blogs to generate per run | `3` |
| `BLOG_UPLOAD` | Enable uploading to Blogger | `true` |
| `BLOG_GENERATE` | Enable content generation | `true` |
| `IMAGE_UPLOAD` | Enable image upload to ImgBB | `true` |
| `SCHEDULE_INTERVAL` | Minutes between scheduled posts | `0` (immediate) |
| `LINKEDIN_UPLOAD` | Enable LinkedIn cross-posting | `false` |

### YouTube Automation

| Variable | Description | Default |
|----------|-------------|---------|
| `PEXELS_API_KEY` | Pexels API key for stock videos | - |
| `PIXABAY_API_KEY` | Pixabay API key for stock videos | - |
| `NEWSAPI_KEY` | NewsAPI key for news fetching | - |

## REJECTED_STATE Behavior

Controls what happens to content that is rejected during approval:

| Value | Behavior |
|-------|----------|
| `delete` | **Default.** Rejected drafts are permanently deleted. |
| `keep` | Rejected drafts are kept as private/draft for later review. |

### Examples

```yaml
# Delete rejected content (default)
REJECTED_STATE: delete

# Keep rejected content as drafts
REJECTED_STATE: keep
```

## Workflow Dispatch

All bots support the following input modes:

| Mode | Description | Input |
|------|-------------|-------|
| **Auto** | Fetches content from RSS/News APIs | (no input) |
| **Link** | Generates content from a specific URL | `--link "https://..."` |
| **Text** | Generates content from a topic prompt | `--text "Topic..."` |

## Secrets Required

| Secret | Used By | Description |
|--------|---------|-------------|
| `GOOGLE_API_KEY` | All | Google/Gemini API key |
| `COHERE_API_KEY` | All | Cohere API key |
| `TELEGRAM_BOT_TOKEN` | All | Telegram bot token |
| `TELEGRAM_CHAT_ID` | All | Telegram chat ID |
| `BLOG_ID` | Blogger, Semiconzone | Blogger blog ID |
| `IMGBB_CLIENT_ID` | Blogger, Semiconzone | ImgBB API key |
| `BLOGGER_BOT_GITHUB_TOKEN` | Blogger | GitHub PAT for dispatch |
| `YOUTUBE_BOT_GITHUB_TOKEN` | YouTube | GitHub PAT for dispatch |
| `SEMICONZONE_BOT_GITHUB_TOKEN` | Semiconzone | GitHub PAT for dispatch |
