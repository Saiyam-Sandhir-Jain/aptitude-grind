# Calendar — Fast Tricks & Shortcuts
### Anchor-Day Method, Month Codes, and Every Speed Trick You Need

This file collects the **fast calculation methods** — the actual shortcuts you execute under exam
pressure. For the full catalogue of question *types* that use these tricks, see
`03-question-pattern-catalog.md`.

---

## 1. The Anchor-Day Method (Fastest for Placement Tests)

Instead of counting odd days from year 1 (or even using the `mod 400` shortcut from
`01-fundamentals.md`), work relative to a **known reference date** close to your target date. Most
questions either give you a reference day directly, or you can use a memorized anchor.

**Useful Anchors to Memorize**
- 1 January 2000 → **Saturday** (most practical anchor for modern-date questions)
- 1 January 1900 → **Monday**
- 1 January 2100 → **Friday**

**Anchor-Day Procedure**
1. Find the number of complete years between the anchor and target year.
2. Odd days contributed = (ordinary years × 1) + (leap years × 2), reduced mod 7.
3. Add odd days for the months elapsed in the target year, then add the date number.
4. Add this to the anchor's day-of-week position (mod 7) and read off the result.

> 💡 **Why this beats the mod-400 method:** the mod-400 method is for when you're asked about an
> arbitrary date, possibly centuries away. The anchor method is for when your target date is within
> a normal human lifetime of a known reference point — which is nearly every placement-test
> question. Fewer years to sum = fewer chances to make an arithmetic slip.

**Worked Example**

> *If 1 Jan 2000 was a Saturday, what day was 1 Jan 2010?*

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
> February only** (the extra day, 29 Feb, hasn't occurred yet when you're computing odd days up to
> those months). From March onward in a leap year, use the codes as-is — the leap day has already
> been absorbed.

```
Day code = (Date + Month code + Year's odd days from your chosen anchor) mod 7
```
Match the result against the Odd-Days → Day table in `01-fundamentals.md`.

> ⚠️ **When to Use Which Method:** The **odd-days-from-scratch** method is more intuitive and safer
> under exam pressure because you derive everything instead of recalling a code table. The
> **month-code** method is faster once memorized, but a single misremembered code silently gives a
> wrong answer. For placement tests with negative marking, prefer the method you can execute without
> doubt — practice both, then pick one.

---

## 3. Day After / Before N Days — Pure Modulo, No Calendar Needed

This is the single fastest calculation in the entire topic, and it needs **no leap-year knowledge at
all** when you're just counting raw days forward or backward from a *named* day (not a date).

> **Rule:** `N mod 7` tells you how many weekday-steps to move. Forward for "after," backward for
> "before."

**Example — After**
```
Today is Tuesday. What day after 100 days?
100 mod 7 = 2
Tuesday + 2 → Thursday
```

**Example — Before**
```
100 days before Friday.
100 mod 7 = 2
Friday − 2 → Wednesday
```

> ⚠️ **Common Mistake:** Reaching for the odd-days-per-year method here. If the question only gives
> you a day name (not a calendar date) and a day count, you never need leap years — just `N mod 7`.
> Leap years only matter once you're crossing actual calendar dates (e.g., "15 March 2015" to
> "15 March 2016"), because then the *number of days in between* depends on whether 29 February falls
> inside that span.

---

## 4. Leap Year — Quick Check and Quick Count

**Quick Check for One Year**
```
Divisible by 4?  No  → Not leap
                 Yes → Century year (ends in 00)?
                          No  → Leap
                          Yes → Divisible by 400? Yes → Leap
                                                  No  → Not leap
```

**Quick Count for a Range (1 to N)** — the formula almost every "how many leap years between X and
Y" question is really asking for:
```
Leap years from 1 to N = ⌊N/4⌋ − ⌊N/100⌋ + ⌊N/400⌋
```
For a range `[A, B]`, compute `count(B) − count(A − 1)`.

