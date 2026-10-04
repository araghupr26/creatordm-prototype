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

## What changed in each commit

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

Across the whole history: `2695f5e` to `d6c8c2d`: 4 files changed, 404 insertions(+), 188 deletions(-). [compare](https://github.com/araghupr26/creatordm-prototype/compare/2695f5e...d6c8c2d)

## Current working tree status

```
clean, nothing to commit
```

## Tracked files

- `.gitignore`: Keeps macOS .DS_Store files out of the repository.
- `CHANGELOG.md`: This file. Regenerated from git history, with diff summaries between commits.
- `README.md`: What the prototype is, the live site link, and the URL options.
- `docs/ig-resource-inbox-flows-v4.pdf`: Tracked file.
- `index.html`: The whole prototype: one self-contained HTML file with styles and script, no build step.
