---
description: Run frontend tests with Vitest
---

Run the React/TypeScript frontend test suite and provide a detailed report.

Execute the following:

1. Navigate to client directory
2. Run vitest if configured, otherwise suggest setup
3. Show test results summary
4. Display coverage report if available
5. Highlight any failing tests

If Vitest is not configured yet, offer to set it up:
- Install dependencies: `npm install -D vitest @testing-library/react @testing-library/jest-dom jsdom`
- Add test configuration to vite.config.ts
- Create test setup file

After running tests (or if no tests exist), provide:
- Test results summary
- Coverage information
- Suggestions for components that need testing
- Recommendations for test improvements
