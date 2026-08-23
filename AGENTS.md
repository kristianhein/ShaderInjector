# Repository Agent Instructions

## Shader compilation scope

Standalone `dxc` may be used only for disposable syntax validation: write to an explicitly temporary output inside the workspace, remove that output afterward.

## Keep routine Git requests fast

When the user asks to create a branch, commit, and/or push existing work:

1. Treat the request as authorization for the named Git operations.
2. Use `git`, not `gh`. Do not run `gh auth status`, browse GitHub, invoke a GitHub publishing workflow, or open a pull request unless the user explicitly asks for it.
3. Do not compile, rebuild, format, or otherwise modify project files merely to commit existing work. Only run validation when the user asks for it or when new code was implemented in the same request.
4. Inspect `git status --short` and a concise diff or diff stat once. Preserve unrelated changes and stage only the intended paths explicitly; never use `git add -A` or `git add .` in a dirty worktree.
5. On this Windows workspace, Git metadata writes may be blocked by the sandbox. For `git switch -c`, `git add`, `git commit`, and `git push`, request the required escalation immediately instead of first attempting a command that is expected to fail.
6. Push with plain `git push -u origin <branch>`. If authentication actually fails, then diagnose authentication outside the restricted sandbox. Do not preflight authentication.
7. Use a concise commit message inferred from the diff when the user does not provide one.
8. Report only the branch name, commit hash/message, push result, and whether uncommitted changes remain.
