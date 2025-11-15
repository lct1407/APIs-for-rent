# UI/UX Design Skill

**Description**: Create beautiful, creative, and user-friendly interfaces with modern design principles

**When to use**: When designing new components, improving UI aesthetics, ensuring accessibility, or creating delightful user experiences

## Instructions

When invoked, you should create visually stunning and highly usable interfaces by following these principles:

## 1. Design System Foundation

### Understanding the Current Design System

First, analyze the existing design system:

```bash
# Review current theme configuration
cat client/src/index.css           # Check CSS variables and Tailwind config
cat client/tailwind.config.js      # Review Tailwind customization
cat client/src/components/ui/*.tsx # Study component patterns
```

**Current Design Elements**:
- **Color Palette**: Vuexy-inspired (Primary: Purple #A78BFA)
- **Component Library**: shadcn/ui patterns
- **CSS Framework**: Tailwind CSS utility-first
- **Typography**: System fonts with careful hierarchy
- **Dark Mode**: Class-based with smooth transitions

### Enhance the Design System

Create or improve the design system:

```css
/* Enhanced color palette with semantic naming */
:root {
  /* Brand Colors */
  --brand-primary: 258 90% 66%;        /* Purple */
  --brand-secondary: 210 40% 96.1%;    /* Light blue-gray */

  /* Semantic Colors */
  --success: 142 71% 45%;              /* Green */
  --warning: 38 92% 50%;               /* Amber */
  --error: 0 84.2% 60.2%;              /* Red */
  --info: 199 89% 48%;                 /* Blue */

  /* Neutral Palette (for sophisticated grays) */
  --neutral-50: 210 20% 98%;
  --neutral-100: 210 20% 95%;
  --neutral-200: 210 20% 90%;
  --neutral-300: 210 20% 80%;
  --neutral-400: 210 20% 60%;
  --neutral-500: 210 20% 45%;
  --neutral-600: 210 20% 35%;
  --neutral-700: 210 20% 25%;
  --neutral-800: 210 20% 15%;
  --neutral-900: 210 20% 10%;

  /* Accent Colors (for visual interest) */
  --accent-pink: 330 85% 65%;
  --accent-orange: 25 95% 60%;
  --accent-teal: 180 75% 50%;
  --accent-indigo: 245 75% 65%;

  /* Gradients */
  --gradient-primary: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  --gradient-success: linear-gradient(135deg, #0BA360 0%, #3CBA92 100%);
  --gradient-sunset: linear-gradient(135deg, #FA709A 0%, #FEE140 100%);
  --gradient-ocean: linear-gradient(135deg, #667eea 0%, #64b3f4 100%);

  /* Spacing Scale (8px base) */
  --space-xs: 0.25rem;    /* 4px */
  --space-sm: 0.5rem;     /* 8px */
  --space-md: 1rem;       /* 16px */
  --space-lg: 1.5rem;     /* 24px */
  --space-xl: 2rem;       /* 32px */
  --space-2xl: 3rem;      /* 48px */
  --space-3xl: 4rem;      /* 64px */

  /* Border Radius */
  --radius-sm: 0.375rem;  /* 6px */
  --radius-md: 0.5rem;    /* 8px */
  --radius-lg: 0.75rem;   /* 12px */
  --radius-xl: 1rem;      /* 16px */
  --radius-full: 9999px;

  /* Shadows (elevation) */
  --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);
  --shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
  --shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.05);

  /* Transitions */
  --transition-fast: 150ms cubic-bezier(0.4, 0, 0.2, 1);
  --transition-base: 200ms cubic-bezier(0.4, 0, 0.2, 1);
  --transition-slow: 300ms cubic-bezier(0.4, 0, 0.2, 1);
  --transition-bounce: 500ms cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
```

## 2. Modern UI Patterns & Trends

### Glassmorphism (Frosted Glass Effect)

Create stunning glass-like components:

```tsx
// Glassmorphism Card
<div className="relative backdrop-blur-xl bg-white/10 dark:bg-black/10
                border border-white/20 dark:border-white/10
                rounded-2xl p-6 shadow-2xl
                before:absolute before:inset-0 before:rounded-2xl
                before:bg-gradient-to-br before:from-white/20 before:to-transparent
                before:opacity-50">
  <div className="relative z-10">
    {/* Content with high contrast for readability */}
    <h3 className="text-xl font-bold text-gray-900 dark:text-white">
      Glassmorphism Card
    </h3>
    <p className="text-gray-700 dark:text-gray-300">
      Beautiful frosted glass effect
    </p>
  </div>
</div>
```

### Neumorphism (Soft UI)

Subtle, extruded UI elements:

```tsx
// Neumorphic Button
<button className="px-6 py-3 rounded-xl font-medium
                   bg-gray-100 dark:bg-gray-800
                   shadow-[5px_5px_10px_#d1d1d1,-5px_-5px_10px_#ffffff]
                   dark:shadow-[5px_5px_10px_#1a1a1a,-5px_-5px_10px_#2a2a2a]
                   hover:shadow-[inset_5px_5px_10px_#d1d1d1,inset_-5px_-5px_10px_#ffffff]
                   dark:hover:shadow-[inset_5px_5px_10px_#1a1a1a,inset_-5px_-5px_10px_#2a2a2a]
                   transition-all duration-200">
  Neumorphic Button
</button>
```

### Gradient Accents

Eye-catching gradient elements:

```tsx
// Gradient Card with Glow
<div className="relative group">
  {/* Animated gradient glow */}
  <div className="absolute -inset-0.5 bg-gradient-to-r from-pink-600 to-purple-600
                  rounded-lg blur opacity-60 group-hover:opacity-100
                  transition duration-1000 group-hover:duration-200
                  animate-tilt"></div>

  {/* Card content */}
  <div className="relative bg-white dark:bg-gray-900 rounded-lg p-6">
    <div className="flex items-center space-x-4">
      <div className="w-12 h-12 rounded-full bg-gradient-to-br
                      from-pink-500 to-purple-600
                      flex items-center justify-center">
        <Icon className="text-white" />
      </div>
      <div>
        <h3 className="font-bold text-gray-900 dark:text-white">
          Premium Feature
        </h3>
        <p className="text-sm text-gray-600 dark:text-gray-400">
          With gradient accent
        </p>
      </div>
    </div>
  </div>
</div>
```

### Micro-interactions & Animations

Delightful user feedback:

```tsx
// Animated Success Button
<button className="group relative px-6 py-3 rounded-lg
                   bg-gradient-to-r from-green-500 to-emerald-600
                   text-white font-medium
                   overflow-hidden
                   transition-all duration-300
                   hover:shadow-lg hover:scale-105
                   active:scale-95">

  {/* Ripple effect on hover */}
  <span className="absolute inset-0 w-0 h-0 m-auto
                   bg-white/30 rounded-full
                   group-hover:w-full group-hover:h-full
                   transition-all duration-500"></span>

  {/* Button content */}
  <span className="relative flex items-center justify-center gap-2">
    <CheckIcon className="w-5 h-5
                         group-hover:rotate-12
                         transition-transform duration-300" />
    <span>Complete</span>
  </span>
</button>
```

### Skeleton Loading (Better than spinners)

```tsx
// Skeleton Card Loader
<div className="animate-pulse">
  <div className="flex space-x-4">
    <div className="rounded-full bg-gray-200 dark:bg-gray-700 h-12 w-12"></div>
    <div className="flex-1 space-y-3 py-1">
      <div className="h-4 bg-gray-200 dark:bg-gray-700 rounded w-3/4"></div>
      <div className="space-y-2">
        <div className="h-3 bg-gray-200 dark:bg-gray-700 rounded"></div>
        <div className="h-3 bg-gray-200 dark:bg-gray-700 rounded w-5/6"></div>
      </div>
    </div>
  </div>
</div>
```

## 3. Advanced Component Patterns

### Hero Sections

```tsx
// Modern Hero with Gradient Background
<section className="relative min-h-screen flex items-center justify-center
                    overflow-hidden bg-gradient-to-br from-purple-600 via-blue-600 to-teal-500">

  {/* Animated background shapes */}
  <div className="absolute inset-0 overflow-hidden">
    <div className="absolute -top-40 -right-40 w-80 h-80
                    bg-pink-500/30 rounded-full blur-3xl
                    animate-blob"></div>
    <div className="absolute -bottom-40 -left-40 w-80 h-80
                    bg-yellow-500/30 rounded-full blur-3xl
                    animate-blob animation-delay-2000"></div>
    <div className="absolute top-40 left-40 w-80 h-80
                    bg-blue-500/30 rounded-full blur-3xl
                    animate-blob animation-delay-4000"></div>
  </div>

  {/* Content */}
  <div className="relative z-10 text-center px-6">
    <h1 className="text-5xl md:text-7xl font-bold text-white mb-6
                   bg-clip-text text-transparent
                   bg-gradient-to-r from-white to-white/80">
      Build Amazing APIs
    </h1>
    <p className="text-xl md:text-2xl text-white/90 mb-8 max-w-2xl mx-auto">
      The most powerful API rental platform for developers
    </p>
    <div className="flex gap-4 justify-center flex-wrap">
      <button className="px-8 py-4 bg-white text-purple-600 rounded-full
                         font-semibold shadow-xl hover:shadow-2xl
                         transform hover:scale-105 transition-all">
        Get Started
      </button>
      <button className="px-8 py-4 bg-white/10 backdrop-blur-lg text-white
                         border border-white/20 rounded-full font-semibold
                         hover:bg-white/20 transition-all">
        Learn More
      </button>
    </div>
  </div>
</section>
```

### Pricing Cards

```tsx
// Premium Pricing Card
<div className="relative group">
  {/* Popular badge */}
  <div className="absolute -top-5 left-1/2 -translate-x-1/2 z-10">
    <span className="bg-gradient-to-r from-purple-600 to-pink-600
                     text-white px-6 py-2 rounded-full text-sm font-bold
                     shadow-lg">
      MOST POPULAR
    </span>
  </div>

  <div className="relative bg-white dark:bg-gray-900 rounded-2xl
                  border-2 border-purple-500 p-8
                  shadow-xl hover:shadow-2xl transition-all duration-300
                  transform hover:-translate-y-2">

    {/* Gradient overlay */}
    <div className="absolute inset-0 bg-gradient-to-br from-purple-500/5 to-pink-500/5
                    rounded-2xl opacity-0 group-hover:opacity-100 transition-opacity"></div>

    <div className="relative">
      {/* Plan name */}
      <h3 className="text-2xl font-bold text-gray-900 dark:text-white mb-2">
        Pro Plan
      </h3>

      {/* Price */}
      <div className="flex items-baseline mb-6">
        <span className="text-5xl font-bold bg-clip-text text-transparent
                       bg-gradient-to-r from-purple-600 to-pink-600">
          $49
        </span>
        <span className="text-gray-500 dark:text-gray-400 ml-2">/month</span>
      </div>

      {/* Features */}
      <ul className="space-y-4 mb-8">
        {features.map((feature, i) => (
          <li key={i} className="flex items-start">
            <CheckCircleIcon className="w-6 h-6 text-purple-600 mr-3 flex-shrink-0" />
            <span className="text-gray-700 dark:text-gray-300">{feature}</span>
          </li>
        ))}
      </ul>

      {/* CTA Button */}
      <button className="w-full py-4 bg-gradient-to-r from-purple-600 to-pink-600
                         text-white rounded-xl font-semibold
                         shadow-lg hover:shadow-xl
                         transform hover:scale-105 active:scale-95
                         transition-all duration-200">
        Choose Plan
      </button>
    </div>
  </div>
</div>
```

### Dashboard Cards with Stats

```tsx
// Beautiful Stat Card
<div className="relative overflow-hidden rounded-2xl
                bg-gradient-to-br from-blue-500 to-blue-600
                p-6 text-white
                shadow-lg hover:shadow-xl transition-shadow">

  {/* Background pattern */}
  <div className="absolute top-0 right-0 opacity-10">
    <svg className="w-32 h-32" viewBox="0 0 100 100">
      <circle cx="50" cy="50" r="40" fill="currentColor" />
    </svg>
  </div>

  <div className="relative">
    {/* Icon */}
    <div className="w-14 h-14 rounded-xl bg-white/20 backdrop-blur-sm
                    flex items-center justify-center mb-4">
      <ChartIcon className="w-8 h-8" />
    </div>

    {/* Value with animation */}
    <div className="text-4xl font-bold mb-2
                    animate-[counter_2s_ease-out_forwards]">
      12,458
    </div>

    {/* Label */}
    <div className="text-blue-100 font-medium mb-3">
      Total API Calls
    </div>

    {/* Trend indicator */}
    <div className="flex items-center text-sm">
      <ArrowUpIcon className="w-4 h-4 mr-1" />
      <span className="font-semibold">23.5%</span>
      <span className="text-blue-100 ml-1">from last month</span>
    </div>
  </div>
</div>
```

## 4. Typography & Hierarchy

### Font Scale System

```tsx
// Typography components with perfect hierarchy
const Typography = {
  H1: ({ children }: { children: React.ReactNode }) => (
    <h1 className="text-5xl md:text-6xl lg:text-7xl font-bold
                   tracking-tight text-gray-900 dark:text-white
                   leading-tight">
      {children}
    </h1>
  ),

  H2: ({ children }: { children: React.ReactNode }) => (
    <h2 className="text-3xl md:text-4xl lg:text-5xl font-bold
                   text-gray-900 dark:text-white">
      {children}
    </h2>
  ),

  H3: ({ children }: { children: React.ReactNode }) => (
    <h3 className="text-2xl md:text-3xl font-semibold
                   text-gray-900 dark:text-white">
      {children}
    </h3>
  ),

  Body: ({ children }: { children: React.ReactNode }) => (
    <p className="text-base md:text-lg text-gray-700 dark:text-gray-300
                  leading-relaxed">
      {children}
    </p>
  ),

  Caption: ({ children }: { children: React.ReactNode }) => (
    <span className="text-sm text-gray-500 dark:text-gray-400">
      {children}
    </span>
  ),
}
```

## 5. Accessibility (a11y) Best Practices

### Keyboard Navigation

```tsx
// Fully accessible dropdown
<div className="relative" onKeyDown={handleKeyDown}>
  <button
    type="button"
    aria-haspopup="true"
    aria-expanded={isOpen}
    onClick={toggle}
    className="focus:outline-none focus:ring-2 focus:ring-purple-500 focus:ring-offset-2
               rounded-lg px-4 py-2"
  >
    Menu
  </button>

  {isOpen && (
    <div
      role="menu"
      aria-orientation="vertical"
      className="absolute mt-2 w-56 rounded-lg shadow-lg bg-white dark:bg-gray-800
                 ring-1 ring-black ring-opacity-5"
    >
      {items.map((item, index) => (
        <button
          key={item.id}
          role="menuitem"
          tabIndex={isOpen ? 0 : -1}
          onClick={() => handleSelect(item)}
          className="w-full text-left px-4 py-2 text-sm
                     hover:bg-gray-100 dark:hover:bg-gray-700
                     focus:outline-none focus:bg-gray-100 dark:focus:bg-gray-700"
        >
          {item.label}
        </button>
      ))}
    </div>
  )}
</div>
```

### Color Contrast

Always ensure WCAG AA compliance (4.5:1 for normal text, 3:1 for large text):

```tsx
// Good contrast examples
<button className="bg-purple-600 text-white">  {/* High contrast */}
  Accessible Button
</button>

<div className="bg-gray-100 text-gray-900">  {/* High contrast */}
  Readable content
</div>

// Avoid low contrast
❌ <button className="bg-gray-200 text-gray-300">  {/* Low contrast */}
```

### Screen Reader Support

```tsx
// Properly labeled interactive elements
<button
  aria-label="Close dialog"
  onClick={onClose}
  className="sr-only focus:not-sr-only"  // Hidden but accessible
>
  <XIcon className="w-6 h-6" />
  <span className="sr-only">Close</span>  // Screen reader only text
</button>

// Live regions for dynamic content
<div aria-live="polite" aria-atomic="true">
  {notification}
</div>
```

## 6. Responsive Design Strategies

### Mobile-First Approach

```tsx
// Mobile-first responsive card grid
<div className="grid grid-cols-1 gap-4
                sm:grid-cols-2 sm:gap-6
                lg:grid-cols-3 lg:gap-8
                xl:grid-cols-4">
  {cards.map(card => (
    <Card key={card.id} />
  ))}
</div>

// Responsive typography
<h1 className="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold">
  Responsive Heading
</h1>

// Responsive padding
<section className="px-4 py-8
                    sm:px-6 sm:py-12
                    lg:px-8 lg:py-16
                    xl:px-12 xl:py-20">
  {content}
</section>
```

### Container Queries (Modern approach)

```tsx
// Using Tailwind's container queries
<div className="@container">
  <div className="@md:flex @md:items-center @md:gap-6">
    <img className="@md:w-48" />
    <div className="@md:flex-1">
      <h2 className="@md:text-2xl">Title</h2>
      <p className="@md:text-base">Description</p>
    </div>
  </div>
</div>
```

## 7. Dark Mode Excellence

### Seamless Dark Mode

```tsx
// Components that look great in both modes
<div className="bg-white dark:bg-gray-900
                border border-gray-200 dark:border-gray-700
                rounded-xl p-6
                shadow-sm dark:shadow-gray-900/50">

  <h3 className="text-gray-900 dark:text-white font-bold mb-2">
    Title
  </h3>

  <p className="text-gray-600 dark:text-gray-400">
    Description that's readable in both modes
  </p>

  <button className="mt-4 px-4 py-2
                     bg-purple-600 hover:bg-purple-700
                     dark:bg-purple-500 dark:hover:bg-purple-600
                     text-white rounded-lg">
    Action
  </button>
</div>
```

### Dark Mode Toggle

```tsx
// Beautiful theme toggle
<button
  onClick={toggleTheme}
  className="relative w-14 h-8 rounded-full
             bg-gray-200 dark:bg-gray-700
             transition-colors duration-300"
  aria-label="Toggle theme"
>
  <span className="absolute left-1 top-1 w-6 h-6 rounded-full
                   bg-white dark:bg-gray-900
                   shadow-md
                   transform transition-transform duration-300
                   dark:translate-x-6
                   flex items-center justify-center">
    {theme === 'dark' ? (
      <MoonIcon className="w-4 h-4 text-purple-500" />
    ) : (
      <SunIcon className="w-4 h-4 text-yellow-500" />
    )}
  </span>
</button>
```

## 8. Form Design

### Beautiful Form Inputs

```tsx
// Modern floating label input
<div className="relative">
  <input
    type="text"
    id="email"
    value={value}
    onChange={onChange}
    placeholder=" "
    className="peer w-full px-4 pt-6 pb-2
               border-2 border-gray-200 dark:border-gray-700
               rounded-xl
               focus:border-purple-500 focus:ring-2 focus:ring-purple-500/20
               bg-white dark:bg-gray-900
               text-gray-900 dark:text-white
               transition-all duration-200
               placeholder-transparent"
  />
  <label
    htmlFor="email"
    className="absolute left-4 top-2
               text-xs text-gray-500 dark:text-gray-400
               transition-all duration-200
               peer-placeholder-shown:top-4 peer-placeholder-shown:text-base
               peer-focus:top-2 peer-focus:text-xs peer-focus:text-purple-600"
  >
    Email Address
  </label>
</div>
```

### Form Validation Feedback

```tsx
// Input with validation states
<div className="space-y-2">
  <input
    type="password"
    className={cn(
      "w-full px-4 py-3 rounded-xl border-2 transition-all",
      error && "border-red-500 bg-red-50 dark:bg-red-900/10",
      success && "border-green-500 bg-green-50 dark:bg-green-900/10",
      !error && !success && "border-gray-200 dark:border-gray-700"
    )}
  />

  {error && (
    <div className="flex items-center gap-2 text-red-600 dark:text-red-400 text-sm">
      <AlertCircleIcon className="w-4 h-4" />
      <span>{error}</span>
    </div>
  )}

  {success && (
    <div className="flex items-center gap-2 text-green-600 dark:text-green-400 text-sm">
      <CheckCircleIcon className="w-4 h-4" />
      <span>Password is strong!</span>
    </div>
  )}
</div>
```

## 9. Animation Best Practices

### Custom Tailwind Animations

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      animation: {
        'fade-in': 'fadeIn 0.5s ease-in-out',
        'slide-up': 'slideUp 0.5s ease-out',
        'slide-down': 'slideDown 0.5s ease-out',
        'scale-in': 'scaleIn 0.3s ease-out',
        'blob': 'blob 7s infinite',
        'tilt': 'tilt 10s infinite linear',
        'shimmer': 'shimmer 2s linear infinite',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { transform: 'translateY(20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
        slideDown: {
          '0%': { transform: 'translateY(-20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
        scaleIn: {
          '0%': { transform: 'scale(0.9)', opacity: '0' },
          '100%': { transform: 'scale(1)', opacity: '1' },
        },
        blob: {
          '0%, 100%': { transform: 'translate(0, 0) scale(1)' },
          '33%': { transform: 'translate(30px, -50px) scale(1.1)' },
          '66%': { transform: 'translate(-20px, 20px) scale(0.9)' },
        },
        tilt: {
          '0%, 50%, 100%': { transform: 'rotate(0deg)' },
          '25%': { transform: 'rotate(1deg)' },
          '75%': { transform: 'rotate(-1deg)' },
        },
        shimmer: {
          '0%': { backgroundPosition: '-1000px 0' },
          '100%': { backgroundPosition: '1000px 0' },
        },
      },
    },
  },
}
```

## 10. Creative Component Ideas

### Notification Toast

```tsx
// Beautiful toast notification
<div className="fixed bottom-4 right-4 z-50
                animate-slide-up">
  <div className="flex items-center gap-4
                  bg-white dark:bg-gray-900
                  border-l-4 border-green-500
                  rounded-lg shadow-2xl p-4
                  min-w-[300px] max-w-md">

    {/* Icon with animated background */}
    <div className="w-10 h-10 rounded-full
                    bg-green-100 dark:bg-green-900/30
                    flex items-center justify-center
                    animate-scale-in">
      <CheckCircleIcon className="w-6 h-6 text-green-600 dark:text-green-400" />
    </div>

    {/* Content */}
    <div className="flex-1">
      <h4 className="font-semibold text-gray-900 dark:text-white">
        Success!
      </h4>
      <p className="text-sm text-gray-600 dark:text-gray-400">
        Your changes have been saved.
      </p>
    </div>

    {/* Close button */}
    <button
      onClick={onClose}
      className="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200
                 transition-colors"
    >
      <XIcon className="w-5 h-5" />
    </button>
  </div>
</div>
```

### Progress Indicator

```tsx
// Animated progress bar
<div className="space-y-2">
  <div className="flex justify-between text-sm">
    <span className="font-medium text-gray-700 dark:text-gray-300">
      Upload Progress
    </span>
    <span className="text-purple-600 dark:text-purple-400 font-semibold">
      {progress}%
    </span>
  </div>

  <div className="h-2 bg-gray-200 dark:bg-gray-700 rounded-full overflow-hidden">
    <div
      className="h-full bg-gradient-to-r from-purple-500 to-pink-500
                 rounded-full transition-all duration-500 ease-out
                 relative overflow-hidden"
      style={{ width: `${progress}%` }}
    >
      {/* Shimmer effect */}
      <div className="absolute inset-0
                      bg-gradient-to-r from-transparent via-white/30 to-transparent
                      animate-shimmer"></div>
    </div>
  </div>
</div>
```

## Output

When using this skill, provide:

1. **Component Code**: Complete, copy-paste ready React/TypeScript components
2. **Styling Details**: Tailwind classes with explanations
3. **Accessibility Notes**: How the component meets a11y standards
4. **Responsive Behavior**: How it adapts to different screen sizes
5. **Dark Mode Support**: How it looks in both light and dark themes
6. **Animation Details**: Any transitions or animations used
7. **Usage Examples**: How to integrate the component
8. **Customization Options**: Props and variants available
9. **Best Practices**: Why certain design decisions were made
10. **Live Preview Suggestions**: Recommendations for testing

## Design Principles to Follow

1. **Less is More**: Clean, uncluttered interfaces
2. **Consistency**: Reuse patterns and components
3. **Hierarchy**: Clear visual hierarchy guides the eye
4. **Contrast**: Sufficient contrast for readability
5. **Whitespace**: Generous spacing improves clarity
6. **Feedback**: Immediate visual feedback for actions
7. **Forgiveness**: Easy to undo mistakes
8. **Accessibility**: Everyone can use the interface
9. **Performance**: Smooth, responsive interactions
10. **Delight**: Small touches that bring joy
