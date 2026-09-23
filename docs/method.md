# PRELICIT elicitation methodology

## Overview

PRELICIT is a toolkit for the survey-based elicitation of economic preferences.

Its core objective is to make choice-based preference elicitation sufficiently
simple and parsimonious for use in large-scale surveys, while retaining
structural interpretability.

Rather than presenting respondents with long lists of choices, PRELICIT relies
on adaptive sequences of binary decisions. Each response determines the next
choice shown to the respondent.

## Adaptive bisection procedure

For each elicitation task, an initial interval containing the relevant
equivalent is defined.

At each step:

1. the midpoint of the current interval is presented to the respondent;
2. the respondent makes a binary choice;
3. the response determines which half of the interval is retained;
4. the procedure continues until the desired precision is reached.

After \(K\) binary choices, the procedure yields an interval

\[
[c^-, c^+]
\]

containing the respondent's elicited equivalent.

This adaptive design reduces the number of decisions required from respondents
relative to exhaustive choice lists.

## Preference domains

PRELICIT implements a common adaptive elicitation framework across several
domains of economic preferences:

- time preferences;
- risk preferences;
- ambiguity attitudes;
- attitudes toward complexity.

Across domains, respondents repeatedly choose between a target prospect and
a simpler comparison option. The value of the comparison option is updated
adaptively according to previous responses, allowing PRELICIT to identify an
interval containing the respondent's equivalent using a small number of binary
choices.

## Time preferences

The time-preference module elicits sooner equivalents.

Respondents choose between a fixed monetary amount received at a later date
and a smaller amount received earlier. The earlier amount is adjusted
adaptively according to previous responses.

The module varies both the delay to the later outcome and, across tasks, the
timing of the earlier outcome. The final elicited interval bounds the amount
received earlier that makes the respondent approximately indifferent between
the two dated outcomes.

## Risk preferences

The risk-preference module elicits certainty equivalents for risky prospects
with known probabilities.

Respondents choose between a lottery and a certain monetary amount. Lotteries
are represented using an urn with a known composition: one ball is drawn and
the monetary payoff depends on its color. Because the composition of the urn
is explicitly known, the probabilities of the possible outcomes are known to
the respondent.

Across tasks, PRELICIT can vary outcome probabilities, payoff levels, and
payoff spreads. The certain amount is adjusted adaptively until an interval
containing the certainty equivalent of the risky prospect is identified.

## Ambiguity attitudes

The ambiguity module preserves the basic structure of the risk task while
removing information about outcome probabilities.

Respondents again choose between an uncertain prospect and a certain monetary
amount. However, the composition of the urn is unknown: respondents know the
set of possible colors and outcomes but do not know how many balls of each
color are contained in the urn.

As a result, the probability of receiving each monetary outcome is not known.

The certain comparison amount is adjusted adaptively to identify an interval
containing the certainty equivalent of the ambiguous prospect.

The design can vary which colors generate the high and low outcomes while
holding the basic choice environment constant. This makes it possible to
compare valuations of risky and ambiguous prospects within a common
elicitation framework.

## Attitudes toward complexity

The complexity module differs from both the risk and ambiguity modules.

Rather than drawing a single ball, all balls in the urn are used to determine
the payoff. Each color is associated with a monetary value and the payoff of
the target option is the arithmetic mean of the values associated with all
balls in the urn.

When the composition of the urn is known, the resulting payoff is therefore
deterministic. The distinction between the target option and the comparison
option does not arise from outcome risk or ambiguity, but from the complexity
of evaluating a multi-component payoff relative to a simple certain amount.

Respondents repeatedly choose between this complex option and a simple certain
amount. The certain amount is adjusted adaptively to identify an interval
containing the respondent's equivalent valuation of the complex option.

This design allows PRELICIT to study systematic heterogeneity in the valuation
of complexity separately from attitudes toward risk and ambiguity.

## Structural estimation

The elicitation procedure produces interval-censored observations rather than
arbitrary point estimates.

These intervals can subsequently be mapped into latent preference parameters
using structural decision models.

PRELICIT is intended to support estimation procedures that explicitly account
for:

- interval censoring;
- heterogeneity in individual preferences;
- respondent-level response noise;
- joint estimation across preference domains.

## Design principles

PRELICIT is developed around four main principles:

1. low respondent burden;
2. simplicity of individual decisions;
3. structural interpretability;
4. explicit treatment of measurement uncertainty and response noise.

## Status

This document describes the initial methodological specification of PRELICIT.
The software implementation is currently under development.
