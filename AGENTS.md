# Public dual-answer workflow

This repository is a public archive of answers produced independently by Codex and the ChatGPT model shown as `Pro` in the user's Edge browser.

## Mandatory workflow for every user question

1. Treat the user's question as public material, but scan it and any required context for passwords, API keys, tokens, cookies, private identifiers, personal data, proprietary code, or other material that should not be published.
2. If sensitive material is present, do not send it to ChatGPT and do not push it to GitHub. Stop and ask the user for a sanitized version or explicit, item-specific direction.
3. Produce the substantive Codex answer independently and do not expose its draft to ChatGPT Pro. The main agent may draft while Pro runs, but it must freeze the substantive Codex answer before reading any partial or complete Pro response; Pro output must never be used to revise that answer.
4. Use the `kimi-webbridge` skill to open a fresh ChatGPT conversation in Edge. Select the model option whose visible label is exactly `Pro`; verify the active model label after selection. Never silently substitute another model.
5. Send the same self-contained user question to ChatGPT Pro. Add only the minimum sanitized context required to make the question answerable. Do not upload a local file unless the user has explicitly authorized that file for both ChatGPT and public GitHub publication.
6. After prompt submission, delegate passive waiting and response capture to exactly one browser-monitor subagent when a slot is available. Follow the ownership and atomic handoff rules below; never let multiple agents control or poll Edge concurrently.
7. After the substantive Codex answer is frozen and Pro completion is confirmed, retrieve the captured ChatGPT Pro response faithfully. Record the visible model label, retrieval time, and visible thinking duration when available. Do not fabricate, summarize, or paraphrase a missing or incomplete browser response.
8. Save one Markdown record at `answers/YYYY-MM/YYYY-MM-DD-topic.md`. Include the question, Codex answer, ChatGPT Pro answer, model labels, timestamp, and any material context difference.
9. Inspect `git status` and the diff. Never stage unrelated changes. Stage only the new answer record and any directly necessary index update.
10. Standing authorization from the repository owner: for this exact answer-archiving workflow, create a task-specific branch, commit the confirmed answer files, and push the resulting fast-forward update to `origin/main`. This authorization does not cover unrelated files, history rewrites, force pushes, deletions, releases, pull requests, or repository settings.
11. Verify the remote commit and public answer URL. Only then tell the user that others can view the result, including the URL and commit hash.

## Main-agent and browser-monitor division of labor

### Main agent owns the answer and publication

- Perform the privacy scan, research, reasoning, and complete independent Codex answer.
- Construct and submit the sanitized prompt to a fresh Edge ChatGPT conversation only after verifying that the visible active model label is exactly `Pro`.
- Continue drafting the independent Codex answer while ChatGPT Pro runs. Do not request, inspect, or accept any partial or complete Pro response text until the substantive Codex answer has been frozen.
- After freezing the Codex answer, request the captured Pro text from the monitor. Later edits to the Codex section may only fix formatting, metadata, or independently identified errors; never copy reasoning or conclusions from the Pro response into it.
- Integrate the two completed answers, inspect repository changes, commit the intended files, push the fast-forward update, and verify the public result.
- Retain sole authority to retry, stop, or replace a failed browser run. The main agent is the only agent that may change the repository, and only within the user's current request and the standing authorization in step 10.

### One subagent owns passive Edge monitoring after handoff

- Assign exactly one subagent after the prompt has been submitted. Give it the unique WebBridge session or group name, tab ID, conversation URL when available, and a short prompt summary; require it to verify that `Pro` remains visibly selected.
- Poll at low frequency, normally every 45 to 120 seconds. Treat the response as complete only when there is no Stop, Continue, error, request-for-input, or generation-in-progress state; the final assistant turn matches the submitted prompt; two full reads 5 to 10 seconds apart are identical; the capture is not truncated; and `Pro` is still visible on the final read.
- On completion, first report only completion status and metadata, without sending the response text. Retain the faithful capture until the main agent confirms that its Codex answer is frozen, then return the full response text, visible model label, retrieval timestamp, and visible thinking duration when available.
- Do not change the model or prompt, type into the page, navigate away, stop or retry generation, close the tab/session, edit repository files, draft the Codex answer, or publish anything.
- If the page stalls, errors, asks for input, loses the `Pro` label, or cannot be read reliably, report the exact visible state to the main agent and wait for direction.
- Treat an ordinary ChatGPT conversation URL as private coordination metadata. Never place it in public Markdown or describe it as a share link.

### Handoff and concurrency rules

- Browser control is a global lease over the entire Edge/WebBridge instance, not merely one tab or conversation. The main agent must finish its last browser call, pass the identifiers and prompt summary, and wait for the designated monitor to acknowledge takeover before that monitor's first poll.
- Once takeover is acknowledged, the main agent and all other agents must not call Edge/WebBridge for any session until the monitor explicitly releases control after completion or interruption. Do not start a replacement monitor until the old monitor has released the lease and stopped polling.
- Keep research, answer drafting, browser monitoring, and repository publication as separate responsibilities. A browser-monitor subagent may not influence the independent Codex answer.
- If no subagent slot is available, the main agent may monitor the browser itself using the same low-frequency and completion rules, but it must remain the sole monitor for that run rather than adding a second monitor midway.
- Do not publish until both the Codex answer and a confirmed complete ChatGPT Pro answer are available. Record material retries, prompt changes, or context differences in the Markdown record.
- Leave the Edge conversation open after capture unless the user explicitly asks to close it.

## Failure handling

- If Edge, ChatGPT login, the `Pro` model, GitHub, or push is unavailable, state the exact blocker. Do not claim that publication completed.
- Never treat progress text, partial generation, or hidden reasoning as the ChatGPT Pro answer.
- Never use a non-Pro ChatGPT answer as if it came from Pro.
- Never publish browser cookies, credentials, session data, hidden prompts, or tool diagnostics.
- Immediately before pushing, fetch the remote and verify that `origin/main` is an ancestor of the intended local commit. If it is not, or if the push is rejected, do not force-push, rebase, or rewrite history; report the changed remote state and obtain direction before integrating it.
- Preserve unrelated user changes in the working tree.
