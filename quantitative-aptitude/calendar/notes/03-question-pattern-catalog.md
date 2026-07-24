# Calendar — Question Pattern Catalog
### Every Way Placement Exams Phrase a Calendar Question, Grouped by the Trick That Solves It

Calendar questions look varied, but almost every one of them reduces to a handful of tricks from
`02-fast-tricks-and-shortcuts.md`. This file catalogues the actual **phrasings** you'll meet in TCS
NQT, Infosys, Wipro, Capgemini, and CAT-style tests, grouped by category, each with the fastest
method and a verified mini-example. Skim this before a test to pattern-match a question to its
solution method in seconds.

---

## Category A — Direct Day Lookup

### A1. Find the Day of a Given Date
> *"What day of the week was 15 August 1947?"*

The most common calendar question by far — direct application of the odd-days / anchor method.
**Method:** §1 or the mod-400 method in `01-fundamentals.md`.
**Answer:** 15 August 1947 was a **Friday**.

---

## Category B — Relative Day Arithmetic (No Calendar Needed)

### B1. Day After N Days
> *"Today is Tuesday. What day will it be after 100 days?"*

**Method:** `N mod 7`, step forward. `100 mod 7 = 2` → Tuesday + 2 = **Thursday**.

### B2. Day Before N Days
> *"100 days before Friday is which day?"*

**Method:** `N mod 7`, step backward. `100 mod 7 = 2` → Friday − 2 = **Wednesday**.

### B3. Yesterday / Tomorrow Questions
> *"Tomorrow is Monday. What was yesterday?"*

**Method:** Anchor on the one day you're told, then count off by ±1. Tomorrow = Monday ⇒ Today =
Sunday ⇒ Yesterday = **Saturday**.

### B4. Chained Relative-Day Questions
> *"Three days after tomorrow is Friday. What day is today?"*

**Method:** Work backward from the known day. "Three days after tomorrow" = today + 4 = Friday ⇒
today = Friday − 4 = **Monday**.

### B5. Mirror-Day Questions
> *"If yesterday was Thursday, what day will it be 100 days after tomorrow?"*

**Method:** First pin down today (yesterday = Thursday ⇒ today = Friday), then tomorrow = Saturday,
then apply B1: `100 mod 7 = 2` → Saturday + 2 = **Monday**.

### B6. Calendar + Clock Combined
> *"It is Monday, 11 PM. What day and time will it be after 30 hours?"*

**Method:** Split into full days + leftover hours: `30 = 24 + 6`. One full day moves Monday →
Tuesday; the remaining 6 hours push 11 PM past midnight into the *next* day, so it lands on
**Wednesday, 5 AM**. (Always check whether the leftover hours cross midnight — that's the part
people forget.)

---

## Category C — Nth / Last Weekday of a Month

### C1. Nth Weekday of a Month
> *"The third Monday of July 2026 falls on which date?"*

**Method:** Find the weekday of the 1st, then add 7 for each subsequent occurrence.
`1 July 2026 = Wednesday` → first Monday = 6th → third Monday = 6 + 14 = **20th**.

### C2. Last Weekday of a Month
> *"Find the last Friday of February 2026 (28-day, non-leap)."*

**Method:** Find the weekday of the last day of the month, then count back in steps of 7 until you
land on the target weekday. **Answer: 27 February 2026** (verified directly against the month).

### C3. Which Weekdays Occur 5 Times
> *"In a 31-day month starting on a Tuesday, which weekdays occur 5 times?"*

**Method:** §5 rule — `L = days − 28`. For 31 days, `L = 3`: the starting weekday and the next two.
Starting Tuesday ⇒ **Tuesday, Wednesday, Thursday**.

### C4. February-Specific Frequency
> *"In a leap year, which weekday occurs 5 times in February?"*

**Method:** 29 days ⇒ `L = 1` ⇒ only the weekday February 1st falls on. In a non-leap February
(28 days, `L = 0`), **no** weekday occurs 5 times — all seven occur exactly 4 times.

---

## Category D — Same Calendar / Repeating Year

### D1. Same Calendar as a Given Year
> *"The calendar for 2026 will be the same as the calendar for which future year?"*

**Method:** Running-odd-day-total from `02-fast-tricks-and-shortcuts.md` §7 — don't assume a fixed
gap. **Answer for 2026 specifically: 2037** (verified; 2026 is ordinary, gap = 11 years).

### D2. Odd-One-Out Calendar
> *"Which of these years has a calendar different from the others: 1997, 2003, 2014, 2025?"*

**Method:** Two years share a calendar only if both are the same type (ordinary/leap) **and** 1
January falls on the same weekday. Check leap/non-leap status first to eliminate options fast, then
compare 1 January weekdays only among years of matching type.

### D3. Calendar Repeats After N Years (Cycle Length)
> *"After how many years does a leap year's calendar typically repeat?"*

**Method:** Table in §7 — typically **28 years** for a leap year (rarely 40, only near a century that
breaks the 4-year leap rule, e.g. spanning 1800/1900/2100). For an ordinary year, typically **6 or
11 years** (rarely 12). Never assume 17 — that number doesn't actually occur.

