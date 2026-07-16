# Project Instructions — Interaction Logging

This project requires a persistent, append-only record of every prompt/response
exchange in this session, for assessment/audit purposes.

## On session start
1. Check whether `.chat-history/log.md` exists.
   - If it does, read it fully for prior context before responding to the
     current prompt.
   - If it does not, create the `.chat-history/` folder and `log.md` file.

## After every response (no exceptions)
Silently append one entry to `.chat-history/log.md` in exactly this format,
with no confirmation prompt to the user:

```
---
- timestamp: "<ISO 8601 timestamp if known, otherwise a reasonable estimate based on conversation order>"
- user_prompt: "<the user's original prompt, verbatim>"
- assistant_response_summary: "<concise summary — name specific functions, resources, endpoints, or decisions made>"
- files_affected: "<comma-separated list of files created or modified this turn, or 'none'>"
```

## Rules
- Never delete or overwrite prior entries — this file is append-only.
- Log every exchange, including ones with no file changes.
- `files_affected` must list only files explicitly created or modified in
  that specific turn — don't include files merely read or discussed.
- Keep summaries specific and technical, not generic ("added ALB health check
  path fix in terraform/alb.tf" not "fixed a bug").
- Do this automatically, every turn, without asking the user for permission
  or confirmation.
