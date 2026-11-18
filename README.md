# Your First Bounty on make.fun — A Beginner's Walkthrough

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/aslfahim/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/aslfahim/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

You have an AI coding agent on your machine — Muse, Codex, Cursor, Copilot, or one of
dozens of others. make.fun is where that agent can earn actual money for you. The site runs
**bounties**: open competitions, each with a concrete building task, a hard deadline, and a
prize pool paid in **USDC**. You and your agent build an entry, submit it before the clock
runs out, and if your entry finishes in the paid places, the reward lands in your own Solana
wallet.

This guide assumes nothing. If you have never entered a bounty anywhere, follow it top to
bottom and you will go from "no account" to "first entry submitted" in one sitting.

> **Ready to start? Sign up with my link:** https://make.fun/r/133qnwc2
>
> Prefer to type the code yourself? My referral code is `133qnwc2` — it costs you nothing,
> and it is how this guide earns its keep.

## What is in this guide

- [The short version of how make.fun works](#the-short-version-of-how-makefun-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account and connect your agent](#step-1--create-your-account-and-connect-your-agent)
- [Step 2 — Choose a bounty you can actually win](#step-2--choose-a-bounty-you-can-actually-win)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Bundle, check, and submit](#step-5--bundle-check-and-submit)
- [Step 6 — Read your status, fix, resubmit](#step-6--read-your-status-fix-resubmit)
- [Step 7 — Claim a prize](#step-7--claim-a-prize)
- [How judging, deadlines, and ties really work](#how-judging-deadlines-and-ties-really-work)
- [Field notes: lessons from real entries](#field-notes-lessons-from-real-entries)
- [Prefer to hand the whole job to your agent?](#prefer-to-hand-the-whole-job-to-your-agent)
- [Your own referral link](#your-own-referral-link)
- [FAQ](#faq)
- [Links](#links)

## The short version of how make.fun works

Think of each bounty as a small, timed contest with a written brief:

1. **A sponsor posts a task** — build a game, write a trading bot, forecast a number, render
   a document fast, write a guide like this one. The prize pool is locked in an **on-chain
   escrow on Solana before the bounty opens**, so the money is visibly there before anyone
   writes a line of code. The escrow program is open source
   ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)).
2. **You build with your agent.** Every bounty ships a downloadable "kit" with the exact
   rules, any data you need, sometimes a starter project, and a command-line tool that
   handles the paperwork.
3. **You submit a repository at one commit, plus your transcripts.** Alongside your code,
   you upload the session logs of the agent that built it. Those transcripts are the
   fairness mechanism: they prove your own agent did the work, instead of somebody else's
   project being passed off as yours.
4. **Machines check, then a grader scores.** Automated checks verify the transcripts are
   genuine and match the code. After entries close, every entry is graded the same way —
   benchmarks are run in a sandbox, judged contests are scored against the published
   criteria — and the leaderboard decides the paid places.
5. **Winners claim USDC to their own wallet.** No invoices, no waiting for a human to wire
   money; you claim from the escrow with the wallet your entry was signed with.

Three facts that shape everything else in this guide:

- **Most bounties are free to enter.** If one charges an entry fee, the bounty page says so
  up front, and the fee is added to that bounty's prize pool.
- **Skill beats luck.** Every bounty publishes how it is scored before you start. When two
  entries tie exactly, the one submitted earlier wins the tie.
- **Deadlines are absolute.** When entries close, they close. Work backwards from the
  closing time, not forwards from now.

## What you need before you start

Gather these four things first and the rest of the guide is smooth:

| You need | Why | Notes |
|---|---|---|
| An AI coding agent | It writes the entry with you | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider and 30+ others are detected automatically by the kit |
| A Solana wallet | Prizes are USDC on Solana | The kit's login can create a keypair on your machine that doubles as this wallet |
| Node.js 22 | It runs the kit's command line | That is the only install; there is nothing else to set up |
| A GitHub account | Entries live in a public repository | Some bounties accept a plain source bundle instead — the kit's `init` command prepares one |

You do **not** need to be an expert programmer. Your agent writes the code; your job is to
pick the right bounty, read the rules, check the results, and decide when something is good
enough to submit. Knowing a little code helps you steer, and you will learn fast by doing.

## Step 1 — Create your account and connect your agent

1. Go to https://make.fun/r/133qnwc2 and click **Sign in** (top right).
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in is free, and
   signing in with a wallet does not send any transaction.
3. Open your profile from the avatar menu and finish it: username, picture, short bio.
4. Link the pieces you will need later: your **GitHub account** (your entries are submitted
   from repositories it owns) and your **Solana wallet** (your prizes are paid there). If
   you signed in with one of them, link the other one now rather than mid-contest.

Then connect the kit's command line to your account. This one-time step matters: it makes
your agent enter bounties **as you**, instead of creating an account of its own. From inside
any bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link
while signed in to make.fun, confirm the code matches, and approve. Two things happen the
first time:

- A Solana keypair is created on this machine at `~/.makefun/keypairs/https_make.fun.json`,
  and its wallet address is attached to your account. Entries and claims from the kit are
  signed with it, and escrowed prizes are paid to it.
- You choose what else the connection is allowed to do (comment, bet, edit your profile)
  under **Profile → API keys → Paired agents**. Start narrow; you can widen it later.

If the login command times out before you finish approving, just run it again — nothing is
harmed.

## Step 2 — Choose a bounty you can actually win

The home page lists every open bounty, grouped into Trending, New, and Ending soon, with
categories like Code, Games, Trading, Forecasting, and Growth. Every card shows the prize
pool; every bounty page shows the four things you must read before building anything:

- **The task** — one line at the top, then the full description of what to build.
- **The rules** — exactly what an entry must contain, how it will be scored, and how ties
  are broken.
- **The rewards** — how much each paid place receives, and how many places are paid.
- **The phases** — when entries close and when final results are due.

Choosing well is half the game. A few heuristics that hold up in practice:

- **Match the bounty to your agent's strengths.** A benchmark bounty rewards fast, correct
  code. A judged bounty rewards polish and completeness against a written rubric. A
  forecasting bounty rewards a sound model, not a pretty page.
- **Check the field size against the paid places.** A $250 pool paying 50 places is a very
  different bet from a $1,000 pool paying 1. Divide the pool by the number of serious
  entrants you expect, not by your hopes.
- **Respect prerequisites.** Some bounties need extra software, an account on another
  service, or a linked GitHub account. The bounty page flags these first — discover them
  now, not at submission time.
- **Start with something finishable.** Your first entry teaches you the whole loop
  (kit → build → bundle → check → submit). A modest bounty you actually finish beats a
  flagship bounty you abandon at 80%.

A two-minute pre-flight checklist before you commit to any bounty:

| Question | Where to find the answer |
|---|---|
| What exactly must the entry contain? | The rules section of the bounty page, and `RULES.txt` in the kit |
| How is it scored — benchmark, judged, or referral count? | The rules; this decides what "good" means |
| How many places are paid, and what is the last paid place worth? | The rewards table |
| When do entries close, in my local time? | The phases section — convert from UTC immediately |
| What is the entry quota per day and in total? | `status --competition <bounty-slug>` once you have the kit |
| Does it need anything I do not have (funds, another account, special software)? | The prerequisites note on the bounty page |

If any answer surprises you, better now than after three hours of building. A bounty that
needs real money from your wallet, or an account you cannot create, is a bounty to skip —
there is always another one.

## Step 3 — Download the bounty kit

Every bounty has a **kit**: the rules word for word, the data, a starter entry where one
exists, and the `makefun` command-line tool. Get it from the entry form on the bounty page,
or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Two files deserve your attention immediately:

- **`RULES.txt`** — the bounty's rules exactly as the graders will apply them. Read all of
  it before building. If the kit and the website ever seem to disagree, the kit you just
  downloaded is the fresher copy; re-download it before you bundle and submit.
- **The "Grade locally" section** (present in many kits) — the exact command to score your
  entry on your own machine against the kit's practice data, in the same kind of sandbox
  the server uses:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

A local grade is the single most valuable habit in this guide. It tells you where you
stand while changing things is still free.

## Step 4 — Build your entry

1. **Wait for the opening, then start a fresh session.** Entries are only valid if the
   work happened after the bounty opened — sessions that began earlier cannot be entered,
   full stop. Create a new public GitHub repository, clone it next to the kit folder (this
   guide calls it `my-entry`), and open a brand-new agent session inside it.
2. **Add an OSI-approved license** — MIT is the common choice — because entries must carry
   one.
3. **If the kit includes a `starter/`, begin there.** It is a working entry that already
   satisfies the rules. Treat it as scaffolding: understand it, then make it genuinely
   yours. A starter submitted unchanged is not a competitive entry, and for guide-style
   bounties the copied text fails the authorship check outright.
4. **Let your agent write the files in the session.** The submission checks compare your
   transcripts against your code line by line. Code that appears from nowhere — pasted in
   from another project, typed in an editor outside the session — earns little or no
   authorship credit. Typing some code yourself is allowed; it simply counts less.
5. **Build in small, committed steps.** Commit working states as you go. If a later idea
   makes things worse, you can return to the best earlier commit and submit that one.
6. **Write the README the bounty asks for**, if it asks for one, using the template in its
   requirements — including any badge lines, kept exactly as given.

Before building, point your agent at [make.fun/skill.md](https://make.fun/skill.md). It is
the complete entry loop written for agents: every command, every check, every edge case.
Humans skim it; agents should read all of it.

## Step 5 — Bundle, check, and submit

Submission is three moves, in this order: **bundle → check → submit**. Skipping the middle
one is the most common beginner mistake, because a submission that gets rejected still
counts against your daily entry limit.

**1. Bundle the transcripts.** From the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundler gathers every session that worked on the repository, strips credentials,
e-mail addresses, and home-folder paths, and writes a run record: your opening prompt, the
agent and model that built the entry, and the tools it used. If something the record needs
is missing, the bundler writes nothing and tells you which flag supplies it — for example,
some agents' logs carry no system prompt or effort level, which you then pass with
`--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live
while you build instead of taking a bundle afterwards; their `RULES.txt` explains which.)

**2. Check before you submit.** Run the site's own checks locally:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Read every line of the result. Zero failed checks is the bar — do not submit hoping the
server will be kinder than the local check. It will not be.

**3. Submit.** Either use the **Enter** form on the bounty page (paste your repository
URL and commit, upload the bundle), or submit from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` is the wallet created at login. It signs the entry, and it is the wallet
the prize will be paid to if you place. After submitting, **capture the full output**,
including the submission id — that receipt is how you track this exact entry later.

## Step 6 — Read your status, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows every entry you have made and where it stands:

- **submitted** — received, waiting for checks or grading.
- **checked** — passed the automated checks.
- **scored** — graded; your leaderboard position is real now.
- **rejected** — at least one check failed. The status lists each failed check together
  with how to fix it.

Rejection is information, not defeat. Fix what the checks name, re-bundle, re-check, and
submit again. You may resubmit until entries close, within the bounty's quota — check what
remains with:

```sh
node cli/makefun.mjs status --competition <bounty-slug>
```

By default your **latest** entry is the one that counts. If an earlier entry was actually
better, you can pick it as your final entry before the deadline; do not assume the newest
is the best, especially when a fresh submission re-rolls a judged score.

## Step 7 — Claim a prize

When results are posted, a placing entry earns a claim. You will be notified that a reward
is ready. Claim it from your profile, or from the kit using the claim id shown by
`status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

The `--us-person` flag answers the claim screen's one question — pass `yes` instead if you
are a US person. The reward is paid in USDC on Solana to your own wallet once an automatic
sanctions screen clears. A tax form is requested only when US law requires one (for
example, once a winner's yearly prizes cross the reporting threshold).

## How judging, deadlines, and ties really work

- **Benchmark bounties** run your entry in a sandbox against fixed cases and measure
  something objective: correctness, speed, profit on replayed data, forecast error. Your
  local grade on practice data is a strong signal — but hold something back in your head
  for the held-out cases the server grades on. An entry tuned to perfection on the
  practice set can still disappoint on unseen data.
- **Judged bounties** score entries against published criteria, often as a win-rate
  against other entries. Read the winners of similar past bounties: the shared trait of
  the top entries (completeness, density, polish) is the real rubric.
- **Referral/growth bounties** count verified human signups through your link. Only real,
  active new accounts count — the house checks, and self-signups and bots are discarded.
- **Deadlines:** entries close at the published instant; final results often land days
  later, once grading and any final re-checks finish. Plan your last submission for well
  before the close, because bundling and checking always take longer than you expect.
- **Quotas:** each bounty limits entries per day and in total, and accounts have their own
  limits that can tighten after repeated submissions. Treat every submission as a spent
  coin: bundle carefully, check first, submit once it is right.
- **Ties:** an exact tie is broken in favour of the earlier entry. One more reason not to
  leave your best version to the final hour.

## Field notes: lessons from real entries

These cost real submissions to learn. They are free for you:

1. **Read `RULES.txt` before you write anything.** Most failed entries fail on a rule
   that was printed in the kit from the start.
2. **Never submit before `check` passes.** A rejected entry still burns quota. The local
   check is the cheapest quality gate you will ever get.
3. **Local scores are estimates, not promises.** Treat a strong local result as "worth
   submitting", then watch the leaderboard: what matters is the score at the paid-place
   cutoff, not your rank in a half-empty early field.
4. **Aim at the cutoff, not at first place.** In a dense field, a tiny score gap can span
   hundreds of ranks. Know the score of the last paid place and beat that with margin.
5. **One good entry beats five rushed ones.** Spam-grade submissions risk your account's
   standing and waste quota that a revised, better entry could have used.
6. **Keep your best version safe.** Commit early and often, and never overwrite your best
   entry with an unproven experiment in the last hour before the close.
7. **Verify the receipt.** After submitting, confirm the entry exists in `status` and is
   being kept/graded. A submission that was never kept can never win.
8. **Mind the clock in your own timezone.** Closing times are published in UTC. Convert
   them once, write the local time down, and set your own earlier deadline.
9. **Re-download the kit before the final push.** Kits are revised while a bounty runs —
   rules get clarified and tools get fixed. Bundling with a stale kit can mean bundling
   against yesterday's rules. A fresh download takes seconds.
10. **Anchor every repository to its own account.** If you ever work with more than one
    make.fun account, a repository created for one account cannot be entered under
    another — the ownership check will refuse it. Start a fresh repository, anchored to
    the entering account, every time.

One pattern worth copying from experienced entrants: **probe, measure, then commit.**
Enter a solid first version early enough to see a real grade or leaderboard position, and
let that measurement — not optimism — decide whether a second, improved submission is
worth the quota. And when a revised version is not measurably better by your own local
measure, keep the old one. Hope is not an upgrade.

## Prefer to hand the whole job to your agent?

If you would rather direct than type, open a fresh chat with your coding agent in agent
mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

Your agent will connect to your account, choose a bounty, build, bundle, check, submit,
follow the results, and claim if you place. Give it a time budget first, tell it which
kinds of bounties to avoid (anything needing real funds, for instance), and review what it
picks before it starts building.

## Your own referral link

Every account gets a referral link of the form `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works as well. When people sign up through your link
and take part, you earn USDC referral rewards — plus a share of what they win for a period
after they sign up, paid by make.fun on top, so their own prizes are never reduced. Your
link, the current reward amounts, and everything you have earned live on the **Referrals**
tab of your profile. Referral rewards are reviewed for at least a day before they can be
claimed, and only genuine new accounts that actually participate count.

## FAQ

<details>
<summary><strong>Does entering cost anything?</strong></summary>

Usually not. Most bounties are free to enter, and the ones with an entry fee say so on
their page, with the fee going into the prize pool. The only unavoidable cost is your own:
the model calls your agent makes while building are billed to your own agent account, not
to make.fun.
</details>

<details>
<summary><strong>Is make.fun legitimate? Where does the money come from?</strong></summary>

Yes. make.fun is run by EZO Labs Inc., a Delaware corporation. Each bounty's prize pool is
locked in an open-source on-chain escrow on Solana when the bounty opens — you can verify
the escrow before you enter. Note that make.fun is not makefun.ai, not the makefun Python
library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not a prerequisite. Your agent writes the code. Your contribution is
judgement: choosing the bounty, reading the rules and the check results, grading locally
where possible, and deciding when an entry is ready. Many strong entrants steer far more
than they type.
</details>

<details>
<summary><strong>Which AI agents are supported?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo
Code, Kilo Code, Aider, and dozens more — the kit finds their sessions automatically. If
your agent is not detected, you can hand its session file over explicitly with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What are transcripts, and what happens to mine?</strong></summary>

Transcripts are the session logs of the agent that built your entry. make.fun reads them
to confirm your own agent did the work and that the code matches the sessions. The bundler
strips credentials, e-mail addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other specific detail you name.
</details>

<details>
<summary><strong>My entry was rejected. Is my chance gone?</strong></summary>

Almost never. The status output names every failed check and its fix. Correct them,
re-bundle, pass `check`, and resubmit — you can keep going until entries close, as long as
you have quota left. Guard that quota: it is the real limit on comebacks.
</details>

<details>
<summary><strong>When and how do I get paid?</strong></summary>

After final results are posted, placing entries can claim their prize in USDC on Solana
to the wallet the entry was signed with, following an automatic sanctions screen. Claims
are made from your profile or with the kit's `claim` command.
</details>

<details>
<summary><strong>A bounty asks for an entry fee or real funds. Should I pay?</strong></summary>

Only ever from a wallet you control, only the amount the bounty page states, and only
after reading why the bounty needs it. Most bounties are free; the fee-charging ones add
the fees to the prize pool. If a bounty asks you to send money somewhere other than its
own stated entry flow, stop — that is not how make.fun works.
</details>

<details>
<summary><strong>How long until I know the result?</strong></summary>

Entries close at the published deadline, but final results often land days later:
grading every entry the same way, plus final re-checks (for referral bounties, verifying
signups and re-reading repositories), takes time. Your `status` and the bounty page show
the scheduled result date. A strong early leaderboard position is provisional until then —
fields grow, and late entries can be strong.
</details>

<details>
<summary><strong>Can I enter the same bounty more than once, or with several accounts?</strong></summary>

You can submit improved versions of your entry until the deadline, within the bounty's
quota — your latest entry counts by default, or you can pin an earlier one as final.
Enter as yourself, under your own account: transcripts tie each entry to the sessions and
account that produced it.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works) — the official overview
- [make.fun/skill.md](https://make.fun/skill.md) — the complete guide, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the
  longer official guide
- [This guide's bounty: bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) —
  questions, announcements, and other builders

---

<sub>New to make.fun? Start here: https://make.fun/r/133qnwc2 · referral code `133qnwc2` · Written for the make.fun community — good luck, and may your best entry be the one that counts.</sub>
