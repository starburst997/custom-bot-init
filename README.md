# Custom Bot Init

A GitHub Action to initialize and configure a GitHub App bot for use in workflows.

## Usage

```yaml
- uses: starburst997/custom-bot-init@v1
  id: bot
  with:
    app-id: ${{ secrets.BOT_ID }}
    private-key: ${{ secrets.BOT_KEY }}

- run: |
    echo "Bot configured as: ${{ steps.bot.outputs.name }}"
    echo "Bot email: ${{ steps.bot.outputs.email }}"
    echo "Bot user ID: ${{ steps.bot.outputs.user-id }}"
    echo "Bot slug: ${{ steps.bot.outputs.slug }}"
```

## Inputs

| Name          | Description            | Required |
| ------------- | ---------------------- | -------- |
| `app-id`      | GitHub App ID          | No       |
| `private-key` | GitHub App private key | No       |

## Outputs

| Name      | Description                |
| --------- | -------------------------- |
| `token`   | Generated GitHub App token |
| `name`    | Configured git user name   |
| `email`   | Configured git user email  |
| `user-id` | Bot user ID                |
| `slug`    | GitHub App slug            |

## What it does

When `app-id` and `private-key` are provided:

1. Generates a GitHub App token using the provided credentials
2. Fetches the app's slug name from GitHub API
3. Configures git with the bot's identity
4. Returns the token and git configuration for use in subsequent steps

When inputs are empty or not provided, both steps are skipped.