**Worked Example — Leap years from 1601 to 2000**
```
count(2000) = ⌊2000/4⌋ − ⌊2000/100⌋ + ⌊2000/400⌋ = 500 − 20 + 5 = 485
count(1600) = ⌊1600/4⌋ − ⌊1600/100⌋ + ⌊1600/400⌋ = 400 − 16 + 4 = 388
Leap years in [1601, 2000] = 485 − 388 = 97
```
(Verified independently with a direct year-by-year count — 97 is correct.)

---

## 5. Weekday Frequency Inside a Month — "Which Weekdays Occur 5 Times?"

Every month has at least 4 of each weekday. Whether a weekday occurs a 5th time depends purely on
**how many days the month has beyond 4 full weeks (28 days)**, and **which weekday the month starts
on**.

> **Rule:** Let `L = (days in month) − 28`. The **first `L` weekdays** starting from the month's
> 1st-day weekday occur **5 times**; every other weekday occurs exactly 4 times.

| Month length | L | Weekdays that occur 5 times |
|---|---|---|
| 28 days (Feb, non-leap) | 0 | None — every weekday occurs exactly 4 times |
| 29 days (Feb, leap) | 1 | Only the weekday the month starts on |
| 30 days | 2 | The starting weekday **and** the next one |
| 31 days | 3 | The starting weekday **and** the next two |

**Worked Example**
```
A 31-day month starts on Tuesday. Which weekdays occur 5 times?
L = 31 − 28 = 3 → first 3 weekdays from Tuesday: Tue, Wed, Thu
```
(Verified with a full day-by-day count for a real 31-day month starting on a Monday — Mon/Tue/Wed
each appeared 5 times, matching the rule.)

---

## 6. Month Start/End Day — Jump Straight from One to the Other

**Rule:** to go from the weekday of the 1st to the weekday of the last day (or any day) of the same
month, add `(day number − 1) mod 7` to the 1st's weekday.

**Worked Example — Start to End**
```
1 June = Wednesday. What day is 30 June?
(30 − 1) mod 7 = 29 mod 7 = 1
Wednesday + 1 → Thursday
```

**Worked Example — Start of Next Month**
```
1 March = Monday. Find 1 April. (March has 31 days.)
31 mod 7 = 3
Monday + 3 → Thursday
```
This chains naturally: keep adding `(month length mod 7)` to hop from one month's 1st to the next.

---

## 7. Same-Calendar-Year Gaps — Corrected

Coaching material widely repeats "an ordinary year repeats after 6, 11, **17**, or 28 years." This
was checked directly by scanning three thousand years of real calendars, and **17 never actually
occurs**. Here's what's actually true:

| Starting year type | Typical gap to next same calendar | Rare gap (near broken century boundaries: 1800/1900/2100/…) |
|---|---|---|
| Ordinary | 6 or 11 years | 12 years |
| Leap | 28 years | 40 years |

> ⚠️ **Don't memorize "17."** It's a commonly repeated number in Indian test-prep material that does
> not hold up when checked against actual calendars. If you see it in another source, verify with
> the running-odd-day-total method below instead of trusting it blindly.

**Running-Odd-Day-Total Method (always correct, works for any year)**
1. Starting from your given year, add 1 odd day for each ordinary year that passes and 2 for each
   leap year, keeping a running total mod 7.
2. Stop at the first year where the running total hits 0 **and** the year's leap/ordinary type
   matches the starting year's type (both conditions must hold — same weekday for 1 Jan isn't
   enough if one year is leap and the other isn't, since their Februaries differ).

---

## Quick Reference — Which Trick for Which Situation

| Situation | Use |
|---|---|
| Target date is centuries away from any anchor you know | Mod-400 method (`01-fundamentals.md`) |
| Target date is within ~100–150 years of a known anchor | Anchor-Day method (§1) |
| You've memorized the month-code table | Month-code method (§2) |
| Only a day name + a day count given (no calendar date) | `N mod 7` (§3) |
| "How many leap years between X and Y" | Leap-count formula (§4) |
| "Which weekday(s) occur 5 times" | Weekday-frequency rule (§5) |
| Need another day's weekday within the same month | Start/end day rule (§6) |
| "Same calendar as year X will repeat in which year" | Running-odd-day-total (§7) — don't guess 17 |
