# sendstack

An open-source email outbound platform. Built as an attempt to recreate something like Instantly.ai — turns out getting emails to reliably land in inboxes is really hard.

**Status: No longer actively maintained.**

## What it does

- Send email campaigns via any SMTP provider (Zoho, Gmail, G-Suite, etc.)
- Campaign grouping & daily send limits
- Link-click + open tracking
- HTML & plain-text templates

## Architecture

```
packages/
├─ email-service/      # crons, workers, DB migrations
├─ graphql-server/     # API consumed by web-app
├─ web-app/            # Next.js front-end
└─ tracking-service/   # Express endpoints for opens/clicks
```

PostgreSQL, pnpm monorepo.

## Setup

```bash
git clone https://github.com/steven4354/sendstack.git
cd sendstack
pnpm install
cp .env.example .env  # fill SMTP keys, DB URL, etc.
pnpm --filter email-service setup:db
```

## Lessons learned

Email deliverability is a deep rabbit hole — domain reputation, warmup, SPF/DKIM/DMARC, content filtering, and more. Building the sending part is straightforward; getting emails into inboxes consistently is the real challenge.
