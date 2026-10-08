# Drops: product requirements document

Author: Archana Raghu Prasad. Status: draft for review, October 2026. Educational concept, not affiliated with Meta. Handles and people are invented.

Companion files: the clickable prototype (`index.html`), the concept deck (`docs/drops-concept-v5.pdf`) and the changelog (`CHANGELOG.md`).

How this document is organised. It follows Jira terminology: one **Initiative** holds **Epics**, an Epic holds **Stories**, **Tasks** and **Bugs**, and a Story or Task holds **Sub-tasks**. **Spikes** are time-boxed research tasks. Keys look like `DROP-12`. Fix versions are **V1** (the core fix) and **V2** (finding things once the library grows, called Later in the deck).

---

## 1. Summary

Creators run comment-to-DM automations. A person comments a keyword on a reel, and a bot sends a DM with a link. Those DMs land in the same inbox as friends. Over weeks the inbox floods with confirmations, follow-ups and promos. Friends' messages get buried, the link is hard to find, and Messages search cannot find "that pasta recipe" because it only matches names.

**Drops** is a library inside Messages for the links and resources creators send. Nothing is deleted and nothing leaves the chat. Automated DMs leave the main list and open into Drops, which is organised around what you asked for and what is waiting on you.

The name follows Meta's format naming (Reels, Stories, Posts, Notes): one plain word for the thing itself. A creator "drops" a link in your DMs.

## 2. Problem

| Who | Problem | Evidence in the prototype |
| --- | --- | --- |
| Heavy commenters | Creator threads push unread friends down the inbox. | Flooded inbox: Emily's unread message sits far below creator promos. |
| Heavy commenters | The link is far up a long thread, under follow-ups. | Scrolling the thread to find the link. |
| Anyone who saved a link weeks ago | Search matches names and accounts only. "pasta" finds nothing. | Messages search with no results. |
| Anyone commenting on creators they do not follow | The DM waits in Requests. You must accept a request for a link you asked for. | Requests (1), then Accept, then the thread appears. |
| Creators | Cleaner inbox must not reduce commenting, since comment counts are their engagement. | Comments and public replies are left alone. |

## 3. Goals and non-goals

**Goals**
1. Friends first: unread friends are visible without scrolling past creator threads.
2. Any link a creator sent is findable in two taps, and by what it was about.
3. Anything that needs the user, or needs the creator, is visible in one place.
4. Do not reduce comment-to-DM participation.

**Non-goals**
- Detecting links in non-automated conversations.
- Moderating or rating creators.
- A general bookmarking product. Drops only holds what arrived through comment-to-DM.
- Expanding shortened links or reading files behind a login.
- Renaming or labelling creators. Their names are theirs.
- Audio or video transcription for summaries.

## 4. Users and jobs

- **The commenter** (primary). Comments keywords on reels, expects a link, wants friends' messages kept apart. Job: "get the thing I asked for, and find it again later."
- **The friend.** Messages the commenter. Job: "be seen, not buried."
- **The creator** (stakeholder). Sends via a third-party tool. Job: "keep my engagement and my funnel intact."

## 5. Success metrics

Proposals only. There is no data behind these yet.

| Metric | Direction | How measured |
| --- | --- | --- |
| Taps to open a friend's chat, heavy commenters | Down | Before vs. after cohort |
| 7-day revisit rate on delivered resources | Up | Drops open events per resource |
| Comment-to-DM participation per user, 90 days | Not down (guardrail) | Holdout comparison |
| Share of resources opened after day 7 | Up | Open events with age |
| Time to find a resource by search | Down | Search to open sequence |
| Resources pinned, aliased or listed (V2) | Up | Action counts |
| Summary edit or alias rate (quality proxy) | Low | Alias set on summarised links |

## 6. Scope

**V1:** friends-first inbox with the floating Drops banner, Drops home (Waiting on you, Waiting for link, Pinned, Recent), requests that land in Waiting on you with no Accept, one follow check, the resource sheet with a one-line summary and a Pin icon, the in-app browser on Open link, delivery rules, noise tucked away.

**V2 (called Later in the deck):** double-tap pin gesture, search by memory with recent searches, topic rows with See all and Customize topics, aliases, flat user lists, Creators you engaged with and creator pages, Recent grouped by creator.

