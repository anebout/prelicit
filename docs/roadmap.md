# PRELICIT development roadmap

PRELICIT is being developed as a reusable toolkit for survey-based elicitation
of economic preferences and related decision attitudes.

The initial development focuses on transforming existing survey implementations
into reusable and documented software components.

## Phase 1 — Project specification

- [x] Create public PRELICIT repository
- [x] Document the general elicitation methodology
- [ ] Define the PRELICIT reference design
- [ ] Define a standard output data format
- [ ] Select an open-source software license

## Phase 2 — oTree implementation

- [ ] Import the existing oTree questionnaire implementation
- [ ] Separate study-specific code from reusable elicitation components
- [ ] Implement a reusable adaptive bisection engine
- [ ] Implement the PRELICIT reference tasks
- [ ] Allow optional customization of task parameters
- [ ] Add example oTree configurations

## Phase 3 — Data processing in R

- [ ] Import PRELICIT/oTree response data
- [ ] Reconstruct elicited intervals
- [ ] Compute interval midpoints
- [ ] Generate model-free preference indicators
- [ ] Produce basic descriptive statistics and diagnostics
- [ ] Export analysis-ready datasets

## Phase 4 — Preference domains

Reference implementations will cover:

- [ ] Risk
- [ ] Time
- [ ] Ambiguity
- [ ] Complexity

The precise analytical treatment of each domain may evolve as the corresponding
research develops.

## Phase 5 — Structural estimation

Potential extensions include:

- [ ] Interval-censored likelihoods
- [ ] Structural risk and time preference parameters
- [ ] Respondent-level response-noise parameters
- [ ] Hierarchical estimation

Structural estimation is planned as an extension of the core elicitation and
model-free analysis toolkit.

## Phase 6 — Documentation and distribution

- [ ] Add worked examples
- [ ] Add automated tests
- [ ] Create user documentation
- [ ] Create a stable software release
- [ ] Archive a release with a DOI
- [ ] Prepare JOSS submission
