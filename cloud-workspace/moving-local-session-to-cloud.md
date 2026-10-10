# Moving a local Claude Code session to the cloud

A cloud session can't open a local chat's history directly. It starts from a
fresh clone of a GitHub repo, so the way across is to put everything in the repo.

1. **Create the GitHub repo** (empty or with a README).
2. **In the local session**, ask Claude to:
   - write a `HANDOFF.md` (or `CLAUDE.md`) covering the goal, decisions made,
     current state, what's left to do, and any gotchas;
   - `git init` (if needed), add the new repo as `origin`, commit everything,
     and push.
3. **Make sure the Claude GitHub App can access the new repo**:
   https://github.com/apps/claude/installations/select_target
4. **Start a cloud session** at https://claude.ai/code and pick the new repo
   (and an environment).
5. **First message in the cloud session:** "Read HANDOFF.md and CLAUDE.md and
   continue from where we left off."

Tips:
- `CLAUDE.md` is loaded automatically in every session, so put lasting
  project context there and session-by-session notes in `HANDOFF.md`.
- Don't commit secrets. Put API keys in the cloud environment's settings instead.
- Raw transcripts are stored locally under `~/.claude/projects/<project>/*.jsonl`.
  You *can* copy one into the repo for reference, but a written summary is
  usually more useful and much smaller.
- From the local CLI, `claude --remote "<task>"` (or `& <task>` inside a session)
  starts a cloud session on the current repo, if your version supports it.
