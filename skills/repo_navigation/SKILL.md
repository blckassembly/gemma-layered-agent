# Skill: Repository Navigation

How the agent moves through an unseen repository without wasting
tokens or losing the thread.

## Procedure
1. **Start from the issue's nouns.** Extract the feature names, error
   strings, and identifiers in the issue. Search for those exact
   strings first — they are the cheapest map of the relevant code.
2. **Read the test files early.** Tests state expected behavior in
   executable form. The failing area's tests are the fastest route to
   the module map.
3. **Follow imports, not folders.** From an entry file, walk its import
   graph two levels deep. Folder browsing is a last resort.
4. **Keep a read ledger.** Note every file read and the one fact taken
   from it. Never re-read a file already in the ledger unless a check
   result contradicts the fact recorded.
5. **Stop conditions.** Investigation ends when the analyzer can name:
   the suspect files, the relevant tests, and at least one piece of
   direct evidence per claim — or can state precisely what remains
   unknown.

## Anti-patterns
- Reading the whole tree "to get oriented" (burns the token budget
  before the thesis exists).
- Opening generated, vendored, or lock files unless the issue names them.
- Guessing a module's behavior from its name instead of reading it.
