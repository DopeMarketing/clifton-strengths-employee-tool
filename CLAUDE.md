# CLAUDE.md - AI Coding Assistant Briefing

## Project Overview
Clifton Strengths Employee Tool is an internal HR platform that helps managers communicate effectively with team members based on their CliftonStrengths profiles. The system parses PDF reports, manages employee strength data, and provides AI-powered communication recommendations.

## Tech Stack
- **Frontend:** Next.js 15 (App Router), TypeScript, Tailwind CSS, Shadcn/ui
- **Backend:** Supabase (PostgreSQL, Auth, Storage, RLS)
- **AI:** OpenAI ChatGPT, Anthropic Claude
- **Integrations:** Google Drive, ADP HR, Google Sheets, Zapier, Twilio
- **Deployment:** Vercel

## Folder Structure

src/
├── app/                    # Next.js app directory - all routes and layouts
│   ├── globals.css        # Global styles and Tailwind imports
│   ├── layout.tsx         # Root layout with providers
│   ├── page.tsx           # Landing page (/)
│   ├── (auth)/            # Auth route group
│   │   ├── login/         # Login page
│   │   ├── signup/        # Signup page
│   │   └── forgot-password/ # Password reset
│   ├── dashboard/         # Protected dashboard
│   ├── employees/         # Employee management
│   │   ├── [id]/          # Individual employee pages
│   │   └── search/        # Employee search
│   ├── upload/            # PDF upload functionality
│   ├── import/            # CSV import tools
│   ├── assessment/        # CliftonStrengths assessment
│   ├── recommendations/   # AI recommendations
│   ├── settings/          # User settings
│   ├── admin/             # Admin-only pages
│   └── api/               # API routes for integrations
├── components/             # React components only
│   ├── ui/                # Shadcn/ui primitives
│   ├── forms/             # Form components
│   ├── layout/            # Layout components (nav, sidebar)
│   └── features/          # Feature-specific components
├── lib/                   # Utilities, configs, pure functions
│   ├── utils.ts           # General utilities
│   ├── validations.ts     # Zod schemas
│   ├── constants.ts       # App constants
│   └── integrations/      # External API clients
├── actions/               # Server actions only
│   ├── auth.ts           # Authentication actions
│   ├── employees.ts      # Employee CRUD actions
│   └── uploads.ts        # File upload actions
├── db/                    # Database layer only
│   ├── index.ts          # Supabase client
│   ├── queries/          # Database queries
│   └── types.ts          # Database types
└── types/                 # TypeScript definitions
    ├── database.ts       # Supabase generated types
    └── app.ts            # App-specific types


## Coding Conventions
- **TypeScript:** Strict mode enabled, no `any` types
- **React:** Server components by default, use `'use client'` only when needed
- **Data access:** Only in `/db` directory, never in components
- **Business logic:** Only in `/lib` and `/actions`, not in components
- **Secrets:** Never in client components, use server actions or API routes
- **Components:** One component per file, named exports
- **Imports:** Absolute imports using `@/` prefix

## Current State (Scaffold Generated)

The following has been built:
- ✅ Complete data model with 12 tables and RLS policies
- ✅ Authentication system with role-based access (Admin, Manager, Employee)
- ✅ Route structure with 16 pages stubbed out
- ✅ Basic UI components using Shadcn/ui
- ✅ Integration placeholders for all external services
- ✅ Supabase client configuration
- ✅ TypeScript types for database schema
- ✅ Environment variable setup

**What works:** User registration, login, basic navigation, database connections  
**What doesn't:** All business features - this is a scaffold ready for development

## V1 Features to Build Next

### Priority 1 - Core Upload & Parsing
1. **PDF parser** that extracts CliftonStrengths top 5 themes from uploaded reports
2. **CSV bulk import** tool with mapping interface to match columns to database fields
3. **Employee profile search** with filters by specific strength themes

### Priority 2 - Intelligence Layer
4. **Notes section** for each employee profile with tagging system
5. **AI-powered communication recommendations** based on employee strength themes
6. **CliftonStrengths Assessment** integration

### Priority 3 - Workflows
7. Employee profile CRUD with strength data display
8. Manager dashboard with team overview
9. Communication recommendation engine

## Never Touch Rules
- **Environment files (.env*):** Never commit or modify without explicit instruction
- **Migration files:** Never edit existing migrations, only create new ones
- **RLS policies:** Never modify without security review
- **Supabase types:** These are generated, never edit manually
- **Package.json scripts:** Don't change without understanding implications

## How to Work on This Project

1. **Always read this file first** before making any changes
2. **Start small:** Pick one feature, implement fully, then move to next
3. **Follow the structure:** Put code in the right directories
4. **Test as you go:** Run `npm run dev` and verify changes work
5. **Build before committing:** Run `npm run build` to catch TypeScript errors
6. **Commit frequently:** Small, focused commits with conventional commit messages
7. **Document debt:** Add to TECHNICAL_DEBT.md if taking shortcuts

## Common Patterns

**Database queries:**
typescript
// Always in /db/queries/
export async function getEmployeeById(id: string) {
  return await supabase
    .from('employees')
    .select('*')
    .eq('id', id)
    .single()
}


**Server actions:**
typescript
// Always in /actions/
'use server'
export async function createEmployee(data: EmployeeInsert) {
  // Validate input
  // Call database query
  // Return result
}


**Components:**
typescript
// Server component by default
export default function EmployeeList() {
  // Fetch data in server component
  return <div>...</div>
}

// Client component when needed
'use client'
export default function UploadForm() {
  // Interactive form logic
}


## Integration Notes
- **Google Drive:** Use for PDF storage and retrieval
- **ADP:** Sync employee data automatically
- **ChatGPT/Claude:** Generate communication recommendations
- **Twilio:** Send SMS reminders to managers
- **Zapier:** Connect to other HR tools

When working on integrations, always:
1. Create client in `/lib/integrations/`
2. Add API routes in `/app/api/`
3. Store credentials securely in Supabase
4. Handle errors gracefully
5. Log integration events in `sync_logs` table