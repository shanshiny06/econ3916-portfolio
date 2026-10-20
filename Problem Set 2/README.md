# Problem Set 2: The Survey That Wasn't Random

ECON 3916 · Module 2: Statistical Reasoning

## The question
After an onboarding redesign, an in-app survey showed satisfaction rising from 3.6 to 4.3 out of 5. This notebook asks how much of that rise is real.

## What I did
- **Phase 1:** Simulated 50,000 users per period with a known truth (true mean satisfaction 3.30 before, 3.40 after), then imposed a response mechanism where the chance of answering depends on satisfaction itself. The simulated survey reproduces the PM's slide: 3.59 before, 4.32 after, while response rates fall from 27% to 15%.
- **Phase 2:** Bootstrapped the mean and median by hand and with `scipy.stats.bootstrap` (percentile and BCa), and ran a coverage simulation with Monte Carlo standard errors.
- **Phase 3:** Ran a Welch t-test with Cohen's d, a power analysis, and a simulation showing that a larger sample does not reduce the bias.
- **Phase 4:** Used AI to implement inverse-probability weighting, revised the prompt once, and checked the result against the known truth.

## Key findings
- The survey's 0.72-point gain is mostly selection: the true improvement is about 0.10 points.
- Bootstrap intervals are narrow but centred on the wrong number; their coverage of the true population mean is 0%.
- The t-test is highly significant (p ≈ 0), but significance cannot detect selection bias.
- A bigger survey makes the estimate more precise, not more accurate: the bias stays at about 0.61 points at every sample size.
- Weighting on engagement and support tickets removes only about 19% of the post-redesign bias (4.14 vs. a true 3.39), because response depends on satisfaction itself, which the covariates cannot capture.

## Recommendation
Survey a random sample of users and follow up with non-respondents, so the people who answer represent everyone.

## Tools
Python, NumPy, pandas, SciPy, statsmodels, scikit-learn, Google Colab. AI assistance: Claude (Anthropic), as documented in the AI Transcript.