**Why the split:** V1 fixes the two problems, friends buried and links lost. V2 helps finding things once the library grows.

## 7. Key rules and decisions

1. **Delivery is decided by deliverable, not button type.** A sequence starts at the private reply to your comment. We scan that creator's later messages for a URL button, a URL in text, or a file or media attachment. `instagram.com` links never count.
   - Deliverable found: **Delivered**.
   - None yet, and the latest message waits on a tap or typed reply: **Waiting on you**.
   - You did your part and nothing arrived: **Waiting for link**.
2. **Requests.** Before: the DM arrives in Requests and you must Accept. After: the same DM appears in Waiting on you with "Wants to send you a link. No need to accept." The only action is Open chat.
3. **One follow check.** "I'm following" reads your follow state once. If you do not follow, it shows a hint and does nothing else. There is no counter and no repeating gate, so the automation cannot be tripped by tapping repeatedly.
4. **Summary, not dialogue.** The resource sheet shows one summary line and a grey "You commented GUIDE on their reel." It does not show the DM text or the caption. Search still reads both.
5. **Names once.** The creator is named once on the sheet. The date is small text. An alias sits in brackets beside the original title and never replaces it.
6. **Noise is tucked away by position.** Messages after the delivered link are tucked away, not deleted. Comments and public replies are untouched.
7. **Link opens something.** Open link opens an in-app browser. A link button inside a creator chat does the same.
8. **Lists are flat.** User-made lists, no nesting. Once any list exists, the add control shrinks to a small chip.

Summary generation, recorded because it reverses an earlier cut: a one-line summary is generated once, when the link is delivered, from the caption and the creator's message. Estimated cost is about $0.0006 per link with a small text model (about 400 tokens in, 40 out), cached. Heavy user at 1,000 links is about 60 cents, once. Text only. The main risk is a wrong summary, so the line stays close to the creator's words and the alias is the user's override.

## 8. Assumptions and open questions

**Assumptions** (to verify)
- Automated DMs are identifiable: tools like ManyChat send through the Messaging API, and docs show an echo flag on app-sent messages.
- The first DM is a Private Reply tied to the comment (one message per comment, within 7 days).
- Later messages tie to the comment by time window, not ID. Two comments on two posts by one creator on the same day are ambiguous.
- Button URLs are readable as structured data (type, url, title).
- Follow state is checkable through the user profile API.
- Reel captions are available.

**Not confirmed**
- Which attachment types Instagram DMs allow from automations.
- Whether a Private Reply's first message can carry a button template.
- How encrypted chats and data exports treat these messages.
- That DM search matches names and accounts only.
- Whether Instagram would fire the creator's "I'm following" tap for you.
- Whether a request can be shown in Drops without accepting it, given spam and safety rules for non-followers.
- Feasibility: Instagram can build this. A third-party app only sees messages for creator accounts that connect it.

## 9. Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Misclassifying a friend's DM as automated | A friend vanishes from the main list | Only messages with the automation signal move. A friend can never be tucked away. |
| Wrong summary | Mistrust | Keep it grounded, allow alias, show nothing when confidence is low |
| Requests bypass lets spam in | Safety | Only requests tied to a comment you made appear in Waiting on you |
| Cleaner inbox lowers commenting | Creator harm | Guardrail metric, holdout rollout |
| Creator tools resume on their own tap | Broken delivery | Keep "I'm following" as a user action, no auto-fire |

## 10. Dependencies

Messaging API signals (echo flag, Private Reply linkage, button payloads), follow-state lookup, comment-to-DM association service, a small text model for summaries, an in-app browser surface.

---

## 11. Backlog

The backlog follows Jira's hierarchy. Priority is P0 to P2. Points are story points. V2 is called "Later" in the concept deck.

| Level | Jira type | Holds | In this PRD |
| --- | --- | --- | --- |
| 2 | Initiative | Epics | DROP-1 (V1), DROP-2 (V2) |
| 1 | Epic | Stories, Tasks, Bugs, Spikes | One per user workflow, DROP-3 to DROP-15 |
| 0 | Story, Task, Bug, Spike | Sub-tasks | Rows in each epic table |
| -1 | Sub-task | Nothing | Nested bullets, keyed like DROP-21.1 |