---

## Category E — Leap Year Reasoning

### E1. Is This Year a Leap Year?
> *"Is 2100 a leap year?"*

**Method:** §4 quick check. 2100 is divisible by 4 and by 100, but **not** by 400 ⇒ **not a leap
year**. (Classic trap — most people stop at "divisible by 4" and get this wrong.)

### E2. Counting Leap Years in a Range
> *"How many leap years are there from 1601 to 2000?"*

**Method:** §4 formula, `count(2000) − count(1600) = 485 − 388 = 97`.

### E3. Century / Leap-Year Reasoning (CAT-style)
> *"Can the last day of a century (a year ending in 00) ever fall on a Tuesday?"*

**Method:** Centuries only ever contribute 5, 3, 1, or 0 odd days (for 100, 200, 300, 400-year
blocks respectively) — never 2, 4, or 6. So a century's last day can only be **Sunday, Monday,
Wednesday, or Friday**, never Tuesday, Thursday, or Saturday.

---

## Category F — Date-to-Date and Span Problems

### F1. Days Between Two Dates
> *"How many days are there between 15 August 2010 and 25 December 2010?"*

**Method:** Convert both to a running day-of-year count (or just subtract), being careful whether the
question wants an inclusive or exclusive count. **Answer: 132 days** (from 15 Aug to 25 Dec,
exclusive of the start date).

### F2. Consecutive Dates Within a Month
> *"If 18 January is a Tuesday, what day is 27 January?"*

**Method:** §6 rule — difference in days mod 7. `27 − 18 = 9`, `9 mod 7 = 2` → Tuesday + 2 =
**Thursday**.

### F3. Same Date, Different Year (Leap-Day Trap)
> *"If 15 March 2015 was a Sunday, what day was 15 March 2016?"*

**Method:** Don't just add 1 odd day for "one year passing" — check whether 29 February falls
**inside the specific span** you're bridging. Here, 29 Feb 2016 falls between the two dates (2016 is
leap and the leap day comes before 15 March), so the gap is **2** odd days, not 1.
Sunday + 2 → **Tuesday**.

---

## Category G — Reverse Problems (Given a Clue, Find the Date/Day)

### G1. Given the Nth Occurrence, Find the 1st Occurrence
> *"The third Saturday of a month falls on the 16th. Find the date of the first Saturday."*

**Method:** Subtract `7 × (N − 1)` days. Third occurrence minus 2 weeks: `16 − 14 = 2`.
**Answer: 2nd.**

### G2. Given the Month's Starting Day, Find a Later Date's Day
> *"A month starts on Wednesday and has 30 days. What day is the 30th?"*

**Method:** §6 rule — `(30 − 1) mod 7 = 29 mod 7 = 1` → Wednesday + 1 = **Thursday**.

### G3. Calendar Matching — Find All Occurrences of a Weekday
> *"If the 15th of a month is a Friday, what other dates in that month are Fridays?"*

**Method:** Every matching weekday is exactly 7 days apart. From the 15th: 1, 8, **15, 22, 29**
(exact list depends on the month length — always list both directions from the known date, not just
forward).

---

## Category H — Logic Puzzles and Word Problems

### H1. Birthday / Recurrence Puzzles
> *"A person was born on a Monday. Is it possible for their birthday to fall on a Monday again every
> single year?"*

**Method:** A birthday repeats on the same weekday only if the gap between birthdays contributes 0
odd days — impossible every year, since every ordinary year contributes 1 odd day and every leap
year contributes 2. It can *only* repeat on the same weekday in the rare years where the running
odd-day total (§7) resets to a multiple of 7, not annually.

### H2. Working-Day Counting
> *"An office is closed every Sunday. If a 31-day month starts on a Saturday, how many working days
> does it have?"*

**Method:** Count how many Sundays fall in the month using the weekday-frequency rule (§5), then
subtract from the total days. A 31-day month starting on Saturday has `L = 3` extra weekdays
(Sat, Sun, Mon occurring 5 times) — so Sunday occurs **5** times ⇒ working days = `31 − 5 = 26`.

### H3. Multi-Clue Logic Puzzles
> *"1 January of a certain year is a Friday, and 1 January of the following year is a Sunday. What
> can you conclude about the certain year?"*

**Method:** The shift from one 1 January to the next equals that year's odd-day contribution.
Friday → Sunday is a shift of **2** odd days, which only a **leap year** contributes ⇒ the certain
year must be a leap year.

---

## Priority Order for Limited Prep Time

If you're short on time, drill these first — they cover the large majority of what actually appears
in placement tests, roughly in order of frequency:

1. **A1** — Find the day for a given date (mod-400 or anchor method)
2. **B1/B2** — Day after/before N days (pure `mod 7`)
3. **E1** — Leap year identification (the century exception is the #1 trap)
4. **C1** — Nth weekday of a month
5. **D1** — Same/repeating calendar year
6. **C3/C4** — Weekday frequency in 28/29/30/31-day months
7. **F1** — Days between two dates
8. **F3** — Same date, different year (leap-day-crossing trap)
9. **E3** — Century reasoning (CAT-style, less common but high-value when it appears)
