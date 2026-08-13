# What actually happened here

This is the repository formerly known as `nirholas/claude-code`. It is the same repository object:
`github.com/nirholas/claude-code` still redirects here. It contains no Anthropic source code and it
will not.

The story is still circulating, parts of it are wrong, and the parts that are right are worth stating
plainly rather than leaving to inference. So here is the record, with the artifacts to check it.

## The leak

On 31 March 2026, Anthropic accidentally published the TypeScript source of Claude Code. Version
2.1.88 of the `@anthropic-ai/claude-code` npm package shipped with a 59.8 MB source map pointing at a
public bucket that held the unobfuscated source: roughly 512,000 lines across about 2,200 files.
Chaofan Shou found it and posted the link. Anthropic later described it as "a release packaging issue
caused by human error, not a security breach," and said the engineer responsible was not fired.

I mirrored it here about 40 minutes later and started building on top of it. The repository grew to
several thousand stars and a large fork network before Anthropic filed a DMCA notice against it.
GitHub processed that notice against the whole network, 8,100 repositories. Anthropic retracted the
network-wide portion the next day and everything else was restored. The notice against this repository
was not retracted. I removed the contents, GitHub let me keep the repository, and this is what remains.

## The correction that matters to everyone else

**Claude Code does not contain, and has never contained, a cryptocurrency wallet or an autonomous
payment system. The x402 payment code that circulated with copies of the leak was mine. I wrote it. It
was not Anthropic's, it was not a hidden feature, and it was not in the leak.**

Several widely-read writeups state that the leak revealed a built-in USDC wallet at
`src/commands/x402/`, and list `/x402 setup`, `/x402 enable` and `/x402 set-limit` as undocumented
Anthropic features. Search engines now repeat it as fact. It is wrong, and it originates with my
working copy of the tree.

Three independent ways to confirm Anthropic never shipped it:

1. **The archived original.** The Internet Archive holds four captures of the original `src.zip` from
   31 March 2026, all with identical content digests, the earliest predating this mirror by about 40
   minutes. It contains 2,203 entries. Filenames matching `x402|wallet|payment|usdc|signer`: zero.
   Full-text search for the string `x402`: zero hits.
2. **The shipped packages.** Versions 2.1.87 and 2.1.89, which bracket the pulled 2.1.88, contain zero
   occurrences of `x402`. The only `usdc` strings in either are the `.usdc` file extension inside the
   bundled ripgrep binary, which is a Pixar 3D format.
3. **The commit history.** In this repository the x402 files appear for the first time in a commit
   timestamped `2026-03-31T10:26:23Z`, roughly two minutes after the bulk import of the leaked files
   finished at `10:24:35Z`. That history is preserved in public forks that survived the takedown.

One false positive probably helped the story along: grepping the leak for `USDC` returns 11 hits, and
all of them are the identifier `calculateUSDCost` in `src/utils/modelCost.ts` and its callers. That is
"USD Cost", the token-pricing function, not the stablecoin.

## Everything I changed, completely

Some copies of the leak have been described as possibly carrying other unidentified modifications.
Here is the full accounting, so the claim can be checked instead of repeated.

The x402 feature was **8 new files**:

```
src/services/x402/client.ts          src/commands/x402/index.ts
src/services/x402/config.ts          src/commands/x402/x402.ts
src/services/x402/index.ts
src/services/x402/paymentFetch.ts
src/services/x402/tracker.ts
src/services/x402/types.ts
```

It touched **4 of Anthropic's source files**, all of them to call into those new modules, plus two of
the docs files I had generated:

| File | Change | What it does |
|---|---|---|
| `src/services/api/client.ts` | +13/-1 | wraps `fetch` with the x402 handler, behind an `isX402Enabled()` check |
| `src/cost-tracker.ts` | +13/-1 | appends a payment total to the `Total cost:` display |
| `src/tools/WebFetchTool/utils.ts` | +43 | catches an HTTP 402 response and retries once with a payment header |
| `src/commands.ts` | small | registers the `/x402` command |
| `docs/subsystems.md`, `docs/commands.md` | small | my own generated docs, not Anthropic's |

Beyond that, and beyond my own additions (the `src/server/web/*` terminal, `src/shims/*` build shims,
type declarations, the `mcp-server/` explorer, Docker and docs), **the only other edits to Anthropic's
files were 48 single blank lines appended by a formatter pass.** No logic, no network destinations, no
telemetry, and no credential handling anywhere in the tree was modified.

