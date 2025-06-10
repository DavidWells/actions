# Setup Claude Tokens

This GitHub Action helps you securely fetch and manage Claude API tokens for use in your GitHub Actions workflows.

## Features

- Securely fetches Claude API tokens from a protected endpoint
- Handles authentication using API keys
- Provides access token, refresh token, and expiration time
- Automatically masks sensitive token values in logs
- Validates response data to ensure token integrity

## Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `api-key` | Yes | API key for authentication with the token endpoint |
| `api-endpoint` | Yes | URL of the API endpoint that provides the tokens |

## Outputs

| Output | Description |
|--------|-------------|
| `access-token` | The Claude API access token |
| `refresh-token` | The refresh token for obtaining new access tokens |
| `expires-at` | The expiration timestamp for the access token |

## Usage

```yaml
name: Example Workflow

on:
  workflow_dispatch:

jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - name: Setup Claude Tokens
        id: claude-tokens
        uses: your-org/get-claude-tokens@v1
        with:
          api-key: ${{ secrets.API_KEY }}
          api-endpoint: 'https://your-token-endpoint.com'

      - name: Use Claude Tokens
        run: |
          echo "Access token expires at: ${{ steps.claude-tokens.outputs.expires-at }}"
          # Use the tokens in your workflow
          # Access token: ${{ steps.claude-tokens.outputs.access-token }}
          # Refresh token: ${{ steps.claude-tokens.outputs.refresh-token }}
```

## Security

- All token values are automatically masked in GitHub Actions logs
- The action validates the response data to ensure token integrity
- API keys should be stored as GitHub Secrets

## Error Handling

The action will fail if:
- The API endpoint returns an empty response
- The response cannot be parsed
- Required token fields are missing from the response

## License

[Add your license information here]
