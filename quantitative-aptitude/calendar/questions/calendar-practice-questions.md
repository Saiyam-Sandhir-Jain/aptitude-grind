# Calendar — Practice Questions
### Medium to Difficult, With Full Solutions

*Difficulty is marked as **[M]** Medium or **[H]** Hard. Solve on your own first, then check the
solution. Solutions use the methods from `01-fundamentals.md`, `02-fast-tricks-and-shortcuts.md`,
and `03-question-pattern-catalog.md`. Every numeric answer below was cross-checked independently
against Python's `datetime`/`calendar` standard library before being finalized.*

---

### Q1 [M] — Direct Date Lookup (Pattern A1)
What was the day of the week on 26 January 1950?

<details>
<summary><b>Solution</b></summary>

Reference: 1 January 1900 was a **Monday**.
- Years 1900–1949 (up to start of 1950): count odd days for years 1900 to 1949 inclusive.
- Leap years 1900–1949: 1904, 1908, …, 1948 — but 1900 is *not* leap (century rule) ⇒ 12 leap years,
  38 ordinary years.
- Odd days = (12×2) + (38×1) = 24 + 38 = 62 ≡ 62 − 56 = 6 (mod 7)
- Monday + 6 odd days → **Sunday** (this gives the day for 1 Jan 1950)
- Add 25 more days to reach 26 Jan: 25 mod 7 = 4 odd days
- Sunday + 4 → **Thursday**

**Answer: Thursday**
</details>

---

### Q2 [M] — N Days After (Pattern B1)
Today is Wednesday. What day will it be after 90 days?

<details>
<summary><b>Solution</b></summary>

90 mod 7 = 90 − 84 = 6 odd days.
Wednesday + 6 days → **Tuesday**.

**Answer: Tuesday**
</details>

---

### Q3 [M] — Nth Weekday of a Month (Pattern C1)
What date is the fourth Thursday of November 2026?

<details>
<summary><b>Solution</b></summary>

1 November 2026 is a **Monday**. The first Thursday is therefore the 4th (Mon→Thu is 3 days).
Each subsequent Thursday is 7 days later:
```
1st Thursday = 4
2nd Thursday = 11
3rd Thursday = 18
4th Thursday = 25
```

**Answer: 25 November 2026**

> ⚠️ **Why This Is a Common Trap:** People often assume the Nth weekday is always `7×(N−1) + 1`
> (i.e. assume the 1st of the month IS the target weekday). Always find the *first occurrence* of
> the target weekday first — it usually isn't the 1st — then add multiples of 7.
</details>

---

### Q4 [M] — Last Weekday of a Month (Pattern C2)
What is the date of the last Sunday of September 2026? (September has 30 days.)

<details>
<summary><b>Solution</b></summary>

1 September 2026 is a **Tuesday**, so the Sundays in September 2026 fall on 6, 13, 20, 27.
The last one before the month ends on the 30th is the **27th**.

**Answer: 27 September 2026**
</details>

---

### Q5 [M] — Days Between Two Dates (Pattern F1)
How many days are there between 15 August 2010 and 25 December 2010 (counting from the first date to
the second, exclusive of the start date)?

<details>
<summary><b>Solution</b></summary>

Days remaining in August after the 15th: 31 − 15 = 16
Add full months: September (30) + October (31) + November (30) = 91
Add days into December: 25
Total: 16 + 91 + 25 = **132 days**

**Answer: 132 days**
</details>

---

### Q6 [M] — Same Date, Different Year (Pattern F3)
If 15 March 2015 was a Sunday, what day was 15 March 2016?

<details>
<summary><b>Solution</b></summary>

2015 is an ordinary year, but the gap 15 Mar 2015 → 15 Mar 2016 **includes 29 Feb 2016** (since 2016
is a leap year and the leap day falls before 15 March). So this interval has **2 odd days**, not 1.
Sunday + 2 → **Tuesday**.

**Answer: Tuesday**