```
Initiative DROP-1  V1  Fix the inbox
  Epic DROP-3  W1 Comment and get the link
    Story DROP-21  Group automated DMs into one resource per sequence
      Sub-task DROP-21.1  Sequence model keyed by comment
  Epic DROP-4  W2 Open Messages: friends first
  ...
Initiative DROP-2  V2  Find it and organise it
  Epic DROP-11  W9 Find it again
  ...
```

Item statuses: To Do unless stated. Epic DROP-15 describes the prototype and is mostly Done.

### Initiative DROP-1: V1, Fix the inbox

Friends first, links findable, nothing waiting unseen. Epics DROP-3 to DROP-10, plus DROP-15 for the prototype.

### Initiative DROP-2: V2, Find it and organise it

Finding things once the library grows. Epics DROP-11 to DROP-14.

#### Epic DROP-3: W1 Comment and get the link (V1, parent DROP-1)

Workflow: I comment a keyword on a reel, the creator replies in public, and a DM sequence starts. The system turns that sequence into one resource with a clear state.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-20 | Spike | Confirm which fields identify an automation-sent message and a Private Reply | P0 | 3 | To Do |
| DROP-21 | Story | Group a creator's automated DMs into one resource per comment sequence | P0 | 8 | To Do |
| DROP-22 | Story | Mark Delivered when a URL button, a text URL or an attachment arrives | P0 | 5 | To Do |
| DROP-23 | Story | Show Waiting on you when the creator needs a tap or a typed reply | P0 | 3 | To Do |
| DROP-24 | Story | Show Waiting for link when I did my part and nothing arrived | P0 | 3 | To Do |
| DROP-25 | Story | Keep a message with a link per bullet as one resource with several links | P1 | 3 | To Do |
| DROP-26 | Story | Treat a prompt after delivery ("Reply YES for the next part") as noise, not a gate | P1 | 2 | To Do |
| DROP-27 | Story | Handle a typed ask ("send me your email") as Waiting on you with Reply in chat | P1 | 3 | To Do |
| DROP-28 | Story | Handle two comments on one creator the same day | P1 | 3 | To Do |
| DROP-29 | Story | Handle the 7-day Private Reply window passing with no link | P1 | 3 | To Do |
| DROP-30 | Story | Keep the resource when the comment or post is deleted, and drop the "You commented" line | P2 | 2 | To Do |
| DROP-31 | Task | Event schema: drop_delivered, drop_waiting_on_you, drop_waiting_for_link | P1 | 2 | To Do |

Detail for the items above:

- **DROP-21** Group a creator's automated DMs into one resource per comment sequence
  - Acceptance criteria:
    - Given an automated DM with an echo flag after my comment, when it arrives, then it joins the resource for that comment.
    - Given a friend's DM, then it is never grouped.
  - DROP-21.1 (Sub-task) Sequence model keyed by comment
  - DROP-21.2 (Sub-task) Time-window matcher
  - DROP-21.3 (Sub-task) Friend exclusion test
  - DROP-21.4 (Sub-task) Backfill existing threads
- **DROP-22** Mark Delivered when a URL button, a text URL or an attachment arrives
  - Acceptance criteria:
    - A URL button, a URL in text and a file or media attachment each mark Delivered.
    - instagram.com links never mark Delivered.
  - DROP-22.1 (Sub-task) Button payload parser
  - DROP-22.2 (Sub-task) Text URL extractor
  - DROP-22.3 (Sub-task) Attachment detector
  - DROP-22.4 (Sub-task) Ignore instagram.com links
- **DROP-28** Handle two comments on one creator the same day
  - DROP-28.1 (Sub-task) Ambiguity rule: attach to the earlier open sequence
  - DROP-28.2 (Sub-task) Log an ambiguity flag
- **DROP-29** Handle the 7-day Private Reply window passing with no link
  - DROP-29.1 (Sub-task) Move to Waiting for link
  - DROP-29.2 (Sub-task) Add a "may not arrive" note

