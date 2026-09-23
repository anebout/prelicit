# PRELICIT methodology

## Overview

PRELICIT is a toolkit for the survey-based elicitation of economic preferences
and related decision attitudes.

Its core objective is to make choice-based preference elicitation sufficiently
simple and parsimonious for use in large-scale surveys while preserving a
transparent link between respondents' choices and economically meaningful
model-free measures.

PRELICIT uses short adaptive binary-choice sequences to locate individual
equivalents.

The reference implementation covers four domains:

- risk;
- time;
- ambiguity;
- complexity.

The PRELICIT reference questionnaire contains:

- 4 risk prospects;
- 4 time prospects;
- 3 ambiguity prospects;
- 1 complexity prospect.

Each prospect is elicited using an adaptive bisection procedure.

The primary outputs of PRELICIT are the elicited intervals and model-free
indicators constructed directly from these intervals. Structural estimation is
deliberately outside the core scope of PRELICIT.

For each task, PRELICIT retains:

1. the lower and upper bounds of the elicited interval;
2. the midpoint of the interval;
3. information on completion of the bisection sequence.

At the domain level, PRELICIT can additionally construct model-free summary
indices and optional standardized or rank-based transformations.

Raw elicited equivalents remain the primary PRELICIT outputs.


# 1. Adaptive elicitation

## 1.1 General principle

For each task, the respondent repeatedly chooses between a target prospect and
a comparison amount.

The comparison amount is updated after each response according to an adaptive
bisection algorithm.

Let respondent \(i\) complete task \(j\). After \(K\) binary choices, the
procedure identifies an interval

\[
[c^-_{ij},c^+_{ij}]
\]

containing the respondent's elicited equivalent for that task.

At each bisection step:

1. a comparison amount is presented;
2. the respondent chooses between the target prospect and the comparison;
3. the response determines which part of the current interval is retained;
4. the next comparison is chosen within the retained interval.

This procedure concentrates questions around the respondent's implied
indifference point while requiring only a small number of simple binary
decisions.


## 1.2 Elicited interval

The elicited object is the interval

\[
[c^-_{ij},c^+_{ij}],
\]

not an exact point of indifference.

The interval should therefore be retained in the PRELICIT output data.

Its width is

\[
w_{ij}=c^+_{ij}-c^-_{ij}.
\]

The width depends on:

- the initial elicitation range;
- the number of completed bisection steps;
- the configuration of the task.


## 1.3 Midpoint

For descriptive analyses and construction of model-free indicators, PRELICIT
also computes the midpoint of the final interval:

\[
\tilde c_{ij}
=
\frac{c^-_{ij}+c^+_{ij}}{2}.
\]

The midpoint is a convenient summary of the information contained in the
elicited interval.

It should not be interpreted as an exactly observed latent indifference point.

PRELICIT therefore always retains both the original interval and its midpoint.


## 1.4 Incomplete bisection sequences

The interval representation naturally accommodates incomplete elicitation
sequences.

If a respondent stops before completing all bisection steps, PRELICIT retains
the interval implied by the choices completed up to that point.

The resulting interval is wider than the interval obtained after a complete
sequence, but the available information is not discarded.


# 2. PRELICIT reference design

The reference design reproduces the preference-elicitation questionnaire on
which PRELICIT is based.

It contains:

| Domain | Number of tasks | Main elicited object |
|---|---:|---|
| Risk | 4 | Certainty equivalent |
| Time | 4 | Sooner equivalent |
| Ambiguity | 3 | Ambiguity equivalent |
| Complexity | 1 | Simplicity equivalent |

The reference parameters are fixed and are reported below.

Using these parameters allows researchers to reproduce the original PRELICIT
instrument and facilitates comparison of results across studies.

PRELICIT also supports configurable implementations, described in Section 7.


# 3. Risk

## 3.1 Risk task

A risk task presents a binary lottery

\[
R_j=(x_j,p_j,y_j),
\]

where:

