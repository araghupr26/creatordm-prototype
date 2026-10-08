# creatordm-prototype changelog

Generated from the git history of this repository. Live site: https://araghupr26.github.io/creatordm-prototype/

Educational concept, not affiliated with Meta. Handles and people in the prototype are invented.

## Commit history (oldest first)

Commits made after this file was generated are listed the next time it is regenerated.

- `2695f5e` `v0.1.0` Add DM to Link concept prototype (2026-10-04)
- `919f4ee` Link the live site from the README (2026-10-04)
- `66035f1` feat(prototype): consistent creator threads and Before/After story (2026-10-04)
- `6a31030` docs(changelog): add changelog with diffs between commits (2026-10-04)
- `d6c8c2d` docs: add v4 concept PDF and link it from the README (2026-10-04)
- `c156479` docs(changelog): add the v4 PDF commit (2026-10-04)
- `046eab6` fix(prototype): make reel and post treatment consistent (2026-10-04)
- `346349c` docs(changelog): add the reel and post consistency fix (2026-10-04)
- `d6c111c` feat(prototype): rename to Drops, message requests, in-app browser, per-post summaries, lists and aliases (2026-10-07)
- `0d68b7a` docs: add Drops concept deck v5 and the PRD (2026-10-07)
- `344e337` docs(changelog): add the Drops rename, v5 deck and PRD commits (2026-10-07)
- `b500b14` docs(prd): rebuild the backlog as initiatives, workflow epics, stories, tasks and sub-tasks (2026-10-07)

## What changed in each commit

### `b500b14` docs(prd): rebuild the backlog as initiatives, workflow epics, stories, tasks and sub-tasks
2026-10-07. 1 file changed, 404 insertions(+), 204 deletions(-)

- modified `docs/PRD.md`

### `344e337` docs(changelog): add the Drops rename, v5 deck and PRD commits
2026-10-07. 1 file changed, 34 insertions(+), 1 deletion(-)

- modified `CHANGELOG.md`

### `0d68b7a` docs: add Drops concept deck v5 and the PRD
2026-10-07. 3 files changed, 340 insertions(+), 4 deletions(-)

- modified `README.md`
- added `docs/PRD.md`
- added `docs/drops-concept-v5.pdf`

### `d6c111c` feat(prototype): rename to Drops, message requests, in-app browser, per-post summaries, lists and aliases
2026-10-07. 1 file changed, 230 insertions(+), 103 deletions(-)

- modified `index.html`

```text
- rename DM to Link to Drops across the prototype
- requests skip Accept in After and land in Waiting on you; one follow check
- iPhone 17 frame with home indicator, mixed crowded inbox, message pop-in
- in-app browser mock on every link action; one-line summary replaces Details
- aliases, flat lists, emoji row, motion pass, design-review fixes
```

### `346349c` docs(changelog): add the reel and post consistency fix
2026-10-04. 1 file changed, 19 insertions(+), 1 deletion(-)

- modified `CHANGELOG.md`

### `046eab6` fix(prototype): make reel and post treatment consistent
2026-10-04. 1 file changed, 15 insertions(+), 12 deletions(-)

- modified `index.html`

```text
One card frame for reels and posts, the Reel marker on every reel in the feed, the same type chip on the resource card, and wording that matches the type.
```

### `c156479` docs(changelog): add the v4 PDF commit
2026-10-04. 1 file changed, 24 insertions(+), 2 deletions(-)

- modified `CHANGELOG.md`

### `d6c8c2d` docs: add v4 concept PDF and link it from the README
2026-10-04. 2 files changed, 2 insertions(+)

- modified `README.md`
- added `docs/ig-resource-inbox-flows-v4.pdf`

### `6a31030` docs(changelog): add changelog with diffs between commits
2026-10-04. 1 file changed, 100 insertions(+)

- added `CHANGELOG.md`

```text
Generate CHANGELOG.md from git history: commit list, what changed in
each commit, a table comparing each commit with the one before it (with
GitHub compare links), working tree status and tracked files.
```

### `66035f1` feat(prototype): consistent creator threads and Before/After story
2026-10-04. 1 file changed, 299 insertions(+), 187 deletions(-)

- modified `index.html`