#### Epic DROP-4: W2 Open Messages: friends first (V1, parent DROP-1)

Workflow: I open Messages and see my friends, not creator threads. A banner tells me Drops has something.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-32 | Story | Move automated DMs out of the main list | P0 | 5 | To Do |
| DROP-33 | Story | Floating banner above the tab bar opens Drops and stays while I scroll | P0 | 3 | To Do |
| DROP-34 | Story | DM tab badge counts friends' unread messages only | P0 | 3 | To Do |
| DROP-35 | Story | Keep read and unread friends and ordinary chats in their normal order | P1 | 2 | To Do |
| DROP-36 | Story | Banner copy "N new links this week" with the creator names | P2 | 1 | To Do |
| DROP-37 | Task | Keep the banner clear of the home indicator and tab bar at 402 x 874 | P2 | 1 | To Do |
| DROP-38 | Story | Setting: Turn off Drops to restore my old inbox | P1 | 3 | To Do |
| DROP-39 | Task | Server-side kill switch for the whole feature | P0 | 2 | To Do |
| DROP-40 | Story | Messages search still finds creator chats by name | P1 | 2 | To Do |

Detail for the items above:

- **DROP-32** Move automated DMs out of the main list
  - Acceptance criteria:
    - Given automated DMs exist, when I open Messages, then none appear in the main list.
    - Nothing is deleted. Go to chat still shows the full thread.
    - A friend who sends a link manually stays in the main list.
  - DROP-32.1 (Sub-task) List filter on the automation signal
  - DROP-32.2 (Sub-task) Friend safety guard
  - DROP-32.3 (Sub-task) Restore path from Drops to the chat
- **DROP-34** DM tab badge counts friends' unread messages only
  - Acceptance criteria:
    - Given 2 unread creator DMs and 1 unread friend DM, then the badge shows 1.

#### Epic DROP-5: W3 Handle a message request (V1, parent DROP-1)

Workflow: A creator I do not follow sends me the link I asked for. Before: I find it in Requests and accept. After: it is already waiting for me.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-41 | Spike | Check spam and safety rules for showing non-follower requests before acceptance | P0 | 3 | To Do |
| DROP-42 | Spike | Confirm what read receipt a creator sees when I open a request I did not accept | P1 | 2 | To Do |
| DROP-43 | Story | A request tied to my comment appears in Waiting on you | P0 | 5 | To Do |
| DROP-44 | Story | Open chat from the card and read the request without accepting | P0 | 5 | To Do |
| DROP-45 | Story | Requests not tied to my comment stay in the normal Requests list | P0 | 2 | To Do |
| DROP-46 | Story | The request resolves into Recent once the creator delivers | P1 | 3 | To Do |
| DROP-47 | Story | Delete and Block stay available in the request chat | P1 | 2 | To Do |
| DROP-48 | Task | Request card copy: "Wants to send you a link. No need to accept." | P2 | 1 | To Do |
| DROP-49 | Story | Before flow: Requests (n) link in blue, with the Accept, Delete and Block bar | P2 | 2 | To Do |

Detail for the items above:

- **DROP-43** A request tied to my comment appears in Waiting on you
  - Acceptance criteria:
    - Only requests tied to a comment I made appear.
    - The card shows the creator and one action: Open chat.
  - DROP-43.1 (Sub-task) Tie the request to a comment
  - DROP-43.2 (Sub-task) Request card with one action
  - DROP-43.3 (Sub-task) Hide it from the Requests list
- **DROP-44** Open chat from the card and read the request without accepting
  - DROP-44.1 (Sub-task) Read-only preview state
  - DROP-44.2 (Sub-task) Reply box visible after the first reply

#### Epic DROP-6: W4 Unlock a gated link (V1, parent DROP-1)