- \(x_j\) is the high monetary outcome;
- \(y_j\) is the low monetary outcome;
- \(p_j\) is the known probability of receiving \(x_j\).

The respondent repeatedly chooses between the lottery and a sure monetary
amount.

The adaptive procedure identifies an interval

\[
[c^-_{iR_j},c^+_{iR_j}]
\]

containing the respondent's certainty equivalent for the lottery.

Its midpoint is

\[
\widetilde{CE}_{ij}
=
\frac{c^-_{iR_j}+c^+_{iR_j}}{2}.
\]

Higher certainty equivalents indicate a higher valuation of the corresponding
risky prospect.


## 3.2 Reference risk prospects

The PRELICIT reference design contains four risk prospects:

| Task | High outcome \(x\) | Probability \(p\) | Low outcome \(y\) |
|---|---:|---:|---:|
| R1 | 80 | 0.25 | 0 |
| R2 | 80 | 0.50 | 0 |
| R3 | 80 | 0.75 | 0 |
| R4 | 100 | 0.50 | 20 |

Thus,

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

The first three prospects vary the probability of the high outcome while
holding monetary outcomes constant.

The fourth prospect changes the payoff support while retaining a probability
of 0.50.


## 3.3 Model-free risk measures

The task-level model-free risk measures are the four certainty-equivalent
midpoints

\[
\widetilde{CE}_{i1},
\widetilde{CE}_{i2},
\widetilde{CE}_{i3},
\widetilde{CE}_{i4}.
\]

These task-level measures are the primary risk outputs.

For applications requiring a single individual-level summary of the reference
design, PRELICIT can compute

\[
RiskRaw_i
=
\frac{1}{4}
\sum_{j=1}^{4}
\widetilde{CE}_{ij}.
\]

Higher values indicate a greater average valuation of the four risky prospects
and therefore greater risk tolerance within the PRELICIT reference design.

This is a model-free empirical index. It is not a structural parameter of a
specific utility function.


## 3.4 Scale-free task measures

For comparisons involving different monetary stakes, a task-level certainty
equivalent can optionally be expressed relative to its payoff range:

\[
RiskRelative_{ij}
=
\frac{\widetilde{CE}_{ij}-y_j}
{x_j-y_j}.
\]

This transformation places the elicited equivalent relative to the low and
high outcomes of the corresponding task.

PRELICIT retains the monetary equivalent even when this relative measure is
computed.


# 4. Time

## 4.1 Time task

A time task elicits the sooner equivalent of a later monetary payment.

Let \(x_j\) denote an amount received at date

\[
t_j+\tau_j,
\]

where \(t_j\) is the sooner date and \(\tau_j\) is the additional delay to the
later payment.

Respondents repeatedly choose between:

- the later payment \(x_j\) at \(t_j+\tau_j\); and
- a comparison amount received at the sooner date \(t_j\).

The comparison amount is updated using the same adaptive bisection principle.

The procedure identifies

\[
[c^-_{iT_j},c^+_{iT_j}],
\]

with midpoint

\[
\widetilde{SE}^{time}_{ij}
=
\frac{c^-_{iT_j}+c^+_{iT_j}}{2}.
\]

A larger sooner equivalent means that a larger sooner payment is required to
make the respondent indifferent to the later payment.

Within a given task, higher values therefore indicate greater patience.


## 4.2 Reference time prospects

The PRELICIT reference design contains four time prospects:

| Task | Later amount | Sooner date | Additional delay |
|---|---:|---|---|
| T1 | 80 | 1 day | 3 months |
| T2 | 80 | 1 day | 6 months |
| T3 | 80 | 1 day | 12 months |
| T4 | 80 | 6 months | 6 months |

T1--T3 vary the delay while keeping the sooner date approximately immediate.

T4 shifts both payments into the future, with the sooner payment occurring
after six months and the later payment an additional six months later.


## 4.3 Model-free time measures

The primary task-level measures are the four sooner-equivalent midpoints

