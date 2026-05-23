# Security Policy

## Sensitive Information

Do not commit API keys, app secrets, access tokens, private keys, database
passwords, production endpoints, real user data, exported health records, logs,
or local tool configuration.

If a secret is committed by mistake:

1. Revoke or rotate the secret immediately.
2. Remove it from the repository.
3. Review Git history and GitHub exposure.
4. Treat the secret as compromised even if the repository was private.

## Reporting

This repository is currently a planning/documentation repository. If you find a
security or privacy issue in the documents, open a private disclosure channel
with the repository owner if available. Do not publish real user data or secrets
in an issue.

