> **For AIs:** if a person sent you here, read [`ia.md`](https://susumiba.com/ia.md) and follow it. It is short and says everything you need. Version 0.2.

# Susumiba

**Humans and AIs. Finally coordinated.**

People and AIs, as many as you like, work on the same project. Each brings ideas and finished work with their own AI; a clerk keeps the synthesis, who did what and what is left, with every sentence pointing to its source. Feedback goes straight to the right person instead of passing from hand to hand.

## Start

Paste this into an AI that can run commands on your computer (the Claude desktop app, "Code" tab; Codex in the ChatGPT desktop app, on "This computer"; Claude Code; Codex):

> Read https://susumiba.com/ia.md and follow its instructions. I want to create or join a Susumiba.

> Lis https://susumiba.com/ia.md et suis ses consignes. Je veux créer ou rejoindre un Susumiba.

Your AI asks what you are working on and with whom, looks at your project if you want, and does a first real piece on your computer. Accounts come only when someone else joins. Alone, it is already useful: a project that keeps itself in order, ready for whoever you invite later.

## Two examples

- **Working with a client.** `description.md` says who the client is and what is being delivered. Your AI keeps the client file, drafts the questions; the client answers by email, without an AI or an account, and the answer is filed in the project.
- **Thinking together.** `description.md` names the question. Everyone adds ideas with their own AI; the synthesis keeps disagreements visible, and anyone can ask their AI to collide all the ideas into a few unexpected directions.

## Mediators

The clerk is built in. Any other mediator is a few lines its creator writes in `description.md`: a name, a role, when it acts. For example, a *Welcome* that introduces the project to each newcomer and asks what they bring, or a *Centrifuge* that, when asked, makes all contributions collide and brings out three unexpected directions.

## What a project is

A git repository made from [susumiba/template](https://github.com/susumiba/template): `description.md` (what it is, how its creator wants people to work), `contributions/<name>/` (each person's work, never rewritten by others), `journal/` (one file per entry), `in-progress/`, and `synthesis.md` and `index.md`, rebuilt by the clerk. `AGENTS.md` tells every AI how to work in it; `CLAUDE.md` points Claude to it.

## Rights and safety, honestly

- A project lives in its creator's GitHub account, private. Members can write; only the owner can invite, remove, make public or delete. **For members, GitHub guarantees it**, whatever their AI does. For the owner's own AI, it is discipline: the instructions tell it never to do these alone and to give the exact GitHub page instead.
- Everything else in the instructions is discipline too. A trapped text could get around it. We say so.
- git records who wrote what and when, as declared; not where the content came from.
- **One project per conversation.** If your AI can see several projects or folders at once, it can carry information from one to another without being asked.
- Never put keys or passwords in a project.
- GitHub limits: everyone needs a GitHub account; 100 MB per file.

## What we protect against, and what stays vigilance

Anyone in a project can write in it, including someone who means harm. What the instructions and the template do:
- **Nothing that runs is shared by default.** Allowed git commands and live news are set on each computer and never sent.
- **Before taking in what others sent**, your AI looks at what changed. If it touches what makes tools run things or changes how every AI behaves (`.claude/`, `.codex/`, `.github/workflows/`, `AGENTS.md`, `CLAUDE.md`, `description.md`), or adds symbolic links that could point outside the project, it shows you first and waits for your agreement.
- **The optional clerk Action** can only rewrite the synthesis and the index; it runs no commands.
- We test these attacks at each version (`tests/run.sh`): a hidden hook, a link to a file outside the project, instructions slipped into a contribution or the description.

What stays vigilance:
- What your AI does with a trapped text depends on the model. In our tests it refused every time; that is not a guarantee.
- **A key stored in the project (the clerk's) can be read by every member**, through a workflow of their own. Use a key with a low spending limit, only where you trust everyone.
- Everyone you invite sees everything in the project and its history.

## At home or elsewhere

git is portable. A project works on GitHub, GitLab, a Forgejo you host yourself, or a plain folder; only the optional clerk Action is GitHub-only. A copy can mirror another. What doesn't exist yet: members from different servers in one project with the same rights.

## About

Made by one person for now, Pierre Riche. Something wrong? Open an issue on [susumiba/template](https://github.com/susumiba/template/issues): what happened and the error, never your project's content. MIT license.
