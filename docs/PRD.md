# Drops: product requirements document

Author: Archana Raghu Prasad. Status: draft for review, October 2026. Educational concept, not affiliated with Meta. Handles and people are invented.

Companion files: the clickable prototype (`index.html`), the concept deck (`docs/drops-concept-v5.pdf`) and the changelog (`CHANGELOG.md`).

How this document is organised. It follows Jira terminology: one **Initiative** holds **Epics**, an Epic holds **Stories**, **Tasks** and **Bugs**, and a Story or Task holds **Sub-tasks**. **Spikes** are time-boxed research tasks. Keys look like `DROP-12`. Fix versions are **V1** (the core fix) and **Later** (finding things once the library grows).

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
| Resources pinned, aliased or listed (Later) | Up | Action counts |
| Summary edit or alias rate (quality proxy) | Low | Alias set on summarised links |

## 6. Scope

**V1:** friends-first inbox with the floating Drops banner, Drops home (Waiting on you, Waiting for link, Pinned, Recent), requests that land in Waiting on you with no Accept, one follow check, the resource sheet with a one-line summary and a Pin icon, the in-app browser on Open link, delivery rules, noise tucked away.

**Later:** double-tap pin gesture, search by memory with recent searches, topic rows with See all and Customize topics, aliases, flat user lists, Creators you engaged with and creator pages, Recent grouped by creator.

**Why the split:** V1 fixes the two problems, friends buried and links lost. Later helps finding things once the library grows.

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

Priority is P0 to P2. Estimates are story points. Everything is `To Do` except items under **Epic DROP-100**, which describe the prototype and are `Done`.

### Initiative DROP-1: Make creator links findable without burying friends

#### Epic DROP-2: Classify and group automated DMs (V1)

Goal: know which messages belong in Drops, and where each resource stands.

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-3 | Spike | Confirm which fields identify an automation-sent message and a Private Reply | P0 | 3 |
| DROP-4 | Story | As a commenter, a creator's automated DMs are grouped as one resource per comment sequence | P0 | 8 |
| DROP-5 | Story | As a commenter, a sequence is marked Delivered when a URL button, text URL or attachment arrives | P0 | 5 |
| DROP-6 | Story | As a commenter, I see Waiting on you when the creator needs a tap or typed reply | P0 | 3 |
| DROP-7 | Story | As a commenter, I see Waiting for link when I did my part and nothing arrived | P0 | 3 |
| DROP-8 | Task | Define the ambiguous-window rule for two comments on one creator the same day | P1 | 2 |
| DROP-9 | Task | Event schema: `drop_delivered`, `drop_waiting_on_you`, `drop_waiting_for_link` | P1 | 2 |

DROP-4 acceptance criteria
- Given an automated DM with an echo flag after my comment, when it arrives, then it joins the resource for that comment.
- Given two comments on one creator the same day, when a message cannot be tied to one, then it attaches to the earlier open sequence and is flagged ambiguous in logs.
- Given a friend's DM, then it is never grouped.

Sub-tasks for DROP-4: DROP-4a sequence model, DROP-4b time-window matcher, DROP-4c friend exclusion test, DROP-4d backfill for existing threads.

DROP-5 acceptance criteria
- A URL button, a URL in message text, and a file or media attachment each mark Delivered.
- `instagram.com` links never mark Delivered.
- A message with a link per bullet is stored as one resource with several links.
- A prompt after delivery ("Reply YES for the next part") is noise, not a new gate.

#### Epic DROP-10: Inbox shows friends first (V1)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-11 | Story | As a commenter, automated DMs leave the main list so only friends and ordinary chats show | P0 | 5 |
| DROP-12 | Story | As a commenter, a floating banner above the tab bar opens Drops and stays visible while I scroll | P0 | 3 |
| DROP-13 | Story | As a commenter, the DM tab badge counts only friends' unread messages | P0 | 3 |
| DROP-14 | Task | Banner copy: "N new links this week" with the creator names | P2 | 1 |
| DROP-15 | Task | Keep the banner clear of the home indicator and tab bar on 402 x 874 | P2 | 1 |

DROP-11 acceptance criteria
- Given automated DMs exist, when I open Messages, then none appear in the main list.
- Nothing is deleted. Opening the creator's profile or Go to chat still shows the full thread.
- A friend I follow who sends a link manually stays in the main list.

DROP-13 acceptance criteria
- Given 2 unread creator DMs and 1 unread friend DM, then the badge shows 1.

