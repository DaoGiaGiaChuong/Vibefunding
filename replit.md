# VibeFunding AI

## Overview

VibeFunding AI is an AI-powered fundraising platform that helps founders connect with investors through intelligent matching, automated outreach generation, pitch deck analysis, and social media content creation. The platform uses Claude AI for text generation and reasoning, with a focus on learning from user feedback over time.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18 with TypeScript and Vite for fast development and optimized production builds.

**UI Component System**: Built on shadcn/ui components (Radix UI primitives) with a custom design system inspired by Linear and Notion. The design emphasizes:
- System-based design with consistent spacing (Tailwind units)
- Inter font family for exceptional legibility
- Sophisticated color palette with HSL-based theming supporting light/dark modes
- Comprehensive component library including cards, forms, data tables, and overlays

**Routing**: Wouter for lightweight client-side routing with the following key pages:
- Dashboard (overview and analytics)
- Investors (search and match with filters)
- Outreach (AI-generated email creation)
- Social (platform-specific content generation)
- Pitch Deck (upload and analysis)
- Analytics (performance tracking)

**State Management**: TanStack Query (React Query) for server state management, providing caching, background updates, and optimistic updates. The queryClient is configured with custom fetch wrappers that handle error states and authentication.

**Styling**: Tailwind CSS with custom configuration extending the base theme. CSS variables enable dynamic theming with support for opacity modifiers. Custom utility classes provide hover/active states with elevation effects.

### Backend Architecture

**Runtime**: Node.js with Express.js providing a REST API architecture.

**Development vs Production**: Separate entry points with Vite middleware for hot module replacement in development and static file serving in production.

**API Design**: RESTful endpoints organized by feature domain:
- `/api/investors` - Investor search, filtering, and matching
- `/api/outreach` - Email generation and management
- `/api/social` - Social media post creation
- `/api/pitch-decks` - Deck upload and AI analysis
- `/api/analytics` - Performance metrics and insights
- `/api/feedback` - User feedback collection for learning loops

**AI Integration**: Anthropic's Claude API (Sonnet 4.5) accessed through Replit's AI Integrations service, which provides API credentials without requiring personal API keys. AI services include:
- Outreach email generation with personalization
- Social post creation for multiple platforms
- Pitch deck analysis with scoring and recommendations

**Pitch Deck Analysis Flow**:
1. User uploads PDF/PowerPoint file via drag-and-drop UI (multer middleware handles file storage)
2. File metadata persisted to `pitch_decks` table with userId foreign key
3. Analysis triggered via POST `/api/pitch-decks/analyze/:id`:
   - PDF text extraction using `pdf-parse` v2 (PDFParse class API)
   - Claude AI analyzes extracted text to identify 7 founder insights:
     - Stage (pre-seed, seed, Series A/B/C)
     - Personality traits (technical, sales-driven, visionary, data-driven)
     - Industry and field
     - Problem statement and solution approach
     - Traction metrics and validation
     - Team background and expertise
     - Funding needs and use of funds
   - Analysis results include overall score (0-100), strengths array, weaknesses array, and recommendations array
4. Results persisted to database via `storage.updatePitchDeck()` method
5. Frontend displays analysis with visual scores, insights cards, and actionable recommendations
6. Extracted founder insights power downstream features (investor matching, accelerator recommendations)

**Intelligent Investor Matching**:
The platform uses pitch deck analysis to create personalized investor matches:
- **Stage Matching**: Investors who fund the founder's current stage receive +30 points (perfect match) or +15 points (adjacent stage)
- **Industry Matching**: Investors focused on the founder's industry receive +40 points (exact match) or +20 points (related industry)
- **Match Scores**: All investors start with base score of 30, with final scores capped at 100
- **Match Reasons**: Each investor includes personalized explanations like "Perfect stage match - invests in seed companies" or "Strong industry focus on AI/ML"
- **Smart Ranking**: Investors sorted by match score descending, ensuring best-fit investors appear first
- **Fallback Behavior**: If no pitch deck is analyzed, random scores (80-99) are assigned for backward compatibility

