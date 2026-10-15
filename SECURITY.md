# Security Policy

## Secrets

Only `.env.example` and credential templates are tracked. Never commit provider keys, local credentials, private documents, or trace files containing user data.

## Reporting

Do not open a public issue containing a live key, private document, or personal data. Rotate exposed credentials first.

## Data

The `data/`, `logs/`, cache, and trace output paths are local runtime state and are ignored by Git.