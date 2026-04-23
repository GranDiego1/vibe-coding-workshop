# LunchLog: PRD

> **This is a reference example.** It shows what a filled-in PRD looks like using the food-waste problem that runs through the workshop. Use it as a "good looks like this" anchor when reading the empty template. Do not copy-paste; your PRD should come from your own evidence.

**Owner:** Diego G.
**Status:** Draft v1
**Last updated:** 2026-04-23

---

## 1. Problem & User

### The problem
Parents of kids 4-10 throw out $30-$60 worth of food every week because their kids' preferences change faster than a weekly grocery run can keep up with.

### The person
Parents of one or two kids ages 4-10 who do one large grocery trip per week, pack lunchboxes most weekdays, and cook the family's weeknight dinners. They are not picky themselves, but their kids are, and the preferences shift. A food that worked on Monday is refused on Wednesday. The parent finds out by seeing a full lunchbox come back at 4pm or a half-eaten plate scraped into the trash at 7pm.

### Why it matters to them
This happens weekly, not occasionally. The financial hit ($30-$60/week, per parent-reported quotes) is meaningful but the bigger cost is emotional: parents describe guilt, a sense of failing a basic parenting task, and frustration that they cannot predict what their own kid will eat. Existing meal-planning tools assume a family eats one meal together. Nobody has built something sized to "one picky kid whose preferences change."

---

## 2. Evidence

The proof this problem is real, not a hunch.

### Key quotes from research
- "I swear I throw out half the grapes I buy every week. My 6yo loves them on Monday, hates them by Thursday." (r/Parenting thread on weekly waste)
- "We lose $40-$60 a week to my kid's changing preferences. The lunchbox comes back untouched 3 days out of 5 and I cannot figure out the pattern." (r/Parenting frustration thread)
- "Tried meal planning apps. None of them account for 'my 7 year old decided today she does not eat cheese anymore'." (r/daddit)
- "Nobody makes a tool that tracks what my kid actually ate. We get a weekly school newsletter, a toy tracker app, but nothing for the one thing we spend the most on: food." (Working Mother community)

### Patterns we saw
- Preferences shift mid-week. Parents describe this as the top trigger for waste, not quantity-buying.
- Parents cannot see what their kid actually ate vs. threw away. Lunchboxes come back and home leftovers are cleaned up before anyone counts.
- Meal-planning tools assume family-wide preferences. Per-kid preferences that change are not modeled.
- Financial pain is specific and named. Multiple parents give dollar amounts in the $30-$60/week range.

### What this tells us
The problem is recurring, expensive, and invisible. Parents already know food waste is a problem but cannot see it happening in real time and cannot act on it because their tools treat the family as one unit. Any solution that makes per-kid preferences visible and useful for next week's shopping has a real audience. Any solution that keeps lumping the family together will not land.

---

## 3. Goals & Success Metrics

### Job to be done
When I am planning this week's groceries, I want to know what my kid actually ate last week, so I can buy less of what they rejected and more of what they finished.

### Success metrics
If this product shipped, we would measure:
1. Active parents log at least 3 meals per week by week 2.
2. Weekly self-reported "food thrown out" drops by 30% within 4 weeks of regular use.
3. 50% of users who complete the first week's logging return for a second week.

---

## 4. Solution Overview

LunchLog is a quick daily check-in for parents to log what their kid ate, didn't eat, and seemed to like. It takes under 60 seconds per day, builds a per-kid profile over a few weeks, and turns that profile into a focused shopping list for next week's grocery run. The promise: "see what your kid actually ate, then shop for that."

---

## 5. Key CUJs (Critical User Journeys)

| Priority | Category | CUJ | Description |
|---|---|---|---|
| P0 | Logging | As a parent, I want to log what my kid ate in under 60 seconds | End-of-day quick log, tapping items from a short list. This is the habit the product lives or dies on. |
| P0 | Insight | As a parent, I want to see which foods my kid rejected vs. finished last week | One summary view per kid. Tells me what to stop buying. |
| P0 | Shopping | As a parent, I want a shopping list shaped by last week's actual eating | List grouped by "buy more," "buy less," "skip this week." The whole reason to log. |
| P1 | Multi-kid | As a parent of two, I want separate profiles per kid | Kids have different preferences. Lumping them together defeats the purpose. |
| P1 | Sharing | As a parent, I want to send the shopping list to my partner | Handoff is a real weekly moment. Email or text, not in-app chat. |
| P2 | School lunches | As a parent, I want to log what came back in the lunchbox | Separate logging moment from dinner. Deferred because schools + adults photographing leftovers is friction-heavy. |

P0 = must have for MVP. P1 = next release. P2 = someday.

---

## 6. MVP Scope

This section expands the P0 CUJs into product detail. Not engineering detail. What does the user see, feel, and expect? What edge behavior should the prototype handle?

