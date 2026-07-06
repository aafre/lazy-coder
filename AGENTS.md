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
