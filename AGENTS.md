# Lazy senior dev rules

Lazy = efficient, not careless. The best code is the code never written.

Before writing any code, stop at the first rung that holds:

1. Does this need to be built at all? (YAGNI)
2. Does it already exist in this codebase? Reuse it.
3. Does the standard library do this? Use it.
4. Does a native platform feature cover it? Use it.
5. Does an already-installed dependency solve it? Use it.
6. Can this be one line? Make it one line.
7. Only then: write the minimum code that works.

The ladder runs after you understand the problem — read the task and the code it touches, trace the flow end to end, then climb. A small diff you don't understand is just a second bug.

Bug fix = root cause, not symptom. Fix the shared function once — grep every caller — not just the reported path.

Rules: no unrequested abstractions, no avoidable dependencies, no unsolicited boilerplate. Deletion over addition. Boring over clever. Fewest files. Shortest working diff wins. Pick the edge-case-correct option when two approaches are the same size.

Not lazy about: understanding the problem, input validation at trust boundaries, error handling that prevents data loss, security, accessibility, anything explicitly requested. Non-trivial logic leaves one runnable check behind (an assert-based self-check or one small test, no frameworks).

## Python (when editing .py files)

Google Python style. If the project configures ruff, run `ruff format . && ruff check --fix .` and fix every finding; don't restate or fight the linter.

- Docstrings on public modules, classes and functions. One-line summary ending in a period, then only the sections that apply. Say what it means, not the type the annotation already states. Classes document public attributes under `Attributes:`.

  ```python
  def fetch_rows(table: str, keys: Sequence[str]) -> dict[str, Row]:
      """Fetches rows from a table by key.

      Args:
          table: Name of the table to read.
          keys: Row keys to fetch. Missing keys are skipped.

      Returns:
          Map of key to row, for keys that were found.

      Raises:
          IOError: The table could not be read.
      """
  ```
- Imports: `import x` for packages and modules; `from x import y` only when `y` is a module (`typing` and `collections.abc` names exempt).
- Exceptions: raise built-ins (`ValueError`) for bad input. Catch the narrowest exception with the smallest `try`. Never `assert` to validate input; asserts belong in tests and self-checks.
- No getters or setters wrapping an attribute; make it public. Properties only for cheap, obvious computation.
- Module-level function over `@staticmethod`; `@classmethod` only for alternate constructors.
- No metaclasses, `__getattr__` tricks, import hooks or dynamic class creation.
- No mutable module-level state.
- Comprehensions: one `for`, at most one `if`; otherwise a loop.
- `if x is None:` when `0` or `""` is a valid value; implicit false (`if items:`) otherwise.
- Annotate public functions. `X | None`, not `Optional[X]`.
- Comments say why, not what. TODO: `# TODO: <link> - <what>`.
