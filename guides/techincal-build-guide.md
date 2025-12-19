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
- [CMS Path](#cms-path)
  - [CMS-1: Discovery & Requirements](#cms-1-discovery--requirements)
  - [CMS-2: Technology Stack Selection](#cms-2-technology-stack-selection)
  - [CMS-3: Hosting & Infrastructure](#cms-3-hosting--infrastructure)
  - [CMS-4: Performance & Optimization](#cms-4-performance--optimization)
  - [CMS-5: Project Management & Workflow](#cms-5-project-management--workflow)
  - [CMS-6: Security Considerations](#cms-6-security-considerations)
- [Custom App Path](#custom-app-path)
  - [APP-1: Discovery & Requirements](#app-1-discovery--requirements)
  - [APP-2: Technology Stack Selection](#app-2-technology-stack-selection)
  - [APP-3: Hosting & Infrastructure](#app-3-hosting--infrastructure)
  - [APP-4: Performance & Optimization](#app-4-performance--optimization)
  - [APP-5: Project Management & Workflow](#app-5-project-management--workflow)
  - [APP-6: Security Considerations](#app-6-security-considerations)
- [Hybrid Path](#hybrid-path)
  - [HYB-1: Discovery & Requirements](#hyb-1-discovery--requirements)
  - [HYB-2: Technology Stack Selection](#hyb-2-technology-stack-selection)
  - [HYB-3: Hosting & Infrastructure](#hyb-3-hosting--infrastructure)
  - [HYB-4: Performance & Optimization](#hyb-4-performance--optimization)
  - [HYB-5: Project Management & Workflow](#hyb-5-project-management--workflow)
  - [HYB-6: Security Considerations](#hyb-6-security-considerations)
- [Section 3: Path Evolution Principles](#section-3-path-evolution-principles)
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

## CMS Path

CMS-based projects (WordPress, Webflow, Drupal, etc.) where clients manage content through admin interfaces with predefined templates.

---

### CMS-1: Discovery & Requirements

> **Reference:** See [Baseline Stakeholder Questions](#baseline-stakeholder-questions) for universal questions.

#### CMS-Specific Discovery Questions

- **Content Control:** How much control does the client need? Can templates work, or do they need custom layouts for each page?
- **Content Types:** What types of content? Posts, pages, products, team members, testimonials, events?
- **Editorial Workflow:** Who publishes content? Do you need approval workflows?
- **User Management:** How many content editors? Different permission levels?
- **Content Migration:** Is there existing content? How much needs to migrate?
- **Integrations:** Email marketing, analytics, forms, payment processors?
- **Long-term:** Will the client manage this themselves post-launch, or do you provide ongoing support?

#### Defining Scale & Constraints

- **Audience Size:** Monthly visits? Concurrent users?
- **Content Volume:** How much content? Update frequency?
- **Geographic Scope:** Single region? Global?
- **Device Requirements:** Desktop-first? Mobile-critical?
- **Technical Constraints:** Existing systems to integrate? Budget limits?
- **Team Constraints:** In-house team? Agency? Hybrid?

#### Project Kickoff Checklist: CMS Path

- [ ] **Discovery Complete**

  - [ ] Business goals documented
  - [ ] Success metrics defined (see [Baseline Success Metrics](#baseline-success-metrics))
  - [ ] Audience/scale understood
  - [ ] Budget & timeline confirmed

- [ ] **Content Strategy**

  - [ ] Content types identified
  - [ ] Content structure documented (hierarchy, relationships)
  - [ ] Existing content audit completed (if applicable)
  - [ ] Migration plan (if needed)
  - [ ] Editorial workflow defined
  - [ ] Approval process documented

- [ ] **Team & Access**

  - [ ] Project stakeholders identified
  - [ ] Decision makers confirmed
  - [ ] Content editors/users identified
  - [ ] Permission levels planned

- [ ] **Technical Planning**

  - [ ] CMS platform selected
  - [ ] Hosting plan determined
  - [ ] Third-party integrations mapped
  - [ ] Performance requirements documented
  - [ ] Security requirements documented (see [Baseline Security Questions](#baseline-security-questions))
  - [ ] Accessibility requirements defined (see [Accessibility Requirements](#accessibility-requirements))
  - [ ] Analytics plan documented (see [Analytics & Tracking](#analytics--tracking))

- [ ] **Design & Brand**

  - [ ] Brand guidelines available
  - [ ] Design direction confirmed
  - [ ] Template/page types defined
  - [ ] Design review cadence set

- [ ] **Ongoing Support**
  - [ ] Support model defined (agency-managed vs client-managed)
  - [ ] Training needs identified
  - [ ] Maintenance plan established

#### Red Flag Questions

- Is the client asking for highly custom page layouts that don't fit template approach?
- Does this project have complex data relationships that don't align with standard content models?
- Is performance critical (real-time data, leaderboards, complex queries)?
- Does the team lack CMS experience but need to manage it long-term?
- Are there integrations that are difficult with this CMS platform?

---

### CMS-2: Technology Stack Selection

#### CMS Platform Considerations

**Decision Framework:** Ease of use, content modeling fit, theme/plugin ecosystem, hosting options, scalability, security track record, support availability, cost (license/hosting/plugins/maintenance), long-term viability.

#### Theme/Plugin Ecosystem

- **Pre-built Themes:** Cost-benefit analysis (speed vs customization needs)
- **Plugin Strategy:** Critical vs nice-to-have plugins; vendor lock-in risks
- **Custom Code:** Where's the line between configuration and custom development?
- **Performance:** Do popular plugins add bloat? Are there lightweight alternatives?

#### Hosting Implications

- **Managed vs Self-Hosted:** Trade-offs (support vs control)
- **Scalability:** Can hosting auto-scale during traffic spikes?
- **Backup & Recovery:** What's the backup strategy?
- **CDN:** Is a CDN necessary? Included or additional cost?

#### CMS Stack Decision Framework

| Decision     | Considerations                                    |
| ------------ | ------------------------------------------------- |
| **Platform** | Ease of use, content model fit, ecosystem, cost   |
| **Theme**    | Design fit, customization effort, performance     |
| **Plugins**  | Essential only? Performance impact? Alternatives? |
| **Hosting**  | Managed or self-hosted? Auto-scaling needed?      |
| **Database** | Does CMS include? Performance requirements?       |

#### Key Trade-offs

- **Speed to Launch vs Long-term Customization:** Pre-built themes are fast; custom development is flexible
- **Ease of Use vs Power:** More user-friendly = fewer advanced features
- **Cost vs Features:** More plugins and customization = higher cost
- **Vendor Lock-in vs Productivity:** Popular CMS = large ecosystem but harder to migrate

#### Red Flag Questions

- Are you building the design from scratch but CMS templates are limited?
- Does the project have custom data structures that don't fit the CMS content model?
- Are critical integrations unavailable for this platform?
- Is the plugin ecosystem unstable or poorly maintained?
- Does performance testing show this platform won't scale for your traffic?

---

### CMS-3: Hosting & Infrastructure

#### Resource Requirements

Use the [Application Resource Requirements Checklist](#application-resource-requirements-checklist) to determine hosting tier.

**Quick Assessment:**

- **Default Hosting Sufficient** (low cost)

  - Static content sites, blogs, marketing sites
  - <50k monthly visits
  - No real-time data or complex queries
  - Standard plugin ecosystem

- **Moderate Resources Needed** (medium cost)

  - Dynamic content (regularly updated)
  - 50k-500k monthly visits
  - E-commerce or membership sites
  - Custom plugins or heavy traffic patterns

- **Premium Resources Required** (higher cost)
  - High-traffic sites (>500k monthly visits)
  - Real-time data, heavy database queries
  - Complex integrations
  - Multiple concurrent editors

#### Deployment Environment Options

| Option                                    | Pros                                   | Cons                               | Best For                              |
| ----------------------------------------- | -------------------------------------- | ---------------------------------- | ------------------------------------- |
| **Managed CMS Hosting**                   | Auto-scaling, support, updates handled | Less control, higher cost          | Most CMS projects                     |
| **Traditional Server (Shared/Dedicated)** | Predictable cost, full control         | Manual scaling, maintenance burden | Small sites, cost-conscious           |
| **Container Hosting (Docker)**            | Scalability, consistency               | More complexity, DevOps needed     | Complex setups, multiple environments |
| **Serverless**                            | Auto-scaling, pay-per-use              | Not ideal for traditional CMS      | Rarely used for CMS                   |

#### Scaling Considerations

- **Traffic Spikes:** Does your hosting auto-scale? What's the trigger and delay?
- **Database Performance:** Will your database handle peak load? Caching strategy?
- **CDN Integration:** Should static assets be served from CDN?
- **Backup & Recovery:** How often? Automated? Tested?

#### Red Flag Questions

- Is your hosting provider actively maintaining the platform version you're on?
- Can you scale quickly during predictable traffic spikes (campaigns, launches)?
- Is the database performance adequate for your content volume and traffic?
- Do you have a documented backup and recovery plan?
- Is there a significant cost jump when you outgrow your current tier?

---

### CMS-4: Performance & Optimization

#### CMS-Specific Performance Priorities

Page load time (<3s), TTFB, caching (browser/server/CDN), database query optimization, plugin performance audit, static asset delivery via CDN.

#### Optimization Targets & Budgets

- **Target Page Load:** <3 seconds (desktop), <5 seconds (mobile)
- **Core Web Vitals:** LCP <2.5s, FID <100ms, CLS <0.1
- **TTFB:** <600ms (if possible)
- **Asset Size:** Images optimized, code minified

#### Monitoring Approach

- **Real User Monitoring (RUM):** Tools like Google Analytics, Sentry
- **Synthetic Monitoring:** Regular performance tests from multiple locations
- **Alerting:** Set thresholds; alert when performance degrades
- **Regular Audits:** Monthly performance reviews

#### Performance Optimization Tactics

- **Caching Strategy:** Page caching, object caching, database query caching
- **Image Optimization:** Lazy loading, responsive images, WebP format
- **CDN Usage:** Serve images, CSS, JS from CDN
- **Plugin Audit:** Remove unused plugins; replace heavy ones
- **Database:** Optimize queries, remove old revisions/drafts

#### Red Flag Questions

- Is your site slower than competitors in the same space?
- Are there specific plugins causing performance degradation?
- Is your TTFB consistently above 1 second?
- Is caching not working as expected?
- Are Core Web Vitals failing?

---

### CMS-5: Project Management & Workflow

#### Team Coordination Structure

**Roles:**

- **Project Manager:** Overall timeline, stakeholder communication, scope management
- **CMS Engineer:** Platform setup, customization, integrations, performance
- **Designer:** Theme customization, UX/UI for admin experience, design system
- **Content Lead:** Content strategy, editorial workflow, training
- **Client Stakeholder:** Content decisions, feedback, approvals

**Communication:**

- Weekly stand-ups (Eng, Design, PM)
- Bi-weekly stakeholder reviews
- Async updates on blockers
- Clear decision log

#### Timeline Phases

| Phase           | Lead   | Duration | Key Activities                                                        | Deliverables                                              |
| --------------- | ------ | -------- | --------------------------------------------------------------------- | --------------------------------------------------------- |
| **Discovery**   | PM     | 1-2w     | Requirements, content structure, platform selection, hosting setup    | Content map, CMS selected, hosting live                   |
| **Design**      | Design | 2-4w     | Wireframes/mockups, admin UI, brand integration, accessibility review | Approved designs, design system, template list            |
| **Development** | Eng    | 2-6w     | CMS config, theme/template dev, plugins, integrations, testing setup  | Staging site, integrations complete, performance baseline |
| **Launch**      | PM     | 1-2w     | Content migration, training, QA, accessibility audit, go-live         | Live site, trained staff, runbook                         |
| **Post-Launch** | PM     | ongoing  | Monitoring, support, optimization, maintenance cadence, handoff       | Stable site, optimization roadmap, handoff complete       |

**Total Typical Timeline:** 8-16 weeks (varies widely)

> **Client Handoff:** See [Client Handoff Checklist](#client-handoff-checklist) in Section 1.

#### Risk Management & Mitigation

| Risk                            | Mitigation                                           |
| ------------------------------- | ---------------------------------------------------- |
| Content not ready for migration | Start content audit early; assign clear ownership    |
| Scope creep                     | Weekly scope management; formal change requests      |
| Performance issues at launch    | Performance testing in Phase 3; baseline established |
| Untrained staff post-launch     | Training sessions in Phase 4; documentation clear    |
| Plugin conflicts/instability    | Testing in staging; vendor support engaged           |
| Integration delays              | Integration work starts early; APIs vetted           |

#### Communication Checkpoints

- **End of Discovery:** CMS selected, content map approved, go/no-go decision
- **End of Design:** Design approved, no surprises, timeline reconfirmed
- **Mid-Development:** Progress on schedule? Any blockers?
- **Pre-Launch:** All testing complete, staff trained, go-live plan finalized
- **Post-Launch:** Issues resolved? Performance acceptable? Optimization roadmap clear?

#### Red Flag Questions

- Is the content team overwhelmed by the CMS learning curve?
- Are timelines slipping? Where and why?
- Is the CMS team blocking content team progress?
- Are critical third-party integrations delayed?
- Is performance testing revealing unexpected issues?

---

### CMS-6: Security Considerations

> **Reference:** See [Baseline Security Questions](#baseline-security-questions) for universal security checklist.

#### CMS-Specific Vulnerabilities

- **Plugin Vulnerabilities:** Outdated plugins are common attack vectors
- **User Account Compromise:** Weak passwords, brute force attacks
- **SQL Injection:** (Less common in modern CMS but possible with custom code)
- **Malware:** Compromised plugins or themes can inject malware
- **Unauthorized Access:** User permissions misconfigured
- **Data Exposure:** Sensitive data in backups or logs

#### CMS Security Best Practices

- **Keep Everything Updated:** CMS, plugins, themes, server OS
- **Strong Passwords:** Enforce strong passwords; consider password managers
- **Limited Plugin Ecosystem:** Use only necessary plugins from trusted vendors
- **Regular Backups:** Automated, tested, stored off-site
- **Web Application Firewall (WAF):** Consider WAF for high-traffic sites
- **User Permissions:** Principle of least privilege
- **Monitoring & Logging:** Log security events; alert on suspicious activity
- **Regular Audits:** Security audits annually or after major changes

#### Data Handling for CMS

- **Customer Data:** Where is it stored? How is it protected? Who has access?
- **Backups:** Encrypted? Stored securely? Retention policy?
- **Third-party Access:** What data do plugins/integrations access? Can you limit it?
- **Compliance:** Document data handling for regulations

#### Red Flag Questions

- Are plugins outdated or no longer maintained?
- Is there no documented backup or disaster recovery plan?
- Are user permissions overly permissive (everyone is admin)?
- Is sensitive customer data being stored in easy-to-access locations?
- Is there no monitoring or alerting for security issues?

---

## Custom App Path

Custom web applications with full-stack control, complex business logic, and custom UI/UX requirements.

---

### APP-1: Discovery & Requirements

> **Reference:** See [Baseline Stakeholder Questions](#baseline-stakeholder-questions) for universal questions.

#### Custom App-Specific Discovery Questions

- **MVP Scope:** What's the absolute minimum to launch? What can wait?
- **Core Features:** What 3-5 features define success?
- **Data Model:** What's the data structure? How do entities relate?
- **Scalability:** Will user growth require horizontal scaling? Database scaling?
- **Integrations:** Third-party APIs? Payment processing? Analytics?
- **Performance Requirements:** Real-time? Offline capability? Global? Latency SLAs?
- **Complexity:** Complex business logic? Real-time features? Machine learning?
- **Team Experience:** Has the team built this type of app before?

#### Defining Scale & Constraints

- **User Base:** Expected users? Concurrent active users?
- **Data Volume:** How much data will be stored/processed?
- **Geographic Scope:** Single region? Global? Latency requirements?
- **Device Requirements:** Web, mobile, both? Desktop-first?
- **Technical Constraints:** Legacy systems to integrate? Tech debt to address?
- **Team Constraints:** In-house team? Contract developers? Offshore?

#### Project Kickoff Checklist: Custom App Path

- [ ] **Discovery Complete**

  - [ ] Business goals documented
  - [ ] Success metrics defined (see [Baseline Success Metrics](#baseline-success-metrics))
  - [ ] User research completed
  - [ ] Market analysis done
  - [ ] Budget & timeline confirmed

- [ ] **MVP Definition**

  - [ ] MVP scope locked
  - [ ] Core features (top 3-5) identified
  - [ ] Non-essential features deferred
  - [ ] User stories written
  - [ ] Acceptance criteria defined

- [ ] **Technical Planning**

  - [ ] Data model designed (entities, relationships)
  - [ ] API design sketched
  - [ ] Architecture diagram created
  - [ ] Third-party integrations mapped
  - [ ] Performance requirements documented
  - [ ] Security requirements documented (see [Baseline Security Questions](#baseline-security-questions))
  - [ ] Accessibility requirements defined (see [Accessibility Requirements](#accessibility-requirements))
  - [ ] Analytics plan documented (see [Analytics & Tracking](#analytics--tracking))
  - [ ] Scalability plan sketched

- [ ] **Team & Skills**

  - [ ] Team composition confirmed
  - [ ] Skill gaps identified
  - [ ] Training needs planned
  - [ ] Decision-making structure clear
  - [ ] Tech lead/architect identified

- [ ] **Design & UX**

  - [ ] User personas created
  - [ ] User journeys mapped
  - [ ] Wireframes for core flows
  - [ ] Design system started
  - [ ] Accessibility requirements noted

- [ ] **DevOps & Infrastructure**
  - [ ] Development environment documented
  - [ ] Staging/testing environment planned
  - [ ] Deployment process sketched
  - [ ] Monitoring/logging strategy outlined
  - [ ] CI/CD pipeline planned

#### Red Flag Questions

- Is the MVP scope still unclear or expanding?
- Does the team lack experience with this type of application?
- Are there critical integrations with uncertain timelines?
- Is the data model overly complex?
- Is scalability an afterthought rather than part of initial design?
- Are non-technical stakeholders expecting unlimited scope?

---

### APP-2: Technology Stack Selection

#### Frontend Framework Considerations

**Decision Framework:** Team expertise, project type (SPA/SSR/static/mobile), performance requirements, scalability, ecosystem size, hiring market, maintenance cadence, learning curve, tooling quality.

#### Backend/API Architecture

**Decision Framework:** Language/framework (team expertise, performance, ecosystem), API style (REST/GraphQL/gRPC), authentication (JWT/OAuth/sessions), real-time needs (WebSockets/SSE), background jobs, caching strategy, scalability approach, testing framework.

#### Database Selection

**Decision Framework:** Data type (relational/document/graph/time-series), query patterns, scalability (vertical/horizontal/sharding), consistency requirements, performance needs, operational burden (managed vs self-hosted), cost, backup/recovery criticality.

#### Third-party Integrations

- **Payment Processing:** Stripe, Square, PayPal?
- **Email:** SendGrid, Mailgun, AWS SES?
- **Analytics:** Google Analytics, Mixpanel, custom?
- **Storage:** AWS S3, GCS, or self-hosted?
- **Authentication:** Auth0, Firebase, custom?
- **Monitoring:** DataDog, New Relic, Sentry?

#### Custom App Stack Decision Framework

| Layer         | Considerations                                 | Options                                |
| ------------- | ---------------------------------------------- | -------------------------------------- |
| **Frontend**  | Team skill, performance, ecosystem             | React, Vue, Angular, Svelte, etc.      |
| **Backend**   | Language, performance, team expertise          | Node, Python, Java, Go, Ruby, etc.     |
| **Database**  | Data model, scalability, consistency           | PostgreSQL, MongoDB, DynamoDB, etc.    |
| **Hosting**   | Cost, scalability, management burden           | AWS, GCP, Azure, Heroku, etc.          |
| **Real-time** | Needed? WebSockets, polling, or cloud service? | Socket.io, GraphQL subscriptions, etc. |

#### Key Trade-offs

- **Speed to Launch vs Long-term Maintainability:** Startups use cutting-edge; enterprises use stable
- **Flexibility vs Opinionation:** Minimal frameworks are flexible; full frameworks are opinionated
- **Performance vs Developer Experience:** Sometimes they conflict
- **Managed Services vs Self-hosted:** Managed = operational simplicity; self-hosted = cost savings + control
- **Consistency vs Performance:** Strong consistency is slower; eventual consistency is faster

#### Red Flag Questions

- Is the team unfamiliar with the chosen stack?
- Is the stack overly complex for the problem?
- Is the chosen database a poor fit for the data model?
- Are critical integrations unavailable for this stack?
- Is the scaling strategy vague or non-existent?
- Is the team relying on new/unstable libraries?

---

### APP-3: Hosting & Infrastructure

#### Resource Requirements

Use the [Application Resource Requirements Checklist](#application-resource-requirements-checklist) to determine hosting needs.

**Quick Assessment:**

- **Default Resources Sufficient**

  - Internal tools, low-traffic prototypes
  - <10k monthly active users
  - Predictable, low-spike traffic patterns
  - Single-region deployment

- **Moderate Resources Needed**

  - SaaS products, moderate user base (10k-100k MAU)
  - Moderate traffic spikes
  - Some real-time features
  - Multi-region nice-to-have

- **Premium Resources Required**
  - High-traffic applications (>100k MAU)
  - Real-time data, streaming queries
  - Global multi-region deployment
  - Complex background processing
  - Strict latency requirements

#### Deployment Environment Options

| Option                                      | Pros                                 | Cons                                    | Best For                            |
| ------------------------------------------- | ------------------------------------ | --------------------------------------- | ----------------------------------- |
| **Platform as a Service (Heroku, Railway)** | Simple deploy, auto-scaling, support | Higher cost, less control               | Startups, rapid iteration           |
| **Container (Docker + Kubernetes)**         | Portable, scalable, reproducible     | Operational complexity, learning curve  | Growing apps, multiple environments |
| **Serverless (AWS Lambda, Functions)**      | Pay-per-use, auto-scaling, simple    | Cold starts, complexity, vendor lock-in | Event-driven, variable traffic      |
| **Traditional Cloud (AWS EC2, GCP VMs)**    | Control, scalability, cost-effective | Operational burden, manual scaling      | Established teams, complex apps     |

#### Infrastructure as Code (IaC)

- Use code to define infrastructure (Terraform, CloudFormation, Pulumi)
- Version control your infrastructure
- Reproducible deployments across environments
- Easy to scale and modify

#### Auto-Scaling & Load Balancing

- **Horizontal Scaling:** More instances under a load balancer
- **Vertical Scaling:** Bigger machines (simpler but limits)
- **Auto-scaling Triggers:** CPU, memory, request queue depth, custom metrics
- **Database Scaling:** Replicas for reads, sharding for writes (complex)

#### Backup & Disaster Recovery

- **Backup Strategy:** Automated daily backups, encrypted, tested
- **Recovery Time Objective (RTO):** How fast can you restore?
- **Recovery Point Objective (RPO):** How much data loss is acceptable?
- **Cross-region Backups:** Critical for high-availability apps
- **Disaster Recovery Plan:** Document step-by-step recovery procedures

#### Red Flag Questions

- Is your hosting provider's support adequate for your team?
- Can you scale quickly during traffic spikes?
- Is database performance adequate? Have you load-tested?
- Do you have a documented and tested disaster recovery plan?
- Is your infrastructure reproducible (IaC)?
- Are there significant cost jumps at each scaling tier?

---

### APP-4: Performance & Optimization

#### Custom App-Specific Performance Priorities

API response time (<200ms), frontend load time (<3s), database query time (<100ms), throughput (req/sec), concurrency (simultaneous users), reliability (uptime SLA).

#### Optimization Targets & Budgets

- **API Latency:** p99 <500ms (adjust based on app type)
- **Throughput:** Define based on user base and growth
- **Frontend Load:** <3s page load (SPAs vary)
- **Core Web Vitals:** LCP <2.5s, FID <100ms, CLS <0.1
- **Uptime:** Define SLA (e.g., 99.9% = 43 minutes downtime/month)

#### Monitoring Approach

- **Application Performance Monitoring (APM):** DataDog, New Relic, Sentry
- **Real User Monitoring (RUM):** Understand actual user experience
- **Synthetic Monitoring:** Regular tests from multiple locations
- **Database Monitoring:** Query performance, slow queries, index usage
- **Infrastructure Monitoring:** CPU, memory, disk, network, costs
- **Alerting:** Set thresholds; page on-call for critical issues

#### Performance Optimization Tactics

- **Caching:** Application-level (Redis), CDN, HTTP caching
- **Database:** Indexes, query optimization, replication for reads
- **API Design:** Pagination, filtering, sparse fieldsets (avoid over-fetching)
- **Frontend:** Code splitting, lazy loading, minification, compression
- **Infrastructure:** Right-sized instances, auto-scaling, CDN
- **Profiling:** Identify bottlenecks before optimizing

#### Red Flag Questions

- Are you hitting performance issues unexpectedly in production?
- Is your database the bottleneck? Have you optimized queries/indexes?
- Is your frontend bundle size growing unchecked?
- Are API responses slow? Are there N+1 query problems?
- Do you lack visibility into production performance?
- Is scalability an afterthought rather than part of design?

---

### APP-5: Project Management & Workflow

#### Team Coordination Structure

**Roles:**

- **Product Manager:** Vision, roadmap, prioritization, stakeholder management
- **Engineering Lead:** Technical decisions, architecture, team velocity
- **Frontend Engineer(s):** UI/UX implementation, performance
- **Backend Engineer(s):** API, database, integrations, scaling
- **QA/Testing:** Test automation, quality assurance
- **Designer:** UX/UI, design system, user research
- **DevOps:** Deployment, infrastructure, monitoring (if team is large)

**Communication:**

- Daily stand-ups (brief, async or sync)
- Weekly planning/sync meetings
- Bi-weekly demos to stakeholders
- Retrospectives bi-weekly or monthly
- Async updates on blockers, decisions
- Clear decision log

#### Timeline Phases

| Phase           | Lead   | Duration | Key Activities                                                      | Deliverables                                        |
| --------------- | ------ | -------- | ------------------------------------------------------------------- | --------------------------------------------------- |
| **Discovery**   | PM     | 2-4w     | Requirements, architecture design, team formation, MVP definition   | Architecture doc, MVP user stories, dev environment |
| **Design**      | Design | 2-4w     | UX research, wireframes, design system, accessibility review        | Approved designs, design system, component library  |
| **Development** | Eng    | 6-16w    | MVP features, API/backend, frontend, testing, performance, security | Staging, MVP features, API docs, test coverage      |
| **Launch**      | PM     | 1-2w     | Final QA, docs, training, accessibility audit, go-live              | Live product, docs, trained team                    |
| **Post-Launch** | PM     | ongoing  | Monitoring, bug fixes, feedback, optimization, handoff              | Stable product, roadmap, handoff complete           |

**Total Typical Timeline:** 12-32 weeks (highly variable)

> **Client Handoff:** See [Client Handoff Checklist](#client-handoff-checklist) in Section 1.

#### Risk Management & Mitigation

| Risk                            | Mitigation                                              |
| ------------------------------- | ------------------------------------------------------- |
| Scope creep                     | MVP locked; formal change process; weekly scope reviews |
| Performance issues at launch    | Load testing in Phase 3; target metrics established     |
| Team communication/coordination | Clear roles, daily stand-ups, decision log              |
| Unexpected technical blockers   | Architecture review early; tech spikes for unknowns     |
| Third-party integration delays  | Integration work early; vendors engaged immediately     |
| Lack of test coverage           | TDD approach; automated testing required                |
| Database scaling issues         | Schema designed for scale; read replicas planned        |

#### Communication Checkpoints

- **End of Discovery:** Architecture approved, MVP clear, team ready, go/no-go
- **End of Design:** UX approved, design system ready, no surprises
- **Mid-Development:** On track? Blockers? Velocity realistic?
- **Pre-Launch:** All features complete? Tests passing? Performance acceptable? Go/no-go
- **Post-Launch:** Issues resolved? Performance acceptable? User feedback positive?

#### Red Flag Questions

- Is scope expanding constantly? MVP in danger?
- Is the team velocity declining? Why?
- Are there architectural concerns not being addressed?
- Is testing falling behind (technical debt)?
- Are performance issues being discovered late?
- Is stakeholder communication breaking down?

---

### APP-6: Security Considerations

> **Reference:** See [Baseline Security Questions](#baseline-security-questions) for universal security checklist.

#### Custom App-Specific Attack Surfaces

- **Authentication Attacks:** Brute force, phishing, weak password resets
- **API Attacks:** Unauthorized access, injection attacks, rate limiting bypass
- **Data Access:** Unauthorized data access, IDOR (Insecure Direct Object Reference)
- **Third-party Risk:** Compromised dependencies, supply chain attacks
- **Infrastructure:** Unpatched servers, misconfigured cloud permissions
- **User Data:** Improper handling, exposure in logs, backups

#### Security Best Practices

- **Secure by Default:** Security built in, not bolted on
- **Least Privilege:** Users have minimum required access
- **Defense in Depth:** Multiple layers of security (application, network, infrastructure)
- **Input Validation:** Validate all input; whitelist expected patterns
- **Output Encoding:** Escape output; prevent XSS attacks
- **Dependency Management:** Keep libraries updated; monitor for vulnerabilities
- **Logging & Monitoring:** Log security events; alert on suspicious activity
- **Code Review:** Security-focused code reviews; threat modeling
- **Testing:** Security testing in QA; penetration testing before launch
- **Documentation:** Document security architecture and decisions

#### Data Handling

- **Customer Data:** Where's it stored? How long? Who has access?
- **Encryption:** What data is encrypted? In transit and at rest?
- **Backups:** Encrypted? Stored securely? Access controlled?
- **Compliance:** Document data handling for regulations (GDPR, CCPA, etc.)
- **Data Retention:** Delete data when no longer needed
- **User Rights:** Can users export/delete their data? Implement easily.

#### Red Flag Questions

- Does your app lack HTTPS/TLS?
- Are passwords not hashed (or hashed with weak algorithms)?
- Are there no rate limits on login or API endpoints?
- Is authentication/authorization logic not reviewed?
- Are dependencies not monitored for vulnerabilities?
- Is sensitive data stored in logs or error messages?
- Is there no documented security testing process?
- Are third-party services over-privileged?

---

## Hybrid Path

Projects using a headless CMS with a custom frontend, combining content management flexibility with frontend control.

---

### HYB-1: Discovery & Requirements

> **Reference:** See [Baseline Stakeholder Questions](#baseline-stakeholder-questions) for universal questions.

#### Hybrid-Specific Discovery Questions

- **Why Headless?** What does headless unlock that a traditional CMS doesn't?
- **Content Model:** What content types? How structured?
- **Editorial Workflow:** Who publishes? Approval process? Versioning?
- **Frontend Complexity:** Why custom? What can't be done with CMS themes?
- **Integration Needs:** What connects to what? APIs between systems?
- **Deployment:** Will frontend and backend deploy independently? Frequency?
- **Team Structure:** Separate content/CMS team and frontend team?
- **Future Evolution:** Starting as hybrid, or migrating from something?

#### Defining Scale & Constraints

- **Audience Size:** Monthly visits? Concurrent users?
- **Content Volume:** How much? Update frequency?
- **Traffic Patterns:** Spikes? Seasonal? Predictable?
- **Geographic Scope:** Single region? Global?
- **Device Requirements:** Desktop, mobile, both?
- **Team Constraints:** In-house? Agency? Hybrid?

#### Project Kickoff Checklist: Hybrid Path

- [ ] **Discovery Complete**

  - [ ] Business goals documented
  - [ ] Success metrics defined (see [Baseline Success Metrics](#baseline-success-metrics))
  - [ ] Audience/scale understood
  - [ ] Budget & timeline confirmed
  - [ ] Why headless? (Rationale clear)

- [ ] **Content Strategy**

  - [ ] Content types and structure defined
  - [ ] Content migration plan (if applicable)
  - [ ] Editorial workflow documented
  - [ ] Approval process defined
  - [ ] Team roles (content vs frontend) clear

- [ ] **Headless CMS Selection**

  - [ ] CMS platform chosen
  - [ ] Content model documented
  - [ ] API documented
  - [ ] Integrations mapped
  - [ ] Hosting/deployment planned

- [ ] **Frontend Architecture**

  - [ ] Frontend framework chosen
  - [ ] Data fetching strategy (API calls, SSR, SSG, ISR?)
  - [ ] Deployment strategy
  - [ ] Performance targets set
  - [ ] Design system planned

- [ ] **Integration & Communication**

  - [ ] API contracts defined
  - [ ] Content to frontend flow documented
  - [ ] Preview system planned (see draft content before publish)
  - [ ] Deployment coordination process
  - [ ] Monitoring/alerting across both systems

- [ ] **Team & Access**

  - [ ] Content team access to CMS configured
  - [ ] Frontend team access to repositories/deployments
  - [ ] Communication structure (standups, syncs)
  - [ ] Decision-making process clear
  - [ ] Escalation path for integration issues

- [ ] **Technical Planning**

  - [ ] Security requirements documented (see [Baseline Security Questions](#baseline-security-questions))
  - [ ] Accessibility requirements defined (see [Accessibility Requirements](#accessibility-requirements))
  - [ ] Analytics plan documented (see [Analytics & Tracking](#analytics--tracking))

- [ ] **Migration Plan (if applicable)**
  - [ ] Current system audit
  - [ ] Content migration scripts
  - [ ] Parallel run period (if needed)
  - [ ] Rollback plan

#### Red Flag Questions

- Is the headless approach justified, or is it overengineering?
- Are the content team and frontend team isolated (poor communication)?
- Is the content model too simple for a headless approach?
- Are there critical integrations with uncertain timelines?
- Is frontend deployment independent from content publishing?
- Is there no preview system for content editors?

---

### HYB-2: Technology Stack Selection

#### Headless CMS Selection

**Decision Framework:** Content model fit, API (REST/GraphQL, performance, rate limits), editorial workflow/versioning/scheduling, integration capabilities/webhooks, hosting (managed/self-hosted/cost), preview capabilities, API performance at scale, learning curve, pricing transparency.

#### Frontend Framework Considerations

**Decision Framework:** Team expertise, performance needs (SSR/SSG/ISR/client-side), scalability, ecosystem (headless CMS libraries), SEO requirements, real-time needs (live updates/webhooks).

#### API Layer & Data Fetching

**Strategies:**

- **Client-side Fetching:** Simple, but slower initial load
- **Server-side Rendering (SSR):** Fetch on each request; good for dynamic content
- **Static Site Generation (SSG):** Build-time fetching; fast, but needs rebuilds for updates
- **Incremental Static Regeneration (ISR):** Rebuild specific pages on-demand
- **Webhooks:** CMS triggers rebuilds when content changes

**Choice depends on:**

- How often does content change?
- Do you need real-time updates?
- What's your deployment frequency?
- How many pages/content items?

#### Integration Points

- **Content to Frontend:** How does content get to the frontend? API calls? Build-time data?
- **Frontend to CMS:** User feedback? Comments? Dynamic data back to CMS?
- **Preview System:** Can editors preview changes before publishing?
- **Webhooks:** Should publishing trigger frontend rebuild?

#### Hybrid Stack Decision Framework

| Decision               | Considerations                                     | Options                            |
| ---------------------- | -------------------------------------------------- | ---------------------------------- |
| **Headless CMS**       | Content model fit, API performance, workflow, cost | Contentful, Sanity, Strapi, etc.   |
| **Frontend Framework** | Performance needs, team skill, ecosystem           | Next.js, Nuxt, Gatsby, Astro, etc. |
| **Data Fetching**      | Update frequency, real-time needs, deployment      | SSG, SSR, ISR, client-side         |
| **Hosting**            | Cost, performance, scalability                     | Vercel, Netlify, AWS, etc.         |

#### Migration Considerations: CMS to Headless

**If you're migrating from traditional CMS:**

1. **Content Audit:** What content exists? Audit for quality and structure.
2. **Content Modeling:** Redesign content model for headless (may be more structured).
3. **Migration Scripts:** Automated migration from old to new CMS.
4. **Parallel Run:** Run both systems in parallel; test thoroughly before cutover.
5. **Rollback Plan:** If headless launch fails, can you revert quickly?
6. **Team Training:** New CMS interface? New frontend deployment? Team needs training.
7. **Testing:** Content works in both systems? API returns correct data?

#### Key Trade-offs

- **CMS Flexibility vs Simplicity:** Headless CMSes are often more powerful but less user-friendly
- **Frontend Freedom vs Complexity:** Custom frontend = more control but more to maintain
- **Real-time vs Performance:** Real-time updates need more infrastructure; static is fast but stale
- **Team Split vs Coordination:** Separate teams move faster but need good communication

#### Red Flag Questions

- Is the headless approach overengineering this project?
- Is the content model too fluid for a structured headless CMS?
- Are frontend and CMS teams siloed with poor communication?
- Is the data fetching strategy vague or problematic?
- Is there no preview system for content editors?
- Are you migrating from a system but no rollback plan?

---

### HYB-3: Hosting & Infrastructure

#### Resource Requirements

Use the [Application Resource Requirements Checklist](#application-resource-requirements-checklist) to determine needs for each layer.

**Quick Assessment:**

- **Backend (CMS) Resources:**

  - Static content, moderate updates → default hosting
  - Dynamic content, high volume → moderate to premium resources

- **Frontend Resources:**
  - Static site generation → CDN + low compute (cheap)
  - Server-side rendering → moderate compute needed
  - Many pages → scalable hosting needed

#### Deployment Environment: Backend (CMS)

- **Managed Headless CMS:** Support, scaling, updates handled
- **Self-hosted:** More control, more operational burden

#### Deployment Environment: Frontend

| Option                                     | Pros                                       | Cons                           | Best For                          |
| ------------------------------------------ | ------------------------------------------ | ------------------------------ | --------------------------------- |
| **Static Hosting + CDN (Vercel, Netlify)** | Simple, fast, cheap, auto-scaling          | Rebuilds needed for updates    | Most headless sites               |
| **Server (Next.js, Nuxt)**                 | Real-time updates, dynamic content         | More operational burden        | Dynamic content, personalization  |
| **Hybrid (ISR)**                           | Fast initial load, updates without rebuild | Complexity, cache invalidation | Large sites with frequent updates |

#### Scaling Considerations: Backend

- Can the CMS API handle your traffic?
- Do you need read replicas for the database?
- Is caching in place (Redis, CDN)?

#### Scaling Considerations: Frontend

- Does your CDN auto-scale?
- Can your build process handle large content volumes?
- Is rebuild time acceptable?
- Do you need webhooks to trigger rebuilds?

#### Migration Considerations: Hosting

**If you're migrating from traditional CMS hosting:**

1. **Parallel Infrastructure:** Run old and new systems during transition
2. **DNS Cutover:** When do you switch traffic?
3. **Content Sync:** Ensure old and new systems stay in sync during parallel run
4. **Downtime Planning:** Some migration requires downtime; plan and communicate
5. **Rollback:** Can you quickly revert if something fails?

#### Red Flag Questions

- Is CMS API performance adequate for your traffic?
- Is rebuild time too long for your content update frequency?
- Do you lack a CDN for global delivery?
- Is there no plan for content sync during migration?
- Are scaling limits unclear or problematic?

---

### HYB-4: Performance & Optimization

#### Hybrid-Specific Performance Priorities

CMS API performance (<200ms), frontend load time (<3s static, <2s SSG), TTFB (server-rendered), rebuild time (<10m for SSG), cache hit rate (CDN/app).

#### Optimization Targets & Budgets

- **API Latency:** p99 <500ms
- **Frontend Load:** <3s (SSG much faster)
- **Core Web Vitals:** LCP <2.5s, FID <100ms, CLS <0.1
- **Rebuild Time:** <10 minutes for full site (depends on size)
- **Cache Hit Rate:** >90% for static assets

#### Monitoring Approach

- **CMS Monitoring:** API response time, query performance
- **Frontend Monitoring:** Page load, Core Web Vitals, user experience
- **CDN Monitoring:** Cache hit rate, edge performance
- **Build Monitoring:** Rebuild time, success/failure rate
- **Alerting:** Performance degradation, failed builds

#### Performance Optimization Tactics

**Backend (CMS):**

- Database optimization, caching, API efficiency

**Frontend:**

- Code splitting, lazy loading, image optimization, minification
- Efficient data fetching (only needed fields)
- CDN for all static assets

**Integration:**

- Webhook-triggered rebuilds for content changes
- Incremental Static Regeneration (ISR) for large sites
- Caching headers and cache invalidation

#### Red Flag Questions

- Is CMS API slow? Have you benchmarked it?
- Is rebuild time unacceptably long?
- Is the frontend bundle size growing unchecked?
- Is there no CDN, or is cache hit rate low?
- Are Core Web Vitals failing?

---

### HYB-5: Project Management & Workflow

#### Team Coordination Structure

**Two-Team Model (common for hybrid):**

**Content/CMS Team:**

- Content strategist/editor
- CMS administrator
- PM (content focus)

**Frontend/Engineering Team:**

- Frontend engineers
- DevOps/Infrastructure
- PM (product focus)

**Shared Roles:**

- Product owner (overall vision)
- Designer (UX/content presentation)
- QA/Testing

**Communication:**

- Daily stand-ups (brief, async preferred)
- Weekly sync (CMS team + frontend team)
- Bi-weekly demos to stakeholders
- Bi-weekly retrospectives
- Clear decision log and escalation path

#### Timeline Phases

| Phase           | Lead   | Duration | Key Activities                                                    | Deliverables                                       |
| --------------- | ------ | -------- | ----------------------------------------------------------------- | -------------------------------------------------- |
| **Discovery**   | PM     | 2-4w     | Requirements, content model, CMS selection, frontend architecture | Content model, CMS selected, frontend architecture |
| **Design**      | Design | 2-4w     | Content structure, UX/UI design, design system, API contract      | Approved designs, content model in CMS, API docs   |
| **Development** | Eng    | 6-12w    | CMS config, content migration, frontend dev, integration testing  | Staging site, content populated, features working  |
| **Launch**      | PM     | 1-2w     | QA, content team training, docs, accessibility audit, go-live     | Live site, trained team, runbook                   |
| **Post-Launch** | PM     | ongoing  | Monitoring, content updates, frontend iterations, handoff         | Stable site, handoff complete                      |

**Total Typical Timeline:** 12-24 weeks

#### Transition Phase (if migrating from CMS)

**Additional phase between Discovery and Design:**

1. **Infrastructure Setup:** New CMS deployed, frontend deployment process ready
2. **Content Migration:** Automated migration scripts, manual cleanup
3. **Testing:** Old system vs new system side-by-side
4. **Parallel Run:** Both systems live; synced content
5. **Cutover:** Switch traffic to new system
6. **Monitoring:** Watch for issues post-cutover
7. **Cleanup:** Decommission old system

> **Client Handoff:** See [Client Handoff Checklist](#client-handoff-checklist) in Section 1.

#### Risk Management & Mitigation

| Risk                                               | Mitigation                                            |
| -------------------------------------------------- | ----------------------------------------------------- |
| Team communication breakdown (content vs frontend) | Regular syncs, shared documentation, clear interfaces |
| Content not ready for migration                    | Early content audit, migration scripts, testing       |
| API changes break frontend                         | API versioning, contract testing, staged rollouts     |
| Rebuild time unacceptable                          | Monitor build times, optimize as needed               |
| Performance issues at launch                       | Load testing, performance budgets, monitoring         |
| Content team frustrated with new CMS               | Training, documentation, support                      |

#### Communication Checkpoints

- **End of Discovery:** Content model approved, CMS + frontend selected, go/no-go
- **End of Design:** API contract finalized, design approved, no surprises
- **Mid-Development:** Teams on track? Integration issues? Blockers?
- **Pre-Launch:** Content migrated? Frontend complete? Performance acceptable? Go/no-go
- **Post-Launch:** Performance good? Content team productive? Issues addressed?

#### Transition Checkpoints (if migrating)

- **Infrastructure Ready:** New systems deployed and tested
- **Migration Scripts:** Content migrated successfully; testing passed
- **Parallel Run:** Both systems live and synced; confidence high
- **Cutover:** Traffic switched; monitoring active
- **Post-Cutover:** Issues resolved, rollback unnecessary

#### Red Flag Questions

- Are the content and frontend teams not communicating effectively?
- Is the content model causing friction between teams?
- Is the migration taking longer than expected?
- Is rebuild time or API performance blocking progress?
- Is the content team resisting the new CMS?

---

### HYB-6: Security Considerations

> **Reference:** See [Baseline Security Questions](#baseline-security-questions) for universal security checklist.

#### Hybrid-Specific Security Concerns

- **API Layer:** CMS API is a new attack surface; needs protection
- **Content Editing:** Who can edit content? Versioning and rollback?
- **Deployment:** Frontend deployment process; who can deploy?
- **Data Sync:** Ensuring data consistency between CMS and frontend cache
- **Webhooks:** CMS->Frontend webhooks; can be misused
- **Dependency Risk:** Both CMS platform and frontend framework have supply chain risk

#### Security Best Practices

**CMS Layer:**

- Keep CMS updated
- Limit API access (authentication, rate limiting)
- Backup content regularly
- Monitor API access

**Frontend Layer:**

- Keep dependencies updated
- Don't expose secrets (API keys, tokens)
- Use HTTPS/TLS
- Validate all input

**Integration:**

- Authenticate webhooks (signed, validated)
- Encrypt data in transit
- Log all API calls
- Monitor for suspicious activity

#### Data Handling

- **Content Data:** Where's it stored (CMS)? Who has access?
- **User Data:** If users can comment/contribute, how's it protected?
- **Backups:** CMS content backed up? Accessible if needed?
- **Compliance:** Document how content and user data are handled

#### Red Flag Questions

- Is the CMS API accessible without authentication?
- Are there no rate limits on the CMS API?
- Are secrets (API keys) exposed in frontend code?
- Is there no backup or disaster recovery plan for content?
- Are webhooks unsigned/unauthenticated?
- Is there no logging of CMS API access?

---

## Section 3: Path Evolution Principles

### When & Why Projects Evolve Between Paths

Projects don't always start and stay in one path. As businesses grow and requirements change, the technical approach often needs to evolve.

**Common Evolution Triggers:**

1. **Growth:** More content, more users, more features -> more complexity needed
2. **Competitive Pressure:** New features require custom development
3. **Team Capability:** Team grows; can now handle more complex solutions
4. **User Experience:** Needs exceed what platform can deliver
5. **Performance:** Outgrown platform limits; need custom infrastructure
6. **Cost:** Initial choice too expensive; need to optimize
7. **Feature Requests:** Users want features that don't fit the platform

---

### CMS -> Hybrid Evolution

**Trigger:** Client wants custom frontend/branding but still needs CMS for content management

**Evolution Path:**

1. Choose headless CMS (may export data from old CMS)
2. Build frontend application
3. Migrate content to new CMS
4. Deploy frontend separately
5. Decommission old CMS (or phase out)

**Timeline:** 2-4 months  
**Effort:** Medium-high  
**Key Risks:** Content migration, team training, parallel operations

---

### CMS -> Custom App Evolution

**Trigger:** What started as a content site now has complex business logic, real-time data, or user interactions

**Evolution Path:**

1. Assess why CMS is insufficient (performance? features? architecture?)
2. Design custom app architecture
3. Build custom app alongside CMS
4. Migrate data/users to new app
5. Retire old CMS

**Timeline:** 3-6 months  
**Effort:** High  
**Key Risks:** Feature parity, data migration, user confusion during transition

---

### Hybrid -> Custom App Evolution

**Trigger:** CMS becomes bottleneck; need full control over content and data

**Evolution Path:**

1. Evaluate whether full custom app is necessary (or just custom backend?)
2. Design custom system
3. Build in parallel with hybrid system
4. Migrate content and users
5. Retire headless CMS (may keep for some content)

**Timeline:** 4-8 months  
**Effort:** High  
**Key Risks:** Maintaining two systems, data consistency

---

### General Evolution Principles

**Plan for Evolution:**

- Don't over-architect for features you don't have yet (YAGNI)
- But design with future growth in mind
- Keep systems modular; easier to replace components
- Document business logic and data models
- Keep an audit of what features you have

**Managing Evolution:**

- **Parallel Operation:** Run old and new systems together briefly
- **Data Migration:** Plan early; automate where possible
- **Testing:** Test feature parity and performance before cutover
- **Rollback Plan:** Can you quickly revert if needed?
- **Team Communication:** Everyone understands the transition
- **Minimize Disruption:** Users don't notice the transition

**Cost-Benefit Analysis:**

- Is evolution worth the cost?
- Can you meet user needs with current path plus optimization?
- Or does new path fundamentally unlock something?

---

### Red Flag Questions

- Are you considering evolution due to poor execution vs true growth?
- Is the new path significantly more complex and costly?
- Do you lack resources to execute the evolution?
- Is there a clear rollback plan if evolution fails?
- Is the team trained for the new path?

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
