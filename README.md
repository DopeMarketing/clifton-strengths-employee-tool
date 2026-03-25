# Clifton Strengths Employee Tool

An intelligent employee communication platform that helps managers understand and adapt their communication style based on each team member's CliftonStrengths profile.

## What This Does

This tool transforms CliftonStrengths assessments into actionable insights for managers. Upload PDF reports or import CSV data to build a comprehensive knowledge base of your team's strengths, then get AI-powered recommendations on how to communicate effectively with each person based on their unique strength profile.

**Built for:** Internal HR teams and people managers who want to improve team communication and engagement

## Tech Stack

- **Frontend:** Next.js 15 with TypeScript and Tailwind CSS
- **Backend:** Supabase (PostgreSQL + Auth + Storage)
- **AI:** OpenAI ChatGPT and Anthropic Claude
- **Integrations:** Google Drive, ADP HR, Google Sheets, Zapier, Twilio
- **Deployment:** Vercel

## Prerequisites

- Node.js 18+ and npm
- Git
- Supabase CLI (`npm install -g supabase`)
- Accounts for: Supabase, Vercel, OpenAI, Anthropic, Google Cloud

## Local Setup

1. **Clone and install dependencies**
   bash
   git clone <your-repo>
   cd clifton-strengths-tool
   npm install
   

2. **Set up environment variables**
   bash
   cp .env.example .env.local
   # Edit .env.local with your values (see table below)
   

3. **Start Supabase local development**
   bash
   supabase start
   # Note the API URL and anon key for .env.local
   

4. **Run the development server**
   bash
   npm run dev
   

5. **Open http://localhost:3000**

## Environment Variables

| Variable | Description | Example |
|----------|-------------|----------|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL | `http://localhost:54321` |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anonymous key | `eyJ0eXAiOiJKV1Q...` |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service key (server-only) | `eyJ0eXAiOiJKV1Q...` |
| `OPENAI_API_KEY` | OpenAI API key for ChatGPT | `sk-proj-...` |
| `ANTHROPIC_API_KEY` | Anthropic API key for Claude | `sk-ant-...` |
| `GOOGLE_CLIENT_ID` | Google OAuth client ID | `123456789.googleusercontent.com` |
| `GOOGLE_CLIENT_SECRET` | Google OAuth secret | `GOCSPX-...` |
| `ADP_CLIENT_ID` | ADP API client ID | `adp_12345` |
| `ADP_CLIENT_SECRET` | ADP API secret | `secret123` |
| `TWILIO_ACCOUNT_SID` | Twilio account SID | `AC1234567890` |
| `TWILIO_AUTH_TOKEN` | Twilio auth token | `auth_token_123` |

## Database Setup

The database schema is automatically applied when you run `supabase start`. It includes:

- **Core tables:** users, organizations, employees, clifton_themes
- **Data tables:** employee_strengths, employee_notes, pdf_reports, csv_imports
- **Integration tables:** api_integrations, sync_logs, communication_recommendations
- **Row Level Security (RLS)** policies for multi-tenant access

To reset the database:
bash
supabase db reset


## Deploy to Vercel

1. **Push your code to GitHub**
2. **Connect to Vercel and deploy**
3. **Set environment variables in Vercel dashboard**
   - Copy from .env.local but update URLs to production Supabase
4. **Update Supabase settings**
   - Add your Vercel domain to allowed origins
   - Set up production database and apply migrations

## Project Structure


src/
├── app/                 # Next.js 15 app directory
│   ├── (auth)/         # Authentication pages
│   ├── dashboard/      # Protected dashboard routes
│   ├── employees/      # Employee management
│   └── api/           # API routes
├── components/         # Reusable React components
│   ├── ui/            # Shadcn/ui components
│   ├── forms/         # Form components
│   └── layout/        # Layout components
├── lib/               # Utility functions and configs
├── actions/           # Server actions
├── db/                # Database queries and types
└── types/             # TypeScript type definitions

supabase/
├── migrations/        # Database migrations
└── seed.sql          # Seed data


## Getting Help

- Check the CLAUDE.md file for AI coding guidance
- Review TECHNICAL_DEBT.md for known limitations
- See ROADMAP.md for upcoming features

## License

Internal use only