Workflow: The creator wants a follow before sending. I follow once and the link unlocks. I cannot break the automation by tapping repeatedly.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-50 | Story | "I'm following" checks my follow state once | P0 | 3 | To Do |
| DROP-51 | Story | Show a one-line hint when I do not follow | P0 | 2 | To Do |
| DROP-52 | Story | Checking state, then unlock: the card moves to Recent with a toast | P1 | 3 | To Do |
| DROP-53 | Task | Remove the repeating in-chat follow gate and its counter | P1 | 2 | To Do |
| DROP-54 | Story | Open profile opens the creator's profile so I can follow | P1 | 2 | To Do |
| DROP-55 | Bug | Tapping "I'm following" repeatedly must not send more than one confirmation | P0 | 1 | To Do |
| DROP-56 | Story | Follow state changed elsewhere updates the card without a refresh | P2 | 2 | To Do |
| DROP-57 | Spike | Confirm whether the platform can fire the creator's "I'm following" tap | P1 | 3 | To Do |

Detail for the items above:

- **DROP-50** "I'm following" checks my follow state once
  - Acceptance criteria:
    - Given I do not follow the creator, when I tap "I'm following", then a hint shows and the state does not change.
    - Given I follow, when I tap, then the state becomes checking, then unlocked.

#### Epic DROP-7: W5 Open and use a resource (V1, parent DROP-1)

Workflow: I open a saved link, remember why I saved it, and get to the page or the chat.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-58 | Story | One-line summary and a grey "You commented KEYWORD on their reel" | P0 | 5 | To Do |
| DROP-59 | Story | Name the creator once and show the date as small text | P1 | 2 | To Do |
| DROP-60 | Story | Pin is a round icon on the sheet art, filled when pinned | P1 | 2 | To Do |
| DROP-61 | Story | Open link opens an in-app browser | P0 | 5 | To Do |
| DROP-62 | Story | Link buttons in creator chats open the same browser | P0 | 3 | To Do |
| DROP-63 | Story | Go to chat opens the thread with the delivered message highlighted | P1 | 3 | To Do |
| DROP-64 | Story | Messages after the link are marked "Tucked away" in the chat | P1 | 3 | To Do |
| DROP-65 | Story | A Tucked away sheet explains what is tucked and shows a count | P2 | 2 | To Do |
| DROP-66 | Task | Define noise by position after delivery, not by wording | P1 | 2 | To Do |
| DROP-67 | Task | Leave comments, public replies and notifications untouched | P0 | 1 | To Do |
| DROP-68 | Task | Remove the Details toggle, quoted message and caption from the sheet; keep them searchable | P1 | 2 | To Do |

Detail for the items above:

- **DROP-58** One-line summary and a grey "You commented KEYWORD on their reel"
  - Acceptance criteria:
    - The sheet never shows the DM text or the caption.
    - The summary is at most two lines.
    - If no summary exists, the line is omitted.
  - DROP-58.1 (Sub-task) Summary service, one call per delivered link, cached
  - DROP-58.2 (Sub-task) Prompt and guardrails: stay close to the creator's words
  - DROP-58.3 (Sub-task) Omit the line when confidence is low
  - DROP-58.4 (Sub-task) Regenerate on request
  - DROP-58.5 (Sub-task) Feedback signal when I set an alias
- **DROP-61** Open link opens an in-app browser
  - Acceptance criteria:
    - Close returns to the sheet.
    - Shortened links are not expanded.
  - DROP-61.1 (Sub-task) Browser sheet with close, lock and host
  - DROP-61.2 (Sub-task) Exit animation on close
  - DROP-61.3 (Sub-task) Domain-only host, no shortened-link expansion
  - DROP-61.4 (Sub-task) Toolbar clear of the home indicator

#### Epic DROP-8: W6 Know what needs me (V1, parent DROP-1)

Workflow: I open Drops and see at once what needs me and what is waiting on a creator.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-69 | Story | Home shows Waiting on you and Waiting for link rows on top | P0 | 5 | To Do |
| DROP-70 | Story | Amber count badge on Waiting on you when above zero | P1 | 1 | To Do |
| DROP-71 | Story | Pinned and Recent rows scroll sideways with resource cards | P0 | 5 | To Do |
| DROP-72 | Story | A new resource highlights in Recent when it lands | P2 | 2 | To Do |
| DROP-73 | Task | Card: colour and a faint type glyph on the art, title once, creator as meta | P1 | 2 | To Do |
| DROP-74 | Task | No pin glyph on cards inside Pinned | P2 | 1 | To Do |
| DROP-75 | Story | In-app notice when a link lands | P1 | 3 | To Do |
| DROP-76 | Story | Optional push notification when a link lands, off by default | P2 | 3 | To Do |
| DROP-77 | Story | Empty states: nothing waiting, no resources yet | P1 | 2 | To Do |
| DROP-78 | Story | Waiting rows start collapsed to keep the home short | P2 | 1 | To Do |

