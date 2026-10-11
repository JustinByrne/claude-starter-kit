# Testing

## Test-driven development
- Use TDD by default for new code and behaviour changes, following red → green → refactor.
- Red: write a test for the next small piece of behaviour and confirm it fails for the expected reason.
- Green: write the minimum code needed to make the test pass.
- Refactor: tidy up the code and tests while keeping them passing.
- TDD is not needed for docs, config, dependency bumps or purely cosmetic changes.

## Bug fixes
- Before fixing a bug, write a test that reproduces it and confirm it fails. The bug is fixed when that test passes.

## Changing existing code
- Before changing existing code that has no tests, add tests that capture its current behaviour.
- A refactor should not need test changes. If a refactor makes existing tests fail, it has changed behaviour: fix the refactor, not the tests.

## Writing tests
- Test behaviour through public interfaces, not implementation details or private methods.
- Each test covers one behaviour, with a name that describes it.
- Cover edge cases and error paths, not just the expected success case: empty input, limits and invalid data.
- Tests must not depend on test order, the current time, randomness or the network. Freeze the clock and use fixed random seeds.

## Test data and external services
- Use the framework's fakes for external APIs, email, queues and similar (e.g. Laravel's `Http::fake()` and `Mail::fake()`) rather than calling real services.
- Test data, fixtures and factories must use made-up values, never real client or personal data.

## Running tests
- During TDD, run only the test being worked on, to confirm red and green.
- When the task is finished, run the tests related to the change and fix any failures until they pass, then run the full suite.
- Report the results. If anything is still failing, say so rather than calling the task done.
- If the full suite has failures unrelated to the change, report them rather than fixing them.
- If a test passes and fails at random, report it rather than re-running it until it passes.

## Failing tests
- Never weaken a test to make it pass: no loosening assertions, changing expected values to match the actual output, skipping or deleting tests, raising timeouts, adding retries, lowering coverage thresholds or changing test config. Find and fix the cause instead.
- If the cause can't be fixed, or the test itself looks wrong, stop and ask before weakening it, and explain why.

## Frameworks and tooling
- Use the project's existing test framework, conventions and tooling (e.g. Laravel's own testing database handling). Follow existing tests for naming, layout and mocking.
- Do not add new testing tools or libraries without asking.
