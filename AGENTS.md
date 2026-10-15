# Repository Working Agreement

1. `src/`, `tests/`, `config/` and `specs/` are the maintained project.
2. Update the matching spec when public behavior changes.
3. Unit tests must not call real model providers.
4. Keep provider-specific behavior behind factory interfaces.
5. Never commit API keys, credential files, interview material, or nested project copies.