\[
\widetilde{SE}^{time}_{i1},
\widetilde{SE}^{time}_{i2},
\widetilde{SE}^{time}_{i3},
\widetilde{SE}^{time}_{i4}.
\]

For applications requiring a single summary of the PRELICIT reference design,

\[
TimeRaw_i
=
\frac{1}{4}
\sum_{j=1}^{4}
\widetilde{SE}^{time}_{ij}.
\]

Higher values indicate greater average patience across the four reference
tasks.

This score is model-free in the sense that its construction requires no
assumption about the functional form of utility or discounting.

It should not, however, be interpreted as a pure structural discount-rate
parameter. Under nonlinear utility, sooner equivalents may depend jointly on
the valuation of monetary outcomes and intertemporal preferences.

The measure is therefore best interpreted as an empirical index of
intertemporal valuation.


## 4.4 Scale-free time measures

When later amounts differ across configurable implementations, PRELICIT can
optionally report

\[
TimeRelative_{ij}
=
\frac{\widetilde{SE}^{time}_{ij}}
{x_j}.
\]

This expresses the sooner equivalent as a fraction of the later monetary
amount.

The monetary sooner equivalent remains the primary output.


# 5. Ambiguity

## 5.1 Ambiguity task

The ambiguity module preserves the main presentation of the risk task while
removing information about the composition of the urn.

Respondents know:

- the possible colors;
- which colors are associated with each monetary outcome;
- the possible monetary outcomes.

However, they do not know how many balls of each color are contained in the
urn.

The probabilities of the monetary outcomes are therefore not objectively known
to the respondent.

The respondent repeatedly chooses between the ambiguous prospect and a certain
monetary amount.

The adaptive procedure identifies

\[
[c^-_{iA_j},c^+_{iA_j}],
\]

with midpoint

\[
\widetilde{AE}_{ij}
=
\frac{c^-_{iA_j}+c^+_{iA_j}}{2},
\]

where \(AE\) denotes the ambiguity equivalent.


## 5.2 Reference ambiguity prospects

The PRELICIT reference design contains three ambiguity prospects.

All three use monetary outcomes of EUR 80 and EUR 0 and correspond to
likelihood levels 0.25, 0.50, and 0.75.

| Task | High outcome | Likelihood level | Low outcome |
|---|---:|---:|---:|
| A1 | 80 | 0.25 | 0 |
| A2 | 80 | 0.50 | 0 |
| A3 | 80 | 0.75 | 0 |

The term "likelihood level" describes the structure of the ambiguity task. It
should not be interpreted as a known objective probability of receiving the
high outcome, since the composition of the urn is unknown.

The three ambiguity tasks are designed to be matched to risk tasks R1, R2, and
R3, respectively.


## 5.3 Model-free ambiguity measures

The primary ambiguity outputs are the three ambiguity-equivalent midpoints

\[
\widetilde{AE}_{i1},
\widetilde{AE}_{i2},
\widetilde{AE}_{i3}.
\]

Because the ambiguity tasks are matched to corresponding risky prospects,
PRELICIT can additionally compute task-level differences

\[
AmbiguityDifference_{ij}
=
\widetilde{AE}_{ij}
-
\widetilde{CE}_{ij},
\qquad j\in\{1,2,3\}.
\]

Under this convention:

- a negative value means that the ambiguous prospect is valued less than the
  matched risky prospect;
- a value of zero means equal valuations;
- a positive value means that the ambiguous prospect is valued more than the
  matched risky prospect.

A negative difference is therefore consistent with ambiguity aversion for that
matched pair.


## 5.4 Aggregate ambiguity index

For applications requiring a single model-free ambiguity summary,

\[
AmbiguityRaw_i
=
\frac{1}{3}
\sum_{j=1}^{3}
AmbiguityDifference_{ij}.
\]

Under this convention:

- higher values indicate greater ambiguity tolerance;
- lower values indicate greater ambiguity aversion.

If a positively oriented ambiguity-aversion measure is preferred, PRELICIT can
also report

\[
AmbiguityAversionRaw_i
=
-
AmbiguityRaw_i.
\]

