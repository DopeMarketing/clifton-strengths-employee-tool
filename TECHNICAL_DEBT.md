# Technical Debt

This file tracks known shortcuts and technical debt in the Clifton Strengths Employee Tool. Each item describes what production-grade implementation looks like and the estimated effort to resolve.

> **Philosophy:** We ship fast by taking smart shortcuts, then invest in making things production-ready. This file ensures we don't forget what needs improvement.

## Debt Items

### 1. Error Handling - Basic Console Logging
**Current state:** Most error handling uses `console.log()` or basic try/catch blocks  
**Production-grade:** Structured logging with levels, error tracking service (Sentry), user-friendly error messages, retry mechanisms for transient failures  
**Estimated effort:** 8 hours

### 2. Rate Limiting - No Protection
**Current state:** API routes have no rate limiting or abuse protection  
**Production-grade:** Implement rate limiting middleware, IP-based throttling, user-specific quotas for file uploads and AI requests, CAPTCHA for auth endpoints  
**Estimated effort:** 6 hours

### 3. File Upload Security - Basic Validation
**Current state:** PDF uploads only check file extension and size  
**Production-grade:** Virus scanning, content type validation, file sanitization, secure storage with signed URLs, upload progress tracking, file corruption detection  
**Estimated effort:** 12 hours

### 4. RLS Policies - Generated Defaults
**Current state:** RLS policies are basic multi-tenant defaults  
**Production-grade:** Security audit of all policies, fine-grained permissions (read/write/delete per role), policy testing suite, documentation of access patterns  
**Estimated effort:** 10 hours

### 5. Testing Infrastructure - No Automated Tests
**Current state:** No unit tests, integration tests, or end-to-end tests  
**Production-grade:** Jest unit tests for utilities and actions, Playwright E2E tests for critical user flows, API testing with realistic data, CI/CD pipeline with test gates  
**Estimated effort:** 15 hours

### 6. Performance Optimization - No Caching
**Current state:** All database queries are uncached, no CDN for static assets  
**Production-grade:** Redis caching for employee data, React Query for client-side caching, CDN for file uploads, database query optimization, lazy loading for large lists  
**Estimated effort:** 10 hours

### 7. AI Integration - No Fallback Strategy
**Current state:** Direct API calls to OpenAI/Claude with no error handling or fallbacks  
**Production-grade:** Multiple AI provider support, graceful degradation when APIs are down, response caching, token usage monitoring, cost controls  
**Estimated effort:** 8 hours

### 8. Data Backup and Recovery - Supabase Default Only
**Current state:** Relies on Supabase automatic backups  
**Production-grade:** Custom backup strategy for file uploads, point-in-time recovery testing, data export functionality, disaster recovery procedures  
**Estimated effort:** 6 hours

### 9. Monitoring and Observability - No Metrics
**Current state:** No application metrics, performance monitoring, or health checks  
**Production-grade:** Application metrics (user activity, feature usage), performance monitoring (page load times, API response times), health check endpoints, alerting for critical failures  
**Estimated effort:** 8 hours

### 10. Email System - No Transactional Emails
**Current state:** Password reset and notifications use basic Supabase auth emails  
**Production-grade:** Branded email templates, transactional email service (SendGrid/Resend), email delivery tracking, unsubscribe management  
**Estimated effort:** 5 hours

---

**Total estimated effort:** 88 hours

## Prioritization Guidelines

**Critical (Security/Data Loss Risk):** Items 3, 4, 8 - Address before handling sensitive HR data  
**High (User Experience):** Items 1, 6, 9 - Important for daily usage reliability  
**Medium (Operational):** Items 2, 5, 7, 10 - Improve maintainability and monitoring  

## Review Schedule

- **Weekly:** Review during development for new debt items
- **Monthly:** Prioritize debt resolution in sprint planning
- **Quarterly:** Full audit of all items and effort estimates