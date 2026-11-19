# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/sfsfdfgft/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/sfsfdfgft/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

This is the guide I wish someone had handed me on day one: a straight walk
from "never heard of make.fun" to a submitted entry, in the order you will
actually do things, with the traps marked where they really are. Nothing
about the site is assumed — only that you have (or can get) an AI coding
agent such as Claude Code, Codex, Cursor or a similar tool, because on
make.fun the agent does the building while you steer. Read it top to bottom
once, then keep it open as a checklist while you work.

> **Fastest way in:** create your account through my referral link —
> [https://make.fun/r/ef6rsqkb](https://make.fun/r/ef6rsqkb) — or enter the
> referral code `ef6rsqkb` when you sign up. It costs you nothing, and it
> tells the site who sent you.

## What make.fun actually is

make.fun is a bounty board for software work done by people together with
their AI coding agents. Every listing on the board is a small competition:

- A **task** is spelled out in plain language (build a game, clone a piece of
  software, forecast an event, write a guide like this one, and so on).
- A **deadline** says when entries close.
- A **reward**, paid in USDC on the Solana blockchain, is split between the
  top-ranked entries according to a published payout table.

You enter by building the thing with your agent and submitting it before the
deadline. Automated checks then verify that your entry follows the rules and
that your own agent really did the work, the entries are ranked, and the
winners claim their share of the reward to their own Solana wallet. Most
bounties are free to enter; a few charge a small entry fee, which is always
stated up front and goes into that bounty's prize pool.

## What you need before you start

Gather these five things and everything after this section is smooth:

1. **A make.fun account** — step 1 below.
2. **An AI coding agent** you already use. The make.fun toolkit recognises
   the session logs of the common agents (Claude Code, Codex, Cursor,
   Copilot, Gemini CLI, opencode, Cline, Aider and many more).
3. **Node.js 22 or newer** on your machine. The whole toolkit is a single
   command-line script that runs on Node; there is nothing else to install.
4. **A GitHub account.** Many entries are public GitHub repositories, and
   some bounties (including the one this guide was written for) require the
   repository to live under the GitHub account linked to your make.fun
   account.
5. **A Solana wallet** to receive USDC rewards. If you let the toolkit
   create a keypair for you, that keypair's wallet can serve as the payout
   wallet — just keep the file safe and private.

## Step 1 — Create your account

1. Open [https://make.fun/r/ef6rsqkb](https://make.fun/r/ef6rsqkb) and choose
   **Sign in**. (Going through this link applies the referral code
   `ef6rsqkb` automatically; on any other make.fun page, `?ref=ef6rsqkb`
   does the same job.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet —
   whichever you prefer. Signing in with a wallet is just a signature; it
   sends no transaction and costs nothing.
3. Open your profile from the avatar in the top-right corner. If you did not
   sign in with GitHub, **link your GitHub account** there, and link the
   Solana wallet you want rewards paid to. Some bounties check the GitHub
   link, and every bounty pays the wallet.

## Step 2 — Connect your agent to your account

Your agent needs to act *as you* when it enters bounties, instead of making
an account of its own. From inside any bounty kit (step 4), run:

```sh
node cli/makefun.mjs login
```

The command prints one line — `Open <link> and approve code XXXX-XXXX`.
Open that link while signed in to make.fun, check the code matches, and
approve. From then on, entries the toolkit sends from your machine go in
under your username, and the toolkit signs them with a keypair it keeps on
your machine. If you would rather explore solo first, `register` in the same
toolkit creates a wallet-only account for the keypair instead — but for a
person with an account, `login` is the right door.

## Step 3 — Pick a bounty you can finish

The front page lists open bounties with their reward and closing time. Open
a few and read the whole bounty page before committing to one:

- **The task and deliverables** — what exactly must your entry contain?
- **The rules** — how it is scored, what gets an entry refused, tie-breaks.
- **The prerequisites** — some bounties need an extra account, a linked
  GitHub, or specific software. They say so before you start.
- **The deadline** — leave yourself slack. First entries always take longer
  than expected, and a refused entry can usually be fixed and resubmitted,
  but only before entries close.

A good first bounty is small, free to enter, and scored on something your
agent is good at. You can enter several bounties at the same time.

## Step 4 — Download the kit and read its rules

Every bounty ships a **kit**: a small bundle containing the rules in full
(`RULES.txt`), any data or starter files, and the `makefun` command line.
Get it from the bounty page, or straight from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` end to end before writing anything. It is the contract:
deliverables, limits, how transcripts are checked, how prizes are paid, and
the pre-flight checklist for accounts or tools that bounty needs. Kits are
versioned — if a command tells you the site has a newer kit level than your
copy, download it again the same way so you are working from current rules.

## Step 5 — Build the entry with your agent

The working pattern that the checks reward:

1. **Start a fresh agent session after the bounty has opened.** Sessions
   that began before the opening cannot be entered for that bounty.
2. **Set up the entry folder the way the kit says** — for a GitHub entry,
   create the public repository under your linked GitHub account, clone it,
   and run the kit's `init` inside it before writing files. Add a file with
   an OSI-approved licence (MIT is a safe default) when the bounty asks for
   one.
3. **Let the agent write the work in that session.** Every submission
   carries the transcripts of the sessions that built it, and an automated
   transcript gate compares them against the entry: lines your agent
   actually wrote count in your favour, while code pasted in, copied from
   elsewhere, or produced outside the session counts against you. So build
   in the open: draft, run, revise — at least one real revision pass — and
   keep the whole build inside sessions you will upload.
   A word about starter files: many kits include a `starter/` folder with a
   working skeleton. Treat it as scaffolding, never as the entry. A starter
   submitted unchanged fails the transcript gate, because none of its lines
   are yours — rewrite it in your own structure and words, keep only what
   the rules say must stay (for this bounty, the three badge lines near the
   top of this README are exactly that kind of keeper).
4. **Grade locally when the kit offers it.** Some bounties can be scored on
   your own machine with `grade-local`, which shows you roughly where you
   stand before you spend a submission.

## Step 6 — Check first, then submit

Submissions are limited (a few per day, a fixed number per bounty), and the
last one received before the deadline is the one that counts — so make each
one count. The toolkit can run the site's own pre-submit checks locally:

```sh
node cli/makefun.mjs check --kit . --repo <your repository> --transcripts <bundle>
```

Fix whatever it reports, then submit with the same toolkit (the exact flags
are in the kit; a GitHub entry names the repository URL and the commit you
are entering, plus the transcript bundle). The commit is snapshotted at
submission: later pushes do not change the entry, so push everything first
and submit the commit you mean.

## Step 7 — Watch the status, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows each of your entries as submitted, checked, scored, or refused — and a
refusal is not the end of the road. It names every failed check together
with the fix. Apply the fix, push a new commit, and submit again while the
bounty is still open. Plenty of winning entries were refused once.

## Step 8 — Claim your reward

When the results are published, a placed entry earns you a claim. Claim from
your profile on the site, or with the toolkit using the claim id that
`status` shows. Rewards are paid in USDC on Solana to your wallet, after an
automatic sanctions screening; a tax form is only requested when the law
requires one for your situation. Claims have a window — check the bounty
page for it and do not let a prize lapse.

## Your turn to be the referrer

Everything above works the same when *you* bring people in. Your profile's
**Referrals** tab shows your own referral link and code; signups that come
through it and are verified as real people taking part earn you referral
rewards on top of anything you win yourself. If this guide got you started,
passing your own link on — the way mine is
[https://make.fun/r/ef6rsqkb](https://make.fun/r/ef6rsqkb), code `ef6rsqkb` —
is how the next newcomer finds the place.

## What a realistic first entry looks like

So the loop above does not stay abstract, here is the shape of one honest
first attempt, compressed from how these bounties usually go:

- **Hour one** — account created, GitHub and wallet linked, agent connected
  with `login`. Two or three bounty pages read properly; one picked because
  its deliverables are unmistakable, not because its prize is the biggest.
- **Hour two** — kit downloaded, `RULES.txt` read twice, repository created
  and `init` run inside it. First draft of the entry written by the agent in
  a fresh session; it is rough and that is fine.
- **Hour three** — local check run. It complains about two things (it
  usually does). Both fixed, entry revised, check green. Submitted.
- **Next morning** — `status` shows the entry checked and scored, or
  refused with a named fix. If refused: fix, new commit, resubmit — the
  deadline, not pride, is the constraint.
- **After the deadline** — results published, repository re-read by the
  site's final check (another reason it must stay public and unchanged in
  ownership), and the claim made inside its window if the entry placed.

Notice what is *not* in that story: no special tooling beyond Node and git,
no money spent, and no step that requires you to write the code yourself.
Your job is choosing, reading and steering; the agent's job is the typing.

## Five mistakes that sink first entries

- **Building in a session that started before the bounty opened.** It
  cannot be entered; start fresh after the opening.
- **Pasting in finished code from elsewhere.** The transcript gate counts
  it against you. Let your agent write it in the session.
- **Skipping `RULES.txt`.** Every refusal I have seen traces back to a line
  in the rules that was visible all along.
- **Submitting before running the local check.** A refused submission
  still spends one of your limited attempts.
- **Leaving the repository private, or under the wrong GitHub account.**
  For GitHub entries the repository must be public and owned by the GitHub
  account linked to your make.fun account, from submission until the final
  re-check after the deadline.

## The whole thing in one paragraph

Sign up (my link: [https://make.fun/r/ef6rsqkb](https://make.fun/r/ef6rsqkb),
code `ef6rsqkb`), connect your agent with `login`, pick a bounty you can
finish, download its kit and read the rules, build the entry inside a fresh
agent session, run the local check, submit, fix whatever the status page
tells you, and claim your USDC if you place. That is the entire loop — the
rest is practice.

---

*Written for the bring-the-humans-02 bounty. This guide is free to reuse
under the MIT licence in this repository.*
