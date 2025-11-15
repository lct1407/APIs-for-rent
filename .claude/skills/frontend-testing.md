# Frontend Testing Skill

**Description**: Test React/TypeScript components with Vitest and React Testing Library

**When to use**: When you need to test React components, hooks, or frontend functionality

## Instructions

When invoked, you should:

1. **Set up testing environment** (if not already configured):
   ```bash
   cd client

   # Install testing dependencies
   npm install -D vitest @testing-library/react @testing-library/jest-dom @testing-library/user-event jsdom @vitest/ui

   # Install additional utilities
   npm install -D @testing-library/react-hooks
   ```

2. **Create test configuration**:

   **vite.config.ts** - Add test configuration:
   ```typescript
   /// <reference types="vitest" />
   import { defineConfig } from 'vite'
   import react from '@vitejs/plugin-react'

   export default defineConfig({
     plugins: [react()],
     test: {
       globals: true,
       environment: 'jsdom',
       setupFiles: './src/test/setup.ts',
       css: true,
     },
   })
   ```

   **src/test/setup.ts** - Test setup:
   ```typescript
   import '@testing-library/jest-dom'
   import { cleanup } from '@testing-library/react'
   import { afterEach } from 'vitest'

   afterEach(() => {
     cleanup()
   })
   ```

3. **Add test scripts to package.json**:
   ```json
   {
     "scripts": {
       "test": "vitest",
       "test:ui": "vitest --ui",
       "test:coverage": "vitest --coverage"
     }
   }
   ```

4. **Write tests** based on component type:

   **UI Component Test** (`src/components/ui/__tests__/button.test.tsx`):
   ```typescript
   import { describe, it, expect, vi } from 'vitest'
   import { render, screen } from '@testing-library/react'
   import userEvent from '@testing-library/user-event'
   import { Button } from '../button'

   describe('Button', () => {
     it('renders with text', () => {
       render(<Button>Click me</Button>)
       expect(screen.getByText('Click me')).toBeInTheDocument()
     })

     it('calls onClick when clicked', async () => {
       const onClick = vi.fn()
       const user = userEvent.setup()

       render(<Button onClick={onClick}>Click me</Button>)

       await user.click(screen.getByText('Click me'))
       expect(onClick).toHaveBeenCalledTimes(1)
     })

     it('applies variant styles', () => {
       render(<Button variant="destructive">Delete</Button>)
       const button = screen.getByText('Delete')
       expect(button).toHaveClass('bg-destructive')
     })

     it('is disabled when disabled prop is true', () => {
       render(<Button disabled>Disabled</Button>)
       expect(screen.getByText('Disabled')).toBeDisabled()
     })
   })
   ```

   **Page Component Test** (`src/pages/user/__tests__/UserDashboard.test.tsx`):
   ```typescript
   import { describe, it, expect, vi } from 'vitest'
   import { render, screen, waitFor } from '@testing-library/react'
   import { BrowserRouter } from 'react-router-dom'
   import { AuthProvider } from '../../../contexts/AuthContext'
   import { ThemeProvider } from '../../../contexts/ThemeContext'
   import UserDashboard from '../UserDashboard'

   const renderWithProviders = (component: React.ReactElement) => {
     return render(
       <BrowserRouter>
         <ThemeProvider>
           <AuthProvider>
             {component}
           </AuthProvider>
         </ThemeProvider>
       </BrowserRouter>
     )
   }

   describe('UserDashboard', () => {
     it('displays user metrics', async () => {
       renderWithProviders(<UserDashboard />)

       await waitFor(() => {
         expect(screen.getByText(/API Calls/i)).toBeInTheDocument()
         expect(screen.getByText(/Credits/i)).toBeInTheDocument()
       })
     })

     it('shows loading state initially', () => {
       renderWithProviders(<UserDashboard />)
       expect(screen.getByText(/Loading/i)).toBeInTheDocument()
     })
   })
   ```

   **Hook Test** (`src/contexts/__tests__/useAuth.test.tsx`):
   ```typescript
   import { describe, it, expect } from 'vitest'
   import { renderHook, waitFor } from '@testing-library/react'
   import { AuthProvider, useAuth } from '../AuthContext'

   const wrapper = ({ children }: { children: React.ReactNode }) => (
     <AuthProvider>{children}</AuthProvider>
   )

   describe('useAuth', () => {
     it('provides auth context', () => {
       const { result } = renderHook(() => useAuth(), { wrapper })
       expect(result.current).toHaveProperty('user')
       expect(result.current).toHaveProperty('login')
       expect(result.current).toHaveProperty('logout')
     })

     it('logs in user successfully', async () => {
       const { result } = renderHook(() => useAuth(), { wrapper })

       await result.current.login('user@example.com', 'password')

       await waitFor(() => {
         expect(result.current.isAuthenticated).toBe(true)
         expect(result.current.user).not.toBeNull()
       })
     })
   })
   ```

