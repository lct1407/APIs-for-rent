---
description: Run backend tests with pytest and show coverage
---

Run the FastAPI backend test suite and provide a detailed report.

Execute the following:

1. Navigate to backend directory
2. Run pytest with verbose output and coverage
3. Show test results summary
4. Display coverage report
5. Highlight any failing tests
6. If tests fail, analyze the failures and suggest fixes

Run: `cd backend && pytest -v --cov=app --cov-report=term-missing`

After running tests, provide:
- Total tests run, passed, failed, skipped
- Coverage percentage by module
- Any test failures with details
- Recommendations for improving coverage
