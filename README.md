# lazy-coder

A minimal `AGENTS.md` that makes AI coding agents write less code, faster, without sacrificing safety.

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

**"Generate a unique ID."**

Without lazy-coder your agent installs `uuid`, imports it, wraps it in a helper:

```js
import { v4 as uuidv4 } from 'uuid';

export function generateId() {
  return uuidv4();
}
```

With lazy-coder:

```js
crypto.randomUUID()
```

Built into every modern runtime — browsers, Node 19+, Deno, Bun. No package, no wrapper.

---

**"Deep clone this object."**

Without lazy-coder your agent writes a recursive clone function with circular reference handling:

```js
function deepClone(obj, seen = new WeakMap()) {
  if (obj === null || typeof obj !== 'object') return obj;
  if (seen.has(obj)) return seen.get(obj);
  const clone = Array.isArray(obj) ? [] : {};
  seen.set(obj, clone);
  for (const key of Object.keys(obj)) {
    clone[key] = deepClone(obj[key], seen);
  }
  return clone;
}
```

With lazy-coder:

```js
structuredClone(obj)
```

Native since 2022. Handles circular refs, dates, maps, sets, array buffers — all the edge cases the hand-rolled version missed.

---

**"Add copy-to-clipboard on this button."**

Without lazy-coder your agent installs `clipboard.js`, initialises it, binds events, and adds fallback for older browsers:

```js
import ClipboardJS from 'clipboard';

const clipboard = new ClipboardJS('.copy-btn');
clipboard.on('success', (e) => { /* show tooltip */ e.clearSelection(); });
clipboard.on('error', (e) => { /* fallback: select + prompt */ });
```

With lazy-coder:

```js
btn.onclick = () => navigator.clipboard.writeText(text);
```

One line. The Clipboard API is native and available in all modern browsers.

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

Most AI agents over-build by default. They add abstractions you didn't ask for, install dependencies for things the platform already handles, and generate boilerplate to feel thorough. The ladder short-circuits this by forcing a priority check before any code is written.

The key insight: the rules explicitly carve out safety — input validation, error handling, security, accessibility are never lazy. A bare "write short code" prompt drops safety. This doesn't.

## License

MIT