Detail for the items above:

- **DROP-69** Home shows Waiting on you and Waiting for link rows on top
  - Acceptance criteria:
    - Waiting on you expands to a card per item with one filled primary action.
    - Waiting for link expands to a card per creator with Go to chat.

#### Epic DROP-9: W7 Trust and control (V1, parent DROP-1)

Workflow: I can see what Drops does, turn it off, and fix what it gets wrong.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-79 | Story | Opt a creator out of Drops so their DMs stay in the main list | P1 | 3 | To Do |
| DROP-80 | Story | Delete a resource from Drops without deleting the chat | P1 | 3 | To Do |
| DROP-81 | Story | Report a wrong summary and fix it with an alias | P1 | 3 | To Do |
| DROP-82 | Task | Privacy review: what is stored, retention and deletion | P0 | 3 | To Do |
| DROP-83 | Story | Accessibility: 44px hit areas, VoiceOver labels, dynamic type | P0 | 5 | To Do |
| DROP-84 | Story | Reduced motion fallback for every animation | P1 | 2 | To Do |
| DROP-85 | Story | Light and dark themes | P1 | 2 | To Do |
| DROP-86 | Story | Offline: cached resources open and the browser shows an offline state | P2 | 3 | To Do |

Detail for the items above:

- **DROP-83** Accessibility: 44px hit areas, VoiceOver labels, dynamic type
  - DROP-83.1 (Sub-task) 44px hit areas without changing the look
  - DROP-83.2 (Sub-task) VoiceOver labels on icon buttons
  - DROP-83.3 (Sub-task) Dynamic type pass

#### Epic DROP-10: W8 Measure and roll out (V1, parent DROP-1)

Workflow: We learn whether Drops helps without hurting creators.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-87 | Task | Instrument the metrics in section 5 | P0 | 3 | To Do |
| DROP-88 | Task | Holdout group for the comment-to-DM participation guardrail | P0 | 3 | To Do |
| DROP-89 | Task | Staged rollout: creators who connect an app first, then all users | P1 | 3 | To Do |
| DROP-90 | Task | Rollback runbook using the kill switch | P0 | 2 | To Do |
| DROP-91 | Task | Dashboard for guardrail metrics | P1 | 3 | To Do |
| DROP-92 | Story | In-app survey after 7 days: did Drops help you find a link? | P2 | 2 | To Do |
| DROP-93 | Spike | Check whether data exports keep button URLs | P2 | 2 | To Do |

#### Epic DROP-11: W9 Find it again (V2, parent DROP-2)

Workflow: Weeks later I remember "that pasta thing" and find it.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-94 | Story | Search matches what the post was about, not only names | P1 | 8 | To Do |
| DROP-95 | Spike | Check how search indexes text the sheet hides | P1 | 2 | To Do |
| DROP-96 | Story | Recent searches, and delete one | P2 | 2 | To Do |
| DROP-97 | Story | See all lists reels and posts with All, Reels and Posts filters | P2 | 3 | To Do |
| DROP-98 | Story | Topic rows from what I comment on | P2 | 5 | To Do |
| DROP-99 | Story | Customize topics: turn a topic row off | P2 | 3 | To Do |
| DROP-100 | Story | Double-tap a card to pin it | P2 | 2 | To Do |
| DROP-101 | Story | Fuzzy match for loose queries like "that pasta thing" | P2 | 3 | To Do |

Detail for the items above:

- **DROP-94** Search matches what the post was about, not only names
  - DROP-94.1 (Sub-task) Index caption, message and summary
  - DROP-94.2 (Sub-task) Ranking and recency
  - DROP-94.3 (Sub-task) Highlight the matched words

#### Epic DROP-12: W10 Organise my way (V2, parent DROP-2)