**Data Storage Strategy**: In-memory storage interface defined in `storage.ts`, designed to be swappable with PostgreSQL/Drizzle ORM implementation. The schema supports:
- Users (authentication)
- Investors (profiles with industry, stage, check size, location)
- Outreach messages (generated emails with context)
- Social posts (platform-specific content)
- Pitch decks (files with analysis results)
- Feedback (learning loop data)

### Database Schema

**ORM**: Drizzle ORM configured for PostgreSQL with type-safe query building and schema validation.

**Key Tables**:
- `users` - Authentication with username/password
- `investors` - Comprehensive profiles with arrays for multi-value fields (industry, stage)
- `outreach_messages` - Links to investors with subject, body, tone, and context
- `social_posts` - Platform and content with timestamps
- `pitch_decks` - File metadata with JSONB analysis results, scores, and recommendations
- `feedback` - Learning data tied to generated items

**Type Safety**: Zod schemas generated from Drizzle tables provide runtime validation and TypeScript types shared between frontend and backend.

### Authentication & Authorization

**Session-based authentication** implemented with express-session and PostgreSQL session store (connect-pg-simple). Features include:
- User registration with bcrypt password hashing (10 salt rounds)
- Login with username/password validation
- Session persistence across requests using secure HTTP-only cookies
- Protected API routes with `requireAuth` middleware
- Trust proxy configuration for Replit environment
- Frontend auth context (AuthProvider) with useAuth hook for user state management
- Logout functionality with session destruction
- Credentials include mode for cross-origin requests

### Design System

**Typography**: Inter font (400-800 weights) with structured hierarchy from 4xl/5xl headings down to small captions.

**Component Patterns**:
- Cards with rounded-xl corners, subtle borders, hover lift effects
- Sidebar navigation with collapsible menu and active states
- Modal overlays with backdrop blur
- Form inputs with validation states
- Progress indicators for multi-step flows
- Blurred buttons over images using backdrop-blur-md

**Color System**: HSL-based with CSS variables enabling theme switching. Supports primary, secondary, muted, accent, and destructive variants. Each variant includes foreground and border color definitions.

**Spacing**: Consistent use of Tailwind spacing units (1, 2, 4, 6, 8, 12, 16, 20) with component padding of p-6 to p-8 and section gaps of gap-8 to gap-12.

## External Dependencies

### AI Services
- **Anthropic Claude API** (`@anthropic-ai/sdk`): Claude Sonnet 4.5 model for text generation and reasoning, accessed through Replit AI Integrations service

### Database
- **Neon Serverless Postgres** (`@neondatabase/serverless`): Serverless PostgreSQL database
- **Drizzle ORM** (`drizzle-orm`, `drizzle-kit`): Type-safe ORM with schema generation and migrations

### UI Libraries
- **Radix UI**: Comprehensive set of headless UI primitives for accessible components (accordion, dialog, dropdown, popover, select, tabs, toast, etc.)
- **shadcn/ui**: Component system built on Radix with Tailwind styling
- **Lucide React**: Icon library
- **react-icons**: Additional icons (social media platforms)

### Form Handling
- **React Hook Form**: Form state management with validation
- **Zod** (`zod`, `@hookform/resolvers`, `drizzle-zod`): Schema validation and type inference

### Utilities
- **TanStack Query**: Server state management with caching and background updates
- **Wouter**: Lightweight routing
- **date-fns**: Date manipulation and formatting
- **class-variance-authority**: Utility for managing CSS class variants
- **tailwind-merge**: Intelligent Tailwind class merging

### Development Tools
- **Vite**: Build tool and dev server with HMR
- **TypeScript**: Type safety across the stack
- **ESBuild**: Fast JavaScript bundler for production builds
- **Replit Development Plugins**: Runtime error overlay, cartographer, dev banner