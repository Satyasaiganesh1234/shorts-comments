# Shorts comments, kept in the moment

**Independent concept project · Mobile interaction design · Android · 360 × 800 dp**

> This is an independent concept and is not affiliated with or endorsed by YouTube. No user research or usability results are claimed here. Replace every bracketed research prompt with evidence you collect.

## The opportunity

Shorts viewers may want context, reactions, or a quick way to join a conversation, but opening comments can interrupt the video and make it harder to return to the exact moment. This concept treats comments as a lightweight layer attached to the video: open, scan, participate, and return with minimal context loss.

**Design question:** How might we make the first useful comment easy to find and responding feel low effort, while preserving a clear, quick return to the Short?

**Working assumptions to validate:** viewers value the video remaining visible; a few relevant comments are more useful than an undifferentiated wall; people need confidence that their multilingual text is preserved; and the sheet must work on constrained devices and connections. These are hypotheses, not findings.

## Success criteria (to validate)

- Viewers can open comments and return to the same Short without losing their place.
- Viewers can find the full thread, sort, react, report, write, and reply without guessing at controls.
- Draft text survives common interruptions such as closing the panel or a transient network failure.
- Controls remain readable and operable with larger text, TalkBack, and one-handed reach.
- The experience does not optimize for comment volume at the expense of safety or viewing wellbeing.

Do not report success until measured. Define a baseline and target after formative research and a pilot usability test: **[INSERT TASK COMPLETION BASELINE/TARGET]**, **[INSERT TIME ON TASK BASELINE/TARGET]**, **[INSERT ERROR/RECOVERY TARGET]**.

## Research plan — run this before calling the design validated

### Interviews

Recruit 8–12 Shorts viewers aged 16–35 in India, deliberately including light and heavy viewers, commenters and non-commenters, and people who use English, Hindi, Hinglish, and regional languages. Include a mix of Android device tiers and connectivity conditions. This is a practical formative sample, not a representative survey. For minors, use an appropriate consent and safeguarding process; exclude them if you cannot do that responsibly.

Run 25–35 minute semi-structured sessions. Ask participants to show or describe their normal behavior rather than endorse a proposed solution.

1. “Think of the last Short where you wanted to read comments. What made you open them?”
2. “Tell me about a time comments interrupted your viewing or helped you understand the video.”
3. “What do you do when there are many replies or the language is unfamiliar?”
4. “When do you decide not to comment? What would make posting feel risky or inconvenient?”
5. “What happens if your connection slows while comments are open?”
6. “How do you expect to get back to the same place in the video?”
7. “What comment content makes you report, block, or leave?”

Capture notes with consent, redact handles and identifying details, and tag observations by behavior and context. Synthesize into themes only when supported by repeated evidence or a clearly noted outlier. Record: **[INSERT THEME + EVIDENCE]**, **[INSERT COUNTEREXAMPLE]**, **[INSERT OPEN QUESTION]**.

### Survey

Use a short survey for directional prevalence after interviews inform the wording. Do not present a convenience sample as representative of India. Ask about behavior frequency, preferred language(s), device/connectivity context, and reasons for opening, not opening, or leaving comments. Pilot comprehension and translation first. Report sample source, dates, n, and limitations: **[INSERT REAL SURVEY DETAILS]**.

### Usability study

Test a clickable prototype with 5–7 target users in two rounds, including TalkBack checks and at least one low-bandwidth simulation. Tasks: open top comments; find and expand a reply thread; sort newest; react; report; write in a preferred language; reply; close and return; recover from offline/error; understand disabled comments. Ask participants to think aloud, then probe confidence and lost context. Record observed behavior, not just preference. Findings: **[INSERT REAL FINDING]**. Changes made: **[INSERT CHANGE + TRACE TO EVIDENCE]**.

## Proposed experience

### Primary flow