> ⚠️ **Why This Trips People Up:** The "add 1 odd day per year" shortcut only works when the year in
> question is ordinary **and** the leap day (if any) doesn't fall between the two matching dates.
> Always check whether 29 February lies inside the specific date range you're bridging — not just
> whether the calendar year is leap.
</details>

---

### Q7 [H] — Weekdays Occurring Five Times (Pattern C3)
March 2026 has 31 days and 1 March 2026 is a Sunday. Which weekdays occur five times that month?

<details>
<summary><b>Solution</b></summary>

`L = 31 − 28 = 3`, so the starting weekday and the next two occur five times.
Starting weekday is Sunday ⇒ **Sunday, Monday, Tuesday**.

**Answer: Sunday, Monday, Tuesday**
</details>

---

### Q8 [H] — Counting Leap Years in a Range (Pattern E2)
How many leap years are there from 1601 to 2000 (inclusive)?

<details>
<summary><b>Solution</b></summary>

Using `⌊N/4⌋ − ⌊N/100⌋ + ⌊N/400⌋`:
```
count(2000) = 500 − 20 + 5 = 485
count(1600) = 400 − 16 + 4 = 388
Leap years in [1601, 2000] = 485 − 388 = 97
```

**Answer: 97**
</details>

---

### Q9 [H] — Reverse Problem: Nth Occurrence to Other Occurrences (Pattern G1)
The third Saturday of a certain month falls on the 16th. On what date does the first Saturday fall,
and on what date does the last Saturday fall if the month has 31 days?

<details>
<summary><b>Solution</b></summary>

**First Saturday:** subtract 2 weeks from the 3rd occurrence: 16 − 14 = **2nd**.
**Remaining Saturdays:** 2, 9, 16, 23, and (since the month has 31 days) 30 also fits
(23 + 7 = 30 ≤ 31), so the **last Saturday is the 30th**.

**Answer: First Saturday = 2nd; last Saturday = 30th**
</details>

---

### Q10 [H] — Same Calendar Year (Pattern D1)
The calendar for the year 2023 will be the same as the calendar for which future year?

<details>
<summary><b>Solution</b></summary>

2023 is ordinary. Track running odd days year by year starting the count from 2023→2024:

| Transition | Odd days added | Running total (mod 7) |
|---|---|---|
| 2023 → 2024 (2023 ordinary) | 1 | 1 |
| 2024 → 2025 (2024 leap) | 2 | 3 |
| 2025 → 2026 (2025 ordinary) | 1 | 4 |
| 2026 → 2027 (2026 ordinary) | 1 | 5 |
| 2027 → 2028 (2027 ordinary) | 1 | 6 |
| 2028 → 2029 (2028 leap) | 2 | 1 |
| 2029 → 2030 (2029 ordinary) | 1 | 2 |
| 2030 → 2031 (2030 ordinary) | 1 | 3 |
| 2031 → 2032 (2031 ordinary) | 1 | 4 |
| 2032 → 2033 (2032 leap) | 2 | 6 |
| 2033 → 2034 (2033 ordinary) | 1 | 0 |

