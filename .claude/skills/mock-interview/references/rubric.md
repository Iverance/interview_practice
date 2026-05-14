# Mock Interview Evaluation Rubric

Scoring guide for all four dimensions. Each is scored 1–5. The overall score is the average rounded to the nearest 0.5, minus 0.25 for each unsolicited hint given after the first.

---

## Problem Comprehension

Measures how well the candidate understood the problem before and during coding.

| Score | Criteria |
|-------|----------|
| 1 | Misunderstood the core problem; coded the wrong thing entirely |
| 2 | Understood the core task but missed critical constraints or input assumptions |
| 3 | Understood the problem correctly; asked some clarifying questions |
| 4 | Strong clarifying questions; caught most edge cases and constraints proactively |
| 5 | Exceptional — proactively identified hidden constraints, ambiguities, and unstated assumptions |

---

## Algorithm & Approach

Measures the quality of the candidate's problem-solving strategy and awareness of complexity.

| Score | Criteria |
|-------|----------|
| 1 | No coherent approach; random or trial-and-error code; no complexity awareness |
| 2 | Brute-force only; aware it's suboptimal but unable to improve |
| 3 | Found a correct working solution; understood its time/space complexity |
| 4 | Found an optimal or near-optimal solution with clear reasoning about tradeoffs |
| 5 | Optimal solution; discussed multiple approaches; considered tradeoffs and follow-up constraints |

---

## Code Quality

Measures the correctness, readability, and robustness of the written code.

| Score | Criteria |
|-------|----------|
| 1 | Buggy, unreadable, or incomplete; doesn't handle basic inputs |
| 2 | Partially working; poor variable names; missing edge cases |
| 3 | Correct for main cases; readable; minor edge case gaps or style issues |
| 4 | Clean, correct, idiomatic Python; handles edge cases; good naming |
| 5 | Production-quality — well-named, correct, handles all edge cases, uses language idioms effectively |

---

## Communication

Measures how clearly the candidate narrated their thought process throughout the session.

| Score | Criteria |
|-------|----------|
| 1 | Silent throughout; interviewer had to prompt for every piece of information |
| 2 | Explained only when directly asked; minimal think-aloud |
| 3 | Explained approach before coding; some narration while implementing |
| 4 | Strong think-aloud throughout; clearly narrated decisions and tradeoffs |
| 5 | Exceptional — framed the problem, narrated code in real time, explained tradeoffs unprompted |

---

## Overall Score Calculation

```
overall = average(comprehension, algorithm, code_quality, communication)
overall = round(overall, 0.5)
overall -= 0.25 × max(0, unsolicited_hints - 1)
```

### Labels

| Score | Label |
|-------|-------|
| 1.0 – 2.0 | No Hire |
| 2.5 – 3.0 | Lean No Hire |
| 3.5 | Borderline |
| 4.0 – 4.5 | Hire |
| 5.0 | Strong Hire |
