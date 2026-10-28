# Setting up sharing (for the AI, version 0.1)

Check `git --version` and `gh auth status`. Offer to install what is missing (on Mac: `brew install git gh`), only with their agreement. Login: `gh auth login --web` opens the browser and shows a short code; if your tool can't show an interactive login, ask the person to run that command themselves. No GitHub account: give them https://github.com/signup and wait.

**Create:** with their agreement, copy their project into `~/Susumiba/<project>`. If it has no git history: `gh repo create <project> --private --template susumiba/template --clone` and bring their files in. If it already has history, keep it: add the template files to it, then `gh repo create <project> --private --source=. --push`. Add the topic `susumiba`. Fill `description.md` with them.

**Invite someone:** only the owner can. Give the owner https://github.com/<owner>/<project>/settings/access and let them click "Add people" with the other person's email or username.

**Join:** `gh api user/repository_invitations`, accept the one for the project with their agreement, then `gh repo clone <owner>/<project> ~/Susumiba/<project>`.

**Then, on this computer only** (after creating and after joining). Anything that makes a tool run commands stays out of the shared files: another member could change it, and it would run on everyone's computer. So these settings are written locally, listed in `.git/info/exclude`, and never sent.
- If your tool asks permission for every command, or can't write in `.git`: offer to allow only the git commands this project needs (`git pull`, `fetch`, `status`, `log`, `add`, `commit`, `push`, and `git config --local susumiba.*`), for this folder, in your tool's local settings. Never full access by default. What it means for the person: no more clicking "allow" for each of these; it changes nothing about what is shared, you still send only what they tell you to.
- If your tool can run a short script before each message: offer live news. Put the script in `.git/susumiba-news.sh` (not shared):
  ```sh
  #!/bin/sh
  git fetch -q 2>/dev/null || exit 0
  new=$(git log --oneline HEAD..@{u} 2>/dev/null)
  [ -n "$new" ] && printf 'Something new just arrived in the project. Pull, then before anything else tell the person what it is, with its content, in a sentence or two:\n%s\n' "$new"
  exit 0
  ```
  and have the tool run `sh "$(git rev-parse --git-dir)/susumiba-news.sh"` before each message.
- If your tool doesn't read `AGENTS.md` by itself: with their agreement, add one line to its own instructions file for this folder: read `AGENTS.md` first.

**Remember their projects** (once, the first time): ask whether you should remember their Susumiba projects so they can talk about them from anywhere. If yes, add to your general instructions (for example `~/.claude/CLAUDE.md` or `~/.codex/AGENTS.md`): "When the person talks about Susumiba or one of their projects, they are in `~/Susumiba/`; read that project's `AGENTS.md`." If no, remember it with `git config --local susumiba.remember no` and don't ask again.

**The clerk with nobody there** (optional, GitHub only): if the project wants its synthesis rebuilt after every push even when no one has a session open, copy https://susumiba.com/actions/clerk.yml to `.github/workflows/clerk.yml`. It needs an Anthropic API key, billed to the owner: the owner adds it themselves as the secret `ANTHROPIC_API_KEY` at https://github.com/<owner>/<project>/settings/secrets/actions. Never take the key in the conversation. Without it, the clerk does nothing and says what is missing.

## What we tested

Hints from our own tests (2026-10-28), not rules; tools change.
- **Claude Code / Claude app, "Code" tab** (2.1.312): default mode is now "auto", which ran a commit without asking. In manual mode, "Yes, and don't ask again" saves to `.claude/settings.local.json` in this folder only, but too narrowly (every `git add`, yet `git commit` only with that exact message): write the permissions yourself, like `"Bash(git commit *)"`. Live news: a `UserPromptSubmit` hook in the same file. Reads `AGENTS.md` through the project's `CLAUDE.md`.
- **Codex** (0.165, CLI and ChatGPT desktop app): its sandbox can't write in `.git` and blocks the network, so it asks for each git command. Its "Allow similar commands" ("don't ask again for commands that start with…") saves to `~/.codex/rules/default.rules`, for the whole computer and only that exact command start: don't use it. Allowed git commands only apply when each runs alone, not chained with `;`, `&&`, `|` or other commands (otherwise everything goes back into the sandbox and fails). What worked: rules like `prefix_rule(pattern=["git", "commit"], decision="allow")` in `.codex/rules/susumiba.rules` inside the project, `.codex/` in `.git/info/exclude`, and the folder trusted (Codex asks "Trust this folder?" when it is opened; or `[projects."<path>"] trust_level = "trusted"` in `~/.codex/config.toml`).
- **Codex in the ChatGPT desktop app:** under the message box, choose "This computer" ("Cet ordinateur"), not "Cloud". Codex on chatgpt.com works in the cloud from GitHub repositories and can't see the person's files.
