# creatorDM prototype: Drops

A clickable concept prototype for Drops, a library for the links and resources that creators send through comment-to-DM automations. It starts in a feed, follows a real comment-to-DM flow, shows the flooded inbox that results, and then shows the Drops fix.

**Live site: https://araghupr26.github.io/creatordm-prototype/**

Concept document (13 pages, flows, delivery rules, edge cases, proposed scope): [docs/drops-concept-v5.pdf](docs/drops-concept-v5.pdf). Product requirements (epics, stories, tasks, bugs): [docs/PRD.md](docs/PRD.md)

Educational concept by Archana Raghu Prasad. Not affiliated with Meta or Instagram. Handles and people are invented. All data is fake, and nothing here detects links from real messages.

## Use it

Open the live site above, or open `index.html` from a download in a browser. The code view on github.com shows the source only. The site runs at the `github.io` address.

On a desktop, the left panel walks through the story and lists extra screens. On a phone, use the Menu and Next bar at the bottom.

URL options:

- `#0` to `#16` jumps to a step in the story.
- `#x0` and up jumps to an extra screen (search, topics, edge cases, labels, creators).
- `?light` switches to the light theme.
- `?board` shows every screen side by side.
- `?shot=N` shows one bare screen. Add `&scroll=Y` to scroll it.

## Notes

One HTML file. No dependencies and no build step. The page asks search engines not to index it.