1. On the Short, tap the comment count or the “Add a comment…” affordance.
2. A bottom sheet rises over a dimmed video. Keep the video playing initially; provide a clear close/chevron control and preserve playback position. Confirm this behavior in research because audio and motion can distract while reading.
3. Show a small set of top-level comments. Each has author/time, body, like/reaction, Reply, overflow, and an explicit “View N replies” thread affordance.
4. “View replies” expands inline; keep the parent comment visible. “View all comments” can be a later pagination step if the platform supports it.
5. Sort with Top and Newest. Selection updates in place and announces the selected sort to assistive technology.
6. Reply focuses the composer and labels the recipient. Submit creates a reply under its parent; preserve the parent context.
7. Close returns to the Short at its existing playback position. Keep draft text if the user closes accidentally; confirm expected behavior with users.

### Copy and states

| State | Display copy / behavior |
|---|---|
| Loading | “Loading comments…”; retain sheet header, avoid fake rows, announce loading once. |
| Empty | “Start the conversation” / “Keep it kind. Your comment will appear here.” |
| Error | “Comments didn’t load” / “Try again when your connection is steadier.” / “Try again” |
| Offline | “You’re offline” / “Reconnect to see the conversation.” Keep an unsent draft locally for this session. |
| Disabled | “Comments are turned off” / “The creator has disabled comments for this video.” Remove composer and sorting controls. |
| Posting | Disable duplicate submit; show “Posting…”; preserve text until server acknowledgement. |
| Post failure | “Couldn’t post. Your comment is still here.” Actions: “Retry” and dismiss. |
| Report | “Report comment” opens a reason sheet: Spam, Harassment, Hate, Misinformation, Other. Confirmation: “Thanks. Your report was sent for review.” |
| Thread | “View 12 replies” / “Hide replies”; show reply count and nesting visually and semantically. |

The prototype uses illustrative sample comments and simplified state behavior. They are not research data or claims about real Shorts users.

## Layout and interaction specs

Use dp as Android layout units. At the 360 × 800 reference frame, maintain 16 dp horizontal gutters. Use a 24 dp top corner radius, 4 × 32 dp drag handle, 56 dp minimum touch targets (visual icons can be 24 dp inside), and 48 dp composer height plus system inset. The sheet opens to 78% of available height (about 624 dp at the reference size), with a compact 85% variant on short screens. Keep a dim scrim behind the sheet and allow scrim tap to close. No swipe-only action: the close affordance is always present.

**Motion:** sheet open/close 280 ms, standard decelerate cubic-bezier(0.2, 0, 0, 1); scrim 220 ms with the same curve. Respect Android “Remove animations” / reduced motion by using an immediate state change. Avoid parallax and looping motion.

**Material 3 extension:** use familiar modal bottom-sheet, chips, text field, icon button, and snackbar patterns. Suggested dark tokens: background #090909; surface #202124; elevated surface #292A2D; primary text #F1F1F1; secondary text #AAAAAA; outline #3B3C3F; selected sort container #D3E3FD with #101820 text; focus ring #A8C7FA. Verify contrast against actual rendered text sizes and platform theme before implementation.

**Typography:** Roboto; title 17 sp/24 line height, body 14 sp/20, metadata and actions 12 sp/16. Support font scaling to 200% without clipping: allow sheet height to expand, body wrap, and composer to grow. Avoid fixed-height comment rows.

**Touch and accessibility:** semantic dialog label “Comments, 482”; announce loading/error/post result through a polite live region; provide explicit labels such as “Like comment by Aarav K.” and “More options for comment by Aarav K.”; selected sort exposes selected state; keyboard focus enters sheet and returns to trigger on close; focus stays within modal while open. Maintain 4.5:1 contrast for normal text. Never rely on color alone for liked/reported states. Test TalkBack order, switch access, landscape prohibition/rotation policy, and large text. Add language metadata per comment where possible; do not assume all text is English.

**Performance and connectivity:** render first comments from cache when available, then reconcile with server; paginate rather than render a large thread at once; use stable IDs and incremental updates; avoid autoplaying media inside comments. Keep draft in memory through transient errors and sheet close; persistence across app restart needs privacy/product review. Provide retry with backoff and do not repeatedly poll offline. These are implementation proposals for PM/engineering feasibility review, not platform guarantees.

## Moderation, wellbeing, and trade-offs