#### Epic DROP-20: Drops home (V1)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-21 | Story | As a commenter, the home shows Waiting on you and Waiting for link rows on top | P0 | 5 |
| DROP-22 | Story | As a commenter, Waiting on you shows an amber count badge when above zero | P1 | 1 |
| DROP-23 | Story | As a commenter, Pinned and Recent rows scroll sideways with resource cards | P0 | 5 |
| DROP-24 | Story | As a commenter, a new resource highlights in Recent when it lands | P2 | 2 |
| DROP-25 | Task | Card: art with colour and a faint type glyph, title once, creator as meta, no title on the art | P1 | 2 |
| DROP-26 | Task | Cards inside Pinned show no pin glyph | P2 | 1 |

DROP-21 acceptance criteria
- Waiting on you expands to a card per item, with one primary filled action per card.
- Waiting for link expands to a card per creator with "Go to chat".
- Rows collapse by default to keep the home short.

#### Epic DROP-30: Message requests skip Accept (V1)

Before keeps Requests then Accept. After removes the step.

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-31 | Story | As a commenter who does not follow a creator, their DM appears in Waiting on you | P0 | 5 |
| DROP-32 | Story | As a commenter, I can open the request chat from Waiting on you and read it without accepting | P0 | 5 |
| DROP-33 | Story | As a commenter, the request resolves into Recent once the creator delivers | P1 | 3 |
| DROP-34 | Task | Request card copy: "Wants to send you a link. No need to accept." | P2 | 1 |
| DROP-35 | Spike | Check spam and safety rules for showing non-follower requests before acceptance | P0 | 3 |
| DROP-36 | Task | Before flow: Requests (n) link in blue, with the Accept, Delete and Block bar | P2 | 1 |

DROP-31 acceptance criteria
- Only requests tied to a comment I made appear.
- The card shows the creator and one action: Open chat.
- A request I did not comment on stays in the normal Requests list.

#### Epic DROP-40: One follow check (V1)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-41 | Story | As a commenter, "I'm following" checks my follow state once | P0 | 3 |
| DROP-42 | Story | As a commenter who does not follow, I see a one-line hint and the button does nothing else | P0 | 2 |
| DROP-43 | Task | Remove the repeating in-chat follow gate and its counter | P1 | 2 |
| DROP-44 | Story | As a commenter, once I follow and tap, the card unlocks and moves to Recent with a toast | P1 | 3 |
| DROP-45 | Spike | Confirm whether the platform can fire the creator's "I'm following" tap | P1 | 3 |

DROP-41 acceptance criteria
- Given I do not follow the creator, when I tap "I'm following", then a hint shows and the state does not change.
- Given I follow, when I tap, then the state becomes "checking" for a short time, then unlocked.
- Tapping repeatedly cannot send more than one confirmation.

#### Epic DROP-50: Resource sheet (V1)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-51 | Story | As a commenter, the sheet shows a one-line summary and a grey "You commented KEYWORD on their reel" | P0 | 5 |
| DROP-52 | Task | Summary service: one call per delivered link, cached | P0 | 5 |
| DROP-53 | Task | Prompt and guardrails: stay close to the creator's words, no invented detail, empty when low confidence | P0 | 3 |
| DROP-54 | Story | As a commenter, the creator is named once and the date is small text | P1 | 2 |
| DROP-55 | Story | As a commenter, Pin is a round icon on the art, filled when pinned | P1 | 2 |
| DROP-56 | Story | As a commenter, Open link opens an in-app browser | P0 | 5 |
| DROP-57 | Story | As a commenter, link buttons in creator chats open the same browser | P0 | 3 |
| DROP-58 | Story | As a commenter, Go to chat opens the thread with the delivered message highlighted | P1 | 3 |
| DROP-59 | Task | Remove the Details toggle, quoted message and caption from the sheet; keep them searchable | P1 | 2 |

DROP-51 acceptance criteria
- The sheet never shows the DM text or the caption.
- The summary is at most two lines.
- If no summary exists, the line is omitted, not filled with placeholder text.

DROP-56 acceptance criteria
- The browser shows a close control, a lock and the host, and a toolbar clear of the home indicator.
- Close returns to the sheet with an exit animation.
- Links show their domain only. Shortened links are not expanded.

Sub-tasks for DROP-52: DROP-52a model selection and cost budget, DROP-52b background job on delivery, DROP-52c cache and regenerate, DROP-52d feedback signal when the user sets an alias.

#### Epic DROP-70: Noise is tucked away (V1)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-71 | Story | As a commenter, messages after the delivered link are marked "Tucked away" in the chat | P1 | 3 |
| DROP-72 | Story | As a commenter, a Tucked away sheet explains what is tucked and shows a count | P2 | 2 |
| DROP-73 | Task | Define noise by position after delivery, not wording | P1 | 2 |
| DROP-74 | Task | Leave comments, public replies and notifications untouched | P0 | 1 |