### P0 CUJ #1: Log what my kid ate in under 60 seconds
**What the user expects:** The user opens the app after dinner. Their kid's name and today's date are pre-populated on the home screen. They see a short list of the most common foods they've logged before, plus a "+ add item" button. They tap foods from the list, and for each one choose "finished," "some," or "none." A big "Done" button at the bottom saves the log. If they have two kids, they swipe or tap to switch kid and repeat.

**Edge behavior:** If they haven't logged anything before, the list is empty and they can type or tap "+ add item" to build it. If they miss a day, there is no guilt-trip, just an unobtrusive "skipped" marker on the week view. If they open the app mid-week and want to log dinner from two days ago, they can tap the date to change it.

**What success looks like:** The parent logs, closes the app, and feels like that took no time. Within a week, the list of common foods is long enough that logging is pure tapping, no typing.

### P0 CUJ #2: See which foods my kid rejected vs. finished last week
**What the user expects:** On the weekly summary view, each kid has a card showing foods broken into three groups: "finished" (green), "some" (yellow), "none" (red). The parent can tap a food to see the specific days and what happened. No charts, no scores. Just the list, sorted by how often each food came up.

**Edge behavior:** If there is only a day or two of data, the view says so and doesn't pretend to show a pattern. If a food was finished on Monday and refused on Thursday, it shows up in both piles with the dates, no forced averaging.

**What success looks like:** The parent scans the red pile, has an "oh, she stopped eating cheese again" realization, and adjusts next week's list without needing the app to tell them what to do.

### P0 CUJ #3: Shopping list shaped by last week's eating
**What the user expects:** From the weekly summary, the parent taps "Build this week's list." The list auto-generates three sections: "Buy more" (foods finished this week), "Same as usual" (mixed), "Skip this week" (refused more than once). Each item has a checkbox. The parent can drag items between sections or delete them. A "Copy list" button puts the result on the clipboard. A "Send to [partner]" button opens the phone's share sheet.

**Edge behavior:** If there isn't enough data yet, the "Skip this week" section is empty and the app says "Log a few more meals to see this." Parents can add items that aren't based on the log (milk, bread, staples) through a "+ add" row.

**What success looks like:** The parent shops, buys less of what the kid rejected, wastes less, and comes back the following week without needing to be reminded.

### Explicitly out of scope for MVP
- No recipe suggestions. The product is about what the kid already ate, not new meals.
- No integrations with grocery delivery services. The list exports as plain text.
- No social or community features. The log is private.
- No nutrition tracking or macros. This is not a diet app.

---

## 7. Requirements & Trade-offs

### Must-haves
1. Logging takes under 60 seconds after the first week of use. If it doesn't, nobody logs.
2. Multi-kid support within the P0 experience, even if MVP ships with a single profile. Two-kid families are a big slice of the audience.
3. The weekly view loads without interpretation. No forced averaging, no AI opinions on top. Parents want the raw view.

### Nice-to-haves
1. Voice logging ("Ava finished her pasta, didn't touch the broccoli").
2. Partner sync so both parents log to the same profile from their own phones.
3. Shopping-list categories grouped by store aisle.

### Trade-offs we are making
- **Manual logging over automatic detection:** We are choosing a parent-driven 60-second log instead of something fancy (photo recognition, plate-weight sensors, etc.) because the friction is in habits, not data capture, and we need this to work without hardware.
- **Weekly granularity over daily insights:** The summary is weekly, not daily, because parents make one shopping run per week. Daily insight would be cool but solves a problem nobody has.
- **No recipe engine in MVP:** Recipes are the most-requested "nice to have" but also the fastest way to turn this into another meal-planning app that gets deleted. We are staying narrow on purpose.

---

## 8. Risks & Open Questions

### What could kill this
- **Habit:** The product only works if parents log 4+ times per week. If end-of-day logging feels like a chore in week 2, it is over. The 60-second bar is not optional.
- **The "I already know" problem:** Some parents may feel they already know what their kid ate. The product has to show them a pattern they didn't know, in week one, or they bounce.
- **Two-parent handoff:** If both parents don't use it, one parent ends up logging everything and the data is incomplete. Partner support is listed as P1 but may need to move up.
- **Monetization:** Parents in the research describe willingness to pay, but the current plan doesn't address pricing model. Freemium? One-time? Subscription?

### Open questions
- Does the "Skip this week" insight actually change shopping behavior, or do parents ignore it and buy the same thing anyway? We need a 2-week test with 10 parents to find out.
- How do we handle foods a kid has never tried? The log assumes a history.
- Is the lunchbox a separate UX or folded into daily logging? P2, but the research is pushing hard for it.
- What happens at the grandparents' house, at daycare, at a party? Off-site meals are a gap.
