# test
MSE 1 ---
### Summary of Changes & Root Cause Diagnosis

1. **What was wrong**:
   - The test suite lacked coverage for `normalize_phone` and `mask_email` error branches entirely, causing test coverage to remain well below the 85% threshold (baseline ~55%, rising to only ~73% with just `test_mask_email_basic`).
   - The codebase was unprotected against untested regressions reaching the default branch.

2. **Why CI caught this automatically**:
   - The GitHub Actions workflow `coverage.yml` ran `pytest --cov=src --cov-fail-under=85` on the `pull_request` event targeting `main`.
   - Because the test suite only covered ~73% of lines in `src/`, pytest exited with a failure code, failing the workflow check.
   - GitHub branch protection enforced this check as a mandatory gate, preventing the pull request from being merged until comprehensive unit tests were added to exceed 85% coverage.