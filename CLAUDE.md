# CLAUDE.md - AI Assistant Guide for APIs-for-Rent

**Last Updated**: 2025-11-15
**Project**: RentAPI - API Services Platform
**Version**: 0.0.0

This document provides comprehensive guidance for AI assistants (like Claude) working on the APIs-for-rent codebase. It explains the project structure, development workflows, conventions, and best practices to follow.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Repository Structure](#repository-structure)
3. [Tech Stack](#tech-stack)
4. [Development Workflow](#development-workflow)
5. [Git Conventions](#git-conventions)
6. [Code Architecture](#code-architecture)
7. [Component Patterns](#component-patterns)
8. [State Management](#state-management)
9. [Routing & Navigation](#routing--navigation)
10. [Styling Conventions](#styling-conventions)
11. [Type System](#type-system)
12. [Common Development Tasks](#common-development-tasks)
13. [Build & Optimization](#build--optimization)
14. [Important Notes for AI Assistants](#important-notes-for-ai-assistants)

---

## Project Overview

**Purpose**: A modern full-featured web application for managing API services with credit-based subscriptions.

**Key Features**:
- Role-based authentication (Admin/User)
- Admin dashboard with analytics, user management, and activity monitoring
- User dashboard with usage metrics, API key management, and billing
- Dark mode support with localStorage persistence
- Responsive design (mobile-first)
- Credit-based subscription system
- Mock authentication (ready for real API integration)

**Demo Credentials**:
- **Admin**: `admin@example.com` / `password`
- **User**: `user@example.com` / `password`

**Development Status**: Active development with recent work on:
- Vuexy-inspired UI improvements (Nov 5, 2025)
- Bundle optimization with code splitting (Nov 5, 2025)
- Complete platform UI implementation (Nov 5, 2025)

---

## Repository Structure

```
APIs-for-rent/
├── client/                          # React TypeScript frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── ui/                 # Reusable UI components (6 files)
│   │   │   │   ├── badge.tsx       # Status badges
│   │   │   │   ├── button.tsx      # CVA-based button variants
│   │   │   │   ├── card.tsx        # Composable card component
│   │   │   │   ├── dropdown.tsx    # Floating menu component
│   │   │   │   ├── input.tsx       # Form input wrapper
│   │   │   │   └── table.tsx       # Data table component
│   │   │   └── layout/             # Layout components (3 files)
│   │   │       ├── MainLayout.tsx  # Primary app wrapper
│   │   │       ├── Navbar.tsx      # Top navigation (145 lines)
│   │   │       └── Sidebar.tsx     # Hierarchical menu (200 lines)
│   │   ├── pages/
│   │   │   ├── public/             # Public pages (3 files)
│   │   │   │   ├── LandingPage.tsx # Marketing homepage
│   │   │   │   ├── LoginPage.tsx   # Authentication
│   │   │   │   └── RegisterPage.tsx # User registration
│   │   │   ├── admin/              # Admin pages (3 files)
│   │   │   │   ├── AdminDashboard.tsx    # KPI & analytics
│   │   │   │   ├── UserManagement.tsx    # User list (347 lines)
│   │   │   │   └── UserDetail.tsx        # User detail/edit view
│   │   │   └── user/               # User pages (2 files)
│   │   │       ├── UserDashboard.tsx     # User metrics
│   │   │       └── UserProfile.tsx       # Account/billing (304 lines)
│   │   ├── contexts/               # React Context API (2 files)
│   │   │   ├── AuthContext.tsx     # Authentication state (195 lines)
│   │   │   └── ThemeContext.tsx    # Dark mode theme (42 lines)
│   │   ├── types/                  # TypeScript definitions
│   │   │   └── index.ts            # User, ApiCall, KPI types
│   │   ├── data/                   # Mock data
│   │   │   └── mockData.ts         # Users, API calls, KPIs, etc.
│   │   ├── lib/                    # Utility functions
│   │   │   └── utils.ts            # cn(), formatters, generators
│   │   ├── assets/                 # Static assets
│   │   ├── App.tsx                 # Main routing & providers (3312 lines)
│   │   ├── main.tsx                # Entry point (230 lines)
│   │   └── index.css               # Tailwind + custom theme
│   ├── public/                     # Static files
│   ├── package.json                # Dependencies & scripts
│   ├── vite.config.ts              # Vite configuration
│   ├── tailwind.config.js          # Tailwind configuration
│   ├── tsconfig.json               # TypeScript root config
│   ├── tsconfig.app.json           # App TypeScript config
│   ├── tsconfig.node.json          # Node TypeScript config
│   ├── eslint.config.js            # ESLint configuration
│   └── postcss.config.js           # PostCSS configuration
├── README.md                        # User-facing documentation
└── CLAUDE.md                        # This file (AI assistant guide)
```

**Total Component Code**: ~1,817 lines (25 TypeScript/TSX files)

---

## Tech Stack

### Core Dependencies
| Package | Version | Purpose |
|---------|---------|---------|
| **react** | 19.1.1 | UI framework |
| **react-dom** | 19.1.1 | React DOM renderer |
| **typescript** | 5.9.3 | Type-safe development |
| **vite** | 7.1.7 | Build tool & dev server |

### Key Libraries
| Package | Version | Purpose |
|---------|---------|---------|
| **react-router-dom** | 7.9.5 | Client-side routing |
| **recharts** | 3.3.0 | Data visualization (charts) |
| **lucide-react** | 0.552.0 | Icon library (24+ icons used) |
| **date-fns** | 4.1.0 | Date formatting & manipulation |
| **tailwindcss** | 3.4.18 | Utility-first CSS framework |
| **class-variance-authority** | 0.7.1 | CVA for component variants |
| **clsx** | 2.1.1 | Conditional classNames |
| **tailwind-merge** | 3.3.1 | Merge Tailwind classes |

### DevDependencies
- **ESLint**: 9.36.0 (flat config format)
- **TypeScript ESLint**: 8.45.0
- **Autoprefixer**: 10.4.21
- **PostCSS**: 8.5.6

---

## Development Workflow

### Initial Setup
```bash
cd APIs-for-rent/client
npm install                    # Install dependencies
npm run dev                    # Start dev server (http://localhost:5173)
```

### Available Scripts
```bash
npm run dev       # Start Vite dev server with HMR
npm run build     # TypeScript check + production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

### Development Server
- **Port**: 5173 (default Vite)
- **HMR**: Enabled (Fast Refresh)
- **TypeScript**: Real-time type checking
- **ESLint**: Runs on save

### Build Output
- **Directory**: `client/dist/`
- **Entry Point**: `index.html`
- **Assets**: Hashed filenames for cache busting

---

## Git Conventions

### Branch Naming
- **Pattern**: `claude/<feature-name>-<session-id>`
- **Examples**:
  - `claude/vuexy-user-list-demo-011CUpatAyvTDKHtj5UNdw7G`
  - `claude/optimize-bundle-size-011CUpZBLTBEz5TnfQdFV7mz`
  - `claude/rent-api-platform-ui-011CUpWbcm1ySuyEck8cN2mg`

### Commit Message Format
```
<type>: <description>

Types:
- feat: New feature
- fix: Bug fix
- refactor: Code refactoring
- docs: Documentation changes
- style: Code style changes (formatting)
- test: Adding/updating tests
- chore: Build/config changes
```

**Examples**:
- `feat: Implement Vuexy-inspired UI improvements for user list and admin interface`
- `feat: Optimize bundle size with code splitting and lazy loading`
- `feat: Implement complete Rent API Services Platform UI`

### Pull Request Workflow
1. Create feature branch from `main`
2. Develop on branch with descriptive commits
3. Push to origin with `-u` flag: `git push -u origin <branch-name>`
4. Create PR to merge back into `main`
5. PRs reviewed and merged by maintainer

### Git Best Practices
- Always develop on designated branch (provided in session context)
- Never push to `main` directly
- Branch names must start with `claude/` for proper access
- Use conventional commit messages
- Keep commits focused and atomic

---

## Code Architecture

### Architecture Pattern
**Context API + Component Composition**

```
Entry Point (main.tsx)
    ↓
App Component (App.tsx)
    ├── ThemeProvider (dark mode management)
    ├── AuthProvider (authentication state)
    └── BrowserRouter (routing)
        └── Routes (lazy-loaded pages)
            ├── Public Routes (/, /login, /register)
            ├── Protected User Routes (/dashboard, /profile)
            └── Protected Admin Routes (/admin/*)
```

### Key Architectural Decisions

1. **No Redux/Zustand**: Uses Context API for simplicity
2. **Mock Data Layer**: Ready for API integration (see `client/src/data/mockData.ts`)
3. **Lazy Loading**: All pages lazy-loaded via React Router
4. **Code Splitting**: Manual chunks for vendors (see vite.config.ts:10-20)
5. **Type-Safe**: Strict TypeScript with comprehensive type definitions
6. **Responsive First**: Mobile-first design with Tailwind breakpoints

---

## Component Patterns

### UI Component Structure (shadcn/ui-inspired)

**Pattern**: Class Variance Authority (CVA) for variants

```typescript
// client/src/components/ui/button.tsx
const buttonVariants = cva(
  "inline-flex items-center justify-center...",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground...",
        destructive: "bg-destructive text-destructive-foreground...",
        outline: "border border-input...",
        // ... more variants
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 rounded-md px-3",
        lg: "h-11 rounded-md px-8",
        icon: "h-10 w-10",
      },
    },
  }
)
```

### Compound Components

**Pattern**: Composable card components

```typescript
// Usage example
<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
    <CardDescription>Description</CardDescription>
  </CardHeader>
  <CardContent>
    {/* Content */}
  </CardContent>
  <CardFooter>
    {/* Footer */}
  </CardFooter>
</Card>
```

### Layout Components

**MainLayout Pattern** (client/src/components/layout/MainLayout.tsx:24):
```typescript
export default function MainLayout({ children }: MainLayoutProps) {
  return (
    <div className="min-h-screen bg-background">
      <Navbar />
      <div className="flex">
        <Sidebar />
        <main className="flex-1 p-6 md:ml-64">
          {children}
        </main>
      </div>
    </div>
  )
}
```

### Protected Route Pattern

**File**: client/src/App.tsx

```typescript
// Example from codebase
<Route
  path="/admin"
  element={
    <ProtectedRoute requireAdmin={true}>
      <Suspense fallback={<div>Loading...</div>}>
        <AdminDashboard />
      </Suspense>
    </ProtectedRoute>
  }
/>
```

---

## State Management

### Context: AuthContext (client/src/contexts/AuthContext.tsx)

**Responsibilities**:
- User authentication state
- Login/logout/register functions
- Role-based access control
- localStorage persistence

**Provided Values**:
```typescript
interface AuthContextType {
  user: User | null;
  login: (email: string, password: string) => Promise<void>;
  register: (userData: RegisterData) => Promise<void>;
  logout: () => void;
  isAuthenticated: boolean;
  isAdmin: boolean;
}
```

**Usage**:
```typescript
import { useAuth } from '../contexts/AuthContext';

function MyComponent() {
  const { user, isAdmin, logout } = useAuth();
  // ...
}
```

### Context: ThemeContext (client/src/contexts/ThemeContext.tsx)

**Responsibilities**:
- Dark/light mode toggle
- localStorage persistence
- Document class manipulation

**Provided Values**:
```typescript
interface ThemeContextType {
  theme: 'light' | 'dark';
  toggleTheme: () => void;
}
```

**Implementation**:
- Adds/removes `dark` class on `document.documentElement`
- Persists to `localStorage` key: `theme`
- Defaults to `light` mode

---

## Routing & Navigation

### Route Structure

**Public Routes** (no authentication required):
- `/` - LandingPage
- `/login` - LoginPage
- `/register` - RegisterPage

**User Routes** (authentication required):
- `/dashboard` - UserDashboard
- `/profile` - UserProfile

**Admin Routes** (admin role required):
- `/admin` - AdminDashboard
- `/admin/users` - UserManagement (list)
- `/admin/users/:id` - UserDetail (detail view)

### Navigation Components

**Sidebar Menu Structure** (client/src/components/layout/Sidebar.tsx):

**Admin Menu**:
- Dashboard (5 groups with sub-items)
- Apps (Email, Chat, Calendar, eCommerce)
- Users (List, View, Edit)
- Pages (Account Settings, FAQ, etc.)
- Charts & Forms

**User Menu**:
- Dashboard
- Profile
- API Keys
- Billing
- Documentation

**Implementation Notes**:
- Active route highlighting with `useLocation()`
- Expandable/collapsible menu groups
- Badge support for notifications
- Lucide icons for visual clarity
- Responsive: hidden on mobile (`md:flex`)

---

## Styling Conventions

### Tailwind CSS Configuration

**File**: client/tailwind.config.js

**Dark Mode**: Class-based (`darkMode: ["class"]`)

**Color System**: Vuexy-inspired palette using CSS custom properties

```css
/* client/src/index.css */
:root {
  --primary: 258 90% 66%;           /* Purple #A78BFA */
  --secondary: 210 40% 96.1%;       /* Light blue-gray */
  --destructive: 0 84.2% 60.2%;     /* Red */
  --success: 142 71% 45%;           /* Green */
  --warning: 38 92% 50%;            /* Orange */
  --info: 199 89% 48%;              /* Blue */
  /* ... */
}

.dark {
  --primary: 258 90% 66%;
  --background: 222.2 84% 4.9%;     /* Dark navy */
  /* ... dark mode overrides */
}
```

### Styling Best Practices

1. **Use Tailwind Utilities First**: Avoid custom CSS unless necessary
2. **CSS Variables for Colors**: Use `bg-primary`, `text-foreground`, etc.
3. **Responsive Prefixes**: `md:`, `lg:`, `xl:` for breakpoints
4. **cn() Utility**: Use for conditional classes (client/src/lib/utils.ts)

```typescript
import { cn } from "@/lib/utils"

<div className={cn(
  "base-classes",
  isActive && "active-classes",
  className
)} />
```

5. **Component Variants**: Use CVA for variant-based styling

---

## Type System

### Core Types (client/src/types/index.ts)

```typescript
export type UserRole = 'admin' | 'user';

export type UserStatus = 'active' | 'suspended' | 'inactive';

export type SubscriptionPlan = 'free' | 'basic' | 'pro' | 'enterprise';

export interface User {
  id: string;
  name: string;
  email: string;
  role: UserRole;
  status: UserStatus;
  avatar?: string;
  credits: number;
  apiKey: string;
  plan: SubscriptionPlan;
  createdAt: Date;
  lastActive: Date;
}

export interface ApiCall {
  id: string;
  userId: string;
  endpoint: string;
  method: string;
  status: number;
  timestamp: Date;
  duration: number;
}

export interface KPIMetric {
  label: string;
  value: string;
  change: string;
  trend: 'up' | 'down';
  icon: string;
}

// ... more types
```

### TypeScript Configuration

**File**: client/tsconfig.app.json

**Key Settings**:
- Target: `ES2022`
- Module: `ESNext`
- Strict: `true`
- JSX: `react-jsx`
- Unused locals/parameters: Error
- No unchecked side effect imports: Enabled

**Path Aliases**: None currently (consider adding `@/` alias for cleaner imports)

---

## Common Development Tasks

### Adding a New Page

1. Create page component in appropriate directory:
   ```typescript
   // client/src/pages/user/NewFeature.tsx
   export default function NewFeature() {
     return (
       <MainLayout>
         <div className="max-w-7xl mx-auto">
           <h1 className="text-3xl font-bold mb-6">New Feature</h1>
           {/* Content */}
         </div>
       </MainLayout>
     )
   }
   ```

2. Add route in `client/src/App.tsx`:
   ```typescript
   const NewFeature = lazy(() => import('./pages/user/NewFeature'))

   // In Routes:
   <Route
     path="/new-feature"
     element={
       <ProtectedRoute>
         <Suspense fallback={<div>Loading...</div>}>
           <NewFeature />
         </Suspense>
       </ProtectedRoute>
     }
   />
   ```

3. Add navigation link in Sidebar (if needed)

### Adding a New UI Component

1. Create component in `client/src/components/ui/`:
   ```typescript
   // client/src/components/ui/new-component.tsx
   import * as React from "react"
   import { cn } from "@/lib/utils"

   export interface NewComponentProps
     extends React.HTMLAttributes<HTMLDivElement> {}

   const NewComponent = React.forwardRef<HTMLDivElement, NewComponentProps>(
     ({ className, ...props }, ref) => {
       return (
         <div
           ref={ref}
           className={cn("base-styles", className)}
           {...props}
         />
       )
     }
   )
   NewComponent.displayName = "NewComponent"

   export { NewComponent }
   ```

2. Export from index (if creating barrel file)
3. Use in pages/components

### Integrating Real API

**Current State**: Mock data in `client/src/data/mockData.ts`

**To Integrate**:

1. Create API service (`client/src/services/api.ts`):
   ```typescript
   const API_BASE_URL = import.meta.env.VITE_API_URL || 'http://localhost:3000/api'

   export const apiService = {
     async get<T>(endpoint: string): Promise<T> {
       const response = await fetch(`${API_BASE_URL}${endpoint}`)
       if (!response.ok) throw new Error('API Error')
       return response.json()
     },

     async post<T>(endpoint: string, data: any): Promise<T> {
       const response = await fetch(`${API_BASE_URL}${endpoint}`, {
         method: 'POST',
         headers: { 'Content-Type': 'application/json' },
         body: JSON.stringify(data)
       })
       if (!response.ok) throw new Error('API Error')
       return response.json()
     }
   }
   ```

2. Update AuthContext to use real API:
   ```typescript
   const login = async (email: string, password: string) => {
     const user = await apiService.post('/auth/login', { email, password })
     setUser(user)
     localStorage.setItem('user', JSON.stringify(user))
   }
   ```

3. Add `.env` file:
   ```
   VITE_API_URL=https://api.example.com
   ```

### Adding a Chart

Using Recharts library:

```typescript
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts'

<ResponsiveContainer width="100%" height={300}>
  <LineChart data={chartData}>
    <CartesianGrid strokeDasharray="3 3" />
    <XAxis dataKey="name" />
    <YAxis />
    <Tooltip />
    <Line type="monotone" dataKey="value" stroke="#A78BFA" strokeWidth={2} />
  </LineChart>
</ResponsiveContainer>
```

**Note**: Charts are code-split into separate chunk (see vite.config.ts:16)

---

## Build & Optimization

### Vite Configuration (client/vite.config.ts)

**Manual Code Splitting**:
```javascript
manualChunks: {
  'react-vendor': ['react', 'react-dom'],      // ~140KB gzipped
  'router': ['react-router-dom'],              // ~50KB
  'charts': ['recharts'],                      // ~150KB+
  'icons': ['lucide-react'],                   // ~50KB
  'date-utils': ['date-fns'],                  // ~30KB
}
```

**Chunk Size Limit**: 1000 KB (increased from default 500 KB)

### Build Optimization Tips

1. **Lazy Load Pages**: Already implemented via `React.lazy()`
2. **Tree Shaking**: Vite handles automatically
3. **Image Optimization**: Place in `public/` folder
4. **Font Optimization**: Use system fonts or Google Fonts
5. **Bundle Analysis**: Run `npm run build` and check output sizes

### Performance Considerations

- **Initial Load**: ~500KB total (with code splitting)
- **Lazy Routes**: Load on demand
- **Dark Mode**: No flash (reads localStorage before render)
- **Charts**: Heavy library, code-split separately

---

## Important Notes for AI Assistants

### Code Style Preferences

1. **TypeScript**: Always use TypeScript, not JavaScript
2. **Functional Components**: Use function declarations, not arrow functions for components
3. **Hooks**: Prefer composition of built-in hooks over custom hooks
4. **Props**: Use TypeScript interfaces for props, extend HTML attributes when appropriate
5. **ForwardRef**: Use for UI components that need DOM access
6. **cn() Utility**: Always use `cn()` for combining classNames
7. **Comments**: Add JSDoc comments for complex functions

### Don't Break These Patterns

1. **Don't** add Redux/Zustand/MobX - use Context API
2. **Don't** create custom CSS files - use Tailwind utilities
3. **Don't** install UI libraries (Material-UI, Ant Design) - use existing shadcn/ui components
4. **Don't** bypass ProtectedRoute - always wrap protected pages
5. **Don't** hardcode colors - use CSS custom properties
6. **Don't** create barrel exports (`index.ts`) unless necessary
7. **Don't** use inline styles - use Tailwind classes

### When Adding New Features

1. **Check existing patterns**: Look for similar implementations first
2. **Maintain consistency**: Follow existing naming conventions
3. **Type safety**: Add/update types in `types/index.ts`
4. **Responsive design**: Always test mobile (use Tailwind breakpoints)
5. **Dark mode**: Ensure new components work in both themes
6. **Accessibility**: Use semantic HTML and ARIA attributes
7. **Performance**: Consider lazy loading for heavy components

### Mock Data Notes

- **Location**: `client/src/data/mockData.ts`
- **Users**: 15 mock users (admin + users)
- **API Calls**: 100 mock API call records
- **Auth**: Mock authentication in AuthContext
- **Ready for API**: Can swap with real API service

### Common Pitfalls to Avoid

1. **Path Imports**: No path alias configured - use relative imports
2. **Environment Variables**: Must be prefixed with `VITE_`
3. **CSS Variables**: Use `hsl(var(--color))` format in Tailwind config
4. **Dark Mode**: Must toggle `dark` class on `document.documentElement`
5. **Protected Routes**: Check both `isAuthenticated` and role
6. **localStorage**: Always JSON.stringify/parse objects

### Testing

**Current Status**: No testing framework configured

**To Add Testing**:
```bash
npm install -D vitest @testing-library/react @testing-library/jest-dom jsdom
```

Add to `package.json`:
```json
"scripts": {
  "test": "vitest",
  "test:ui": "vitest --ui"
}
```

### Recommended Improvements

1. **Path Alias**: Add `@/` alias for cleaner imports
2. **API Service Layer**: Create proper API service abstraction
3. **Error Boundaries**: Add React error boundaries
4. **Loading States**: Standardize loading UI
5. **Toast Notifications**: Add toast library (e.g., sonner)
6. **Form Validation**: Add form library (e.g., react-hook-form + zod)
7. **Testing**: Add Vitest + Testing Library
8. **Storybook**: Add for component documentation
9. **Environment Config**: Add development/staging/production configs

---

## Quick Reference

### File Locations Cheat Sheet

| What | Where |
|------|-------|
| Add new page | `client/src/pages/[public\|admin\|user]/` |
| Add UI component | `client/src/components/ui/` |
| Add layout component | `client/src/components/layout/` |
| Add route | `client/src/App.tsx` |
| Add type | `client/src/types/index.ts` |
| Add utility | `client/src/lib/utils.ts` |
| Mock data | `client/src/data/mockData.ts` |
| Theme colors | `client/src/index.css` |
| Config | `client/vite.config.ts`, `client/tailwind.config.js` |

### Command Cheat Sheet

```bash
# Development
cd client && npm run dev              # Start dev server
npm run build                         # Production build
npm run preview                       # Preview build
npm run lint                          # Run linter

# Git
git checkout -b claude/feature-name-sessionid  # Create branch
git add .                             # Stage changes
git commit -m "feat: Description"     # Commit
git push -u origin branch-name        # Push to remote
```

### Color Reference

```
Primary: Purple (#A78BFA)
Secondary: Light blue-gray
Success: Green
Warning: Orange
Destructive: Red
Info: Blue
```

---

## Changelog

| Date | Change |
|------|--------|
| 2025-11-15 | Initial CLAUDE.md creation |
| 2025-11-05 | Vuexy UI improvements implemented |
| 2025-11-05 | Bundle optimization with code splitting |
| 2025-11-05 | Complete platform UI implementation |

---

## Support & Resources

- **Repository**: https://github.com/lct1407/APIs-for-rent
- **Issues**: GitHub Issues
- **Documentation**: README.md (user-facing), CLAUDE.md (AI assistant)

---

**Last Updated**: 2025-11-15
**Maintained By**: Claude Code AI Assistant
**Version**: 1.0.0