- **Engagement vs. wellbeing:** comments can create connection and context, but can also pull attention away from the video or encourage compulsive checking. Keep the entry point clear without adding urgency, streaks, or a persistent notification badge. Consider pausing video only if research shows simultaneous audio/video harms comprehension; expose that choice or follow platform convention.
- **Creator interests:** creator hearts and visible replies can strengthen community, but can create perceived favoritism. Keep creator reactions visually secondary and label them accessibly.
- **Moderation risk:** sorting “Top” can amplify harmful or polarizing content. Honor safety ranking and moderation rules; reporting must be reachable from each comment; do not imply a report is an immediate removal. Consider hiding/reporting controls and blocked-user behavior in follow-up scope.
- **Low-end Android:** avoid heavy blur, complex nested animation, and loading many replies at once. The video layer should not be repeatedly recreated when the sheet opens. Validate frame stability and memory with engineering on representative devices.
- **Translation:** in-language composition is essential; machine translation can distort tone. Treat translation as an explicit, reversible product capability only after research and policy review.

## Flow map

```text
Short playing
 ├─ tap comment entry → loading → comments list
 │   ├─ top/newest → reordered list
 │   ├─ view replies → expanded thread → reply composer → posted reply
 │   ├─ react → reaction state
 │   ├─ overflow → report reason → confirmation
 │   ├─ composer → posting → posted / retryable failure
 │   └─ close/scrim → same Short and playback position
 ├─ no comments → empty state → composer
 ├─ request failure → error → retry
 ├─ no connection → offline → reconnect/retry, preserve draft
 └─ comments disabled → explanation, no composer or sort
```

## Prototype and design review

Open `shorts-comments-prototype.html` in a browser. It is a self-contained interaction prototype sized for a phone viewport. The buttons above the video switch between ready, loading, empty, error, offline, and disabled states. The sheet demonstrates opening/closing, sorting, posting, reply focus, reactions, and reporting. The thread expansion and server-backed behaviors are illustrative and must be completed in Figma or a coded handoff before claiming production fidelity.

### Figma build checklist

- Create Android frame 360 × 800; set layout grid to 4 columns, 16 dp margins, 8 dp gutters.
- Make components with variants: sheet (loading/ready/empty/error/offline/disabled), comment (top-level/reply/liked/creator-heart), sort chip (selected/unselected), composer (idle/focused/typing/posting/error), report reason sheet.
- Use Auto Layout for the sheet, variable-height comment body, and composer; define tokens above as styles/variables.
- Add prototype links for all branches in the flow map; include keyboard/focus and reduced-motion annotations.
- Use only fictional handles and clearly label the artifact as an independent concept.

### Design review narrative

1. **Problem:** the comment journey risks breaking the viewing moment.
2. **Evidence:** present only collected evidence: [INSERT REAL FINDING + METHOD + N].
3. **Principle:** comments should feel attached to the Short, with a reliable return path.
4. **Design:** show the sheet, top-to-thread transition, composer, and failure recovery.
5. **Trade-offs:** discuss video continuity, moderation ranking, creator recognition, and device/network constraints.
6. **Validation:** report task observations and unresolved issues, with sample and limitations.
7. **Next:** prioritize one change tied to evidence and one engineering question.

## What you still need to do

- Recruit and run the real interviews, survey, and usability sessions; add no invented quotes or numbers.
- Replace every bracketed placeholder with source-linked notes and explain contradictions.
- Rebuild/extend the prototype in Figma using the component checklist; validate all branches with participants.
- Review moderation, privacy, draft persistence, video playback, ranking, and analytics decisions with PM, engineering, and policy partners.
- Capture actual device screenshots and accessibility checks for the final case study.

## Case-study evidence checklist

- [ ] Research screener, consent approach, dates, participant composition, and limitations
- [ ] Interview guide, anonymized evidence excerpts, affinity themes, and counterexamples
- [ ] Survey instrument, sampling method, response count, and directional limitations
- [ ] Before/after flow and annotated wireframes linked to specific findings
- [ ] Figma prototype link and state coverage
- [ ] Usability task script, observed issues, iteration log, and final measured results
- [ ] Accessibility review (contrast, text scaling, TalkBack, touch targets)
- [ ] Feasibility notes from PM/engineering and open questions
- [ ] Honest reflection: what changed, what did not work, and what you would test next
