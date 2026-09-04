# loop-smoke

Private smoke test for the agent loop: runs `anthropics/claude-code-action` with the org secret
`CLAUDE_CODE_OAUTH_TOKEN` and shows the full output. Use it to verify a new token before rotating
the secret. Trigger via the Actions tab or `gh workflow run smoke.yml`.
