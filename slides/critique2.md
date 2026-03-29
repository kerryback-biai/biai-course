# Slide Deck Critique — Round 2

## Critical

| # | Finding | Source |
|---|---------|--------|
| 1 | **Password exposed in public repo** — `build.sh` contains plaintext password and the repo is public. Anyone can read it. Decision: accept risk (security through obscurity is sufficient for course access control). | Devil's Advocate |
| 2 | **HPE Fortune citation is fabricated** — "Fortune, 'How HPE's CFO Built an AI Agent,' October 2024" doesn't exist. Real article is from Feb 2026 with a different title. | Devil's Advocate |
| 3 | **DUNNIXER still wrong** — Title now says "Eight Dimensions" but the actual source article has 6. The slide author invented 2 extra dimensions. Students will read the article and notice. | Devil's Advocate |

## Warning

| # | Finding | Source |
|---|---------|--------|
| 4 | **Gartner "70%" attribution unverifiable** — "(Gartner)" was added but this specific stat may not be from Gartner. Adding a false citation is worse than none. | Devil's Advocate |
| 5 | **Sessions 3 and 4 lack explicit `---` separators** between slides (unlike all other decks). Works via implicit `##` splitting but inconsistent. | Clarity |
| 6 | **Session 4 production pipeline step-flow uses HTML entities** (`&#128337;` etc.) for icons — inconsistent with plain numbers used everywhere else. | Clarity |
| 7 | **Session 6 teaser says "Next session"** instead of the "Wednesday's session" pattern used by all others. | Correctness |
| 8 | **Morgan Stanley citation** — "AI at Work case, 2024" is vague. Should match whatever document students actually receive as pre-reading. | Devil's Advocate |

## Suggestion

| # | Finding | Source |
|---|---------|--------|
| 9 | Session 5 homework adds "complete deployment profile draft" not in course design — minor scaffolding addition. | Correctness |
| 10 | Session 8 capstone timing is tight (30 min breakout = exactly 5 min x 6 people, zero buffer). | Devil's Advocate |
| 11 | "What If You're Not Ready?" slide is good — builds credibility, doesn't undermine course. | Devil's Advocate |
| 12 | Converted quote slides to centered-statements work well — no loss of persuasive force. | Devil's Advocate |
