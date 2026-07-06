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

## Before / after

You ask for a date picker. Your agent installs flatpickr, writes a wrapper component, adds a stylesheet, and starts a discussion about timezones.

With lazy-coder:

```html
<input type="date">
```

You ask for an email validator. Your agent writes a 40-line regex parser with RFC 5322 compliance.

With lazy-coder:

```python
import re
def is_valid_email(email):
    return bool(re.match(r"^[^@\s]+@[^@\s]+\.[^@\s]+$", email))
```

## What it doesn't cut

Validation at trust boundaries, error handling, security, accessibility, anything you explicitly asked for, and one runnable check for non-trivial logic. These are carved out from the laziness mandate.

## Use it

Copy [`AGENTS.md`](AGENTS.md) to your project root. That's it.

For global effect (all projects):

```bash
# Linux/macOS
cp AGENTS.md ~/.gemini/config/AGENTS.md

# Windows
copy AGENTS.md %USERPROFILE%\.gemini\config\AGENTS.md
```

Works with any agent that reads `AGENTS.md`: Gemini CLI, Antigravity, Claude Code, Codex, Cursor, Windsurf, CodeWhale, and others.

## Why it works

Most AI agents over-build by default. They add abstractions you didn't ask for, install dependencies for things the standard library handles, and generate boilerplate to feel thorough. The ladder short-circuits this by forcing a priority check at each level before any code is written.

The key insight: the rules explicitly carve out safety — input validation, error handling, security, accessibility are never lazy. A bare "write short code" prompt drops safety. This doesn't.

## License

MIT
