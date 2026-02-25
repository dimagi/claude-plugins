---
description: Interactively review a plan across architecture, code quality, tests, and performance before any code changes.
---

Review this plan thoroughly before making any code changes. For every issue or recommendation, explain the concrete tradeoffs, give me an opinionated recommendation, and ask for my input before assuming a direction.

My engineering preferences (use these to guide your recommendations):

* DRY is good, but don't over-abstract — duplication is preferable to the wrong abstraction. Flag obvious repetition, but don't force shared code where the use cases might diverge.
* Well-tested code is non-negotiable. I'd rather have too many tests than too few — but tests must be fast. We use pytest. Prefer strategies that avoid hitting the database unnecessarily: separate business logic from DB access so it can be tested with plain unit tests, use factory patterns (factory_boy) for tests that do need the DB, and use mocking where separation isn't practical. Be thoughtful about when a test actually needs `@pytest.mark.django_db`.
* I want code that's "engineered enough" — not under-engineered (fragile, hacky) and not over-engineered (premature abstraction, unnecessary complexity).
* I err on the side of handling more edge cases, not fewer; thoughtfulness > speed.
* Bias toward explicit over clever.

## BEFORE YOU START

Ask if I want one of two options:

1. **BIG CHANGE**: Work through this interactively, one section at a time (Architecture → Code Quality → Tests → Performance) with at most 4 top issues in each section.
2. **SMALL CHANGE**: Work through interactively ONE question per review section.

Use `AskUserQuestion` for this choice before proceeding to any review section.

## 1. Architecture review

Evaluate:

* Overall system design and component boundaries.
* Dependency graph and coupling concerns.
* Data flow patterns and potential bottlenecks.
* Scaling characteristics and single points of failure.
* Security architecture (auth, data access, API boundaries).

## 2. Code quality review

Evaluate:

* Code organization and module structure.
* DRY violations — flag clear repetition, but note where duplication might be intentional or where abstracting would couple things that shouldn't be coupled.
* Error handling patterns and missing edge cases (call these out explicitly).
* Technical debt hotspots.
* Areas that are over-engineered or under-engineered relative to my preferences.

## 3. Test review

Evaluate:

* Test coverage gaps (unit, integration, e2e).
* Test quality and assertion strength.
* Missing edge case coverage — be thorough.
* Untested failure modes and error paths.
* Test performance: flag tests that hit the DB unnecessarily or use slow fixtures. Call out opportunities to separate logic from DB access so it can be tested as plain unit tests without `@pytest.mark.django_db`. Where separation isn't feasible, suggest mocks or factories to keep the suite fast.

## 4. Performance review

Evaluate:

* N+1 queries and database access patterns.
* Memory-usage concerns.
* Caching opportunities.
* Slow or high-complexity code paths.

## For each issue you find

For every specific issue (bug, smell, design concern, or risk):

* Describe the problem concretely, with file and line references.
* Present 2–3 options, including "do nothing" where that's reasonable.
* For each option, specify: implementation effort, risk, impact on other code, and maintenance burden.
* Give me your recommended option and why, mapped to my preferences above.
* Then use `AskUserQuestion` to ask whether I agree or want to choose a different direction before proceeding.

## Workflow and interaction

* Do not assume my priorities on timeline or scale.
* After each section, use `AskUserQuestion` to ask for my feedback before moving on.

## Formatting rules

* NUMBER issues (Issue 1, Issue 2, …).
* Give LETTERS for options (A, B, C, …).
* When using `AskUserQuestion`, label each option clearly with the issue NUMBER and option LETTER so I don't get confused.
* Make the recommended option always the 1st option.
* Output the explanation and pros/cons of each section's questions AND your opinionated recommendation and why, then use `AskUserQuestion`.
