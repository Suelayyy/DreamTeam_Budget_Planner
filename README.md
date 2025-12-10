# BudgetBuddy - Budget Planner Application

## Overview

BudgetBuddy is a playful and visually engaging budget planning application designed to make personal finance management enjoyable. The application focuses on beautiful data visualization through animated charts and graphs, providing users with an intuitive way to track income, expenses, and budget allocations. Drawing inspiration from modern fintech apps like Mint and YNAB, it emphasizes clarity, instant visual feedback, and a friendly user experience.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React with TypeScript, using Vite as the build tool and development server.

**Routing**: Client-side routing implemented with Wouter, a lightweight alternative to React Router. The application currently has a single main route (Dashboard) with a 404 fallback page.

**State Management**: Component-level state using React hooks (useState, useMemo). No global state management library is currently implemented - data flows through props and local component state.

**UI Component Library**: shadcn/ui components built on Radix UI primitives, providing accessible and customizable UI elements. The design system uses the "new-york" style variant with custom theming.

**Styling Approach**: Tailwind CSS with custom design tokens defined in CSS variables. The application supports both light and dark themes with a comprehensive color system including primary, secondary, accent, and chart-specific colors.

**Data Visualization**: Recharts library for rendering interactive pie charts and bar charts with custom tooltips and animations.

**Animation Library**: Framer Motion for component animations, transitions, and visual effects throughout the interface.

**Form Handling**: React Hook Form with Zod validation schemas (infrastructure in place via @hookform/resolvers and drizzle-zod).

**Design Philosophy**: The application follows a "playful professionalism" approach with emphasis on visual hierarchy, gradient backgrounds, animated interactions, and clear data presentation. Typography uses DM Sans for headings/body and Inter for data labels.

### Backend Architecture

**Server Framework**: Express.js running on Node.js with TypeScript.

**Build Strategy**: Server code is bundled using esbuild with selective dependency bundling to optimize cold start times. Common server dependencies are bundled while others remain external.

**API Structure**: Routes are registered through a centralized `registerRoutes` function in `server/routes.ts`. API endpoints are prefixed with `/api`.

**Static File Serving**: Production builds serve the compiled Vite frontend from the `dist/public` directory with SPA fallback routing.

**Development Mode**: In development, Vite's middleware mode is used with HMR support over WebSocket at `/vite-hmr`. The index.html is dynamically reloaded with cache-busting query parameters.

**Logging**: Custom logging middleware captures request method, path, status code, response time, and JSON response bodies for API calls.

**Storage Abstraction**: An `IStorage` interface defines CRUD operations with a current in-memory implementation (`MemStorage`). This abstraction allows for future database integration without changing business logic.

### Data Storage Solutions

**Current Implementation**: In-memory storage using JavaScript Maps for user data. This is a temporary solution suitable for development but will require migration to persistent storage.

**Planned Database**: PostgreSQL via Neon serverless driver. The infrastructure is configured with Drizzle ORM for type-safe database operations and migrations.

**Schema Definition**: Database schema defined in `shared/schema.ts` using Drizzle's schema builder. Currently defines a `users` table with id, username, and password fields. Schema validation uses drizzle-zod for runtime type checking.

**ORM Configuration**: Drizzle is configured to use PostgreSQL dialect with migrations stored in the `./migrations` directory. The configuration requires a `DATABASE_URL` environment variable.

**Future Considerations**: The application will need additional tables for transactions, budget categories, and monthly data once backend implementation progresses beyond the current user authentication scaffold.

### Authentication and Authorization

**Authentication Library**: Passport.js with local strategy (dependencies installed but not yet implemented in codebase).

**Session Management**: Express-session with support for both memory store (memorystore) and PostgreSQL store (connect-pg-simple) backends.
**Current State**: Authentication routes and middleware are not yet implemented - the codebase shows a scaffold with user schema defined but no active authentication flow.

### External Dependencies

**UI Component System**: Radix UI primitives (@radix-ui/*) for accessible, unstyled component foundations including dialogs, dropdowns, tooltips, popovers, and form controls.

**Data Fetching**: TanStack Query (React Query) v5 for server state management, caching, and data synchronization. Custom query functions are configured in `lib/queryClient.ts` with infinite stale time and disabled refetching.

**Styling Utilities**: 
- Tailwind CSS for utility-first styling with PostCSS processing
- class-variance-authority (cva) for component variant management
- clsx and tailwind-merge for conditional class composition

**Charts and Visualization**: Recharts for declarative chart components built on D3.js primitives.

**Animation**: Framer Motion for component animations, transitions, and gesture handling.

**Date Handling**: date-fns for date manipulation and formatting operations.

**Form Validation**: Zod for schema validation with integration into React Hook Form and Drizzle ORM.

**Development Tools**:
- @replit/vite-plugin-runtime-error-modal for error overlays
- @replit/vite-plugin-cartographer for code mapping
- @replit/vite-plugin-dev-banner for development environment indicators

**Build and Bundling**:
- Vite for frontend builds and development server
- esbuild for server-side bundling with selective dependency inclusion
- tsx for TypeScript execution in development

**HTTP Client**: The application uses native fetch API with custom wrapper functions for API requests defined in `lib/queryClient.ts`.

**Icon Library**: Lucide React for consistent, customizable SVG icons throughout the interface.

**Carousel Component**: Embla Carousel React for touch-enabled, accessible carousels.
