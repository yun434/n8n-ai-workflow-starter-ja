# Security Policy

## Do Not Commit Secrets

Never commit real values for:

- API keys
- OAuth client secrets
- n8n credentials
- Slack bot tokens
- webhook URLs from production workflows
- private hostnames, internal IP addresses, or personal domains

Use `.env.example` only as a template. Copy it to `.env` locally and replace placeholder values there.

## Notes

- Replace `POSTGRES_PASSWORD=change-me` before running outside a throwaway local environment.
- Use HTTPS for public webhook endpoints.
- Review exported n8n workflow JSON before publishing. n8n exports may include IDs and metadata from your instance.
- Prefer n8n's credential store over hardcoded secrets in workflow nodes.

## Reporting Security Issues

Please open a private security advisory or contact the maintainer directly if you find a secret or unsafe default in this repository.
