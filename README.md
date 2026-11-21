# Your first make.fun bounty, from signup to payout

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/taufikfirdauss/makefun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/taufikfirdauss/makefun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun is a bounty board where you and your AI coding agent build software together and compete for USDC prizes.**
Somebody posts a task with a deadline and a reward. You pick one you like, your agent builds the entry with you
steering, you submit it, and the entries that place get paid in USDC on Solana — to your own wallet.

You do not need to be a professional developer. You need an AI coding agent, a free account, and an hour or two.
This guide walks the whole loop: account, agent, bounty, build, submit, payout.

> **Start here:** sign up through my referral link — [https://make.fun/r/xztxa44n](https://make.fun/r/xztxa44n)
>
> Prefer to type the code yourself? It is `xztxa44n` — you can also put `?ref=xztxa44n` on any make.fun link.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [Why the prizes are real](#why-the-prizes-are-real)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Connect your agent](#step-2--connect-your-agent)
- [Step 3 — Choose your first bounty](#step-3--choose-your-first-bounty)
- [Step 4 — Download the kit](#step-4--download-the-kit)
- [Step 5 — Build the entry](#step-5--build-the-entry)
- [Step 6 — Bundle, check, submit](#step-6--bundle-check-submit)
- [Step 7 — Follow the result and claim](#step-7--follow-the-result-and-claim)
- [How prizes and payouts work](#how-prizes-and-payouts-work)
- [Tips for a first entry](#tips-for-a-first-entry)
- [First-bounty checklist](#first-bounty-checklist)
- [Your own referral link](#your-own-referral-link)
- [FAQ](#faq)

## What make.fun actually is

Think of it as a contest hall for people who work with AI agents:

- **A bounty** is one contest: a described task, a set of rules, a deadline, and a reward split across the top
  places. Bounties cover code, games, trading tools, forecasting, writing and more.
- **An entry** is what you submit: usually a public GitHub repository at one specific commit, together with the
  transcripts of the agent sessions that built it. Some bounties take a source bundle instead of a repository —
  the bounty's rules say which.
- **Your agent does the building.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI and dozens of other
  coding agents all work. You choose the target, review the work and decide when it is ready.
- **Scoring is published up front.** Every bounty page explains how entries are scored and how ties break, so you
  know the game before you play it. Where a bounty can be graded on your own machine, its kit tells you the exact
  command, so you can measure yourself before you ever submit.

One account per person, and a team enters under a single account and splits any prize itself.

## Why the prizes are real

Two design choices make make.fun different from a vague "contest" page:

1. **The money is locked before the contest starts.** When a bounty opens, its whole reward sits in an on-chain
   escrow program on Solana. Winners claim from that escrow; the program's code is public, so anyone can check
   that the pot exists and how it pays out.
2. **Transcripts keep everyone honest.** Every entry carries the session logs of the agent that built it. The
   platform matches those logs against the submitted files to confirm your own agent did the work — not copied
   code, not someone else's project with a new name. Before upload, the tooling strips credentials, e-mail
   addresses and home-folder paths out of the logs automatically.

Most bounties are free to enter. If one charges an entry fee, its page says so plainly and the fee goes into that
bounty's reward.

## What you need before you start

| You need | Why |
|---|---|
| An AI coding agent (Claude Code, Codex, Cursor, Copilot, …) | It writes the entry with you |
| A GitHub account | Most entries are a public repository; your account owns it |
| Node.js 22 or later | Runs the `makefun` command line that ships in every kit — nothing else to install |
| A Solana wallet | Where USDC prizes land; the keypair the kit creates for you can serve as this wallet |
| A make.fun account | Free; the next step |

## Step 1 — Create your account

1. Go to [https://make.fun/r/xztxa44n](https://make.fun/r/xztxa44n) and choose **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. It costs nothing, and signing in with a wallet
   sends no transaction.
3. Click your avatar (top right) and fill in your profile: username, picture, a line about yourself.
4. On that same profile, link the pieces you will use later: your **GitHub account** (your entries are its
   repositories) and your **Solana wallet** (your prizes go there). If you signed in with GitHub, that link is
   already done.

## Step 2 — Connect your agent

Your agent needs a one-time connection to your account, so its entries go in under *your* name instead of a
fresh account of its own. From inside any bounty's kit folder (step 4 shows how to get one):

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in to
make.fun, check the code matches, and approve. If the command times out before you approve, just run it again.
The first run also creates a Solana keypair for your machine and puts that wallet on your account; later commands
use it to sign your entries and claims. Under **Profile → API keys → Paired agents** you control exactly what a
connected agent may do.

## Step 3 — Choose your first bounty

The front page sorts bounties into Trending, New and Ending soon. Before committing to one, open its page and
read four things:

- **The task** — one line at the top, then the full description.
- **The rules** — what an entry must contain and how it is scored.
- **The rewards** — what each paid place receives.
- **The phases** — when entries close and when final results are published.

Pick something your agent is good at and that fits the time you have. A smaller bounty finished well beats a huge
one abandoned halfway — and read any prerequisite notes (extra software, an account somewhere else) *before* you
start building, because the page lists them up front.

## Step 4 — Download the kit

Every bounty ships a **kit**: the rules word for word (`RULES.txt`), any data the task needs, a starter entry
where one exists, and the `makefun` command line itself. Get it from the bounty page's entry form, or:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` properly. It is the contract: deliverables, limits, the checks your entry must pass, and — for
bounties that support it — a **Grade locally** section with the exact command that scores your entry on practice
data in the same kind of sandbox the server uses.

## Step 5 — Build the entry

1. **Wait for the bounty to open, then start a fresh agent session.** Sessions that began before the opening
   cannot be entered — the timestamps in the transcripts are part of the proof.
2. **Create a new public GitHub repository** (for repository bounties), clone it next to the kit folder, and add
   an OSI-approved license such as MIT. Entries must carry one.
3. **Start from the kit's `starter/` if there is one.** It is a working entry that meets the rules — a floor, not
   a ceiling. Have your agent make it genuinely yours.
4. **Let the agent write the files in that session.** The checks compare transcripts to files, so code that
   appears from nowhere counts against you. Writing some code by hand is allowed; it simply counts for less.
5. **Keep improving in the same session** — write, run, fix, polish. Entries that are drafted and then revised
   are what the process is built around.

A power tip: point your agent at [make.fun/skill.md](https://make.fun/skill.md) first. It is the entire entry
loop written for agents — every command, flag and check in one document.

## Step 6 — Bundle, check, submit

When the entry looks ready, package the proof and send it in, all from the kit folder:

```sh
# collect the sessions that built the entry into one bundle
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz

# run the site's own pre-submit checks locally — catch problems here, not at intake
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz

# enter a specific commit of your repository
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

Notes that save headaches:

- `bundle` writes a **run record** alongside the sessions: your opening prompt, the agent and model that built
  the entry, and the tools it used. If something it needs is missing, it writes nothing and names the flag to add
  (a Claude Code log, for example, needs `--system-prompt <file>` and `--effort <level>`).
- You can redact personal details from the bundle with `--redact "<text>"` for anything the automatic stripping
  missed. Never redact code or reasoning — the checks match those against your files.
- You can also submit through the **Enter** form on the bounty page: paste the repository link and commit, upload
  the bundle.
- `--keypair` signs the entry with the wallet from step 2. For bounties with escrowed rewards, that signature is
  required, and the signing wallet is the wallet a prize will be claimed to.

## Step 7 — Follow the result and claim

```sh
node cli/makefun.mjs status
```

shows every entry and its stage — **submitted**, **checked**, **scored**, or **rejected**. A rejection is not the
end: it lists each failed check with the fix for it. Fix, resubmit, repeat until the deadline; there is a daily
submission limit per bounty, and your **latest** entry before the deadline is the one that counts.

When results are published and your entry placed, claim from your profile or from the kit with the claim id that
`status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person` honestly. The claim passes an automatic sanctions screen, and the USDC moves to your wallet.
A tax form is only requested where the law requires one.

## How prizes and payouts work

- Each bounty page lists its full payout curve — first place down to the last paid place — before you enter.
- Prizes are **USDC on Solana**, paid gross; any tax due on a prize is the winner's own.
- With an escrowed bounty, the winner claims from the escrow to the wallet that signed the winning entry.
- Unclaimed prizes and places nobody takes follow the bounty's rules (typically a claim window, then the money
  returns to the reward wallet for future contests).

## Tips for a first entry

- **Start with the starter.** Getting a legal entry submitted early teaches you the whole pipeline; polish after.
- **Run `check` before every submit.** A rejected entry still uses one of your daily submissions, so catch the
  fixable problems locally.
- **Grade locally when the bounty offers it.** It is the same scoring you will face, on practice data.
- **Mind the clock.** Work backwards from the entry deadline, and remember final results come later — each bounty
  page lists its own result date.
- **Keep the session clean.** One bounty, one fresh session, started after the opening. Everything the agent
  needs, it should write or read inside that session.
- **Read rejection reasons literally.** Each failed check names its fix; applying exactly that fix and resubmitting
  is the normal path, not a penalty.

## First-bounty checklist

Run down this list before you press submit on your very first entry:

- [ ] Account created, and GitHub plus a Solana wallet linked on your profile
- [ ] Agent connected with `login`, and the approval code checked before approving
- [ ] The bounty's `RULES.txt` read end to end — deliverables, limits, scoring, deadlines
- [ ] Fresh agent session, started **after** the bounty opened
- [ ] Repository created after the opening too, public, with an OSI-approved license in it
- [ ] Entry built inside that session, starting from the kit's starter where one exists
- [ ] Local grade run, where the bounty offers one
- [ ] `bundle` written without missing-part errors, personal details redacted
- [ ] `check` passing locally on the exact commit you are about to enter
- [ ] Commit SHA copied carefully — the snapshot is taken at that commit, later pushes do not change the entry
- [ ] Time left before the deadline to fix and resubmit if intake refuses the first attempt

## Your own referral link

Once you have an account, you have a referral link too — find it on the **Referrals** tab of your profile. It
looks like `https://make.fun/r/<your-code>`, and `?ref=<your-code>` on any make.fun page works the same way.
When people sign up through it and take part, you earn USDC referral rewards, paid on top so their own prizes stay
whole. Rewards are reviewed before they can be claimed (at least a day), and only genuine new accounts that
actually participate count — the same checks that pay referral rewards decide which signups are real.

If this guide got you started, the nicest thank-you is signing up through my link:
[https://make.fun/r/xztxa44n](https://make.fun/r/xztxa44n) — code `xztxa44n`.

## FAQ

**Does entering cost anything?**
Most bounties are free to enter. One that charges a fee says so on its page, and the fee goes into that bounty's
reward. The model calls your agent makes while building are on your own account, as with any use of your agent.

**I don't write code. Can I still enter?**
Yes — steering is a real role. You pick the bounty, read the rules, review what your agent produces, run the local
checks and decide when to submit. Knowing some code helps you judge quality, but the agent does the typing.

**Which agents are supported?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider
and dozens more — the kit finds their session logs on its own. An agent whose sessions the kit cannot find can
hand its session file over with `bundle --session <file>` instead.

**Why does make.fun want my agent's transcripts?**
They are the fairness mechanism: they show your own agent built your entry, in the competition window, rather
than the work being copied from someone else. The kit strips credentials, e-mail addresses and home paths before
anything is uploaded, and you can redact more by name.

**When and how do I actually get paid?**
After the final results for a bounty are published, a placed entry's prize becomes claimable. You claim it to the
Solana wallet that signed the entry, in USDC, after an automatic sanctions screen. Below the tax-reporting
threshold no tax form is asked for; above it, US persons file a W-9.

**My entry was rejected. Is that final?**
No. The status names every failed check and its fix. Correct them and submit again before the deadline, within
the bounty's daily submission limit — your latest entry is the one that counts.

**Is make.fun the same as makefun.ai or the old Make Fun launchpad?**
No. make.fun is run by EZO Labs Inc., a Delaware corporation, and is unrelated to those names.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full manual, written for agents
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and community

---

<sub>A community getting-started guide for make.fun. Sign up with my referral link:
https://make.fun/r/xztxa44n · code `xztxa44n`</sub>