```text
Rework the story after review and make every creator chat deliver the
resource its DM to Link card promises.

Story and inbox
- Split the story into Before (today's flow and pain) and After.
- Red number on the DM tab; unread thread at the top; flooded inbox
  with unread friends between creator threads; read cue once the link
  arrived; Messages search that finds nothing for "pasta".
- Step 2 types the comment; longer feed with unrelated posts and stories.
- American names throughout; notes row uses different people.

DM to Link
- Waiting on you (Open profile, I'm following, Reply in chat) and
  Waiting for link rows; card shows what the creator said and a clipped
  caption with more/less instead of an AI summary.
- Message with a clickable link per bullet; hostname-only links.
- Tucked away narrowed to messages after the link.
- Removed creator labels, copy buttons, shortened-link expansion.

Consistency
- Generate each creator thread from the data: tap, keyword, follow gate,
  repeated gate, typed reply, link in text, bullets. Your response is
  always in the thread before the resource.
- Working profile sheet, repeated gate on a missed follow, real message
  box that unlocks a typed ask, Go to chat highlight, previews from the
  last real message.
- Fix elliptical story rings in comment rows.
```

### `919f4ee` Link the live site from the README
2026-10-04. 1 file changed, 3 insertions(+), 1 deletion(-)

- modified `README.md`

```text
The code view on github.com shows source only, so point readers at the
github.io address where the prototype runs.
```

### `2695f5e` Add DM to Link concept prototype (v0.1.0)
2026-10-04. 3 files changed, 757 insertions(+)

- added `.gitignore`
- added `README.md`
- added `index.html`

```text
Single-file clickable prototype: a feed-first story, a real comment-to-DM
thread, the flooded inbox, and the DM to Link library (Pinned, Recent,
topics, creators, labels, noise handling). Includes a phone layout,
a README, and page metadata.

Educational concept, not affiliated with Meta. Handles are invented.
```

## Differences between commits

Each row compares a commit with the one before it. The compare link opens the full line-by-line diff on GitHub.

| From | To | Change | Full diff |
|---|---|---|---|
| `2695f5e` | `919f4ee` | 1 file changed, 3 insertions(+), 1 deletion(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/2695f5e...919f4ee) |
| `919f4ee` | `66035f1` | 1 file changed, 299 insertions(+), 187 deletions(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/919f4ee...66035f1) |
| `66035f1` | `6a31030` | 1 file changed, 100 insertions(+) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/66035f1...6a31030) |
| `6a31030` | `d6c8c2d` | 2 files changed, 2 insertions(+) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/6a31030...d6c8c2d) |
| `d6c8c2d` | `c156479` | 1 file changed, 24 insertions(+), 2 deletions(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/d6c8c2d...c156479) |
| `c156479` | `046eab6` | 1 file changed, 15 insertions(+), 12 deletions(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/c156479...046eab6) |
| `046eab6` | `346349c` | 1 file changed, 19 insertions(+), 1 deletion(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/046eab6...346349c) |
| `346349c` | `d6c111c` | 1 file changed, 230 insertions(+), 103 deletions(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/346349c...d6c111c) |
| `d6c111c` | `0d68b7a` | 3 files changed, 340 insertions(+), 4 deletions(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/d6c111c...0d68b7a) |
| `0d68b7a` | `344e337` | 1 file changed, 34 insertions(+), 1 deletion(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/0d68b7a...344e337) |
| `344e337` | `b500b14` | 1 file changed, 404 insertions(+), 204 deletions(-) | [compare](https://github.com/araghupr26/creatordm-prototype/compare/344e337...b500b14) |

Across the whole history: `2695f5e` to `b500b14`: 6 files changed, 1190 insertions(+), 235 deletions(-). [compare](https://github.com/araghupr26/creatordm-prototype/compare/2695f5e...b500b14)

## Current working tree status

```
clean, nothing to commit
```

## Tracked files

- `.gitignore`: Keeps macOS .DS_Store files out of the repository.
- `CHANGELOG.md`: This file. Regenerated from git history, with diff summaries between commits.
- `README.md`: What the prototype is, the live site link, and the URL options.
- `docs/PRD.md`: Tracked file.
- `docs/drops-concept-v5.pdf`: Tracked file.
- `docs/ig-resource-inbox-flows-v4.pdf`: Tracked file.
- `index.html`: The whole prototype: one self-contained HTML file with styles and script, no build step.