Workflow: I group links the way I think about them.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-102 | Story | Add an alias from a greyed prompt beside the title | P2 | 3 | To Do |
| DROP-103 | Story | Add a link to a list, or start a list | P2 | 5 | To Do |
| DROP-104 | Story | Once lists exist the add control shrinks to a small chip | P2 | 2 | To Do |
| DROP-105 | Story | My lists show under Pinned on the home | P2 | 3 | To Do |
| DROP-106 | Task | Alias and list names are searchable | P2 | 2 | To Do |
| DROP-107 | Story | Rename and reorder lists | P2 | 3 | To Do |
| DROP-108 | Story | Alias suggestion chips from topic and title | P2 | 2 | To Do |

Detail for the items above:

- **DROP-102** Add an alias from a greyed prompt beside the title
  - Acceptance criteria:
    - The alias shows in Drops and in search.
  - DROP-102.1 (Sub-task) Alias shows in brackets, never replaces the title
  - DROP-102.2 (Sub-task) One-tap suggestions
  - DROP-102.3 (Sub-task) Only I see it
- **DROP-103** Add a link to a list, or start a list
  - Acceptance criteria:
    - Lists are flat. No nesting.
    - A link can sit in several lists.
    - Removing a link from a list does not delete the resource.
  - DROP-103.1 (Sub-task) Pick or create sheet
  - DROP-103.2 (Sub-task) Suggestions from tags
  - DROP-103.3 (Sub-task) Create list action

#### Epic DROP-13: W11 Browse by creator (V2, parent DROP-2)

Workflow: One creator sent me several links, and I want them together.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-109 | Story | Creators you engaged with: the full list, most recent first | P2 | 3 | To Do |
| DROP-110 | Story | Creator page with their chat and every resource, each tied to its comment | P2 | 5 | To Do |
| DROP-111 | Story | Recent groups cards by creator when they sent several | P2 | 3 | To Do |
| DROP-112 | Story | Open chat from the creator page | P2 | 1 | To Do |
| DROP-113 | Story | Topic tags on creators | P2 | 2 | To Do |

#### Epic DROP-14: W12 Revisit and share (V2, parent DROP-2)

Workflow: I come back to links I forgot, and share the post with a friend.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-114 | Story | Resurface resources I have not opened after N days | P2 | 5 | To Do |
| DROP-115 | Story | Forward the reel or post to a friend, so they trigger their own DM | P2 | 5 | To Do |
| DROP-116 | Story | Archive after 30 days (closes the "Older" open question) | P2 | 3 | To Do |
| DROP-117 | Story | Export a list as text | P2 | 3 | To Do |
| DROP-118 | Story | Share the link from the browser toolbar | P2 | 2 | To Do |
| DROP-119 | Story | Combined "Follow and continue" button | P2 | 5 | To Do |

#### Epic DROP-15: W13 Prototype and design quality (Prototype, parent DROP-1)

Workflow: The clickable prototype and the work around it. Cross-cutting, already built.

| Key | Type | Summary | Priority | Points | Status |
| --- | --- | --- | --- | --- | --- |
| DROP-120 | Story | iPhone 17 frame | P1 | 3 | Done |
| DROP-121 | Story | Before and After story flows with a mixed crowded inbox | P1 | 5 | Done |
| DROP-122 | Story | Messages pop in after a tap instead of being pre-populated | P1 | 3 | Done |
| DROP-123 | Story | Emoji row in the comment sheet adds to the comment | P2 | 1 | Done |
| DROP-124 | Story | Design review (emil-design-eng) fixes | P1 | 5 | Done |
| DROP-125 | Story | Motion pass (/animate) | P1 | 5 | Done |
| DROP-126 | Story | In-app browser mock on every link action | P1 | 5 | Done |
| DROP-127 | Story | One-line summary replaces Details | P1 | 3 | Done |
| DROP-128 | Story | Aliases, flat lists and the Add to list sheet | P2 | 5 | Done |
| DROP-129 | Task | Rename from "DM to Link" to "Drops" in the prototype, README and docs | P1 | 2 | Done |
| DROP-130 | Task | Concept deck v5 (13 pages) and this PRD | P1 | 3 | Done |
| DROP-131 | Bug | Delivered link buttons in non-story creator chats were inactive (active check allowed only the story chat) | P0 | 1 | Done |
| DROP-132 | Bug | The story chat link button toasted but did not re-render (handler returned before render) | P1 | 1 | Done |
| DROP-133 | Bug | The comment composer sat under the home indicator (fixed with 34px bottom padding) | P1 | 1 | Done |
| DROP-134 | Bug | The Requests link was red (now blue) | P2 | 1 | Done |
| DROP-135 | Bug | The request thread did not scroll to the newest message | P2 | 1 | Done |
| DROP-136 | Bug | Card render passed the array index as the inPin flag | P2 | 1 | Done |
| DROP-137 | Bug | In a 402px wide browser window the comment field sits 27px above the bottom edge and the check expects 30px | P2 | 1 | Open |
| DROP-138 | Task | Watch the motion in a real browser and tune by feel | P2 | 1 | Open |
| DROP-139 | Story | Drag to dismiss on the sheet handle | P2 | 3 | Backlog |
| DROP-140 | Task | Figma restructure into flows, components and auto-layout (blocked by the Figma MCP call limit) | P2 | 5 | Blocked |

