# DreamRest - Sleep Monitor & Dream Journal

## Overview

DreamRest is a wellness-focused web application designed to help users track their sleep patterns, record dreams, and gain insights into their rest quality. The application combines sleep logging functionality with dream journaling, presenting data through intuitive visualizations and personalized health recommendations. Built with a calming, wellness-oriented design inspired by apps like Calm and Headspace, it prioritizes user comfort and ease of use while providing meaningful sleep analytics.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Build System**
- React 18 with TypeScript for type-safe component development
- Vite as the build tool and development server, providing fast hot module replacement
- Wouter for lightweight client-side routing (single-page application)

**UI Component Strategy**
- Shadcn/ui component library built on Radix UI primitives for accessible, customizable components
- Tailwind CSS for utility-first styling with custom design tokens
- Framer Motion for smooth, organic animations that enhance the wellness aesthetic
- Custom theming system with light/dark mode support via ThemeProvider context

**State Management**
- TanStack Query (React Query) for server state management, caching, and data synchronization
- Local React state for form inputs and UI interactions
- Context API for global application state (theme preferences)

**Design System**
- Typography: DM Sans/Inter for data readability, Playfair Display for headlines
- Color system: Custom HSL-based palette with CSS variables for theme switching
- Spacing: Tailwind's spacing scale (3, 4, 6, 8, 12, 16) for consistent layouts
- Rounded corners and generous whitespace to promote relaxation
- Responsive grid system: mobile-first with breakpoints at md (768px)

### Backend Architecture

**Server Framework**
- Express.js REST API server handling CRUD operations for sleep logs
- Custom Vite middleware integration for seamless development experience
- Logging middleware for request tracking and debugging

**API Design**
- RESTful endpoints following resource-based patterns:
  - `GET /api/sleep-logs` - Retrieve all logs (sorted by date descending)
  - `GET /api/sleep-logs/:id` - Retrieve single log
  - `POST /api/sleep-logs` - Create new log with validation
  - `DELETE /api/sleep-logs/:id` - Remove log
- JSON request/response format with standardized error handling
- Zod schema validation on incoming data to ensure type safety

**Data Storage Pattern**
- Abstract storage interface (IStorage) allowing flexible backend implementations
- In-memory storage (MemStorage) for development/demo purposes
- Database-ready architecture via Drizzle ORM configuration for PostgreSQL migration
- Storage layer handles data sorting, filtering, and UUID generation

### Data Model

**Sleep Log Schema**
- Primary fields: date, bedtime, wake time, quality (1-10 scale)
- Lifestyle factors: exercise flag, caffeine intake, stress level (1-5)
- Dream tracking: optional text entry and tag array
- Metadata: location, creation timestamp, unique ID
- Validation: Zod schemas ensure data integrity before persistence

**User Schema**
- Defined but not actively used (authentication not implemented)
- Prepared for future user-specific data isolation

### External Dependencies

**Database & ORM**
- Drizzle ORM configured for PostgreSQL via `@neondatabase/serverless`
- Schema definitions use Drizzle's type-safe column builders
- Migration system via Drizzle Kit (`db:push` script)
- Connection pooling through Neon's serverless driver

**Third-Party UI Libraries**
- Recharts for data visualization (line charts, bar charts for sleep patterns)
- Radix UI primitives for 20+ accessible component patterns (dialogs, popovers, sliders, etc.)
- Embla Carousel for potential content carousels
- CMDK for command palette functionality

**Developer Tools**
- ESBuild for production bundling (server-side)
- TSX for TypeScript execution in development
- PostCSS with Autoprefixer for CSS processing
- Replit-specific plugins for development environment integration

**Browser APIs**
- Geolocation API for location tracking (optional feature)
- Web Speech API for voice-to-text dream journaling (VoiceRecorder component)

**Utilities**
- date-fns for date manipulation and formatting
- nanoid for generating unique identifiers
- clsx and tailwind-merge for conditional className composition
- class-variance-authority for component variant management

### Key Architectural Decisions

**Monorepo Structure**
- Shared types and schemas in `/shared` directory consumed by both client and server
- Type safety across the full stack using TypeScript path aliases
- Single source of truth for data models via Drizzle schema definitions

**Development vs Production**
- Development: Vite middleware serves React app through Express
- Production: Pre-built static assets served from `dist/public`
- Environment-aware logging and error handling

**Performance Optimizations**
- Query client configured with infinite stale time to reduce refetching
- Lazy loading of Replit-specific plugins in development only
- Responsive charts that adapt to container width

**Accessibility & UX**
- All interactive components built on Radix primitives ensure ARIA compliance
- Keyboard navigation support throughout the application
- Focus management in modals and dialogs
- Screen reader friendly with semantic HTML and proper labeling