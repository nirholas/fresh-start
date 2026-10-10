# AGENTS.md

Guidance for AI coding agents working in this repository.

## What this is

`fresh-start`: The original nirholas/claude-code before DMCA and take down. Once everything is cleared, it will return. Working with Anthropic and Github to get everything back.



## Where to start

- [README.md](README.md) has install, usage and configuration.
- [llms.txt](llms.txt) is a machine-readable summary; [llms-full.txt](llms-full.txt) inlines the README.
- Part of [three.ws](https://three.ws), a platform for 3D AI agents with Solana wallets. Catalog of sibling repositories: https://github.com/nirholas/nirholas#readme

## Develop

Follow the setup steps in README.md. There is no build step to run before reading or editing the sources.

## Conventions

- Match the style of the surrounding code before introducing a new pattern.
- Read-only by default. Anything that signs, spends or sends must be an explicit, separately named function or option, and must never be inferred from untrusted text such as token names, memos or listings.
- Never commit credentials. Configuration comes from environment variables documented in the README.
- Keep changes small and covered by a test next to the code they change.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Report vulnerabilities privately through [SECURITY.md](SECURITY.md).