Detail for the items above:

- **DROP-120** iPhone 17 frame
  - DROP-120.1 (Sub-task) 402 x 874 screen
  - DROP-120.2 (Sub-task) Island 126 x 37
  - DROP-120.3 (Sub-task) Home indicator 134 x 5 at 8px
  - DROP-120.4 (Sub-task) Screen radius 55
- **DROP-121** Before and After story flows with a mixed crowded inbox
  - DROP-121.1 (Sub-task) Read and unread creators and friends
  - DROP-121.2 (Sub-task) Pending requests
  - DROP-121.3 (Sub-task) Flooded inbox
- **DROP-122** Messages pop in after a tap instead of being pre-populated
  - DROP-122.1 (Sub-task) Diff-based pop on new messages
  - DROP-122.2 (Sub-task) 450ms pop window
- **DROP-124** Design review (emil-design-eng) fixes
  - DROP-124.1 (Sub-task) Creator named once, no title text on the art
  - DROP-124.2 (Sub-task) No pin glyph in Pinned
  - DROP-124.3 (Sub-task) Amber count badge on Waiting on you
  - DROP-124.4 (Sub-task) Filled primary buttons: I'm following, Open chat, Reply in chat
  - DROP-124.5 (Sub-task) Request copy: "Wants to send you a link. No need to accept."
  - DROP-124.6 (Sub-task) Pin as a round icon on the sheet art
  - DROP-124.7 (Sub-task) Micro text raised to 12px
  - DROP-124.8 (Sub-task) 44px hit areas without changing the look
- **DROP-125** Motion pass (/animate)
  - DROP-125.1 (Sub-task) --ease-out and --ease-drawer tokens
  - DROP-125.2 (Sub-task) Sheet enter and exit
  - DROP-125.3 (Sub-task) Screen push and pop
  - DROP-125.4 (Sub-task) 160ms exit on closers
  - DROP-125.5 (Sub-task) Press scale on :active
  - DROP-125.6 (Sub-task) Reduced-motion fallback
  - DROP-125.7 (Sub-task) Hover gating
- **DROP-127** One-line summary replaces Details
  - DROP-127.1 (Sub-task) Hand-written line for each of 19 resources
  - DROP-127.2 (Sub-task) Grey "You commented KEYWORD" line

Totals: 2 initiatives, 13 epics, 121 Level 0 items, 67 sub-tasks.

---

## 12. Release plan

1. **Prototype review.** Walk the prototype with 5 heavy commenters. Pass if they find a saved link in under 2 taps.
2. **Spikes** in Epics DROP-3, DROP-5, DROP-6 and DROP-10 answer the open feasibility questions.
3. **V1 build**: Initiative DROP-1, Epics DROP-3 to DROP-10.
4. **Measurement** (Epic DROP-10) ships before rollout, not after.
5. **V2** (Initiative DROP-2, Epics DROP-11 to DROP-14) only if V1 shows revisit and search demand.

## 13. Out of scope for this document

Visual specs (see the prototype and the deck), Instagram's own ranking and ads, creator-side tooling, and monetisation.