#### Epic DROP-60: Find it again (Later)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-61 | Story | As a commenter, search matches what the reel or post was about, not only names | P1 | 8 |
| DROP-62 | Story | As a commenter, recent searches show and I can delete one | P2 | 2 |
| DROP-63 | Story | As a commenter, See all lists reels and posts for a topic with All, Reels and Posts filters | P2 | 3 |
| DROP-64 | Story | As a commenter, Customize topics lets me turn topic rows off | P2 | 3 |
| DROP-65 | Story | As a commenter, double-tapping a card pins it | P2 | 2 |
| DROP-66 | Spike | Check how search indexes caption and message while the sheet hides them | P1 | 2 |

#### Epic DROP-80: Organise your way (Later)

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-81 | Story | As a commenter, I add an alias from a greyed prompt beside the title | P2 | 3 |
| DROP-82 | Story | As a commenter, I add a link to a list, or start a list | P2 | 5 |
| DROP-83 | Story | As a commenter, once lists exist the control shrinks to a small chip | P2 | 2 |
| DROP-84 | Story | As a commenter, my lists show under Pinned on the home | P2 | 3 |
| DROP-85 | Task | Alias and list names are searchable | P2 | 2 |
| DROP-86 | Story | As a commenter, I see Creators you engaged with and a creator page | P2 | 5 |

DROP-81 acceptance criteria
- The alias shows in brackets beside the original title and never replaces it.
- Only I see it. It shows in Drops and in search.

DROP-82 acceptance criteria
- Lists are flat. No nesting, no parent topic.
- A link can sit in several lists.
- Removing a link from a list does not delete the resource.

#### Epic DROP-90: Measurement and rollout

| Key | Type | Summary | Priority | Points |
| --- | --- | --- | --- | --- |
| DROP-91 | Task | Instrument the metrics in section 5 | P0 | 3 |
| DROP-92 | Task | Holdout group for the comment-to-DM participation guardrail | P0 | 3 |
| DROP-93 | Task | Staged rollout: creators who connect an app first, then all users | P1 | 3 |
| DROP-94 | Task | Kill switch to restore the old inbox | P0 | 2 |
| DROP-95 | Spike | Check whether data exports keep button URLs | P2 | 2 |

#### Epic DROP-100: Prototype and portfolio quality (Done)

Everything here is in the clickable prototype. Bugs are listed with their cause.

| Key | Type | Summary | Status |
| --- | --- | --- | --- |
| DROP-101 | Story | iPhone 17 frame, 402 x 874, island, home indicator 134 x 5 at 8px | Done |
| DROP-102 | Story | Before and After flows, with a mixed crowded inbox (read and unread creators and friends, pending requests) | Done |
| DROP-103 | Story | New messages pop in instead of being pre-populated | Done |
| DROP-104 | Story | Emoji row in the comment sheet adds to the comment | Done |
| DROP-105 | Story | Motion pass: sheet and screen enter and exit, press scale, reduced motion, hover gating | Done |
| DROP-106 | Story | In-app browser mock on every link action | Done |
| DROP-107 | Task | Rename from "DM to Link" to "Drops" in the prototype, README and docs | Done |
| DROP-108 | Task | Concept deck v5 (13 pages) with screenshots from the current prototype | Done |
| DROP-109 | Bug | Delivered link buttons in non-story creator chats were inactive. Cause: the active check only allowed the story chat. Fixed. | Done |
| DROP-110 | Bug | The story chat's link button toasted but did not re-render. Cause: the handler returned before `render()`. Fixed. | Done |
| DROP-111 | Bug | The comment composer sat under the home indicator. Fix: 34px bottom padding. | Done |
| DROP-112 | Bug | The Requests link was red. It is now blue. | Done |
| DROP-113 | Bug | Request thread did not scroll to the newest message. Fix: include `req:` in the scroll-to-bottom rule. | Done |
| DROP-114 | Bug | Card render passed the array index as the `inPin` flag. Fix: explicit lambdas. | Done |
| DROP-115 | Bug | In a 402 px wide browser window the comment field sits 27px above the bottom edge and the check expects 30px. Not investigated. | Open |
| DROP-116 | Task | Figma restructure into flows, components and auto-layout. Blocked by the Figma MCP call limit. | Blocked |
| DROP-117 | Task | Motion has been checked in code and screenshots, not watched in a real browser | Open |

---

## 12. Release plan

1. **Prototype review.** Walk the prototype with 5 heavy commenters. Pass if they find a saved link in under 2 taps.
2. **Spikes** DROP-3, DROP-35, DROP-45 and DROP-95 answer the open feasibility questions.
3. **V1 build**: Epics DROP-2, DROP-10, DROP-20, DROP-30, DROP-40, DROP-50, DROP-70.
4. **Measurement** (DROP-90) ships before rollout, not after.
5. **Later** (DROP-60, DROP-80) only if V1 shows revisit and search demand.

## 13. Out of scope for this document

Visual specs (see the prototype and the deck), Instagram's own ranking and ads, creator-side tooling, and monetisation.
