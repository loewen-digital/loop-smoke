# loop-smoke

Smoke test for the agent loop: runs `anthropics/claude-code-action` with the org secret
`CLAUDE_CODE_OAUTH_TOKEN`, `show_full_output: true`, and a one-word prompt. Use it to verify a
token right after rotating the secret:

```bash
gh workflow run smoke.yml --repo loewen-digital/loop-smoke
```

A green run prints `OK`; a bad token prints `401 OAuth access token is invalid`.

This repository is **public on purpose**: the organisation is on the GitHub Free plan, and org
secrets only reach public repositories there. Private repositories need the secret set per repo
(`gh secret set CLAUDE_CODE_OAUTH_TOKEN -R owner/repo`) or a Team plan.

## Setting the secret without a trailing newline

Pasting into the interactive `gh secret set` prompt appends the line break to the value, and the
API then answers `401 OAuth access token is invalid`. The first step of the smoke workflow reports
`length` vs `trimmed_length` so this is caught immediately. Set the secret from the clipboard:

```bash
gh secret set CLAUDE_CODE_OAUTH_TOKEN --org loewen-digital --visibility all --body "$(pbpaste | tr -d '[:space:]')"
```
