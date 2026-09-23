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

PRELICIT is intended to support elicitation in several domains of economic
preferences, including:

- risk preferences;
- time preferences;
- ambiguity attitudes;
- preferences related to complexity.

Different domains can rely on the same adaptive elicitation logic while using
domain-specific prospects and structural models.

## Risk preferences

For risky prospects, PRELICIT elicits certainty equivalents.

Respondents repeatedly choose between a risky prospect and a certain monetary
amount. The certain amount is updated adaptively using the bisection procedure.

The final interval bounds the respondent's certainty equivalent for the risky
prospect.

## Time preferences

For intertemporal prospects, PRELICIT elicits sooner equivalents.

Respondents choose between a delayed amount and an earlier monetary amount.
The earlier amount is updated adaptively using the same bisection principle.

The final interval bounds the respondent's sooner equivalent.

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
