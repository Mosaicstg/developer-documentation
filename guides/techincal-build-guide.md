# Technical Build Guide: Three Paths

A decision-focused guide for internal teams (Engineering, Design, Project Management) covering three project paths: CMS-based, Custom Application, and Hybrid. Each path follows the same decision framework with path-specific guidance.

---

## Table of Contents

- [Section 0: Path Selection Framework](#section-0-path-selection-framework)
- [Section 1: Shared Foundations](#section-1-shared-foundations)
  - [Baseline Stakeholder Questions](#baseline-stakeholder-questions)
  - [Baseline Success Metrics](#baseline-success-metrics)
  - [Baseline Security Questions](#baseline-security-questions)
  - [Accessibility Requirements](#accessibility-requirements)
  - [Analytics & Tracking](#analytics--tracking)
- [Section 2: QA & Testing](#section-2-qa--testing)
- [Section 3: Project Execution](#section-3-project-execution)
  - [Discovery & Requirements](#discovery--requirements)
  - [Technology Stack Selection](#technology-stack-selection)
  - [Hosting & Infrastructure](#hosting--infrastructure)
  - [Performance & Optimization](#performance--optimization)
  - [Project Management & Workflow](#project-management--workflow)
  - [Security Considerations](#security-considerations)
- [Section 4: Path Evolution](#section-4-path-evolution)
- [Appendix: Red Flag Questions](#appendix-red-flag-questions)
- [Embedded Resources](#embedded-resources)
  - [Application Resource Requirements Checklist](#application-resource-requirements-checklist)
  - [Hosting & Performance Notes](#hosting--performance-notes)

---

## Section 0: Path Selection Framework

### Quick Diagnostic: Which Path Are You On?

Answer these questions to identify your project path:

1. **Will the client/users primarily manage content through an admin interface with predefined templates?**

   - Yes → CMS Path
   - No, need fully custom UI/UX → Custom App Path
   - Partially (content in CMS, custom frontend) → Hybrid Path

2. **Is the core value proposition content management and ease of editing?**

   - Yes → CMS Path
   - No, complex data/logic/interactions → Custom App Path
   - Mixed → Hybrid Path

3. **Does the team need to maintain separation between content management and frontend presentation?**

   - No, integrated is fine → CMS Path
   - Yes, they're separate concerns → Hybrid Path
   - Custom solution → Custom App Path

4. **What's the primary technical constraint?**
   - Budget/timeline/team size (keep it simple) → CMS Path
   - Performance/scalability/unique requirements → Custom App Path
   - Content flexibility + custom frontend → Hybrid Path

---

### Path Characteristics Matrix

| Characteristic             | CMS Path                              | Custom App Path                     | Hybrid Path                               |
| -------------------------- | ------------------------------------- | ----------------------------------- | ----------------------------------------- |
| **Control**                | Templated, structured                 | Full control                        | Content structured, frontend free         |
| **Flexibility**            | Moderate (within CMS)                 | Unlimited                           | High (frontend + content)                 |
| **Development Speed**      | Fast (theme/plugins)                  | Slower (build from scratch)         | Medium-fast (headless + frontend)         |
| **Team Size**              | Small (1-2 Eng)                       | Medium-Large (multiple specialties) | Medium (content + frontend split)         |
| **Client Technical Skill** | Low (admin UI)                        | Medium-High (may interact with API) | Low-Medium (CMS UI + frontend users)      |
| **Maintenance**            | Moderate (updates/plugins)            | Ongoing (code ownership)            | Moderate (both layers)                    |
| **Scalability**            | Limited by CMS platform               | Unlimited (custom architecture)     | Limited by CMS (backend flexible)         |
| **Cost (long-term)**       | Low-Moderate                          | Moderate-High                       | Moderate                                  |
| **Typical Use Cases**      | Blogs, marketing sites, content-heavy | SaaS, web apps, complex logic       | Modern marketing sites, headless commerce |

---

### Decision Flow: Which Path for Your Project?

```
START: New Project
│
├─ Is this primarily a CONTENT MANAGEMENT project?
│  │
│  ├─ YES → Will you need a custom frontend separate from content management?
│  │         │
│  │         ├─ NO  → CMS PATH
│  │         └─ YES → HYBRID PATH
│  │
│  └─ NO → Do you need full control over UI/UX and custom business logic?
│          │
│          ├─ YES → CUSTOM APP PATH
│          └─ NO  → Reconsider CMS Path
│
```

---

### Key Differences at a Glance

**CMS Path**

- Platform: WordPress, Webflow, Drupal (traditional)
- Hosting: Managed hosting, simple scaling
- Development: Theme customization, plugin integration
- Team: Small, generalist
- Best for: Content sites, marketing, blogs

**Custom App Path**

- Platform: React/Vue/Angular + Node/Django/Rails + Database
- Hosting: Containers, serverless, traditional servers
- Development: Full-stack custom build
- Team: Multiple specialties (frontend, backend, database)
- Best for: SaaS, web apps, complex interactions

**Hybrid Path**

- Platform: Headless CMS (Contentful, Sanity, Strapi) + Frontend Framework
- Hosting: CMS separately, frontend separately
- Development: CMS structure + custom frontend
- Team: Content/CMS specialists + frontend engineers
- Best for: Modern marketing sites, content-driven apps with custom UI

---

## Section 1: Shared Foundations

Baseline requirements applicable to all project paths. Individual path sections reference and extend these foundations.

---

### Department Responsibilities

| Section Type    | Lead   | Support     |
| --------------- | ------ | ----------- |
| Discovery       | PM     | Eng, Design |
| Stack Selection | Eng    | PM          |
| Hosting         | Eng    | PM          |
| Performance     | Eng    | PM          |
| Project Mgmt    | PM     | Eng, Design |
| Security        | Eng    | PM          |
| QA              | Eng/QA | PM, Design  |

---

### Baseline Stakeholder Questions

- What are the primary business goals for this project?
- Who are the primary users/audience?
- What problems does this solve for them?
- How will success be measured?
- What's the timeline from discovery to launch?
- What's the budget range?
- Who are the key decision-makers?
- What are the hard constraints (budget, timeline, technology)?

---

### Baseline Success Metrics

- **Performance:** Load time, uptime, responsiveness
- **User Engagement:** Bounce rate, time on site, pages per session
- **Business Goals:** Conversions, leads, revenue, signups
- **Team Satisfaction:** Ease of maintenance, support burden
- **Accessibility:** WCAG compliance level achieved

---

### Baseline Security Questions

Path-specific security details in individual path sections.

1. **Data Protection:** What data is being collected? How is it stored and encrypted?
2. **User Authentication:** How are users logging in? Multi-factor authentication?
3. **Access Control:** Who can access what? Principle of least privilege?
4. **Third-party Risk:** What third-party services have access? What permissions?
5. **Updates & Patching:** How are security updates applied? Automated?
6. **Backups:** Are backups automated? Tested? Stored securely?
7. **Monitoring:** Are security issues logged and monitored?
8. **Compliance:** What regulations apply? (GDPR, CCPA, HIPAA, PCI-DSS, etc.)
9. **Incident Response:** What's the plan if security is breached?

---

### Accessibility Requirements

Address during Discovery and validate during QA.

#### WCAG Compliance Level

- [ ] **Level A (minimum):** Basic accessibility—required for all projects
- [ ] **Level AA (standard):** Industry standard—recommended for most projects
- [ ] **Level AAA (enhanced):** Highest level—for accessibility-focused projects

#### Core Accessibility Checklist

**Visual:**

- [ ] Color contrast meets WCAG standards (4.5:1 for normal text, 3:1 for large text)
- [ ] Text is resizable up to 200% without loss of functionality
- [ ] Information is not conveyed by color alone
- [ ] Images have meaningful alt text (or empty alt for decorative images)
- [ ] Focus indicators are visible

**Navigation:**

- [ ] All functionality is keyboard accessible
- [ ] Focus order is logical and intuitive
- [ ] Skip links are provided for repetitive content
- [ ] Page titles are descriptive and unique

**Content:**

- [ ] Headings are hierarchical and descriptive
- [ ] Links have descriptive text (not "click here")
- [ ] Form fields have associated labels
- [ ] Error messages are clear and identify the field

**Media:**

- [ ] Videos have captions
- [ ] Audio has transcripts
- [ ] Animations can be paused or disabled
- [ ] No content flashes more than 3 times per second

**Technical:**

- [ ] Semantic HTML is used correctly
- [ ] ARIA labels are used where needed (and correctly)
- [ ] Pages work with screen readers (VoiceOver, NVDA, JAWS)
- [ ] Site works with browser zoom and text-only zoom

#### Accessibility Testing

- **Automated Testing:** Run Lighthouse, axe, or WAVE during development
- **Manual Testing:** Keyboard navigation, screen reader testing
- **User Testing:** Include users with disabilities when possible
- **Audit Cadence:** Test at end of each phase; full audit before launch

#### Red Flag Questions

- Is accessibility being deferred to "later"?
- Are designers unaware of contrast requirements?
- Is there no budget for accessibility testing?
- Are interactive elements not keyboard accessible?
- Is the site unusable without a mouse?

---

### Analytics & Tracking

Address during Discovery; implement during Development.

#### Analytics Planning Checklist

- [ ] **Platform Selected:** Google Analytics, Mixpanel, Plausible, custom?
- [ ] **Key Events Identified:** What user actions matter? (signups, purchases, downloads)
- [ ] **Conversion Goals Defined:** What counts as success?
- [ ] **Privacy/Consent:** Cookie consent banner needed? GDPR/CCPA compliance?
- [ ] **Data Retention:** How long is data stored? Who has access?

#### Path-Specific Considerations

- **CMS Path:** Often plugin-based (easy setup, limited customization)
- **Custom App Path:** Custom event tracking, more granular control
- **Hybrid Path:** Track both CMS content performance and frontend interactions

---

### Client Handoff Checklist

Use this checklist for all paths. Path-specific items noted inline.

- [ ] **Credentials & Access**

  - [ ] All login credentials documented and transferred
  - [ ] Admin accounts created for client team
  - [ ] Third-party service access transferred (hosting, DNS, analytics, monitoring)
  - [ ] Code repository access (Custom App/Hybrid only)
  - [ ] CI/CD pipeline access (Custom App/Hybrid only)
  - [ ] Password manager entries shared

- [ ] **Documentation**

  - [ ] User guide delivered (CMS: content editing; Custom App: admin/operations)
  - [ ] Technical documentation (architecture, integrations, API docs for Custom App/Hybrid)
  - [ ] Deployment procedures (Custom App/Hybrid)
  - [ ] Runbook for common operations (Custom App/Hybrid)
  - [ ] Troubleshooting guide / FAQ

- [ ] **Training**

  - [ ] Content editor training completed (CMS/Hybrid)
  - [ ] Admin/operations training completed
  - [ ] Developer onboarding documentation (if client will maintain)
  - [ ] Training recordings available

- [ ] **Support & Maintenance**
  - [ ] Support agreement signed
  - [ ] Escalation contacts documented
  - [ ] Maintenance schedule established
  - [ ] Backup verification completed
  - [ ] Monitoring handoff (dashboards, alerts) (Custom App/Hybrid)

---

## Section 2: QA & Testing

Testing strategy applicable to all paths. Path-specific notes in each path's Project Management section.

---

### Testing Types

| Type                      | What It Tests                        | When                               | Who                  |
| ------------------------- | ------------------------------------ | ---------------------------------- | -------------------- |
| **Unit Testing**          | Individual functions/components      | During development                 | Engineering          |
| **Integration Testing**   | Components working together          | During development                 | Engineering          |
| **End-to-End (E2E)**      | Full user flows                      | Before launch, after major changes | Engineering/QA       |
| **Visual Regression**     | UI hasn't changed unexpectedly       | After UI changes                   | Engineering/QA       |
| **Accessibility Testing** | WCAG compliance                      | Every phase                        | QA/Design            |
| **Performance Testing**   | Load time, throughput, scalability   | Before launch                      | Engineering          |
| **Security Testing**      | Vulnerabilities, penetration testing | Before launch                      | Engineering/External |
| **User Acceptance (UAT)** | Meets business requirements          | Before launch                      | PM/Client            |

---

### Testing by Phase

#### Discovery

- [ ] Define acceptance criteria for features
- [ ] Identify critical user flows to test
- [ ] Establish performance targets
- [ ] Document accessibility requirements

#### Design

- [ ] Review designs for accessibility (contrast, focus states, etc.)
- [ ] Validate user flows are testable
- [ ] Identify edge cases

#### Development

- [ ] Unit tests written alongside code
- [ ] Integration tests for API/database interactions
- [ ] Accessibility testing (automated + manual)
- [ ] Code review includes test coverage check

#### Launch

- [ ] Full E2E test suite passes
- [ ] Performance testing against targets
- [ ] Security scan/penetration test (if applicable)
- [ ] UAT sign-off from stakeholders
- [ ] Accessibility audit complete

#### Post-Launch

- [ ] Monitor for production issues
- [ ] Regression testing after bug fixes
- [ ] Ongoing performance monitoring

---

### Test Coverage Expectations

| Path           | Unit                | Integration      | E2E    | Accessibility | Performance |
| -------------- | ------------------- | ---------------- | ------ | ------------- | ----------- |
| **CMS**        | Low (mostly config) | Medium (plugins) | Medium | Required      | Required    |
| **Custom App** | High                | High             | High   | Required      | Required    |
| **Hybrid**     | Medium-High         | High (API layer) | High   | Required      | Required    |

---

### UAT (User Acceptance Testing) Process

1. **Define Scope:** What features/flows are being tested?
2. **Create Test Cases:** Based on user stories and acceptance criteria
3. **Assign Testers:** Client stakeholders, internal PM, or end users
4. **Execute Tests:** Testers follow test cases, document issues
5. **Triage Issues:** Prioritize (blocker, critical, minor, nice-to-have)
6. **Fix & Retest:** Engineering fixes; testers verify
7. **Sign-off:** Formal approval to proceed to launch

---

### Red Flag Questions

- Is there no testing strategy documented?
- Is test coverage an afterthought?
- Are accessibility tests being skipped?
- Is UAT rushed or skipped?
- Are performance tests only run in production?
- Is there no regression testing after bug fixes?

---

## Section 3: Project Execution

Unified guidance for all project paths. Path-specific content marked with [CMS], [APP], or [HYB] tags.

---

### Discovery & Requirements

> **Reference:** See [Baseline Stakeholder Questions](#baseline-stakeholder-questions) for universal questions.

#### Path-Specific Discovery Questions

**[CMS]** Content-focused:

- **Content Control:** How much control does the client need? Can templates work, or do they need custom layouts for each page?
- **Content Types:** What types of content? Posts, pages, products, team members, testimonials, events?
- **Editorial Workflow:** Who publishes content? Do you need approval workflows?
- **User Management:** How many content editors? Different permission levels?
- **Content Migration:** Is there existing content? How much needs to migrate?
- **Integrations:** Email marketing, analytics, forms, payment processors?
- **Long-term:** Will the client manage this themselves post-launch, or do you provide ongoing support?

**[APP]** Custom application-focused:

- **MVP Scope:** What's the absolute minimum to launch? What can wait?
- **Core Features:** What 3-5 features define success?
- **Data Model:** What's the data structure? How do entities relate?
- **Scalability:** Will user growth require horizontal scaling? Database scaling?
- **Integrations:** Third-party APIs? Payment processing? Analytics?
- **Performance Requirements:** Real-time? Offline capability? Global? Latency SLAs?
- **Complexity:** Complex business logic? Real-time features? Machine learning?
- **Team Experience:** Has the team built this type of app before?

**[HYB]** Headless-focused:

- **Why Headless?** What does headless unlock that a traditional CMS doesn't?
- **Content Model:** What content types? How structured?
- **Editorial Workflow:** Who publishes? Approval process? Versioning?
- **Frontend Complexity:** Why custom? What can't be done with CMS themes?
- **Integration Needs:** What connects to what? APIs between systems?
- **Deployment:** Will frontend and backend deploy independently? Frequency?
- **Team Structure:** Separate content/CMS team and frontend team?
- **Future Evolution:** Starting as hybrid, or migrating from something?

#### Defining Scale & Constraints

- **Audience Size:** Monthly visits? Concurrent users? [APP: Expected users? Concurrent active users?]
- **Content Volume:** How much content? Update frequency? [APP: Data volume?]
- **Geographic Scope:** Single region? Global? [APP: Latency requirements?]
- **Device Requirements:** Desktop-first? Mobile-critical?
- **Technical Constraints:** Existing systems to integrate? Budget limits? [APP: Legacy systems? Tech debt?]
- **Team Constraints:** In-house team? Agency? Hybrid? [APP: Contract developers? Offshore?]

#### Project Kickoff Checklist

- [ ] **Discovery Complete**

  - [ ] Business goals documented
  - [ ] Success metrics defined (see [Baseline Success Metrics](#baseline-success-metrics))
  - [ ] Audience/scale understood
  - [ ] Budget & timeline confirmed
  - [ ] [APP] User research completed, market analysis done
  - [ ] [APP] MVP scope locked, core features identified
  - [ ] [HYB] Why headless? (Rationale clear)

- [ ] **Content Strategy** [CMS/HYB]

  - [ ] Content types identified
  - [ ] Content structure documented (hierarchy, relationships)
  - [ ] Existing content audit completed (if applicable)
  - [ ] Migration plan (if needed)
  - [ ] Editorial workflow defined
  - [ ] Approval process documented
  - [ ] [HYB] Team roles (content vs frontend) clear

- [ ] **Technical Planning**

  - [ ] [CMS] CMS platform selected
  - [ ] [HYB] Headless CMS chosen, content model documented, API documented
  - [ ] [APP] Data model designed (entities, relationships)
  - [ ] [APP] API design sketched, architecture diagram created
  - [ ] [APP] Frontend framework chosen
  - [ ] [HYB] Frontend framework chosen, data fetching strategy determined
  - [ ] Hosting plan determined
  - [ ] Third-party integrations mapped
  - [ ] Performance requirements documented
  - [ ] Security requirements documented (see [Baseline Security Questions](#baseline-security-questions))
  - [ ] Accessibility requirements defined (see [Accessibility Requirements](#accessibility-requirements))
  - [ ] Analytics plan documented (see [Analytics & Tracking](#analytics--tracking))
  - [ ] [APP] Scalability plan sketched

- [ ] **Team & Access**

  - [ ] Project stakeholders identified
  - [ ] Decision makers confirmed
  - [ ] [CMS/HYB] Content editors/users identified, permission levels planned
  - [ ] [APP] Team composition confirmed, skill gaps identified, tech lead/architect identified
  - [ ] [HYB] Content team access to CMS configured, frontend team access to repositories/deployments

- [ ] **Design & UX**

  - [ ] Brand guidelines available
  - [ ] Design direction confirmed
  - [ ] [CMS] Template/page types defined
  - [ ] [APP/HYB] User personas created, user journeys mapped
  - [ ] [APP/HYB] Wireframes for core flows, design system started
  - [ ] Design review cadence set

- [ ] **DevOps & Infrastructure** [APP/HYB]

  - [ ] Development environment documented
  - [ ] Staging/testing environment planned
  - [ ] Deployment process sketched
  - [ ] Monitoring/logging strategy outlined
  - [ ] [APP] CI/CD pipeline planned
  - [ ] [HYB] API contracts defined, preview system planned, deployment coordination process

- [ ] **Ongoing Support**
  - [ ] Support model defined (agency-managed vs client-managed)
  - [ ] Training needs identified
  - [ ] Maintenance plan established
  - [ ] [HYB] Migration plan (if applicable): current system audit, migration scripts, parallel run period, rollback plan

---

### Technology Stack Selection

#### [CMS] Platform Considerations

**Decision Framework:** Ease of use, content modeling fit, theme/plugin ecosystem, hosting options, scalability, security track record, support availability, cost (license/hosting/plugins/maintenance), long-term viability.

**Theme/Plugin Ecosystem:**

- **Pre-built Themes:** Cost-benefit analysis (speed vs customization needs)
- **Plugin Strategy:** Critical vs nice-to-have plugins; vendor lock-in risks
- **Custom Code:** Where's the line between configuration and custom development?
- **Performance:** Do popular plugins add bloat? Are there lightweight alternatives?

**Stack Decision Framework:**

| Decision     | Considerations                                    |
| ------------ | ------------------------------------------------- |
| **Platform** | Ease of use, content model fit, ecosystem, cost   |
| **Theme**    | Design fit, customization effort, performance     |
| **Plugins**  | Essential only? Performance impact? Alternatives? |
| **Hosting**  | Managed or self-hosted? Auto-scaling needed?      |
| **Database** | Does CMS include? Performance requirements?       |

#### [APP] Stack Considerations

**Frontend Framework:** Team expertise, project type (SPA/SSR/static/mobile), performance requirements, scalability, ecosystem size, hiring market, maintenance cadence, learning curve, tooling quality.

**Backend/API:** Language/framework (team expertise, performance, ecosystem), API style (REST/GraphQL/gRPC), authentication (JWT/OAuth/sessions), real-time needs (WebSockets/SSE), background jobs, caching strategy, scalability approach, testing framework.

**Database:** Data type (relational/document/graph/time-series), query patterns, scalability (vertical/horizontal/sharding), consistency requirements, performance needs, operational burden (managed vs self-hosted), cost, backup/recovery criticality.

**Stack Decision Framework:**

| Layer         | Considerations                                 | Options                                |
| ------------- | ---------------------------------------------- | -------------------------------------- |
| **Frontend**  | Team skill, performance, ecosystem             | React, Vue, Angular, Svelte, etc.      |
| **Backend**   | Language, performance, team expertise          | Node, Python, Java, Go, Ruby, etc.     |
| **Database**  | Data model, scalability, consistency           | PostgreSQL, MongoDB, DynamoDB, etc.    |
| **Hosting**   | Cost, scalability, management burden           | AWS, GCP, Azure, Heroku, etc.          |
| **Real-time** | Needed? WebSockets, polling, or cloud service? | Socket.io, GraphQL subscriptions, etc. |

**Third-party Integrations:** Payment processing (Stripe, Square, PayPal), email (SendGrid, Mailgun, AWS SES), analytics (Google Analytics, Mixpanel, custom), storage (AWS S3, GCS, self-hosted), authentication (Auth0, Firebase, custom), monitoring (DataDog, New Relic, Sentry).

#### [HYB] Headless CMS Selection

**Decision Framework:** Content model fit, API (REST/GraphQL, performance, rate limits), editorial workflow/versioning/scheduling, integration capabilities/webhooks, hosting (managed/self-hosted/cost), preview capabilities, API performance at scale, learning curve, pricing transparency.

**Frontend Framework:** Team expertise, performance needs (SSR/SSG/ISR/client-side), scalability, ecosystem (headless CMS libraries), SEO requirements, real-time needs (live updates/webhooks).

**Data Fetching Strategies:**

- **Client-side Fetching:** Simple, but slower initial load
- **Server-side Rendering (SSR):** Fetch on each request; good for dynamic content
- **Static Site Generation (SSG):** Build-time fetching; fast, but needs rebuilds for updates
- **Incremental Static Regeneration (ISR):** Rebuild specific pages on-demand
- **Webhooks:** CMS triggers rebuilds when content changes

**Choice depends on:** Content change frequency, real-time update needs, deployment frequency, number of pages/content items.

**Stack Decision Framework:**

| Decision               | Considerations                                     | Options                            |
| ---------------------- | -------------------------------------------------- | ---------------------------------- |
| **Headless CMS**       | Content model fit, API performance, workflow, cost | Contentful, Sanity, Strapi, etc.   |
| **Frontend Framework** | Performance needs, team skill, ecosystem           | Next.js, Nuxt, Gatsby, Astro, etc. |
| **Data Fetching**      | Update frequency, real-time needs, deployment      | SSG, SSR, ISR, client-side         |
| **Hosting**            | Cost, performance, scalability                     | Vercel, Netlify, AWS, etc.         |

#### Key Trade-offs

- **Speed to Launch vs Long-term Customization:** [CMS] Pre-built themes are fast; custom development is flexible | [APP] Startups use cutting-edge; enterprises use stable
- **Ease of Use vs Power:** [CMS] More user-friendly = fewer advanced features | [APP] Minimal frameworks are flexible; full frameworks are opinionated
- **Cost vs Features:** [CMS] More plugins and customization = higher cost | [APP/HYB] Managed services = operational simplicity; self-hosted = cost savings + control
- **Vendor Lock-in vs Productivity:** [CMS] Popular CMS = large ecosystem but harder to migrate | [APP] Consistency vs Performance: Strong consistency is slower; eventual consistency is faster

---

### Hosting & Infrastructure

#### Resource Requirements

Use the [Application Resource Requirements Checklist](#application-resource-requirements-checklist) to determine hosting tier.

| Tier         | CMS                                             | Custom App                                    | Hybrid                                         |
| ------------ | ----------------------------------------------- | --------------------------------------------- | ---------------------------------------------- |
| **Default**  | <50k visits, static content, standard plugins   | <10k MAU, internal tools, predictable traffic | Static CMS, low updates, SSG frontend          |
| **Moderate** | 50k-500k visits, e-commerce, custom plugins     | 10k-100k MAU, some real-time features         | Dynamic CMS, SSR frontend, moderate API volume |
| **Premium**  | >500k visits, complex queries, multiple editors | >100k MAU, global, strict SLA, real-time data | High-volume API, ISR, complex integrations     |

#### Deployment Environment Options

| Option                               | Pros                                   | Cons                                  | Best For              |
| ------------------------------------ | -------------------------------------- | ------------------------------------- | --------------------- |
| **Managed CMS Hosting**              | Auto-scaling, support, updates handled | Less control, higher cost             | CMS projects          |
| **PaaS (Heroku, Railway)**           | Simple deploy, auto-scaling, support   | Higher cost, less control             | APP rapid iteration   |
| **Containers (Docker/K8s)**          | Portable, scalable, reproducible       | Operational complexity, DevOps needed | APP/HYB multi-env     |
| **Static + CDN (Vercel, Netlify)**   | Simple, fast, cheap, auto-scaling      | Rebuilds needed for updates           | HYB frontend          |
| **Server (Next.js, Nuxt)**           | Real-time updates, dynamic content     | More operational burden               | HYB dynamic content   |
| **Traditional Cloud (EC2, GCP VMs)** | Control, scalability, cost-effective   | Operational burden, manual scaling    | APP established teams |

#### Scaling Considerations

- **Traffic Spikes:** Does hosting auto-scale? What's the trigger and delay?
- **Database Performance:** [CMS] Will database handle peak load? Caching strategy? | [APP] Read replicas? Sharding needs? | [HYB] CMS API performance? Read replicas?
- **CDN Integration:** Should static assets be served from CDN? [HYB] Cache hit rate acceptable?
- **Backup & Recovery:** How often? Automated? Tested? [HYB] Both CMS and frontend backed up?
- **Build Process:** [HYB] Can build process handle large content volumes? Rebuild time acceptable? Webhooks to trigger rebuilds?

#### Migration Considerations [HYB]

If migrating from traditional CMS hosting:

1. **Parallel Infrastructure:** Run old and new systems during transition
2. **DNS Cutover:** When do you switch traffic?
3. **Content Sync:** Ensure old and new systems stay in sync during parallel run
4. **Downtime Planning:** Some migration requires downtime; plan and communicate
5. **Rollback:** Can you quickly revert if something fails?

---

### Performance & Optimization

#### Performance Priorities by Path

| Priority        | CMS                           | Custom App                           | Hybrid                             |
| --------------- | ----------------------------- | ------------------------------------ | ---------------------------------- |
| **Page Load**   | <3s full page load            | <3s initial load, fast interactions  | <3s static, <2s SSG                |
| **API/Backend** | TTFB <600ms                   | API <200ms, DB queries <100ms        | CMS API <200ms                     |
| **Throughput**  | Handle traffic spikes         | Requests/sec, concurrent users       | Rebuild time <10m (SSG)            |
| **Caching**     | Browser/server/CDN cache      | Application-level (Redis), CDN, HTTP | CDN/app cache, cache hit rate >90% |
| **Other**       | Plugin audit, DB optimization | Uptime SLA (99%, 99.9%, 99.99%?)     | TTFB (server-rendered)             |

#### Optimization Targets & Budgets

- **Page Load:** <3 seconds (desktop), <5 seconds (mobile)
- **Core Web Vitals:** LCP <2.5s, FID <100ms, CLS <0.1
- **TTFB:** <600ms [CMS] | <200ms [APP API] | <200ms [HYB CMS API]
- **Asset Size:** Images optimized, code minified
- **API Latency:** [APP] p99 <500ms | [HYB] p99 <500ms
- **Uptime:** [APP] Define SLA (e.g., 99.9% = 43 minutes downtime/month)
- **Rebuild Time:** [HYB] <10 minutes for full site (depends on size)

#### Monitoring Approach

- **Real User Monitoring (RUM):** Google Analytics, Sentry
- **Synthetic Monitoring:** Regular performance tests from multiple locations
- **Application Performance Monitoring (APM):** [APP] DataDog, New Relic, Sentry
- **Database Monitoring:** [APP/HYB] Query performance, slow queries, index usage
- **Infrastructure Monitoring:** [APP] CPU, memory, disk, network, costs
- **Build Monitoring:** [HYB] Rebuild time, success/failure rate
- **Alerting:** Set thresholds; alert when performance degrades
- **Regular Audits:** Monthly performance reviews

#### Performance Optimization Tactics

**Caching:**

- [CMS] Page caching, object caching, database query caching
- [APP] Application-level (Redis), CDN, HTTP caching
- [HYB] CDN and application caching, caching headers and cache invalidation

**Database:**

- [CMS] Optimize queries, remove old revisions/drafts
- [APP] Indexes, query optimization, replication for reads
- [HYB] Database optimization, caching, API efficiency

**Frontend:**

- Code splitting, lazy loading, image optimization, minification
- [HYB] Efficient data fetching (only needed fields)
- [APP] Bundle size monitoring

**API Design:** [APP]

- Pagination, filtering, sparse fieldsets (avoid over-fetching)

**Infrastructure:**

- Right-sized instances, auto-scaling, CDN
- [APP] Profiling to identify bottlenecks before optimizing

**Integration:** [HYB]

- Webhook-triggered rebuilds for content changes
- Incremental Static Regeneration (ISR) for large sites

---

### Project Management & Workflow

#### Team Coordination Structure

**Roles by Path:**

**[CMS]**

- Project Manager, CMS Engineer, Designer, Content Lead, Client Stakeholder

**[APP]**

- Product Manager, Engineering Lead, Frontend Engineer(s), Backend Engineer(s), QA/Testing, Designer, DevOps (if team is large)

**[HYB]** (Two-team model common)

- Content/CMS Team: Content strategist/editor, CMS administrator, PM (content focus)
- Frontend/Engineering Team: Frontend engineers, DevOps/Infrastructure, PM (product focus)
- Shared: Product owner, Designer, QA/Testing

**Communication:**

- Daily stand-ups (brief, async or sync)
- Weekly planning/sync meetings [APP/HYB] | Weekly stand-ups [CMS]
- Bi-weekly demos to stakeholders
- Bi-weekly retrospectives [APP/HYB]
- Async updates on blockers
- Clear decision log

#### Timeline Phases

| Phase           | Lead   | Duration                               | Key Activities                                          | Deliverables                     | Path Notes                    |
| --------------- | ------ | -------------------------------------- | ------------------------------------------------------- | -------------------------------- | ----------------------------- | ----------------------------------------- | -------------------------------------------------------- |
| **Discovery**   | PM     | 1-2w [CMS] / 2-4w [APP/HYB]            | Requirements, platform selection, hosting setup         | Platform selected, hosting live  | [CMS] Content structure       | [APP] Architecture design, MVP definition | [HYB] Content model, CMS + frontend selected             |
| **Design**      | Design | 2-4w                                   | Wireframes/mockups, design system, accessibility review | Approved designs, design system  | [CMS] Admin UI, template list | [APP/HYB] UX research, component library  | [HYB] API contract                                       |
| **Development** | Eng    | 2-6w [CMS] / 6-16w [APP] / 6-12w [HYB] | Platform config, development, integrations, testing     | Staging site, features working   | [CMS] Theme/plugins           | [APP] API/backend/frontend                | [HYB] CMS config, content migration, integration testing |
| **Launch**      | PM     | 1-2w                                   | QA, training, accessibility audit, go-live              | Live site, trained team, runbook | [CMS] Content migration       | [APP] User docs                           | [HYB] Content team training                              |
| **Post-Launch** | PM     | ongoing                                | Monitoring, optimization, handoff                       | Stable site, handoff complete    | All paths                     |

**Total Typical Timeline:** 8-16w [CMS] | 12-32w [APP] | 12-24w [HYB]

> **Client Handoff:** See [Client Handoff Checklist](#client-handoff-checklist) in Section 1.

#### Transition Phase [HYB]

If migrating from traditional CMS, additional phase between Discovery and Design:

1. Infrastructure setup (new CMS deployed, frontend deployment ready)
2. Content migration (automated scripts, manual cleanup)
3. Testing (old vs new system side-by-side)
4. Parallel run (both systems live, synced content)
5. Cutover (switch traffic)
6. Monitoring (watch for issues post-cutover)
7. Cleanup (decommission old system)

#### Risk Management & Mitigation

| Risk                            | Mitigation                                                        | Path    |
| ------------------------------- | ----------------------------------------------------------------- | ------- |
| Content not ready for migration | Start content audit early; assign clear ownership                 | CMS/HYB |
| Scope creep                     | MVP locked [APP]; weekly scope management; formal change requests | All     |
| Performance issues at launch    | Load testing in Phase 3; target metrics established               | All     |
| Untrained staff post-launch     | Training sessions in Phase 4; documentation clear                 | CMS/HYB |
| Plugin conflicts/instability    | Testing in staging; vendor support engaged                        | CMS     |
| Integration delays              | Integration work starts early; APIs vetted                        | All     |
| Team communication breakdown    | Regular syncs, shared documentation, clear interfaces             | HYB     |
| API changes break frontend      | API versioning, contract testing, staged rollouts                 | HYB     |
| Rebuild time unacceptable       | Monitor build times, optimize as needed                           | HYB     |
| Unexpected technical blockers   | Architecture review early; tech spikes for unknowns               | APP     |
| Lack of test coverage           | TDD approach; automated testing required                          | APP     |
| Database scaling issues         | Schema designed for scale; read replicas planned                  | APP     |

#### Communication Checkpoints

- **End of Discovery:** Platform selected, requirements approved, go/no-go decision
- **End of Design:** Design approved, no surprises, timeline reconfirmed | [HYB] API contract finalized
- **Mid-Development:** On track? Blockers? Velocity realistic?
- **Pre-Launch:** All testing complete, team trained, go-live plan finalized | [HYB] Content migrated? Frontend complete?
- **Post-Launch:** Issues resolved? Performance acceptable? | [HYB] Content team productive?

---

### Security Considerations

> **Reference:** See [Baseline Security Questions](#baseline-security-questions) for universal security checklist.

#### Path-Specific Attack Surfaces

**[CMS]**

- Plugin vulnerabilities (outdated plugins are common attack vectors)
- User account compromise (weak passwords, brute force attacks)
- SQL injection (less common in modern CMS but possible with custom code)
- Malware (compromised plugins or themes can inject malware)
- Unauthorized access (user permissions misconfigured)
- Data exposure (sensitive data in backups or logs)

**[APP]**

- Authentication attacks (brute force, phishing, weak password resets)
- API attacks (unauthorized access, injection attacks, rate limiting bypass)
- Data access (unauthorized data access, IDOR)
- Third-party risk (compromised dependencies, supply chain attacks)
- Infrastructure (unpatched servers, misconfigured cloud permissions)
- User data (improper handling, exposure in logs, backups)

**[HYB]**

- API layer (CMS API is a new attack surface; needs protection)
- Content editing (who can edit content? versioning and rollback?)
- Deployment (frontend deployment process; who can deploy?)
- Data sync (ensuring data consistency between CMS and frontend cache)
- Webhooks (CMS->Frontend webhooks; can be misused)
- Dependency risk (both CMS platform and frontend framework have supply chain risk)

#### Security Best Practices

**Universal:**

- Secure by default (security built in, not bolted on)
- Least privilege (users have minimum required access)
- Defense in depth (multiple layers of security)
- Input validation (validate all input; whitelist expected patterns)
- Output encoding (escape output; prevent XSS attacks)
- Dependency management (keep libraries updated; monitor for vulnerabilities)
- Logging & monitoring (log security events; alert on suspicious activity)
- Code review (security-focused code reviews; threat modeling)
- Testing (security testing in QA; penetration testing before launch)
- Documentation (document security architecture and decisions)

**Path-Specific:**

- **[CMS]** Keep everything updated (CMS, plugins, themes, server OS); limited plugin ecosystem; WAF for high-traffic sites
- **[APP]** Authentication/authorization logic reviewed; rate limits on login/API endpoints; infrastructure as code
- **[HYB]** CMS API secured (authentication, rate limiting); webhooks authenticated (signed, validated); secrets not exposed in frontend code

#### Data Handling

- **Customer Data:** Where's it stored? How long? Who has access? [CMS] What data do plugins/integrations access?
- **Encryption:** What data is encrypted? In transit and at rest?
- **Backups:** Encrypted? Stored securely? Access controlled? [HYB] Both CMS and frontend backed up?
- **Compliance:** Document data handling for regulations (GDPR, CCPA, etc.)
- **Data Retention:** Delete data when no longer needed
- **User Rights:** Can users export/delete their data? Implement easily.

---

## Section 4: Path Evolution

### When & Why Projects Evolve

Projects don't always start and stay in one path. Common triggers: growth, competitive pressure, team capability, user experience needs, performance limits, cost optimization, feature requests.

**Evolution Paths:**

| From → To               | Trigger                                | Timeline   | Effort      | Key Risks                                 |
| ----------------------- | -------------------------------------- | ---------- | ----------- | ----------------------------------------- |
| **CMS → Hybrid**        | Custom frontend needed, still need CMS | 2-4 months | Medium-high | Content migration, team training          |
| **CMS → Custom App**    | Complex business logic, real-time data | 3-6 months | High        | Feature parity, data migration            |
| **Hybrid → Custom App** | CMS bottleneck, need full control      | 4-8 months | High        | Maintaining two systems, data consistency |

**Evolution Principles:**

- **Plan:** Don't over-architect (YAGNI), but design for growth; keep systems modular; document business logic
- **Manage:** Parallel operation; plan data migration early; test feature parity; have rollback plan; communicate transition; minimize user disruption
- **Cost-Benefit:** Is evolution worth the cost? Can current path + optimization meet needs? Does new path unlock something fundamental?

---

## Appendix: Red Flag Questions

Consolidated warning signs organized by topic. If you answer "yes" to any of these, pause and reassess.

**Discovery & Requirements:**

- [CMS] Client asking for highly custom page layouts that don't fit template approach?
- [CMS] Complex data relationships that don't align with standard content models?
- [CMS] Performance critical (real-time data, leaderboards, complex queries)?
- [CMS] Team lacks CMS experience but needs to manage it long-term?
- [APP] MVP scope still unclear or expanding?
- [APP] Team lacks experience with this type of application?
- [APP] Critical integrations with uncertain timelines?
- [APP] Data model overly complex?
- [APP] Scalability an afterthought rather than part of initial design?
- [HYB] Headless approach justified, or is it overengineering?
- [HYB] Content team and frontend team isolated (poor communication)?
- [HYB] Content model too simple for a headless approach?
- [HYB] No preview system for content editors?

**Technology Stack:**

- [CMS] Building design from scratch but CMS templates are limited?
- [CMS] Custom data structures that don't fit CMS content model?
- [CMS] Critical integrations unavailable for this platform?
- [CMS] Plugin ecosystem unstable or poorly maintained?
- [APP] Team unfamiliar with chosen stack?
- [APP] Stack overly complex for the problem?
- [APP] Database a poor fit for the data model?
- [APP] Critical integrations unavailable for this stack?
- [APP] Scaling strategy vague or non-existent?
- [APP] Relying on new/unstable libraries?
- [HYB] Content model too fluid for structured headless CMS?
- [HYB] Data fetching strategy vague or problematic?
- [HYB] Migrating from system but no rollback plan?

**Hosting & Infrastructure:**

- Hosting provider not actively maintaining platform version?
- Can't scale quickly during predictable traffic spikes?
- Database performance inadequate for content/traffic volume?
- No documented backup and recovery plan?
- Significant cost jump when outgrowing current tier?
- [APP] Infrastructure not reproducible (IaC)?
- [HYB] CMS API performance inadequate for traffic?
- [HYB] Rebuild time too long for content update frequency?
- [HYB] No CDN for global delivery?
- [HYB] No plan for content sync during migration?

**Performance:**

- Site slower than competitors in same space?
- [CMS] Specific plugins causing performance degradation?
- [CMS] TTFB consistently above 1 second?
- [CMS] Caching not working as expected?
- Core Web Vitals failing?
- [APP] Hitting performance issues unexpectedly in production?
- [APP] Database the bottleneck? Queries/indexes optimized?
- [APP] Frontend bundle size growing unchecked?
- [APP] API responses slow? N+1 query problems?
- [APP] Lack visibility into production performance?
- [HYB] CMS API slow? Benchmarked?
- [HYB] Frontend bundle size growing unchecked?
- [HYB] Cache hit rate low?

**Project Management:**

- [CMS] Content team overwhelmed by CMS learning curve?
- Timelines slipping? Where and why?
- [CMS] CMS team blocking content team progress?
- Critical third-party integrations delayed?
- Performance testing revealing unexpected issues?
- [APP] Scope expanding constantly? MVP in danger?
- [APP] Team velocity declining? Why?
- [APP] Architectural concerns not being addressed?
- [APP] Testing falling behind (technical debt)?
- [APP] Performance issues discovered late?
- [APP] Stakeholder communication breaking down?
- [HYB] Content and frontend teams not communicating effectively?
- [HYB] Content model causing friction between teams?
- [HYB] Migration taking longer than expected?
- [HYB] Rebuild time or API performance blocking progress?
- [HYB] Content team resisting new CMS?

**Security:**

- [CMS] Plugins outdated or no longer maintained?
- No documented backup or disaster recovery plan?
- [CMS] User permissions overly permissive (everyone is admin)?
- Sensitive customer data stored in easy-to-access locations?
- No monitoring or alerting for security issues?
- [APP] App lacks HTTPS/TLS?
- [APP] Passwords not hashed (or hashed with weak algorithms)?
- [APP] No rate limits on login or API endpoints?
- [APP] Authentication/authorization logic not reviewed?
- [APP] Dependencies not monitored for vulnerabilities?
- [APP] Sensitive data stored in logs or error messages?
- [APP] No documented security testing process?
- [APP] Third-party services over-privileged?
- [HYB] CMS API accessible without authentication?
- [HYB] No rate limits on CMS API?
- [HYB] Secrets (API keys) exposed in frontend code?
- [HYB] Webhooks unsigned/unauthenticated?
- [HYB] No logging of CMS API access?

**QA & Testing:**

- No testing strategy documented?
- Test coverage an afterthought?
- Accessibility tests being skipped?
- UAT rushed or skipped?
- Performance tests only run in production?
- No regression testing after bug fixes?

**Path Evolution:**

- Considering evolution due to poor execution vs true growth?
- New path significantly more complex and costly?
- Lack resources to execute the evolution?
- No clear rollback plan if evolution fails?
- Team not trained for new path?

---

## Embedded Resources

### Application Resource Requirements Checklist

**Data & Queries**

- [ ] Static/finite datasets only
- [ ] Dynamic (constantly updated) data
- [ ] Real-time data ingestion
- [ ] Query frequency: on-demand / periodic / continuous

**Traffic**

- [ ] Expected monthly volume
- [ ] Peak concurrent users
- [ ] Spike triggers (emails, seasonal, events)

**Application**

- [ ] % requests requiring DB queries
- [ ] Heavy computations/processing?
- [ ] Concurrent actions?
- [ ] Caching strategy in place?

**Resource Decision**

- [ ] Default hosting
- [ ] Moderate resources
- [ ] Premium resources
- [ ] Auto-scaling needed?

---

### Hosting & Performance Notes

**Dynamic Content Requires Adequate Hosting Resources**

Sites serving dynamic content (real-time leaderboards, live data) need more than default hosting resources.

**Types of Data Queries:**

1. **Static Data** - Pulling from finite, existing datasets (no real-time updates)
2. **Dynamic Data** - Pulling existing data that's constantly being updated
3. **Real-Time Queries** - Ingesting and serving data as it's generated

**Performance Considerations:**

- Traffic spikes and batch requests (e.g., mass emails) can overwhelm underpowered servers
- Multiple concurrent actions compound server load

**Case Study:**

Lambda Legal handled 300k monthly visits at peak traffic with minimal server impact—a high-traffic site that doesn't require dynamic data pulling, demonstrating that traffic volume alone doesn't determine hosting needs.
