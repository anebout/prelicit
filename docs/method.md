# PRELICIT methodology

## Overview

PRELICIT is a toolkit for the survey-based elicitation of economic preferences
and related decision attitudes.

Its core objective is to make choice-based preference elicitation sufficiently
simple and parsimonious for use in large-scale surveys while preserving a
transparent link between respondents' choices and economically meaningful
objects.

PRELICIT uses short adaptive binary-choice sequences to locate individual
equivalents. The standard implementation covers four domains:

- risk,
- time,
- ambiguity,
- complexity.

The benchmark questionnaire contains:

- 4 risk prospects,
- 4 time prospects,
- 3 ambiguity prospects,
- 1 complexity prospect.

Each prospect is elicited using an adaptive bisection procedure. The primary
outputs of PRELICIT are model-free measures constructed directly from the
elicited intervals. Structural estimation is not required to use the toolkit.

For each domain, PRELICIT returns:

1. the elicited interval for every task;
2. the midpoint of every interval;
3. a raw individual-level domain score;
4. a standardized domain score;
5. optional rank or percentile transformations.

The standardized score is the default summary measure. It preserves
information on distances between respondents while expressing the measure in
standard-deviation units.

---

# 1. Adaptive elicitation

## 1.1 General principle

For each task, the respondent repeatedly chooses between a target prospect and
a comparison amount.

The comparison amount is updated after each response according to a bisection
algorithm.

After \(K\) binary choices, the procedure identifies an interval

\[
[c^-_{ij},c^+_{ij}]
\]

containing the elicited equivalent of respondent \(i\) for task \(j\).

The width of the final interval depends on:

- the initial elicitation range;
- the number of bisection steps;
- whether the respondent completed the full sequence.

The method therefore naturally accommodates incomplete sequences: a respondent
who stops before the final step simply has a wider elicitation interval.

---

## 1.2 Midpoint

For descriptive analyses and construction of model-free indicators, PRELICIT
uses the midpoint of the final interval:

\[
\tilde c_{ij}
=
\frac{c^-_{ij}+c^+_{ij}}{2}.
\]

The midpoint is not treated as the true latent equivalent. It is a convenient
summary of the interval identified by the adaptive procedure.

Users interested in interval-censored structural estimation should use the
original lower and upper bounds rather than replacing the interval by its
midpoint.

---

# 2. Risk

## 2.1 Task

A risk task presents a binary lottery

\[
R_j=(x_j,p_j,y_j)
\]

and elicits its certainty equivalent.

The respondent chooses repeatedly between the lottery and a sure monetary
amount.

The adaptive procedure returns an interval

\[
[c^-_{iR_j},c^+_{iR_j}]
\]

containing the respondent's elicited certainty equivalent.

Its midpoint is

\[
\tilde c_{iR_j}
=
\frac{c^-_{iR_j}+c^+_{iR_j}}{2}.
\]

---

## 2.2 Benchmark risk prospects

The benchmark implementation uses four risk prospects:

\[
R_1=(80,0.25,0),
\]

\[
R_2=(80,0.50,0),
\]

\[
R_3=(80,0.75,0),
\]

and

\[
R_4=(100,0.50,20).
\]

The four tasks generate variation in both probability and payoff structure.

---

## 2.3 Model-free risk score

The raw risk score is the average certainty-equivalent midpoint across the four
risk tasks:

\[
RiskRaw_i
=
\frac{1}{4}
\sum_{j=1}^{4}
\tilde c_{iR_j}.
\]

Higher values indicate a greater valuation of risky prospects and are therefore
interpreted as greater risk tolerance.

The default standardized measure is

\[
RiskZ_i
=
\frac{RiskRaw_i-\overline{RiskRaw}}
{sd(RiskRaw)}.
\]

Thus:

- \(RiskZ_i=0\) corresponds to the sample mean;
- \(RiskZ_i=1\) corresponds to one sample standard deviation above the mean;
- higher values indicate greater risk tolerance.

---

# 3. Time

## 3.1 Task

A time task elicits the sooner equivalent of a later monetary payment.

For a payment \(x_j\) received at date \(t_j+\tau_j\), respondents repeatedly
choose between the later payment and an amount available at the sooner date
\(t_j\).

The procedure returns

\[
[c^-_{iT_j},c^+_{iT_j}],
\]

with midpoint

\[
\tilde c_{iT_j}
=
\frac{c^-_{iT_j}+c^+_{iT_j}}{2}.
\]

A larger sooner equivalent means that the respondent requires a larger amount
at the sooner date to give up the later payment and therefore indicates greater
patience.

---

## 3.2 Benchmark time prospects

The benchmark implementation uses four time prospects:

| Task | Later amount | Sooner date | Additional delay |
|------|--------------|-------------|------------------|
| T1 | 80 | 1 day | 3 months |
| T2 | 80 | 1 day | 6 months |
| T3 | 80 | 1 day | 12 months |
| T4 | 80 | 6 months | 6 months |

These tasks vary both the length of the delay and, for T4, the timing of the
sooner outcome.

---

## 3.3 Model-free patience score

The raw time score is

\[
TimeRaw_i
=
\frac{1}{4}
\sum_{j=1}^{4}
\tilde c_{iT_j}.
\]

