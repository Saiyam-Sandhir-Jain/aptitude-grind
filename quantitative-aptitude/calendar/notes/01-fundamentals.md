# Calendar — Fundamentals
### Odd Days, Leap Years & the Day-of-the-Week Formula

## Why Calendar Problems Matter

Calendar questions test whether you can find the **day of the week** for a given date, or work
backward/forward from a known day. They show up constantly in placement tests (TCS NQT, Infosys,
Wipro, Capgemini) and in CAT/other reasoning sections, usually as 1–2 quick-scoring questions **if**
you know the odd-days method cold. The entire topic rests on one idea: *the calendar repeats every
7 days, so only the remainder after dividing by 7 matters.*

---

## 1. Odd Days

> **Definition:** In a given period, the number of days **more than complete weeks** is called the
> number of **odd days**.

For example, 17 days = 2 complete weeks (14 days) + 3 extra days ⇒ 3 odd days. Only the odd-day count
matters for finding the day of the week — full weeks never shift the day.

### 1.1 Odd Days in a Year
- 1 ordinary year = 365 days = 52 weeks + 1 day ⇒ **1 odd day**
- 1 leap year = 366 days = 52 weeks + 2 days ⇒ **2 odd days**

### 1.2 Odd Days in Centuries

**Century Odd-Day Table — memorize this**

| Period    | Odd Days |
|-----------|----------|
| 100 years | 5        |
| 200 years | 3        |
| 300 years | 1        |
| 400 years | 0        |

**Why 400 years gives 0:** 100 years = 76 ordinary + 24 leap years = (76×1 + 24×2) = 124 odd days =
17 weeks + 5 days ⇒ 5 odd days. So 400 years = (5×4) + 1 extra leap day (400 itself is a leap
century) = 21 ≡ 0 (mod 7).

> 💡 **Pattern:** Every 4th century (400, 800, 1200, 1600, 2000, 2400, …) has **0 odd days** —
> meaning the calendar of year Y is identical to the calendar of year Y + 400. This is why 2000 and
> 2400 have the exact same calendar.

---

## 2. Leap Years

> **Leap Year Rule**
> 1. Every year divisible by 4 is a leap year — **unless** it is a century year (ends in 00).
> 2. A century year is a leap year only if it is divisible by **400**.

**Quick Classification**
- **Leap:** 1948, 2004, 1676, 2000, 1600, 2400 (divisible by 4; century years also divisible by 400)
- **Not leap:** 2001, 2002, 2003, 2005 (not divisible by 4); 1800, 1900, 2100, 2300 (century years
  *not* divisible by 400)

> ⚠️ **Common Mistake:** Students often forget the century exception and assume any year divisible
> by 4 is automatically a leap year. **1900 is divisible by 4 but is NOT a leap year** (not divisible
> by 400). Always check century years separately.

---

## 3. Mapping Odd Days to a Day of the Week

Once you compute the total number of odd days for a period (taking the result mod 7), map it using:

| Odd Days | 0   | 1   | 2   | 3   | 4   | 5   | 6   |
|----------|-----|-----|-----|-----|-----|-----|-----|
| Day      | Sun | Mon | Tue | Wed | Thu | Fri | Sat |

This table is anchored on the fact that **1 January, 1 AD was a Monday** in the proleptic Gregorian
calendar used for these problems, giving Sunday = 0 odd days as the baseline.

---

## 4. General Method: Finding the Day for Any Date

To find the day of the week on date `D` of month `M`, year `Y`:

1. Split `Y - 1` (up to the end of the previous year) into:
   - Number of 400s → always 0 odd days
   - Remaining 100s (0 to 3) → 5, 3, or 1 odd days respectively
   - Remaining years → (ordinary years × 1) + (leap years × 2)
2. Add the odd days contributed by the **months elapsed so far in year Y** (Jan 1 to the last day of
   the previous month), remembering to use 29 for February in a leap year.
3. Add the day number `D` of the current month.
4. Sum everything, take mod 7, and read off the day from the Odd Days → Day table.

### Worked Example — 15 August 2010

**Step 1: Years up to 2009.**
- 1600 years → 0 odd days; 400 years (nearest 400-year block) → 0 odd days
- Remaining 9 years (2001–2009): 2004 and 2008 are leap ⇒ 2 leap + 7 ordinary
  = (2×2) + (7×1) = 11 ≡ 4 odd days

**Step 2: Months elapsed (Jan–Jul 2010) + 15 days of Aug.**
```
31+28+31+30+31+30+31+15 = 227 days = 32 weeks + 3 days ⇒ 3 odd days
```

**Step 3: Total.**
```
0 + 0 + 4 + 3 = 7 ≡ 0 (mod 7) ⇒ Sunday
```
15 August 2010 was indeed a **Sunday**.

> 💡 **Faster Alternative:** For placement-test speed, most people skip the "years since year 1"
> method entirely and instead work **relative to a known anchor date** (e.g., "1 Jan 2000 was a
> Saturday" or "1 Jan 1 was Monday") using only the years *between* the anchor and the target date.
> This is faster and less error-prone — see `02-tricks-shortcuts-and-question-patterns.md` for the
> anchor-date and month-code methods.

---

## Key Takeaways

- Everything reduces to counting **odd days** and taking the result mod 7.
- Memorize: 100y → 5, 200y → 3, 300y → 1, 400y → 0 odd days.
- Leap year = divisible by 4, except century years, which need divisibility by 400.
- Always double check whether February in the target year has 28 or 29 days.
