# econ3916-portfolio
# Problem Set 3: The Number Nobody Can Reproduce

ECON 3916 · Module 2: Causal Thinking & SQL

## The question
A dashboard reported average revenue per West-region customer as 1,240 dollars; Finance got 812. This notebook finds out which number is right, writes a rule that would have caught the error, and asks whether the West's account-management programme actually raised revenue.

## What I did
- **Phase 1:** Built a customers and an orders table in DuckDB (3,500 customers, 2,200 in the West, about 23,000 orders), with revenue driven by order count. Reproduced both numbers and wrote a check that warns when a join changes the row count.
- **Phase 2:** Set 15% of regions to NULL, showed how a `!=` filter silently drops them, fixed it with `IS DISTINCT FROM`, and used a window function to put each customer's revenue beside their region's average.
- **Phase 3:** Simulated the programme with a known true effect, compared naive and adjusted estimates, and showed how controlling for support tickets breaks the estimate.
- **Phase 4:** Used AI to write a SQL reviewer, ran it on my own queries, and reported what it caught and what it missed.

## Key findings
- The correct figure is about 801 dollars per customer. Joining orders before averaging counted each customer once per order, pushing the average to about 1,214 dollars.
- A fan-out check that compares row counts before and after a join fires on the bad query (2,200 rows to 14,655) and stays silent on the correct one.
- `WHERE region != 'West'` returned 1,086 customers instead of 1,611: the 525 customers with no recorded region vanish from every regional comparison.
- With a true programme effect of 50 dollars, the naive comparison says 335; adjusting for account size gives 57; adding support tickets as a control flips it to minus 55.
- The AI-written reviewer flagged the fan-out that produced the 1,240 and the NULL filter, raised no false alarms on the corrected queries, but understated the risk of `WHERE region = 'West'` and measured fan-out on whole tables rather than on the rows each query used.

## Recommendation
Before any number goes on a slide: check that every join keeps one row per unit being averaged, report missing values in filtered columns, and control only for characteristics fixed before the programme began.

## Tools
Python, DuckDB, pandas, NumPy, statsmodels, Google Colab. AI assistance: Claude (Anthropic), as documented in the AI Transcript.
