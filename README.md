# Even My Grandma Can Do It

Let AI do the thinking. Handle the simple steps yourself.

A Codex skill for people who use AI for almost everything and want to spend fewer tokens on routine execution. Instead of having an agent run every prepared script, test, commit, and pull request, get clear instructions you can follow yourself.

The name is playful. The guidance should always be patient, respectful, and beginner-friendly.

## How it works

The AI handles work that needs judgment: implementation, debugging, choosing the right tests, and resolving conflicts. When the remaining action is straightforward, it hands you:

1. The exact app or terminal and working directory to use.
2. A copy-ready command or a specific UI action.
3. What a successful result should look like.
4. When to stop and which error details to share.

Small, safe sequences stay in one response so you do not need another chat turn after every command. If you prefer interactive coaching, ask for one step at a time.

## Install

### Ask your agent

With the Codex skill installer available, ask:

```text
Install the skill from https://github.com/masa-rafik/even-my-grandma-can-do-it
```

This repository is private. Your installation environment must have access to it.

### Manual installation on macOS or Linux

You need GitHub CLI (`gh`) installed and signed in to an account with repository access.

1. In your terminal, create the skills parent folder:

   ```sh
   mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
   ```

2. Clone this repository into that folder:

   ```sh
   gh repo clone masa-rafik/even-my-grandma-can-do-it "${CODEX_HOME:-$HOME/.codex}/skills/even-my-grandma-can-do-it"
   ```

   A successful clone creates a folder containing `SKILL.md` and `agents/openai.yaml`. If the destination already exists, stop: the skill may already be installed. Do not delete or overwrite it blindly.

3. Start a new Codex session if the skill is not yet listed, then invoke it as shown below.

## Use

Mention the skill in your request:

```text
$even-my-grandma-can-do-it
Implement the fix, then show me how to run the tests and create the commit myself.
```

Other examples:

```text
$even-my-grandma-can-do-it
The script is ready. Tell me exactly where and how to run it, and what success looks like.
```

```text
$even-my-grandma-can-do-it
Help me push this branch and open a pull request. Give me one step at a time.
```

## What stays with the AI

- Unsolved bugs, implementation decisions, and Git conflicts.
- Diagnosing a failed command before suggesting another attempt.
- Checking that commands match the actual project rather than guessing.
- Explaining risks before destructive, production, or publishing operations.

This is not a refusal-to-work skill. If you explicitly ask the agent to execute the task or finish end-to-end, it should honor that request within its permissions.

## Safety and expectations

Commit guidance should stage only relevant files and review the staged diff. Pull-request guidance should distinguish committing locally from pushing and publishing remotely. Never paste secrets into the chat; share only the relevant, redacted error lines when something fails.

The agent must not claim that a test passed or a PR exists merely because it provided instructions. Results remain unverified until there is evidence.

Token savings depend on the task. The goal is fewer unnecessary tool calls and chat round trips, not a guaranteed reduction or pushing difficult work onto you.

## Repository contents

- [`SKILL.md`](SKILL.md): behavior and handoff rules loaded by the agent.
- [`agents/openai.yaml`](agents/openai.yaml): skill display metadata and a suggested prompt.

This skill provides guidance, not bundled automation scripts. It reuses your project's existing commands and can help prepare a reusable helper when that is genuinely useful.
