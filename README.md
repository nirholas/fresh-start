# Fresh Start

<!-- three.ws:badges -->
[![GitHub stars](https://img.shields.io/github/stars/nirholas/fresh-start?style=flat&logo=github)](https://github.com/nirholas/fresh-start/stargazers) [![Last commit](https://img.shields.io/github/last-commit/nirholas/fresh-start?style=flat)](https://github.com/nirholas/fresh-start/commits) [![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat)](https://github.com/nirholas/fresh-start/pulls) [![AI agent friendly](https://img.shields.io/badge/AI%20agents-AGENTS.md%20%2B%20llms.txt-6d5dfc?style=flat)](https://github.com/nirholas/fresh-start/blob/HEAD/AGENTS.md)
<!-- /three.ws:badges -->


This is the repository formerly known as `nirholas/claude-code`, the most widely forked mirror of the
Claude Code source leak of 31 March 2026. It is the same repository object, so
`github.com/nirholas/claude-code` still redirects here.

**It contains no Anthropic source code, and it will not.** The contents were removed after Anthropic's
DMCA notice. That notice has not been retracted.

## Read this instead

**[HISTORY.md](HISTORY.md)** is the full record: what leaked and how, what the DMCA did and did not
cover, and the correction that still needs making.

The short version of the correction: **Claude Code has never contained a cryptocurrency wallet or an
autonomous payment system.** The x402 payment code that circulated with copies of this leak was mine.
I wrote it, on top of the leaked tree, while building a project of my own. It was not Anthropic's and
it was not in the leak. Several popular writeups still report it as an undocumented Anthropic feature.
[HISTORY.md](HISTORY.md) shows three independent ways to verify that it is not, and gives a complete
accounting of every file I changed.

If you are auditing a copy of the leak you already hold, `grep -r x402 src/` is the test.

## Do not run copies of the leak

The leaked tree imports internal packages that do not exist on the public npm registry, and squatters
publish malicious packages under exactly those names. Installing dependencies from any copy of this
codebase can execute arbitrary code on your machine. There were also genuinely trojanized "Claude Code
leak" repositories in circulation in April 2026, documented by Zscaler ThreatLabz, distributing Vidar
and GhostSocks through a Windows executable. Use the official Claude Code CLI from Anthropic.


## License

All rights reserved. See [LICENSE](LICENSE).

<!-- three.ws:growth -->
## Support the project

If fresh-start saves you time, **[star it on GitHub](https://github.com/nirholas/fresh-start)**. Stars are how other developers and AI agents find the repositories worth trusting, and they cost you one click.

Know someone who would use it? [Post on X](https://twitter.com/intent/tweet?text=fresh-start%3A%20The%20original%20nirholas%2Fclaude-code%20before%20DMCA%20and%20take%20down&url=https%3A%2F%2Fgithub.com%2Fnirholas%2Ffresh-start) · [Share on Bluesky](https://bsky.app/intent/compose?text=fresh-start%3A%20The%20original%20nirholas%2Fclaude-code%20before%20DMCA%20and%20take%20down%20https%3A%2F%2Fgithub.com%2Fnirholas%2Ffresh-start) · [Share on LinkedIn](https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fgithub.com%2Fnirholas%2Ffresh-start) · [Submit to Hacker News](https://news.ycombinator.com/submitlink?u=https%3A%2F%2Fgithub.com%2Fnirholas%2Ffresh-start&t=fresh-start%3A%20The%20original%20nirholas%2Fclaude-code%20before%20DMCA%20and%20take%20down) · [Share on Reddit](https://www.reddit.com/submit?url=https%3A%2F%2Fgithub.com%2Fnirholas%2Ffresh-start&title=fresh-start%3A%20The%20original%20nirholas%2Fclaude-code%20before%20DMCA%20and%20take%20down)

## Built for AI agents too

Coding agents and LLM tooling can read this repo directly: [AGENTS.md](./AGENTS.md), [llms.txt](./llms.txt), [llms-full.txt](./llms-full.txt). Point an agent at `https://github.com/nirholas/fresh-start` and it has the context it needs.

## More from the same author

- [All repositories by nirholas](https://github.com/nirholas/nirholas#readme): the full catalog, grouped by topic
- [three.ws](https://three.ws): the platform for 3D AI agents with Solana wallets, a skill marketplace and x402 payments
- Questions or ideas: [open an issue](https://github.com/nirholas/fresh-start/issues) or [start a discussion](https://github.com/nirholas/fresh-start/discussions)

## Contributors

[![Contributors](https://contrib.rocks/image?repo=nirholas/fresh-start)](https://github.com/nirholas/fresh-start/graphs/contributors)

## Star history

[![Star History Chart](https://api.star-history.com/svg?repos=nirholas/fresh-start&type=Date)](https://www.star-history.com/#nirholas/fresh-start&Date)

<!-- /three.ws:growth -->
