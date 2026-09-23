# PRELICIT

**PRELICIT** is a toolkit for survey-based elicitation of economic preferences.

The project aims to provide simple, reusable, and theoretically grounded tools
for eliciting individual economic preferences in large-scale surveys and
experiments.

## Scope

PRELICIT is designed to support preference elicitation in several domains,
including:

- risk preferences
- time preferences
- ambiguity attitudes
- complexity-related preferences

The initial implementation focuses on adaptive binary-choice procedures that
limit respondent burden while retaining enough information for structural
estimation.

## Design principles

PRELICIT is built around four principles:

1. simplicity for respondents;
2. compatibility with large-scale surveys;
3. structural interpretability;
4. explicit treatment of response noise and measurement uncertainty.

## Current status

PRELICIT is currently under active development.

The first public version documents the elicitation methodology, planned data
structure, and software architecture. Implementation of the elicitation engine
and estimation routines is ongoing.

## Methodology

The core elicitation procedure relies on adaptive binary choices using a
bisection algorithm.

For a given prospect, successive binary choices progressively narrow the
interval containing the respondent's certainty or equivalent value.

The resulting interval-censored observations can then be used directly in
structural estimation rather than being reduced to arbitrary point estimates.

Detailed methodological documentation is available in [`docs/`](docs/).

## Research applications

The elicitation methodology underlying PRELICIT has been used in empirical
research combining economic preferences with general-population survey data.

Related replication materials are available at:

https://doi.org/10.3886/E251164V2

## Citation

A formal software citation will be provided with the first stable release.

If you use PRELICIT or adapt its methodology, please cite the corresponding
methodological and application papers.

## Development roadmap

Planned components include:

- adaptive bisection elicitation engine;
- risk-preference module;
- time-preference module;
- ambiguity module;
- complexity module;
- standardized response-data format;
- structural estimation routines;
- documentation and worked examples;
- interfaces for survey and experimental platforms.

## License

A software license will be added following institutional review.

## Contributing

PRELICIT is under active development. Issues and suggestions are welcome.


