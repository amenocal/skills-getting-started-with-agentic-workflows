---
name: Update GitHub Info
description: >
  Fetches the latest posts from the GitHub Blog and Changelog,
  updates site/content/github-info.md, and opens a pull request
  for Mona to review.

on:
  schedule:
    - cron: "0 8 * * *"   # daily at 08:00 UTC
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

tools:
  github:
    mode: gh-proxy
    toolsets: [default]
  web-fetch:
  edit:

safe-outputs:
  create-pull-request:
    title-prefix: "[ai] "
    labels: [automation, github-info]
    reviewers: [amenocal]
    draft: false
    if-no-changes: warn
    allowed-files:
      - site/content/github-info.md

network:
  allowed:
    - github.blog
    - github.changelog
    - github.com
    - awesome-copilot.github.com

timeout-minutes: 15
strict: true
---

You are Mona's content assistant. Your task is to update the GitHub info page
with the latest news from the GitHub Blog and Changelog, then open a pull
request for Mona to review.

## Step 1 — Read editorial guidelines

Read `notes/mona-notes.md` to understand Mona's editorial preferences before
making any changes.

## Step 2 — Gather the latest GitHub news

Fetch both sources and identify the most recent, developer-relevant updates:

- Web-fetch **https://github.blog/latest/** — latest GitHub Blog posts.
- Web-fetch **https://github.blog/changelog/** — latest GitHub Changelog entries.
- Web-fetch **https://awesome-copilot.github.com/workflows/** — curated community agentic workflows.

Focus on items that are practical and help developers learn or use GitHub faster.
Skip marketing announcements that have no direct developer impact.

## Step 3 — Update site/content/github-info.md

Edit `site/content/github-info.md`:

- Replace or extend the **"Latest GitHub Updates"** section with a concise,
  up-to-date list of the most relevant recent items you found.
- Each entry should be a short bullet: a bold title followed by one sentence
  describing the change and why it matters to developers.
- Always note the source (GitHub Blog, GitHub Changelog, or Awesome Copilot Workflows) at the end of each
  bullet.
- Follow Mona's editorial guidelines from `notes/mona-notes.md` throughout.
- Do **not** modify any other section of the file.

## Step 4 — Open a pull request

Create a pull request with your changes so Mona can review before anything
goes live. Use a clear, descriptive title that mentions that it is a website update, today's date and the
sources you pulled from.