These differences are descriptive model-free indicators rather than structural
parameters from a particular model of decision under ambiguity.


# 6. Complexity

## 6.1 Mirror-task principle

The PRELICIT complexity task is a deterministic mirror of a corresponding risk
task.

In the risk task, one ball is drawn from an urn and the realized color
determines the monetary payoff.

In the complexity task, the payoff is instead determined using all balls in
the urn.

Each color is associated with a monetary value and the payoff is the arithmetic
mean of the monetary values associated with all balls.

Because the composition of the urn is known in the complexity task and all
balls enter the calculation, the final payoff is deterministic.

The task therefore removes outcome stochasticity while retaining the need to
evaluate and aggregate the payoff information represented by the urn.


## 6.2 Simplicity equivalent

The complexity module elicits a simplicity equivalent.

Let

\[
SE_i
\]

denote the respondent's simplicity equivalent for the deterministic mirror
prospect.

PRELICIT identifies an interval

\[
[c^-_{iC},c^+_{iC}]
\]

containing this equivalent.

Its midpoint is

\[
\widetilde{SE}_i
=
\frac{c^-_{iC}+c^+_{iC}}{2}.
\]


## 6.3 Reference complexity prospect

The current PRELICIT reference design contains one complexity task.

It is the deterministic mirror of the 0.50 risk prospect with monetary outcomes
EUR 80 and EUR 0.

The corresponding objective benchmark is

\[
EV
=
0.50\times80
+
0.50\times0
=
40.
\]

Thus the reference complexity task is matched to risk prospect R2.


## 6.4 Model-free complexity measures

The primary complexity output is the simplicity-equivalent midpoint

\[
\widetilde{SE}_i.
\]

The difference between the simplicity equivalent and the objective benchmark is

\[
ComplexityComponent_i
=
\widetilde{SE}_i-EV.
\]

For the PRELICIT reference task,

\[
ComplexityComponent_i
=
\widetilde{SE}_i-40.
\]

Under this convention:

- zero corresponds to valuation at the objective benchmark;
- a negative value means that the deterministic complex prospect is valued
  below its objective benchmark;
- a positive value means that it is valued above its objective benchmark.

For applications preferring an index increasing in complexity aversion,
PRELICIT can report

\[
ComplexityAversionRaw_i
=
EV-\widetilde{SE}_i.
\]

Higher values of this sign-reversed measure indicate a larger penalty assigned
to the complex deterministic prospect.


## 6.5 Risk-complexity decomposition

Because the reference complexity task is paired with risk prospect R2, PRELICIT
can construct the model-free identity

\[
CE_i-EV
=
(CE_i-SE_i)
+
(SE_i-EV).
\]

Using midpoint measures,

\[
\widetilde{CE}_{i2}-40
=
(\widetilde{CE}_{i2}-\widetilde{SE}_i)
+
(\widetilde{SE}_i-40).
\]

This yields three quantities:

\[
ConventionalRisk_i
=
\widetilde{CE}_{i2}-40,
\]

\[
StochasticityComponent_i
=
\widetilde{CE}_{i2}-\widetilde{SE}_i,
\]

and

\[
ComplexityComponent_i
=
\widetilde{SE}_i-40.
\]

The decomposition requires no parametric utility or probability-weighting
model.

PRELICIT reports these quantities as model-free descriptive indicators.


# 7. Reference and configurable implementations

## 7.1 Reference implementation

The PRELICIT reference implementation reproduces the benchmark questionnaire
described above.

Its purpose is to facilitate:

- replication;
- reuse of the original elicitation instrument;
- comparability across studies;
- accumulation of evidence using a common design.

Researchers wishing to use the original PRELICIT instrument should retain the
reference task parameters unchanged.


## 7.2 Configurable implementation

PRELICIT also supports controlled customization of the elicitation design.

The configurable mode preserves the main structure of the reference
instrument while allowing researchers to adapt monetary outcomes to their
application.

For the risk and ambiguity modules, the core probability or likelihood levels