Higher values indicate greater patience.

The default standardized measure is

\[
PatienceZ_i
=
\frac{TimeRaw_i-\overline{TimeRaw}}
{sd(TimeRaw)}.
\]

Higher values therefore indicate greater patience.

### Interpretation

This measure is model-free in the sense that its construction requires no
assumption about the functional form of utility or discounting.

It should not, however, be interpreted as a pure structural measure of time
preference. Under nonlinear utility, sooner equivalents can depend jointly on
utility curvature and discounting.

The model-free score is therefore best interpreted as an empirical measure of
intertemporal valuation.

---

# 4. Ambiguity

## 4.1 Principle

Ambiguity attitudes are measured by comparing the valuation of an ambiguous
prospect with the valuation of a matched risky prospect.

For ambiguity task \(A_j\), let

\[
\tilde c^{amb}_{iA_j}
\]

denote the midpoint of the elicited equivalent for the ambiguous prospect, and

\[
\tilde c^{risk}_{iA_j}
\]

the midpoint for the corresponding risky benchmark.

The task-level ambiguity difference is

\[
d^{A}_{ij}
=
\tilde c^{amb}_{iA_j}
-
\tilde c^{risk}_{iA_j}.
\]

If the ambiguous prospect is valued less than its matched risky benchmark, then

\[
d^{A}_{ij}<0,
\]

which is consistent with ambiguity aversion.

---

## 4.2 Model-free ambiguity score

With three benchmark ambiguity tasks, define

\[
AmbiguityRaw_i
=
\frac{1}{3}
\sum_{j=1}^{3}
d^{A}_{ij}.
\]

Under this convention:

- larger values indicate greater ambiguity tolerance;
- smaller values indicate greater ambiguity aversion.

The standardized score is

\[
AmbiguityToleranceZ_i
=
\frac{AmbiguityRaw_i-\overline{AmbiguityRaw}}
{sd(AmbiguityRaw)}.
\]

Higher values indicate greater ambiguity tolerance.

For applications where a measure of ambiguity *aversion* is preferred, users
can simply reverse the sign:

\[
AmbiguityAversionZ_i
=
-
AmbiguityToleranceZ_i.
\]

---

# 5. Complexity

## 5.1 Principle

Complexity attitudes are measured by comparing the valuation of a complex
prospect with that of a simpler economically matched benchmark.

Let

\[
\tilde c^{simple}_{iC}
\]

denote the midpoint of the equivalent elicited for the simple prospect and

\[
\tilde c^{complex}_{iC}
\]

the midpoint for the corresponding complex prospect.

Define the complexity penalty as

\[
ComplexityRaw_i
=
\tilde c^{simple}_{iC}
-
\tilde c^{complex}_{iC}.
\]

If

\[
\tilde c^{complex}_{iC}
<
\tilde c^{simple}_{iC},
\]

then

\[
ComplexityRaw_i>0,
\]

meaning that the respondent values the complex representation less than the
simple benchmark.

Higher values are therefore interpreted as greater complexity aversion.

---

## 5.2 Standardized complexity score

The default standardized score is

\[
ComplexityAversionZ_i
=
\frac{ComplexityRaw_i-\overline{ComplexityRaw}}
{sd(ComplexityRaw)}.
\]

Higher values indicate greater complexity aversion.

---

# 6. Standardization

## 6.1 Default transformation

PRELICIT standardizes individual-level domain scores using the sample mean and
standard deviation:

\[
Z_i
=
\frac{S_i-\bar S}{sd(S)},
\]

where \(S_i\) denotes the corresponding raw domain score.

The standardized measures are therefore relative measures within the analytical
sample.

By construction:

\[
E[Z]=0,
\qquad
sd(Z)=1.
\]

The principal advantage over rank transformations is that z-scores preserve
information about distances between respondents.

For example, an individual whose raw score lies far above the mean remains far
above the mean after standardization.

---

## 6.2 Sample dependence

Because z-scores depend on the mean and standard deviation of the reference
sample, they are not intrinsically comparable across independently standardized
datasets.

For replication, longitudinal analysis, or comparisons across samples,
researchers should either:

1. retain and report the raw scores;
2. use a common reference mean and standard deviation;
3. pool samples before standardization when substantively appropriate.

PRELICIT therefore always retains raw scores in addition to standardized
scores.

---

# 7. Optional rank-based measures

Rank and percentile transformations are available as optional robustness
measures.

For a raw score \(S_i\), a rank-based transformation uses only the respondent's
relative position in the empirical distribution.

Rank transformations have two advantages:

- robustness to extreme values;
- minimal reliance on cardinal differences between raw scores.

Their main disadvantage is that they discard information on distances between
respondents.

For this reason, PRELICIT uses standardized raw scores as the default and ranks
as an optional transformation.

---

# 8. Recommended output variables

A standard PRELICIT implementation should retain three levels of information.

## 8.1 Task-level outputs

For every respondent and prospect:

- lower interval bound;
- upper interval bound;
- interval width;
- midpoint;
- number of completed bisection steps.

For example:

```text
risk_r1_lower
risk_r1_upper
risk_r1_midpoint
risk_r1_width

time_t1_lower
time_t1_upper
time_t1_midpoint
time_t1_width
