# VibeFunding AI - Design Guidelines

## Design Approach
**System-Based Design** drawing inspiration from Linear and Notion's modern SaaS aesthetics. This B2B productivity platform prioritizes clarity, efficiency, and professional polish with sophisticated interactions and data-dense layouts.

## Typography System
- **Primary Font**: Inter (Google Fonts) - exceptional legibility for data-heavy interfaces
- **Display Font**: Inter (700-800 weight) for headings and CTAs
- **Hierarchy**:
  - Page Titles: text-4xl/5xl font-bold
  - Section Headers: text-2xl/3xl font-semibold
  - Card Titles: text-lg font-semibold
  - Body Text: text-base (15-16px) font-normal
  - Captions/Metadata: text-sm font-medium
  - Button Text: text-sm font-semibold

## Layout System
**Spacing Units**: Tailwind units of 1, 2, 4, 6, 8, 12, 16, 20 for consistent rhythm
- Component padding: p-6 to p-8
- Section spacing: gap-8 to gap-12
- Card margins: space-y-6
- Page containers: max-w-7xl mx-auto px-8

## Component Library

### Navigation
- **Top Navigation Bar**: Sticky header with logo, main navigation, search bar, notifications icon, user avatar
- **Sidebar** (Dashboard): Fixed left sidebar (w-64) with collapsible menu, icons + labels, active state indicators, organized by feature sections

### Core Components
- **Cards**: Rounded corners (rounded-xl), subtle borders, hover lift effect (shadow transition), padding p-6
- **Data Tables**: Zebra striping, sortable headers, action buttons on hover, pagination
- **Stats Tiles**: Large numbers with trend indicators, mini sparkline charts, percentage changes
- **Progress Indicators**: Multi-step progress bars for upload/analysis flows, percentage completion rings

### Forms & Inputs
- **Text Inputs**: Prominent labels above fields, helper text below, validation states (success/error borders), placeholder text
- **Textareas**: Auto-expanding for outreach/social post generation, character count displays
- **File Upload**: Drag-and-drop zones with clear upload states, file preview thumbnails, progress bars
- **Buttons**: Primary (bold CTA), Secondary (outlined), Tertiary (text-only), sizes sm/md/lg
- **Blurred Buttons on Images**: When buttons overlay hero images or photo backgrounds, apply backdrop-blur-md with semi-transparent background

### Data Display
- **Investor Cards**: Profile image, name, firm, investment focus tags, match score badge, quick action buttons
- **Match Score Visualization**: Circular progress indicators (0-100%), breakdown bars for sub-scores
- **Generated Content Previews**: Email/social post mockups in realistic UI containers (email client, Twitter card)
- **Analytics Charts**: Line graphs for trends, bar charts for comparisons, minimal axes, data point hover states

### Overlays
- **Modals**: Centered, max-w-2xl, backdrop blur, slide-in animation, clear close button
- **Side Panels**: Right-side slide-out (w-1/3) for detail views, editing contexts
- **Tooltips**: Small, contextual, subtle shadows, appear on icon hovers
- **Notifications**: Toast messages (top-right), success/info/warning/error variants

## Page Layouts

### Marketing Landing Page (Pre-Login)
- **Hero Section**: Full-width (h-screen), compelling headline, subheadline, primary CTA button with backdrop-blur, secondary "Watch Demo" button, hero image showing platform dashboard screenshot
- **Features Grid**: 3-column grid showcasing AI Matching, Outreach Generation, Pitch Deck Analysis with icons and descriptions
- **How It Works**: Step-by-step process (numbered 1-2-3-4), visual flow diagram
- **Social Proof**: Founder testimonials, investor logos carousel, success metrics
- **Pricing Tiers**: 3-column comparison table (Starter/Pro/Enterprise)
- **Final CTA**: Strong conversion section with benefits recap

### Dashboard (Post-Login)
- **Header**: Welcome message, quick stats row (4 metrics), date range selector
- **Main Content Grid**: 
  - Left: Recent activity feed, upcoming tasks
  - Center: Featured investor matches (scrollable cards)
  - Right: AI-generated content suggestions
- **Quick Actions Bar**: Floating action buttons for "Find Investors", "Generate Outreach", "Upload Pitch Deck"

### Investor Search
- **Filters Sidebar** (left, w-1/4): Industry, stage, check size, location dropdowns, active filter badges
- **Results Grid** (center/right, w-3/4): 2-column investor cards, infinite scroll, sort options, match score visible
- **Detail Panel**: Slides in from right when investor selected, full profile, contact history, generate outreach CTA

### Outreach Generator
- **Input Section**: Multi-field form (investor selection, context inputs, tone selector)
- **AI Generation Area**: Loading state with progress indicator, generated email in realistic preview, edit inline, regenerate button
- **Revision History**: Sidebar showing past versions, learning feedback options (thumbs up/down)

### Pitch Deck Uploader
- **Upload Zone**: Large drag-drop area, file type indicators (PDF/PPT), processing animation
- **Analysis Results**: Slide-by-slide breakdown, strengths/weaknesses cards, overall score gauge, actionable recommendations list
- **Export Options**: Download PDF report, share link buttons

## Images
- **Hero Image**: Dashboard screenshot or founder working on laptop with platform visible, positioned right side of hero or as background with overlay
- **Feature Icons**: Use Heroicons (outline style) from CDN for consistency
- **Investor Profile Photos**: Circular avatars, placeholder initials when no photo
- **Platform Screenshots**: Throughout landing page showing actual interface in use
- **No custom SVG generation**: All icons from Heroicons library

## Animation Philosophy
**Minimal and purposeful only**:
- Page transitions: Simple fade-ins
- Card hovers: Subtle lift (transform scale 1.02)
- Loading states: Skeleton screens, spinner for AI generation
- No scroll-triggered animations, no parallax effects

This design system ensures VibeFunding AI feels professional, efficient, and trustworthy while maintaining visual interest through strong hierarchy, generous spacing, and polished components.