\[
0.25,\qquad 0.50,\qquad 0.75
\]

are retained.

Researchers may modify monetary outcomes while preserving this common
probability/likelihood structure.

This restriction maintains a close connection to the PRELICIT reference design
and facilitates comparison across implementations.


## 7.3 Bisection-compatible outcomes

Configurable monetary outcomes must generate a valid bisection tree.

PRELICIT therefore checks proposed task parameters before generating the
questionnaire.

A valid configuration must ensure that the successive comparison amounts
generated by the bisection procedure remain simple integer monetary amounts.

Configurations that do not satisfy the bisection constraints are rejected by
the software.

The exact admissibility rule is determined by the elicitation range and the
number of bisection steps and is enforced automatically rather than left to the
user.


## 7.4 Optional complexity extensions

The reference design contains only the 0.50 complexity mirror task.

The configurable framework can additionally support deterministic mirror tasks
corresponding to the 0.25 and 0.75 risk structures.

This gives the optional matched structure

\[
R_{0.25}\leftrightarrow C_{0.25},
\]

\[
R_{0.50}\leftrightarrow C_{0.50},
\]

\[
R_{0.75}\leftrightarrow C_{0.75}.
\]

These additional complexity tasks are extensions of the PRELICIT framework and
are not part of the original reference questionnaire.

When such extensions are used, the relevant deterministic benchmark for each
mirror task is calculated from the corresponding payoff structure.


# 8. Standardization and transformations

## 8.1 Primary measures

The primary PRELICIT measures are always the untransformed elicitation outputs:

- interval bounds;
- interval widths;
- midpoint equivalents;
- task-level model-free differences where applicable.

Raw measures should be retained even when additional transformations are used.


## 8.2 Z-score standardization

For applications requiring standardized variables, any individual-level score
\(S_i\) can optionally be transformed into

\[
Z_i
=
\frac{S_i-\bar S}
{sd(S)}.
\]

The resulting variable has sample mean zero and sample standard deviation one.

Z-scores can be useful when:

- comparing effect sizes across domains;
- displaying several PRELICIT measures in the same regression or figure;
- expressing associations in standard-deviation units.

They are not the default PRELICIT measurement scale.


## 8.3 Sample dependence of z-scores

Z-scores depend on the mean and standard deviation of the sample used for
standardization.

They are therefore not intrinsically comparable across datasets standardized
independently.

For replication, longitudinal analysis, or comparisons across samples,
researchers should:

1. retain and report the underlying raw measures;
2. use a common reference mean and standard deviation where appropriate; or
3. pool samples before standardization when substantively justified.


## 8.4 Rank and percentile transformations

Rank and percentile transformations are available as optional analysis tools.

They can be useful when researchers wish to reduce sensitivity to extreme
values or focus on respondents' relative positions in the empirical
distribution.

Their main limitation is that they discard information about cardinal distances
between respondents.

For this reason, PRELICIT treats ranks and percentiles as optional
transformations rather than primary outputs.


# 9. Recommended output variables

A standard PRELICIT implementation should retain task-level data, domain-level
indicators, and questionnaire metadata.


## 9.1 Task-level outputs

For every respondent and every task, PRELICIT should retain:

- lower interval bound;
- upper interval bound;
- interval width;
- midpoint;
- number of completed bisection steps;
- task identifier;
- task parameters.

Example variable names include:

```text
risk_r1_lower
risk_r1_upper
risk_r1_midpoint
risk_r1_width
risk_r1_steps

risk_r2_lower
risk_r2_upper
risk_r2_midpoint
risk_r2_width
risk_r2_steps

time_t1_lower
time_t1_upper
time_t1_midpoint
time_t1_width
time_t1_steps

ambiguity_a1_lower
ambiguity_a1_upper
ambiguity_a1_midpoint
ambiguity_a1_width
ambiguity_a1_steps

complexity_c50_lower
complexity_c50_upper
complexity_c50_midpoint
complexity_c50_width
complexity_c50_steps
