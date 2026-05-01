# Trial Task — PR Review Agent

- **Time:** 6 hrs cap. Stop at the cap.
- **Stack:** Python or TypeScript/JavaScript — your choice. Any agent framework. Any LLM.
- **Deliverable:** GitHub repo + link to a real PR where your agent ran end-to-end.
- **Using AI to do the task?** OK, actually preferred and encouraged. BUT you will defend architecture decisions live at the interview. Not variable names. Architecture and design intent. Make sure you understand what you ship.

---

## Goal

Build an agent that takes one PR URL. Agent goes to GitHub, reviews the PR, leaves real comments, and assigns real reviewers with comments to each one explaining what to focus on.

That's it. Real GitHub writes — not a stdout simulation.

---

## How we test

```bash
python main.py https://github.com/<org>/<repo>/pull/<n> --mode conservative
# or
node index.js https://github.com/<org>/<repo>/pull/<n> --mode aggressive
```

One positional arg: the PR URL.
One flag: `--mode conservative|aggressive`.

We will run your agent against a PR in our test repo and watch GitHub live to see what it does.

---

## What the agent must do

- Read the PR (diff, files, metadata) via the GitHub API
- Reason about the changes using an LLM
- Decide: auto-approve OR escalate to humans
- If auto-approve: leave a summary comment and approve
- If escalate: pick reviewers, assign them on GitHub, and leave each one a comment explaining what to look at — citing specific files, lines, or findings (not generic "please review")
- Both modes (`conservative`, `aggressive`) must work and produce visibly different behavior — bias toward escalation vs auto-approval

---

## Hard requirements

1. **Real GitHub writes.** Actual review comments. Actual reviewer assignments. Actual approve action when warranted. No stdout simulation.
2. **Handle large PRs.** PRs in our test set may go up to **5,000 additions / 5,000 deletions**. Don't choke on big diffs.
3. **Mode flag works.** `--mode conservative` and `--mode aggressive` produce meaningfully different decisions.
4. **Clear LLM observability.** For every LLM call, we must be able to see: the prompt sent, the model used, the output received, token usage, latency. Use whatever you prefer — but we need to *see* what the model saw and what it returned. This matters.

---

## Submission

1. **Repo link** — public, or invite `@us-asad`
2. **Link to one real PR where your agent ran end-to-end.** We will click it and read the comments and assignments your agent left. This is the truth of whether your agent works.
3. **README** Include a `README.md` that explains how to install, configure, and run your agent.
4. *(Optional)* Note which AI tools you used while building

---

## What we are judging

- Quality of the comments your agent leaves on the real PR you submit
- Architectural choices (we will ask you about them)
- LLM call observability
- How you handle ambiguity in this spec
- Code quality

We will check your code. We will click your demo PR. We will run your agent on a fresh PR of ours. Then we'll talk.