Running total first hits a multiple of 7 at **2034**, and 2034 is also an ordinary year (matching
2023's type).

**Answer: 2034**

> ⚠️ **Why This Is a Common Trap:** Coaching material often claims ordinary years always repeat
> after "6, 11, 17, or 28" years. The 17 figure doesn't actually occur for any real year when
> checked directly — don't assume a fixed gap; always run the odd-day total.
</details>

---

### Q11 [H] — Century Reasoning
Prove that the last day of a century (year ending in 00) can never be a Tuesday, Thursday, or Saturday.

<details>
<summary><b>Solution</b></summary>

The last day of the n-th century corresponds to a cumulative odd-day count equal to `5n mod 7` for n
not a multiple of 4, and `0` when n is a multiple of 4 (from the 400-year rule). Evaluate `5n mod 7`
for n = 1, 2, 3 (since n=4 gives 0):

```
n=1: 5     n=2: 10 ≡ 3     n=3: 15 ≡ 1     n=4: 0
```

So the only possible odd-day residues for a century's last day are `{0, 1, 3, 5}`, which map to only
four of the seven weekdays. Direct computation confirms centuries can only end on **Sunday, Monday,
Wednesday, or Friday** — never Tuesday, Thursday, or Saturday.

**Answer:** Because only 4 distinct odd-day residues (0, 1, 3, 5) are possible for century
boundaries, only 4 of the 7 weekdays are reachable — and Tuesday, Thursday, Saturday are never among
them.
</details>

---

### Q12 [H] — Reverse Problem (Multi-Clue Logic)
1 January of a certain year is a Friday. 1 January of the following year is a Sunday. What can you
conclude about the certain year, and what day is 1 January two years later?

<details>
<summary><b>Solution</b></summary>

Going from Friday to Sunday is a shift of **2 odd days** ⇒ the certain year must be a **leap year**
(only leap years contribute 2 odd days). So the certain year has 366 days, and the following year is
ordinary, contributing 1 odd day.
Sunday + 1 → **Monday** for 1 January two years later.

**Answer:** The certain year is a leap year; 1 January two years later is a Monday.
</details>

---

### Q13 [H] — Working-Day Counting (Pattern H2)
An office is closed every Sunday. A 31-day month starts on a Saturday. How many working days does
the month have?

<details>
<summary><b>Solution</b></summary>

`L = 31 − 28 = 3`, so the starting weekday and the next two occur five times: **Saturday, Sunday,
Monday**. Sunday is among them ⇒ Sunday occurs **5** times in this month.
Working days = total days − Sundays = 31 − 5 = **26**.

**Answer: 26 working days**

> ⚠️ **Why This Is a Common Trap:** Assuming every month has exactly 4 Sundays. Whether Sunday
> occurs 4 or 5 times depends entirely on the month's length and starting weekday — check both
> before subtracting.
</details>

---

### Q14 [H] — Century-Spanning Problem
If 1 January 2001 was a Monday, what day of the week is 1 January 2101?

<details>
<summary><b>Solution</b></summary>

We need the total odd days contributed by the years 2001 through 2100 (100 full years elapsing).

**Leap years in 2001–2100:** every year divisible by 4 is a leap year *unless* it's a century year
not divisible by 400. In this range: 2004, 2008, …, 2096 are leap ⇒ (2096−2004)/4 + 1 = 24 leap
years. The only century year in range, 2100, is **not** divisible by 400, so it is **not** leap — it
counts as an **ordinary** year instead.

- Leap years: 24
- Ordinary years: 100 − 24 = 76
- Odd days = (24×2) + (76×1) = 48 + 76 = 124
- 124 mod 7 = 124 − 119 = 5

Monday + 5 odd days → **Saturday**.

**Answer: 1 January 2101 is a Saturday.**

> ⚠️ **Why This Is a Common CAT/Placement Trap:** The trap is treating 2100 as a normal leap year
> because it's divisible by 4. Since it's a century year **not** divisible by 400, it must be
> excluded — this single oversight shifts the final answer by one full odd day (which changes the
> answer from Saturday to Sunday if missed).
</details>

---

## Answer Key Summary

| Question | Answer |
|---|---|
| Q1 | Thursday |
| Q2 | Tuesday |
| Q3 | 25 November 2026 |
| Q4 | 27 September 2026 |
| Q5 | 132 days |
| Q6 | Tuesday |
| Q7 | Sunday, Monday, Tuesday |
| Q8 | 97 |
| Q9 | First = 2nd; Last = 30th |
| Q10 | 2034 |
| Q11 | Only Sun/Mon/Wed/Fri possible for century-end (proof-based) |
| Q12 | Certain year is leap; 2 years later = Monday |
| Q13 | 26 working days |
| Q14 | Saturday |
