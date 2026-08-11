# Fresh Start

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

## What came out of it

The x402 work continues as [`nirholas/agenti`](https://github.com/nirholas/agenti), a wallet for AI
agents: pay x402 APIs, receive USDC, on EVM and Solana, with MCP client support. Same idea, none of
anyone else's code in it.

## License

All rights reserved. See [LICENSE](LICENSE).
