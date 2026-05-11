---
title: Mole
slug: mole
order: 2
summary: A local Mac maintenance tool. Start by seeing where disk space went, then preview cleanup for dev caches, installers, app leftovers, and temporary files.
section: tools
section_title: Tools
section_order: 28
source_url: https://github.com/tw93/Mole
---

# Mole

`Mole` is a local Mac maintenance tool.

We recommend it not because you should delete everything with one command, but because it helps you understand your local environment first: what is using disk space, which caches are safe to review, and which project artifacts are no longer useful.

<h2 id="what-is-mole">What Mole Is</h2>

If you use a Mac for development, design, or content work, disk space gets eaten slowly.

Common causes include:

- Xcode, simulators, Node, npm, and browser caches
- installer files sitting in Downloads
- app preferences, launch agents, and cache leftovers after uninstalling apps
- old project build artifacts
- uncertainty about what is safe to delete

`Mole` puts these maintenance actions into one command-line tool. It can analyze disk usage, preview cleanup, clean development caches, find installer files, uninstall apps, and show system status.

<h2 id="why-recommend">Why We Recommend It</h2>

AI coding does not only happen in the cloud. Your local environment affects the experience too.

When disk space is tight or caches are messy, many problems get harder to reason about: slow installs, slow builds, dependency errors, simulator bloat, or a laptop that constantly spins up.

`Mole` helps you see the problem first, then decide whether cleanup is actually needed.

<h2 id="safe-start">Start with Safe Preview</h2>

For your first run, do not start with `mo clean`.

Use this order:

```bash
mo analyze
mo clean --dry-run
mo purge --dry-run
```

- `mo analyze`: see where disk space went
- `mo clean --dry-run`: preview system and dev cache cleanup without deleting
- `mo purge --dry-run`: preview project artifact cleanup without deleting

Read the output first, then decide whether to run the real cleanup.

<h2 id="install">Install</h2>

Use Homebrew:

```bash
brew install mole
```

After installation, start with help:

```bash
mo --help
```

<h2 id="common-commands">4 Common Commands</h2>

### Analyze Disk Usage

```bash
mo analyze
```

Best for the first run. It helps you see where the space went.

### Preview Cleanup

```bash
mo clean --dry-run
```

Use this before cleaning. Do not skip `--dry-run`.

### Preview Project Artifact Cleanup

```bash
mo purge --dry-run
```

Useful if you work across many projects and want to review old build artifacts.

### Check System Status

```bash
mo status
```

Use it to inspect CPU, memory, disk, network, and system health.

<h2 id="when-not-to-use">When Not to Use It</h2>

Do not run real cleanup immediately if:

- you do not understand the `--dry-run` output
- you are working on an important project without committing or backing up
- you are unsure whether a directory is required by a project
- you only want to see how much you can delete

Pause and ask AI to explain the `--dry-run` output first. Keep what you do not understand.

<h2 id="ai-workflow">How It Relates to AI Coding</h2>

Some AI coding problems look like model problems, but are actually local environment problems.

For example:

- dependency installation is slow
- builds fail in strange ways
- disk space is low
- simulators and caches fill the drive
- old build artifacts confuse debugging

`Mole` does not write code for you, but it helps keep your local development environment clearer, lighter, and easier to reason about.

<h2 id="common-issues">Common Issues</h2>

- Can I run `mo clean` directly?
  Not for the first run. Start with `mo clean --dry-run`.
- Can I use `mo uninstall` directly?
  Only after confirming the app and reviewing what leftovers will be removed.
- Does it work on Windows?
  Mole is mainly for macOS.
- How is it related to CleanMyMac or AppCleaner?
  It covers some similar needs, but is more command-line oriented and developer-friendly.
