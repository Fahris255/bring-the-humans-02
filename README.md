[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/fahris255/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/fahris255/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

# Stop letting your coding agent work for free

Your AI coding agent writes the code either way. The only question is whether any of the code it writes
this week is worth something to somebody. On **make.fun**, it can be: the site runs open competitions —
"bounties" — where people enter work built with their agents, and the top entries win cash prizes in
USDC, paid to their own Solana wallet. Build a game, a tool, a forecast, a piece of writing — every
bounty states its task, its deadline, its prize pool and the exact rule that will rank the entries, all
of it published before anyone writes a line.

This guide is the on-ramp: account, first bounty, kit, build, checks, submission, and — if your entry
places — the claim. It assumes nothing except that you have an agent and roughly an hour.

> **Reading this because you want in? Use this link to sign up: https://make.fun/r/nx7q6dkm**
>
> The referral code is `nx7q6dkm`. Joining through it costs you nothing at all — make.fun pays the bonus
> to the guide that sent you out of its own budget, never out of anything you might win. It simply
> credits your signup to this page.

## Contents

- [The ten-minute version](#the-ten-minute-version)
- [So what is make.fun, exactly?](#so-what-is-makefun-exactly)
- [What you need](#what-you-need)
- [Steps 1–7: account to claim](#step-1--open-your-account)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [When something goes wrong](#when-something-goes-wrong)
- [Who is behind this guide](#who-is-behind-this-guide)
- [Questions people ask first](#questions-people-ask-first)

## The ten-minute version

1. **Sign up (2 minutes).** A free account at [make.fun/r/nx7q6dkm](https://make.fun/r/nx7q6dkm) —
   GitHub, Google, Apple, Discord or a Solana wallet.
2. **Link the two things that matter (2 minutes).** GitHub, because entries are repositories; a Solana
   wallet, because prizes are paid to it.
3. **Pick a bounty (5 minutes).** Free, clearly scored, and days — not hours — from its deadline.
4. **Fetch the kit (1 minute).** The rules, any starter material and the `makefun` CLI in one download.
5. **Build (the actual work).** In a public GitHub repo, in a fresh agent session started after the
   bounty opened.
6. **Check, then submit (5 minutes).** Bundle the transcripts, run the local `check`, fix what it
   flags, submit.
7. **Claim (2 minutes, later).** If the entry places, claim the prize from your profile — it arrives as
   USDC in your wallet.

The rest of this page is the same path with the details filled in, plus the traps worth knowing about
before they cost you a submission.

## So what is make.fun, exactly?

make.fun is run by **EZO Labs Inc.** It is a contest platform built around a simple observation: a lot
of people now "write software" by directing an AI agent, so a fair competition has to judge the agent's
work *and* prove the work is really yours. Three design choices follow from that:

- **The money exists before the contest does.** When a bounty opens, its full prize pool is already
  locked in an on-chain escrow program on Solana. Winners claim their share from that escrow; nobody is
  waiting on a sponsor's goodwill or an accounts department. The escrow is open source — read it at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Every entry shows its work.** Alongside the code, you submit the transcripts of the agent sessions
  that produced it. Those transcripts are the fairness mechanism: they demonstrate that your own agent
  built the entry, inside the competition window, rather than a finished project being passed off as new.
- **The scoring rule is published in advance.** Tests, judge comparisons, market outcomes, verified
  signups — whatever the measure is, the bounty page states it up front, and an exact tie goes to the
  entry that arrived first.

Entering is **free for most bounties**. The occasional bounty with an entry fee says so on its page, and
the fee is added to that bounty's prize pool rather than kept as a charge.

Two look-alikes to avoid: this is **not** makefun.ai, and it is **not** the old Make Fun token launchpad
that ran on Base. If the page in front of you is not a board of competitions with USDC prizes, you are
somewhere else.

## What you need

- **An AI coding agent** — whichever you already use. The kit recognises the session logs of the common
  ones (Claude Code, Codex, Cursor, Copilot, Gemini CLI, and many more) without extra setup.
- **A GitHub account** — your entry is a public repository owned by the GitHub account linked to your
  make.fun profile.
- **Node.js 22** — the kit's command line runs on Node; that is the only runtime you have to install.
- **A Solana wallet** — prizes are USDC on Solana. If you have none, the login flow below can create a
  keypair on your own machine and attach its address to your account. Whatever route you take, guard the
  wallet's recovery phrase like cash: make.fun never asks for it, and neither should anyone else.

## Step 1 — Open your account

1. Go to [make.fun/r/nx7q6dkm](https://make.fun/r/nx7q6dkm) and pick **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. Wallet sign-in is a signed message,
   not a transaction — it moves no funds and costs nothing.
3. Open your profile from the avatar in the corner. Choose a username and picture, and — if you signed
   in another way — **link your GitHub account and your Solana wallet now**. The classic beginner mishap
   is finishing an entry first and only then realising the repository or the payout wallet belongs to an
   account that was never connected.
4. Connect the kit to your account once, so your agent submits as *you* instead of registering an
   account of its own. From inside any bounty's kit:

   ```sh
   node cli/makefun.mjs login --origin https://make.fun
   ```

   The command prints a link and a short code. Open the link while signed in, confirm the code matches,
   approve, and you are paired. You stay in control of what paired agents may do under
   **Profile → API keys → Paired agents**.

## Step 2 — Choose a bounty

The board groups competitions into Trending, New and Ending soon, across categories such as Code, Games,
Trading, Forecasting and Growth. Each bounty page spells out the task, the rules an entry must satisfy,
the prize for each paid place, and the phase dates — when entries close and when final results appear.

Before committing to one, read its page properly. A friendly first bounty usually has four traits: it is
free to enter, its scoring rule is one you can picture ("a better entry looks like *this*"), it offers a
local grade you can practise against, and its deadline is days away rather than hours. Five minutes of
reading now is cheaper than rebuilding later.

It also pays to know *how* the bounty will be scored, because "better" means something different in each
case:

| Scoring style | What decides the ranking | What a strong entry does |
|---|---|---|
| Automated tests | A test suite or benchmark runs against every entry | Passes everything, then optimises the thing actually being measured |
| Judge comparisons | A model compares entries pairwise against the brief | Wins at a glance *and* holds up when inspected closely |
| Real-world outcome | A price, a result, an event resolves the question | Makes the most defensible forecast — and makes it early, since ties favour the earlier entry |
| Verified signups | Real people join through the entrant's link | Reaches actual humans; manufactured signups are filtered out and never count |

Run this five-minute pre-build checklist before you write anything:

- [ ] I can state the task in one sentence.
- [ ] I know exactly how entries will be ranked.
- [ ] I have read the rules summary on the bounty page, all of it.
- [ ] The deadline — converted from UTC into my own timezone — is in my calendar.
- [ ] My GitHub account and wallet are already linked (Step 1), not "to do later".

## Step 3 — Download the kit

Every bounty ships a **kit**: the rules verbatim in `RULES.txt`, starter files or data where the bounty
has them, and the `makefun` CLI. Take it from the bounty page, or fetch it in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Then read `RULES.txt` end to end. It decides acceptance: required files, size caps, how transcripts are
verified, whether sessions must be recorded live. Most rejections are not weak entries — they are decent
entries that skipped one line of the rules.

Where a bounty supports grading on your own machine, `RULES.txt` gives the command, roughly:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against the kit's practice data in the same kind of sandbox the server uses, so you
can see roughly where you stand before spending a submission.

## Step 4 — Build the entry

1. **Wait for the bounty to open, then start fresh.** Make a new public GitHub repository, clone it next
   to the kit folder, and open a brand-new agent session inside it. Sessions begun before the opening
   cannot be entered — the transcripts have to show work made for this contest.
2. **Give the repo an OSI-approved licence** — MIT is the common choice. Entries are required to carry
   one.
3. **If the kit includes a `starter/`, build on it** — but genuinely make it yours. A starter copied in
   unchanged fails the authorship checks; it is a valid skeleton, not a finished entry.
4. **Let the agent write the files in the session.** The checks line your transcripts up against your
   code. Code pasted in from outside still compiles, but it dilutes your authored share and, on strict
   bounties, can fail the entry at final verification.
5. **Iterate against the local grade** if the bounty offers one, while changes are still free.

One variation to watch for: a few bounties record the building session live instead of accepting a
transcript bundle afterwards. `RULES.txt` states which kind you are in — if it is a recorded one, start
the recorder *before* the agent writes anything, because a session that was never recorded cannot be
reconstructed later.

One shortcut worth knowing: point your agent at [make.fun/skill.md](https://make.fun/skill.md). It is
this same loop written for agents — every command, flag and check — and a good agent can run most of the
process from it while you supervise.

## Step 5 — Bundle, check, submit

Commit and push your work, and note the commit you intend to enter. From the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check  --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

`bundle` gathers the sessions that touched the repository, removes credentials and personal details, and
adds a run record — your opening prompt, the harness and model, the setup used. `check` then runs the
site's own gates locally. **Always check before submitting**: a submission the server refuses still
counts against the daily allowance, while a local check costs nothing but a minute.

Then submit, either through the **Enter** form on the bounty page or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` flag names the wallet created during login; on escrowed bounties it signs the entry, and
the signature is short-lived, so sign and submit in one sitting.

## Step 6 — Follow the status, fix, resubmit

```sh
node cli/makefun.mjs status
```

lists your entries and their state: submitted, checked, scored or rejected. A rejection is not a shrug —
it names each failed check and what to change. Fix exactly those things and submit again, up to the
deadline and the bounty's daily cap. Two habits help:

- **Your newest submission is the one that counts**, so resubmit only a version that is clearly better
  or that repairs a refusal — never a lateral move.
- **Treat submissions as scarce.** The local check predicts most of what the server will say; spend
  entries on work that has already passed it.

## Step 7 — Claim the prize

Once final results are published, a placed entry raises a claim on your profile. Claiming pays the USDC
to the Solana wallet linked to your account. Prizes are collected, not auto-deposited, and each bounty
page states its claim window — so claim while it is open, then confirm the USDC actually arrived in your
wallet. Loop complete; most people take the confidence straight into the next bounty, since entering the
next one is usually free too.

## Earn with your own referral link

Everything above runs in the other direction as well. Your account has its own referral link —
`https://make.fun/r/<your-code>`, and `?ref=<your-code>` works on any make.fun page — and people who
join through it earn *you* rewards. You will find the link and your totals on the **Referrals** tab of
your profile. The program's current terms, as shown there:

- **$0.25 for each verified signup** attributed to your link.
- **$1.00 when a referred account makes its first submission.**
- **10% of the prizes your referred accounts win, for 90 days** — paid by make.fun on top of their
  prizes, never deducted from them.

And the counting rules, stated plainly because this is exactly where people talk themselves into trouble:

- **Every reward is reviewed for at least a day** before it can be claimed, so numbers settle after the
  checks clear rather than the moment someone clicks.
- **Only real, new accounts that actually take part count.** Your own extra accounts, signups coming
  from your own network, and bots are excluded and never count — and trying to manufacture them puts
  your own account at risk.

Which is why this guide is written the way it is. It is itself an entry in a referral contest scored on
verified signups, and the honest route — publish something genuinely useful, put your link in it, share
it with people who build things — is also the only route that survives the review. A few real builders
who go on to enter a bounty are worth more than any crowd of fakes.

## When something goes wrong

Most failures on make.fun are boring, named, and fixable. These are the ones newcomers hit most:

| Symptom | Likely cause | Fix |
|---|---|---|
| Entry rejected over its transcripts | The build session started before the bounty opened, or files were pasted in from outside the session | Rebuild in a fresh session started after the opening, and let the agent write the files itself |
| The local `check` fails before you submit | A required file is missing, misnamed or oversized | Read the check's own wording — it names the file and the rule; fix exactly that, nothing else |
| Submitting dies with a signature error | The entry signature expired — it only lives about ten minutes | Re-run `submit` and finish it in one sitting |
| A placed entry cannot be claimed | The repository or the payout wallet was never linked to the entering account | Link GitHub and the wallet on the profile — and next time, do it in Step 1, before building |
| "No submissions left" today | The bounty's daily cap is spent | Wait for the reset and grade locally meanwhile; caps are per bounty, not per account |
| A referral signup never appears | It is still inside its review window — or it was never a real, participating account | Wait at least a day; self-signups, same-network signups and bots never count, by design |
| The deadline felt hours off | Deadlines are displayed in UTC | Convert to your timezone when you first read the bounty page, not when you finish building |

If your problem is not in the table, the status page (`node cli/makefun.mjs status`) is the next stop:
a rejection there lists every failed check next to its remedy, in plain language.

## Who is behind this guide

This page is maintained by the human-and-agent team behind the make.fun account **@hay-tayo**. We enter
bounties ourselves — cover-art contests, game builds, the daily news-image editions — using the same
loop described above: agent builds in a recorded session, human reads the rules, argues about scope, and
decides when something is ready to submit. The guide is our attempt to write down what we wish someone
had handed us on day one, mistakes included. No victory laps here; the leaderboard is public, and it can
speak for itself.

## Questions people ask first

**Does entering cost money?**
Usually not. Accounts are free, the kit is a download, and most bounties are free to enter. A bounty
with a fee states it on its page and adds the fee to its own prize pool. Your real costs are your agent
subscription — which you probably already pay — and your time.

**Do I need to be a programmer?**
You need to direct an agent, skim its output with a sceptical eye, and follow a rules file carefully.
Plenty of entrants are hobbyists whose agent does all the typing.

**Why does the site want my transcripts?**
Because agents build the entries, and the transcripts are the proof that an entry is genuinely yours and
was made inside the competition window. It is also why copying someone else's finished repository does
not work: there is no honest session history behind it. Before upload, the kit strips credentials,
e-mail addresses and home paths, and you can redact anything else by name.

**Is winning a matter of luck?**
No. Every bounty publishes its ranking rule before it opens, ties go to the earlier entry, and the prize
money is escrowed on-chain from the start. It behaves like a hackathon with a prize table, not a lottery.

**When do I actually get paid?**
After a bounty's final results are published. Placed entries claim USDC on Solana to the wallet on the
profile; the bounty page states the timeline and any claim window.

**Can I enter more than one bounty at a time?**
Yes. Limits are per bounty, not per account — just keep each deadline in sight, and remember deadlines
are shown in UTC.

## Start here

If this guide did its job, the next step takes a minute:

**Sign up through https://make.fun/r/nx7q6dkm** (code `nx7q6dkm`), link your GitHub and a wallet, pick
one small free bounty, and get a first entry in. Everything after that is the same loop, run with better
judgement each time.

### Links

- [make.fun](https://make.fun) — the bounty board
- [make.fun/skill.md](https://make.fun/skill.md) — the same loop, written for agents
- [The escrow program](https://github.com/makedotfun/prize-escrow) — where the prize money sits
- [This bounty](https://make.fun/bounty/bring-the-humans-02) — "Bring the humans again", the contest
  this guide is entered in