Scope limit, stated plainly: this accounting is complete through `2026-03-31T12:43Z`, which is where
the public fork history I can verify against ends. If you hold a copy from later, diff it against the
archived original and publish what you find.

## Why it looked planted

A careful forensic writeup of this mirror listed seven properties of the x402 code as evidence it had
been covertly injected: no `tengu_` GrowthBook feature flag, when all 58 other features have one;
defensive `try { require(...) } catch {}` at every integration point instead of static imports; absent
from the 17 `prompts/` build-out documents; no tests; no telemetry, in a codebase that logs roughly 651
event types; no new npm dependencies, rolling its own secp256k1 and EIP-712 signing on native Node
crypto; and self-contained enough to remove without a trace.

Every one of those observations is accurate. Here is the other explanation for them, which is the
actual one. I could not register a GrowthBook flag I have no access to. I used defensive requires
because a tree reconstructed from a source map does not compile cleanly and I did not want my feature
to be the thing that broke the build. I did not add my feature to the 17 documents describing how to
rebuild Anthropic's codebase, because it is not part of Anthropic's codebase. I did not wire it into
Anthropic's telemetry exporters, because sending events into their pipeline would have been worse in
every direction. And I kept it dependency-free and self-contained because that is how you build on a
base you may need to rebase or throw away.

The signature of "a feature added quickly to a fork by someone outside the company" and the signature
of "a covert injection" overlap almost completely. Flagging that is fair analysis. What the code
cannot show you is intent, so here it is: I was building a project, not hiding a payload. The clearest
evidence is contemporaneous. Eight hours after committing it, when someone accused me in the reply
thread of secretly adding payment code, I answered in that same thread that it was x402 and that it
was not secret. I never claimed it was Anthropic's.

Where I was wrong is narrower, and I will name it. I published in-progress work on top of a freshly
leaked tree, in a repository whose name read as a faithful mirror, at the exact moment thousands of
people were cloning it as a reference copy. Whatever I intended, that is how the confusion got
manufactured, and that part is on me.

## This repository was never the malware campaign

A separate thing happened in the same news cycle and the two get conflated. Between 1 and 3 April
2026, threat actors published fake "Claude Code leak" repositories containing a `.7z` archive with a
Rust dropper, `ClaudeCode_x64.exe`, that installed Vidar v18.7 and GhostSocks. It was covered by The
Register, Help Net Security, TechRadar and others.

Zscaler ThreatLabz published the indicators of compromise. They name three things: the repositories
`leaked-claude-code/leaked-claude-code` and `my3jie/leaked-claude-code`, and the publisher account
`idbzoomh1`. This account is named in none of it. There were no binaries, no releases and no
installers here, only TypeScript in a git tree.


## Verify all of it yourself

```bash
# The archived original: no payment code of any kind
curl -sL "https://web.archive.org/web/20260331090815id_/https://pub-aea8527898604c1bbb12468b1581d95e.r2.dev/src.zip" -o orig.zip
unzip -Z1 orig.zip | grep -icE "x402|wallet|payment|signer"     # -> 0

# Anthropic's shipped bundles, either side of the pulled release
npm pack @anthropic-ai/claude-code@2.1.89
tar xzf claude-code-2.1.89.tgz -O | grep -c x402                # -> 0

# The DMCA notice and the next-day partial retraction, in GitHub's own archive
# github.com/github/dmca -> 2026/03/2026-03-31-anthropic.md
#                        -> 2026/04/2026-04-01-anthropic-retraction.md
```

If you are checking a copy of the leak you already hold, `grep -r x402 src/` is the only durable test.
Directory counts have decayed: clean forks that are still maintained have since added directories of
their own, so counting `src/services` or `src/commands` now produces false positives.

## Do not run copies of the leak

Worth repeating regardless of where your copy came from. The leaked tree imports internal packages
that do not exist on the public npm registry, and squatters publish malicious packages under exactly
those names, so installing dependencies from any copy of this codebase can execute arbitrary code on
your machine. Use the official Claude Code CLI from Anthropic.

## Status

The DMCA notice against this repository has not been retracted. This repository holds no Anthropic
code. If that changes, this file will say so.
