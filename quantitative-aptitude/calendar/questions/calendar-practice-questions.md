# Calendar — Practice Questions
### Medium to Difficult, With Full Solutions

*Difficulty is marked as **[M]** Medium or **[H]** Hard. Solve on your own first, then check the
solution. Solutions use the odd-days method from `01-fundamentals.md`.*

---

### Q1 [M] — Direct Date Lookup
What was the day of the week on 26 January 1950?

<details>
<summary><b>Solution</b></summary>

Reference: 1 January 1900 was a **Monday**.
- Years 1900–1949 (up to start of 1950): count odd days for years 1900 to 1949 inclusive of leap years.
- Leap years 1900–1949: 1904, 1908, …, 1948 — but 1900 is *not* leap (century rule) ⇒ 12 leap years,
  38 ordinary years.
- Odd days = (12×2) + (38×1) = 24 + 38 = 62 ≡ 62 − 56 = 6 (mod 7)
- Monday + 6 odd days → **Sunday** (this gives the day for 1 Jan 1950)
- Add 25 more days to reach 26 Jan: 25 mod 7 = 4 odd days
- Sunday + 4 → **Thursday**

**Answer: Thursday**
</details>

---

### Q2 [M] — N Days After
Today is Wednesday. What day will it be after 90 days?

<details>
<summary><b>Solution</b></summary>

90 mod 7 = 90 − 84 = 6 odd days.
Wednesday + 6 days → **Tuesday**.

**Answer: Tuesday**
</details>

---

### Q3 [M] — Same Date, Different Year
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

### Q4 [M] — Same Calendar Year
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
</details>

---

### Q5 [H] — Century Reasoning
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

### Q6 [H] — Reverse Problem
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

### Q7 [H] — Multi-Step Combined Problem
If 1 January 2001 was a Monday, find the day of the week on 29 February 2004, and verify 2004 is
indeed a leap year using the divisibility rule.

<details>
<summary><b>Solution</b></summary>

**Leap year check:** 2004 / 4 = 501 exactly, and 2004 is not a century year, so **2004 is a leap
year**. ✓

**Odd days from 1 Jan 2001 to 1 Jan 2004** (years 2001, 2002, 2003 — all ordinary):
3 × 1 = 3 odd days. Monday + 3 → **Thursday** (this is 1 Jan 2004).

**Odd days from 1 Jan 2004 to 29 Feb 2004:**
January has 31 days → 31 mod 7 = 3 odd days (this brings us to 1 Feb).
Add 28 more days to reach 29 Feb: 28 mod 7 = 0 odd days.
Total: 3 + 0 = 3 odd days.

Thursday + 3 → **Sunday**.

**Answer: 29 February 2004 was a Sunday.**
</details>

---

### Q8 [H] — Century-Spanning Problem
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
| Q3 | Tuesday |
| Q4 | 2034 |
| Q5 | Only Sun/Mon/Wed/Fri possible for century-end (proof-based) |
| Q6 | Certain year is leap; 2 years later = Monday |
| Q7 | Sunday |
| Q8 | Saturday |
