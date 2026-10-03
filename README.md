# Beeper Companion

Beeper Companion sits beside Beeper Desktop on your Mac. It sees what's waiting on you across every chat network, drafts replies in your voice with the coding agent you already pay for, and puts them in Beeper's compose box for you to send. It never sends a message unless you click Send.

This is a closed alpha for friends. It runs on Macs with Apple silicon, on macOS 13 or later, and has been tried on macOS 26 and 27.

## What you need first

1. **Beeper Desktop**, signed in: [beeper.com/download](https://www.beeper.com/download).
2. **Beeper's local API turned on.** In Beeper, open Settings → Integrations and switch on "Allow connections" under "Beeper Desktop API". Companion can't flip this for you. Its first-run window tells you if it's still off.
3. **A coding agent, installed and signed in:** [Claude Code](https://claude.com/claude-code) or Codex. Companion runs it to read and draft, and the work counts against that agent's subscription.

## Install

1. Download [Beeper-Companion-arm64.zip](https://github.com/coordinationresearch/companion-releases/releases/latest/download/Beeper-Companion-arm64.zip).
2. Open it, then open **Beeper Companion**. macOS asks whether to open an app downloaded from the internet. Click Open.
3. Companion moves itself into your Applications folder and opens again from there.
4. The first-run window walks you through the rest:
   - **Beeper's approval.** Beeper shows a dialog asking whether to let Companion connect. Set "Expires in" to **Never** (it defaults to 30 days), leave "Allow sensitive actions" on, and click Approve. If you keep 30 days, Companion asks you to approve again when it runs out. That's one click.
   - **Accessibility** (required): lets Companion see which chat Beeper has open. On macOS 27, it's listed under Privacy & Security as "Device Control and Data Access".
   - **Full Disk Access** (optional): lets Companion read Contacts and your Messages history, to name chats and know who you talk to. Without it, the window says what's missing.
   - It shows the agent it found, and installs the beeper-assistant skill into that agent. The skill lets the agent read and draft in Beeper from your terminal too. Used that way, it needs Node and the Beeper CLI (`brew install beeper/tap/cli`, which needs [Homebrew](https://brew.sh)). The app itself needs neither.
5. It ends on Home: what you've let drop, with replies already written.

## Updates

Companion checks for a new version every few hours and downloads it in the background. It restarts itself into the new version once your Mac has sat idle for 15 minutes, and never while it's writing a draft. To update sooner, use **Restart to Update** in the menu bar menu. **Check for Updates** in the same menu checks right away.

## What it does on its own, and how to stop it

**Agent Drafts are on.** When a chat needs a reply, Companion writes a draft into that chat's compose box in Beeper. It never sends. To turn this off, open Settings → Background and switch off **Agent Drafts and automatic Briefs**.

**It reports counts, never text.** Beeper Companion sends its developers a short report once a day and when something keeps failing. It holds counts and settings, such as which permissions are on and how many drafts it placed, and never a message, a name, or a Chat. Settings → **Send Diagnostics** turns it off, and Settings → **Send Report…** sends one now.

## What it keeps on your Mac

Everything lives in `~/Library/Application Support/Beeper Companion/`. Nothing below leaves your Mac, except the count report above.

- **The Store** (`companion.db`) keeps the full text of every prompt Companion sent your agent and every reply it got back, so you can see why it drafted what it did. To delete it, quit Companion (menu bar → Quit Beeper Companion), then delete `companion.db`, `companion.db-wal`, and `companion.db-shm`.
- **The Message Corpus** (`corpus.db`) is a copy of the messages you've sent and received on every network, with the people behind them. Companion uses it to find what you dropped and to answer questions about your history. To delete it, open Settings → Message Corpus and click **Delete Message Corpus…**. It's built again only if you turn it back on.

## Uninstall

Quit Companion, drag it from Applications to the Trash, and delete `~/Library/Application Support/Beeper Companion/`. Then remove the beeper-assistant skill from your agent's skills folder.

## Something wrong?

Tell Chappy, and use **Send Report…** in Settings so he gets the counts. Mention which version you're on: the menu's **Check for Updates** line shows it.