5. **Mock external dependencies**:

   **Mock API calls**:
   ```typescript
   import { vi } from 'vitest'

   vi.mock('../services/api', () => ({
     apiService: {
       get: vi.fn(() => Promise.resolve({ data: [] })),
       post: vi.fn(() => Promise.resolve({ success: true })),
     }
   }))
   ```

   **Mock localStorage**:
   ```typescript
   const localStorageMock = {
     getItem: vi.fn(),
     setItem: vi.fn(),
     clear: vi.fn(),
   }
   global.localStorage = localStorageMock as any
   ```

6. **Run tests**:
   ```bash
   cd client

   # Run all tests
   npm test

   # Run in watch mode
   npm test -- --watch

   # Run with UI
   npm run test:ui

   # Run with coverage
   npm run test:coverage

   # Run specific test file
   npm test button.test

   # Run tests matching pattern
   npm test -- --grep "Button"
   ```

7. **Test coverage goals**:
   - UI Components: 80%+ coverage
   - Page Components: 70%+ coverage
   - Hooks/Contexts: 90%+ coverage
   - Utilities: 95%+ coverage

8. **Common test patterns**:

   **Testing async operations**:
   ```typescript
   it('loads data asynchronously', async () => {
     render(<MyComponent />)

     await waitFor(() => {
       expect(screen.getByText('Data loaded')).toBeInTheDocument()
     })
   })
   ```

   **Testing user interactions**:
   ```typescript
   it('handles form submission', async () => {
     const user = userEvent.setup()
     const onSubmit = vi.fn()

     render(<MyForm onSubmit={onSubmit} />)

     await user.type(screen.getByLabelText('Email'), 'test@example.com')
     await user.click(screen.getByRole('button', { name: /submit/i }))

     expect(onSubmit).toHaveBeenCalledWith({ email: 'test@example.com' })
   })
   ```

   **Testing conditional rendering**:
   ```typescript
   it('shows error message when error occurs', () => {
     render(<MyComponent error="Something went wrong" />)
     expect(screen.getByText('Something went wrong')).toBeInTheDocument()
   })
   ```

   **Testing with React Router**:
   ```typescript
   import { MemoryRouter } from 'react-router-dom'

   it('navigates to dashboard', async () => {
     render(
       <MemoryRouter initialEntries={['/']}>
         <App />
       </MemoryRouter>
     )
   })
   ```

## What to Test

### ✅ Do Test:
- Component renders correctly
- User interactions (clicks, typing, form submissions)
- Conditional rendering based on props/state
- Error states and loading states
- Accessibility (ARIA labels, keyboard navigation)
- Integration with contexts
- Navigation and routing

### ❌ Don't Test:
- Implementation details (internal state, private methods)
- Third-party library internals
- CSS styles (unless critical to functionality)
- Mocked functions (test behavior, not mocks)

## Best Practices

1. **Write tests from user perspective**: Use accessible queries (getByRole, getByLabelText)
2. **Avoid implementation details**: Don't test internal state, test behavior
3. **Use userEvent over fireEvent**: Simulates real user interactions
4. **Clean up after tests**: Use cleanup() or automatic cleanup
5. **Mock external dependencies**: Don't make real API calls
6. **Test edge cases**: Empty states, error states, loading states
7. **Keep tests simple**: One assertion per test when possible

## Troubleshooting

**Issue**: "Cannot find module" errors
- Ensure vite.config.ts has correct path resolution
- Check tsconfig.json paths configuration

**Issue**: Tests timing out
- Increase timeout in vitest config
- Check for infinite loops or missing awaits

**Issue**: "Not wrapped in act(...)" warnings
- Use waitFor() for async updates
- Ensure all state updates are awaited

## Output

Provide:
1. Test results summary (passed/failed/skipped)
2. Coverage report (lines, branches, functions)
3. Failed test details with debugging info
4. Suggestions for improving test coverage
5. Any identified gaps in testing
