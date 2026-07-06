# lazy-coder

A minimal `AGENTS.md` that makes AI coding agents write less code, faster, without sacrificing safety.

**19 lines. No plugin. No install. No dependencies.**

## What it does

Gives your AI agent a 7-rung decision ladder to climb before writing any code:

1. Does this need to exist? (YAGNI) → skip it
2. Already in the codebase? → reuse it
3. Standard library does it? → use it
4. Native platform feature? → use it
5. Installed dependency? → use it
6. One line? → one line
7. Only then → minimum code that works

The agent reads the problem first, *then* climbs. Lazy about the solution, never about understanding.

## What it doesn't cut

Validation at trust boundaries, error handling, security, accessibility, anything you explicitly asked for, and one runnable check for non-trivial logic. These are carved out from the laziness mandate.

## Use it

Copy [`AGENTS.md`](AGENTS.md) to your project root. That's it.

For global effect (all projects):

```
# Linux/macOS
cp AGENTS.md ~/.gemini/config/AGENTS.md

# Windows
copy AGENTS.md %USERPROFILE%\.gemini\config\AGENTS.md
```

Works with any agent that reads `AGENTS.md`: Gemini CLI, Antigravity, Claude Code, Codex, Cursor, Windsurf, CodeWhale, etc.

## Origin

Distilled from [ponytail](https://github.com/DietrichGebert/ponytail) by analyzing which parts of its plugin carry the actual behavioral weight. The full ponytail plugin ships 6 skill files, mode levels, audit/review commands, and a benchmark suite. This repo keeps only the load-bearing ideas:

- The decision ladder (the core mechanism)
- "Understand first" guard (prevents wrong-problem laziness)
- Root-cause bug fix rule
- Explicit non-negotiables (what makes it safe — a bare "be terse" prompt drops safety)
- Minimal test obligation
- Edge-case correctness preference

Everything else (mode switching, comment conventions, display commands) is UI chrome that doesn't change what code gets written.

## License

MIT
