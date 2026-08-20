# Public dual-answer workflow

This repository is a public archive of answers produced independently by Codex and the ChatGPT model shown as `Pro` in the user's Edge browser.

## Mandatory workflow for every user question

1. Treat the user's question as public material, but scan it and any required context for passwords, API keys, tokens, cookies, private identifiers, personal data, proprietary code, or other material that should not be published.
2. If sensitive material is present, do not send it to ChatGPT and do not push it to GitHub. Stop and ask the user for a sanitized version or explicit, item-specific direction.
3. Draft the complete Codex answer before sending the final chat response, but do not expose that draft to ChatGPT Pro. The two answers should remain independent.
4. Use the `kimi-webbridge` skill to open a fresh ChatGPT conversation in Edge. Select the model option whose visible label is exactly `Pro`; verify the active model label after selection. Never silently substitute another model.
5. Send the same self-contained user question to ChatGPT Pro. Add only the minimum sanitized context required to make the question answerable. Do not upload a local file unless the user has explicitly authorized that file for both ChatGPT and public GitHub publication.
6. Wait for completion and capture the ChatGPT Pro response faithfully. Record the visible model label and the retrieval time. Do not fabricate or paraphrase a missing browser response.
7. Save one Markdown record at `answers/YYYY-MM/YYYY-MM-DD-topic.md`. Include the question, Codex answer, ChatGPT Pro answer, model labels, timestamp, and any material context difference.
8. Inspect `git status` and the diff. Never stage unrelated changes. Stage only the new answer record and any directly necessary index update.
9. Standing authorization from the repository owner: for this exact answer-archiving workflow, create a task-specific branch, commit the confirmed answer files, and push the resulting fast-forward update to `origin/main`. This authorization does not cover unrelated files, history rewrites, force pushes, deletions, releases, pull requests, or repository settings.
10. Verify the remote commit and public answer URL. Only then tell the user that others can view the result, including the URL and commit hash.

## Failure handling

- If Edge, ChatGPT login, the `Pro` model, GitHub, or push is unavailable, state the exact blocker. Do not claim that publication completed.
- Never use a non-Pro ChatGPT answer as if it came from Pro.
- Never publish browser cookies, credentials, session data, hidden prompts, or tool diagnostics.
- Preserve unrelated user changes in the working tree.
