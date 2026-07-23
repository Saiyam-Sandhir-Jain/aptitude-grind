# Calendar — Tricks, Shortcuts & Question Patterns
### Anchor-Day Method, Month Codes & What Repeats in TCS / CAT

## 1. The Anchor-Day Method (Fastest for Placement Tests)

Instead of counting odd days from year 1, work relative to a **known reference date** that is close
to your target date. Most questions either give you a reference day directly, or you can use a
memorized anchor.

**Useful Anchors to Memorize**
- 1 January, 1 AD → Monday
- 1 January, 1600 (or 2000) → Saturday
- 1 January, 2000 → Saturday (most practical anchor for modern-date questions)

**Anchor-Day Procedure**
1. Find the number of complete years between the anchor and target year.
2. Odd days contributed = (ordinary years × 1) + (leap years × 2), reduced mod 7.
3. Add odd days for the months elapsed in the target year, then add the date number.
4. Add this to the anchor's day-of-week position (mod 7) and read off the result.

**Example — Using an Anchor**

*If 1 Jan 2000 was a Saturday, what day was 1 Jan 2010?*
- Years 2000–2009 (10 years elapsed up to 1 Jan 2010)
- Leap years in that span: 2000, 2004, 2008 → 3 leap years; ordinary years: 7
- Odd days = (3×2) + (7×1) = 13 ≡ 6 (mod 7)
- Saturday + 6 odd days → **Friday**

---

## 2. Month Codes Method (a.k.a. Doomsday-style Shortcut)

A faster alternative used heavily in coaching materials: assign each month a fixed **code**
representing its odd-day contribution from 1 January of a non-leap year up to the 1st of that month.

**Month Codes — Non-Leap Year**

| Month | Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec |
|-------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| Code  | 0   | 3   | 3   | 6   | 1   | 4   | 6   | 2   | 5   | 0   | 3   | 5   |

> 💡 **Leap Year Adjustment:** For a **leap year**, subtract 1 from the codes of **January and
> February only** (since the extra day, 29 Feb, hasn't occurred yet when computing odd days up to
> those months). From March onward in a leap year, use the codes as-is since the leap day has
> already been "absorbed."

**Putting It Together**
```
Day code = (Date + Month code + Year's odd days from anchor century) mod 7
```
Match the result against the Odd-Days → Day table from `01-fundamentals.md`.

> ⚠️ **When to Use Which Method:** The **odd-days-from-scratch** method (Notes 1) is more intuitive
> and safer under exam pressure because you derive everything instead of recalling a code table. The
> **month-code** method is faster once memorized, but a single misremembered code silently gives a
> wrong answer. For placement tests with negative marking, prefer the method you can execute without
> doubt.

---

## 3. Same Calendar Repeats

> **Rule:** Two years have the **same calendar** if:
> 1. Both are ordinary years or both are leap years, **and**
> 2. The total number of odd days between them (summed year by year) is a multiple of 7.

**Example**

Find the next year with the same calendar as 2007 (an ordinary year).
- 2007 → 2008: ordinary year, 1 odd day. Running total: 1
- 2008 → 2009: 2008 is leap, 2 odd days. Running total: 3
- 2009 → 2010: ordinary, 1 odd day. Running total: 4
- 2010 → 2011: ordinary, 1 odd day. Running total: 5
- 2011 → 2012: ordinary, 1 odd day. Running total: 6
- 2012 → 2013: 2012 is leap, 2 odd days. Running total: 8 ≡ 1
- Continue... total odd days reach a multiple of 7 at **2018** (11 years later)

This is a classic recurring question type: *"Calendar for 2007 will be the same as calendar for
which year?"* → Answer: **2018**.

> 💡 **Speed Rule of Thumb:** For an ordinary year to repeat, you typically need **6, 11, or 17
> years** later (rarely other gaps), and the target year must also be ordinary. For a leap year, it
> usually repeats after **28 years** (or sometimes 12/40 depending on century boundaries). Don't
> blindly memorize this — verify with the running-odd-day-total method above, since century
> boundaries (1800, 1900, 2100) break the usual pattern.

---

## 4. Common Question Types in TCS NQT, CAT & Similar Exams

Based on recurring patterns across placement and competitive exams, Calendar questions almost always
fall into one of these categories:

### Category 1: Find the Day for a Given Date
*"What day of the week was 15 August 1947?"* — direct application of the odd-days method. Very
common as a standalone question in TCS NQT and SSC/Bank exams.

### Category 2: Day N Days After/Before a Given Day
*"Today is Monday. What day will it be after 61 days?"* — take N mod 7 and count forward (or
backward) from the given day. **No leap year logic needed** unless the range spans a different-length
month setup (irrelevant here since we're just counting days, not months).

### Category 3: Same Calendar / Repeating Year
*"The calendar for 2005 is the same as the calendar for which year?"* — use the running-odd-day-total
method above.

### Category 4: Given One Date's Day, Find Another Date's Day (Different Year)
*"If 8 Dec 2007 was Saturday, what day was 8 Dec 2006?"* — find odd days *between* the two dates
(same month/date, different year) and shift accordingly. Because month and date match, you only need
to account for the number of odd days contributed by the intervening year(s) — no month calculation
required. This is the fastest sub-type once you recognize it.

### Category 5: Century / Leap-Year Reasoning (CAT-style, trickier)
*"Can the last day of a century ever be a Tuesday?"* — requires knowing that centuries (100, 200,
300, 400 years) only ever contribute 5, 3, 1, or 0 odd days, so the last day of *any* century can
only be **Sunday, Monday, Wednesday, or Friday** — never Tuesday, Thursday, or Saturday. CAT and
other reasoning-heavy exams like to test this kind of derived property rather than a direct date
lookup.

### Category 6: Reverse Problems — Find the Year or Date
*"In which year after 2000 will 1 January fall on a Sunday, given some constraint?"* — work backward
from the odd-day requirement. Less common but appears in trickier CAT-adjacent sets.

---

## Exam Strategy Summary

- Identify the category first — it tells you which shortcut applies (don't default to full odd-day
  counting from year 1 if a same-date/different-year shortcut applies).
- For "N days after/before" questions, just do N mod 7 — don't overthink with leap years.
- For "same calendar" questions, track the running odd-day total year by year; stop at the first
  multiple of 7.
- Always double-check century years (1800, 1900, 2100, …) for the leap year exception — these are
  the most common trap in tricky questions.
- Practice the odd-days method until it's automatic — speed comes from not having to think about
  *why* each step works, only executing it.
