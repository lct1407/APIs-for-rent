---
description: Generate beautiful, production-ready React components
---

Generate a stunning, fully-functional React component with modern design.

When invoked, ask the user what component they need, then create it following these principles:

## Component Generation Process

### 1. Understand Requirements

Ask clarifying questions:
- What is the component's purpose?
- What data will it display?
- What interactions does it need?
- Should it have variants (sizes, colors)?
- Where will it be used (page, modal, sidebar)?

### 2. Design the Component

Create a component that includes:

**Visual Design**:
- Beautiful gradients or solid colors
- Proper spacing and padding
- Smooth shadows
- Rounded corners
- Hover/focus states

**Functionality**:
- All necessary props
- TypeScript types
- Event handlers
- State management (if needed)

**Accessibility**:
- ARIA labels
- Keyboard navigation
- Focus indicators
- Screen reader support

**Responsiveness**:
- Mobile-first design
- Breakpoint adaptations
- Touch-friendly on mobile

**Dark Mode**:
- Full dark mode support
- Proper contrast

### 3. Component Template Structure

```tsx
import React from 'react'
import { cn } from '@/lib/utils'
import { Icon } from 'lucide-react'

// TypeScript interface
interface ComponentNameProps {
  // Props with descriptions
  variant?: 'default' | 'primary' | 'secondary'
  size?: 'sm' | 'md' | 'lg'
  className?: string
  children?: React.ReactNode
  onClick?: () => void
  // ... other props
}

// Component with forwardRef if needed
export const ComponentName = React.forwardRef<
  HTMLDivElement,
  ComponentNameProps
>(({
  variant = 'default',
  size = 'md',
  className,
  children,
  onClick,
  ...props
}, ref) => {
  return (
    <div
      ref={ref}
      className={cn(
        // Base styles
        "relative transition-all duration-200",

        // Variant styles
        variant === 'default' && "bg-white dark:bg-gray-900",
        variant === 'primary' && "bg-purple-600 text-white",
        variant === 'secondary' && "bg-gray-100 dark:bg-gray-800",

        // Size styles
        size === 'sm' && "p-2 text-sm",
        size === 'md' && "p-4 text-base",
        size === 'lg' && "p-6 text-lg",

        // Custom className
        className
      )}
      onClick={onClick}
      {...props}
    >
      {children}
    </div>
  )
})

ComponentName.displayName = 'ComponentName'
```

### 4. Common Component Patterns

**Stat Card**:
```tsx
interface StatCardProps {
  title: string
  value: string | number
  change?: number
  icon: React.ReactNode
  trend?: 'up' | 'down'
  color?: 'blue' | 'green' | 'purple' | 'orange'
}

export function StatCard({
  title,
  value,
  change,
  icon,
  trend = 'up',
  color = 'blue'
}: StatCardProps) {
  // Beautiful gradient card implementation
}
```

**Modal/Dialog**:
```tsx
interface ModalProps {
  isOpen: boolean
  onClose: () => void
  title: string
  children: React.ReactNode
  size?: 'sm' | 'md' | 'lg' | 'xl'
}

export function Modal({ isOpen, onClose, title, children, size = 'md' }: ModalProps) {
  // Beautiful modal with backdrop, animations, and focus trap
}
```

**Data Table**:
```tsx
interface TableProps<T> {
  data: T[]
  columns: Column<T>[]
  onRowClick?: (row: T) => void
  loading?: boolean
}

export function Table<T>({ data, columns, onRowClick, loading }: TableProps<T>) {
  // Beautiful table with sorting, pagination, and responsive design
}
```

**Feature Card**:
```tsx
interface FeatureCardProps {
  icon: React.ReactNode
  title: string
  description: string
  gradient?: boolean
}

export function FeatureCard({ icon, title, description, gradient }: FeatureCardProps) {
  // Eye-catching feature card with hover effects
}
```

### 5. Add Advanced Features

**Animations**:
```tsx
// Add smooth animations
className={cn(
  "transform transition-all duration-300",
  "hover:scale-105 hover:shadow-xl",
  "active:scale-95"
)}
```

**Loading States**:
```tsx
{loading ? (
  <div className="animate-pulse">
    <div className="h-4 bg-gray-200 dark:bg-gray-700 rounded"></div>
  </div>
) : (
  <div>{content}</div>
)}
```

**Error States**:
```tsx
{error && (
  <div className="rounded-lg bg-red-50 dark:bg-red-900/10 border border-red-200 dark:border-red-800 p-4">
    <div className="flex items-center gap-2 text-red-600 dark:text-red-400">
      <AlertCircle className="w-5 h-5" />
      <span className="font-medium">{error}</span>
    </div>
  </div>
)}
```

**Empty States**:
```tsx
{data.length === 0 && (
  <div className="text-center py-12">
    <div className="w-16 h-16 mx-auto mb-4 rounded-full bg-gray-100 dark:bg-gray-800 flex items-center justify-center">
      <Icon className="w-8 h-8 text-gray-400" />
    </div>
    <h3 className="text-lg font-semibold text-gray-900 dark:text-white mb-2">
      No items found
    </h3>
    <p className="text-gray-600 dark:text-gray-400">
      Get started by creating your first item.
    </p>
  </div>
)}
```

### 6. Include Usage Example

Always provide a usage example:

```tsx
// Example usage
import { ComponentName } from '@/components/ComponentName'

function MyPage() {
  return (
    <ComponentName
      variant="primary"
      size="lg"
      onClick={() => console.log('clicked')}
    >
      Beautiful Content
    </ComponentName>
  )
}
```

### 7. Add Storybook Documentation (Optional)

```tsx
// ComponentName.stories.tsx
import type { Meta, StoryObj } from '@storybook/react'
import { ComponentName } from './ComponentName'

const meta: Meta<typeof ComponentName> = {
  title: 'Components/ComponentName',
  component: ComponentName,
  tags: ['autodocs'],
}

export default meta
type Story = StoryObj<typeof ComponentName>

export const Default: Story = {
  args: {
    variant: 'default',
    children: 'Default Component',
  },
}

export const Primary: Story = {
  args: {
    variant: 'primary',
    children: 'Primary Component',
  },
}
```

## Output

When generating a component, provide:

1. **Full Component Code**: Complete, production-ready TypeScript/React code
2. **File Location**: Where to save it (e.g., `client/src/components/ui/ComponentName.tsx`)
3. **Dependencies**: Any new packages needed
4. **Usage Example**: How to use the component
5. **Props Documentation**: Description of all props
6. **Variants**: All available variants/sizes
7. **Accessibility Notes**: How it meets a11y standards
8. **Responsive Behavior**: How it adapts to screen sizes
9. **Dark Mode**: How it looks in dark mode
10. **Customization**: How to customize/extend it

## Component Categories

**UI Components**:
- Buttons, Inputs, Cards, Badges, Avatars
- Dropdowns, Modals, Tooltips, Popovers
- Tables, Lists, Grids

**Layout Components**:
- Containers, Sections, Dividers
- Navigation, Breadcrumbs, Pagination
- Sidebars, Headers, Footers

**Data Display**:
- Charts, Graphs, Stats Cards
- Tables, Lists, Grids
- Timeline, Progress, Meters

**Feedback**:
- Alerts, Toasts, Notifications
- Loading Spinners, Skeletons
- Error States, Empty States

**Forms**:
- Text Inputs, Textareas, Selects
- Checkboxes, Radios, Switches
- File Uploads, Date Pickers

**Marketing**:
- Hero Sections, Features, Testimonials
- Pricing Cards, CTAs, Footers
- Stats, Logos, Partners

Ask me what component you'd like to generate!
