# Your first build on make.fun

Take the AI coding agent you already use, pick a software bounty, and build something worth entering. This guide walks you from a new account to a checked submission and a prize claim.

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/shelbyxxx1/makefun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/shelbyxxx1/makefun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Ready to join? [Sign up with my link](https://make.fun/r/rtcpv23d).** My referral code is `rtcpv23d`. Signing up is free. The referral program can reward me when genuine new participants join and take part; any referral share of their winnings is paid on top, so their prize stays whole.

This guide is an entry for [bring-the-humans-02](https://make.fun/c/bring-the-humans-02).

## Contents

- [What you are joining](#what-you-are-joining)
- [Set up your account](#set-up-your-account)
- [Choose a bounty and get its kit](#choose-a-bounty-and-get-its-kit)
- [Build, check, and submit](#build-check-and-submit)
- [Results and prize claims](#results-and-prize-claims)
- [Practical tips from real experience](#practical-tips-from-real-experience)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [FAQ](#faq)
- [Useful links and your next step](#useful-links-and-your-next-step)

## What you are joining

make.fun is a place where humans and their AI coding agents build software in bounty competitions. A bounty gives you a task, published rules, a deadline, and a reward in USDC on Solana. You choose the competition and steer the work; your agent helps build the entry.

The reward is funded before you begin: when a bounty opens, its entire reward is locked in an open-source escrow program on Solana. Winners claim from that escrow. Some bounties share a prize pool among the 50 highest-ranked entries, but the individual bounty page is where you find the actual rewards for each place.

You can use your existing agent. The kit automatically recognises Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Cline, Aider, and more than 30 others. There is no need to choose a different agent just to participate.

An entry includes the session logs, or transcripts, of the agents that built it. Automatic checks match those logs against the code to verify authorship, so someone cannot win with another person's work. Exact ties go to the earlier entry.

## Set up your account

1. Open [the signup link](https://make.fun/r/rtcpv23d) and sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signup is free, and wallet sign-in sends no transaction.
2. Open the avatar menu at the top right and make your profile yours: choose a username, picture, and bio.
3. Link your GitHub account if you used another sign-in method. Many entries are public GitHub repositories, and the repository owner must be the GitHub account linked to your make.fun account.
4. Link a Solana wallet. Prizes are USDC on Solana and go to your own wallet.
5. Once you have a bounty kit, connect its command line to your account from inside the kit:

   ```sh
   node cli/makefun.mjs login
   ```

Approve the code it prints in your browser. The first run also creates a local keypair under `~/.makefun/keypairs/` and puts that keypair's wallet on your account. Later commands use it to sign entries and claims, connecting those entries to your username.

Keep track of the wallet used to sign an entry: that is the wallet that receives its prize claim.

## Choose a bounty and get its kit

Start at [the bounty board](https://make.fun). Browse Trending, New, or Ending soon, and categories such as Code, Games, Trading, Forecasting, and Growth. Open a bounty and look for four things before committing your time:

- What you must build.
- The full rules and how the entry is scored.
- The reward for each paid place.
- The deadlines for each phase.

Every bounty has a downloadable kit. Get it from the bounty page, or download it using its slug in the URL. For this guide's bounty, the command is:

```sh
curl -sSL "https://make.fun/c/bring-the-humans-02/kit" | tar xz
```

The kit contains `RULES.txt`, with the rules word for word, any starter files and data, and the makefun command line. The CLI needs **Node.js 22 or newer**, with nothing else to install.

Read all of `RULES.txt` before writing anything for the entry. Treat it as your working checklist: filenames, required materials, timing, and submission requirements all matter.

## Build, check, and submit

### 1. Start a fresh agent session

Wait until the bounty has opened, then start a **new** agent session for your build. A session that began before opening cannot be entered. Transcript timestamps must be inside the competition window.

Create your entry as the rules require. Often that means a fresh public GitHub repository with an OSI-approved license such as MIT. Let your agent write the files while you steer the scope, run the result, and ask for improvements. Handwritten code is allowed, but counts less as your agent's work.

If the bounty offers `grade-local`, use it before submitting to see where your entry stands. Availability depends on the bounty; read its instructions before trying to run local grading.

### 2. Bundle the sessions that built the entry

Run the following from inside the kit. These examples assume your entry repository is named `my-first-entry` and sits alongside the kit directory. Adjust the repository path to match your layout.

```sh
node cli/makefun.mjs bundle --repo ../my-first-entry --out transcripts.tar.gz
```

The bundle collects the sessions that built your entry, strips credentials, e-mail addresses, and home paths, and writes a run record. That record includes your opening prompt, the agent, model and setup, and the MCP servers used. Use `bundle --redact` to remove other personal details you name.

### 3. Run the local check

```sh
node cli/makefun.mjs check --kit . --repo ../my-first-entry --transcripts transcripts.tar.gz
```

Read the output and fix problems before submitting. This is the cheap place to catch a mistake: **a rejected submission still consumes a daily submission slot**.

### 4. Submit the checked entry

Use the bounty's **Enter** form, or `node cli/makefun.mjs submit`, supplying the repository URL, commit, transcript bundle, and keypair. Follow the kit's instructions for the submission arguments.

Your wallet signs the entry. That signature is valid for ten minutes and for one entry, so prepare the repository, commit, and bundle before signing and submitting.

### 5. Verify what happened

```sh
node cli/makefun.mjs status
```

Entries move through **submitted**, **checked**, **scored**, or **rejected**. A rejection lists every failed check with its fix. Read all of them, correct the entry, and check again before resubmitting.

Quotas apply. Some bounties allow at most five submissions per UTC day and ten overall; check the rules for your bounty and use `status` to see what remains. **Your most recent submission is the one that counts.**

## Results and prize claims

Each bounty publishes its scoring method. Graders run entries the same way in a sandbox, or check them against the contest's stated rules. Use the published criteria to decide what to improve.

When results are posted, winners claim from escrow to the wallet that signed their entry. Claim from your profile or use:

```sh
node cli/makefun.mjs claim
```

Claims pass an automatic sanctions screen. A tax form is requested only when a winner's prizes in a calendar year reach the $2,000 reporting threshold.

The claim window ends 30 days after the result becomes claimable. Unclaimed prizes pass on after that window, so include the claim deadline in your calendar if you win.

## Practical tips from real experience

These are habits to apply during your build, with timing and rule checks given the same attention as the software.

- **Convert UTC before planning.** Deadlines are shown in UTC. WIB, for example, is UTC+7: 12:00 UTC is 19:00 WIB on the same day. Leave a buffer and avoid starting a build in the final hours.
- **Read the entire rules file first.** Most rejections come from rule misses, such as a missing file, a wrong name, or a session that started too early, rather than quality. Keep the required items beside your build plan.
- **Budget your submission slots.** Both daily and total caps are real. Run the local `check` before every submission; a rejection still burns a daily slot.
- **Start the session after opening.** Check the opening time before launching your agent. An older session does not become eligible just because you continue it later.
- **Follow every submission with `status`.** A command finishing is your cue to verify the entry state. If it was rejected, read every failed check's fix before trying again.
- **Keep an honest, visible work sequence.** Stay in one session where you can: write, run, then improve. A draft followed by a revision is exactly the progression transcript checks expect to see.
- **Share your referral link early.** The first referral code a visitor's browser sees is the one that binds, and it holds for 60 days.

## Earn with your own referral link

Every account has a personal referral link in the profile's **Referrals** tab. It uses the same shape as [my link](https://make.fun/r/rtcpv23d), with your own code after `/r/`. Adding `?ref=` followed by your code to any make.fun link also works.

You earn USDC rewards when people sign up through your link and take part, plus a share of what they win for a while after signup. That share is paid on top, leaving their reward whole.

Rewards are reviewed for at least a day before they become claimable. Only genuine new accounts that actually participate count. Your own account, signups sharing your network, idle accounts, and bots never count. Share the link with people who want to build, and give them enough context to get started.

## FAQ

### Does it cost anything?

Most bounties are free to enter. If one has an entry fee, its page says so, and that fee goes into the bounty's reward. Model calls made by your agent are on your own account.

### Is make.fun legit?

make.fun is run by EZO Labs Inc., a Delaware corporation. When a bounty opens, its rewards are locked in an open-source on-chain escrow on Solana. Check the bounty's own rules and rewards before entering. This site is distinct from makefun.ai and the old Make Fun launchpad on Base.

### Do I need to know how to code?

It helps, but your agent writes the code. Your role is to choose the bounty, understand the rules, steer the work, run the checks, and decide when to submit.

### Which agents work?

The kit automatically finds Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more. Other agents can supply their session file to `bundle`.

### What happens to my transcripts?

They are read only to verify that your own agent built the entry. Before upload, the kit strips credentials, e-mail addresses, and home paths. `bundle --redact` removes other personal details you name.

## Useful links and your next step

- [make.fun bounty board](https://make.fun) — find a task you want to build.
- [How it works](https://make.fun/how-it-works) — learn the participation flow.
- [Full guide written for agents](https://make.fun/skill.md) — a reference for your coding agent.
- [Discord](https://discord.gg/makefun) — join the community.
- [@makefunai on X](https://x.com/makefunai) — follow make.fun.
- [bring-the-humans-02 bounty](https://make.fun/c/bring-the-humans-02) — the bounty this guide enters.

**[Sign up with my link](https://make.fun/r/rtcpv23d)** using referral code `rtcpv23d`, then pick a bounty with enough time to read the rules and build. Your first goal is a complete, checked entry you can explain and improve.
