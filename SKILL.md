---
name: even-my-grandma-can-do-it
description: "Save AI tokens by handing routine developer actions to the user with beginner-friendly, copy-ready steps: running prepared scripts, tests, builds, commits, and pull requests. Use for token-saving or DIY guidance and mechanical follow-up after AI work. Not a substitute for debugging, implementation, or an explicit request for agent execution."
---

# Even My Grandma Can Do It

Spend AI effort on judgment; let the user handle straightforward execution. The title is playful, never a reason to patronize the user. Write guidance in the user's language even though this skill is written in English.

## Choose the right handoff

- Default to user execution for a prepared, understandable action with a clear success signal: run an existing script, start a dev server, run a known test/build, open a generated artifact, review a diff, create a scoped commit, or open a pull request.
- Do the work that still needs reasoning: implementation, choosing the right test, preparing a reusable script, interpreting failures, reviewing sensitive changes, and resolving conflicts. Do not hand over an unsolved problem disguised as a simple command.
- Honor an explicit request to execute or finish end-to-end. Do not repeatedly push work back after the user asks you to do it. If they cannot access the terminal or interface, offer an accessible route or perform the authorized action.
- Do not invent chores or scripts just to enable a handoff. Reuse project commands when they exist. Create a small reusable helper only when repetition or complexity justifies it; keep destructive or publishing actions out of automatic helpers.

## Prepare once, explain concretely

Use context already available. Inspect only the minimum missing facts needed to give correct commands: actual project path, script/package command, shell, branch, and relevant prerequisites. Do not scan the whole repository for a routine handoff. Never guess filenames, package managers, test results, remote names, or PR base branches.

Give a short numbered sequence, with one action per step:

1. Say where to act: which app, terminal, and working directory. For terminal commands, provide a separate, shell-appropriate `cd` command using the actual quoted path.
2. Give the exact command in a copyable code block, or the exact visible UI control to click. Avoid unexplained placeholders. If a value is unknown, show how to find it before using it.
3. Explain the expected result briefly: an output marker, exit status, file, browser URL, or visible state. Say when a server is expected to keep running and how to stop it.
4. Give a stop condition: if the result differs or a command fails, stop and share the failed command plus the relevant error lines, with secrets removed.

Keep a small safe sequence in one reply; do not require a new chat turn after every successful command. Pause at a meaningful decision or risk boundary, not after every keystroke. For a beginner who requests interactive coaching, give one step at a time and wait.

Say what remains unverified. User instructions are not evidence of execution: never claim a test passed, a commit exists, or a PR was created until results establish it.

## Workflow-specific safeguards

### Scripts, tests, and builds

Confirm the command exists and describe meaningful side effects. State required setup only when relevant. Do not silently run a command you just assigned to the user. Prefer a short repeatable command over watching verbose output or repeated polling. Ask for a concise result, not entire logs; never request tokens, credentials, or a full environment dump.

### Commits

Start with branch/status and diff review. Stage only explicit task-related paths, then review `git diff --cached` before committing. Account for previously staged unrelated changes; do not commit or unstage them without direction. Provide a suitable commit message. Avoid blanket staging, force operations, resets, and history rewrites. If changes contain secrets, are unexpectedly broad, or conflict, stop and help diagnose.

### Pull requests

Separate local commit, remote push, and PR creation so the user understands what publishes data. Establish the intended remote, head branch, and base branch before giving exact commands. Check for an existing PR to avoid duplicates. Prepare a concise title and body from known changes, marking unrun tests honestly. Use the project's existing CLI or browser flow; do not require installing a tool when an available route suffices. Never instruct bypassing failed checks. Once a user-created PR URL is known, follow any host requirement to register/link it to the thread.

### Risk boundaries

User execution is not a safety loophole. Do not hand over destructive commands, production changes, credential operations, force pushes, merges, or deployments as routine chores. Explain consequences, establish scope and authorization, and use the applicable specialized workflow. For an error, do not suggest blind retries: inspect the relevant evidence, correct the cause, and hand back the next safe action.

## Keep the savings real

Lead with: “You can do this part yourself to save tokens. Here's how.” Adapt naturally to the user's language. Keep the explanation shorter than the task warrants; no lectures about token usage, repeated reminders, speculative token estimates, or unnecessary confirmations. Finish with exactly what result to report only if further AI work depends on it; otherwise let the user finish without another message.
