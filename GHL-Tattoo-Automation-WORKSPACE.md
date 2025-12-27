# GHL Tattoo Automation - Project Workspace

**Purpose:** Single source of truth for AI-assisted GHL Tattoo Artist automation work. Designed for session continuity and context efficiency.

**Companion Docs:** [artist-config.md](./artist-config.md), [conversational-ai-config.md](./conversational-ai-config.md), [workflow-build-notes.md](./workflow-build-notes.md)

**Update Frequency:** Daily to weekly (especially "This Week" section)

**Last Updated:** 2025-12-27

---

## Project: GHL Tattoo Artist Meta DM Automation + Booking System

**Status:** 🟡 Active Development
**Start Date:** 2024-12-14
**Target Launch:** 2025-12-20 (Tony Raz - First Client)
**Current Phase:** Testing & Validation

---

## Quick Links

**Project Management:**
- **ClickUp List:** https://app.clickup.com/9017265590/v/l/li/901708663844

**Code & Deployment:**
- **Repository:** https://github.com/launchmaniac/ghl-tattoo-artist-Meta-DM-AI-Responder-automation-jw
- **Build Environment:** Agency OS (testing), Launch Maniac account (testing)

**Documentation:**
- **Activity Log (Google Doc):** https://docs.google.com/document/d/1YiVnq9Uy5wDDi8VaBB0XwJgOIBxaZR--Cm8_CA6GfnY/edit
- **A2P Messaging Templates:** https://docs.google.com/document/d/1FItAQ6nWEIGGVPukbHmhHxb3sBts6CmSwLe-SJ4EI7c/edit
- **Technical Configs:** artist-config.md, conversational-ai-config.md, workflow-build-notes.md

**Other:**
- **Tony's GHL Sub-Account:** Tony Raz Tattoo

---

## ClickUp Integration Configuration

**Sync Status:** 🟢 Synced

**Configuration:**
- **Workspace ID:** `9017265590`
- **List ID:** `901708663844` - GHL Tattoo Automation
- **List URL:** https://app.clickup.com/9017265590/v/l/li/901708663844

**Epic Links:**
| Epic | ID | Priority | Status | URL |
|------|----|----------|--------|-----|
| PROJECT OVERVIEW | 86dyx3nrq | - | Reference | https://app.clickup.com/t/86dyx3nrq |
| EPIC 1: Booking Workflow | 86dyw209r | High | Complete | https://app.clickup.com/t/86dyw209r |
| EPIC 2: A2P Registration | 86dyw21x4 | Urgent | In Progress | https://app.clickup.com/t/86dyw21x4 |
| EPIC 3: Meta DM Responder | 86dyw250q | High | In Progress | https://app.clickup.com/t/86dyw250q |

**Last Synced:** 2025-12-22

**ClickUp MCP Reference:** `C:\Users\Launch Maniac\.claude\ClickUp-MCP-Reference.md`

---

## Project Snapshot

### What We're Building

Building a reusable GHL automation template for tattoo artists to handle Instagram/Facebook DM pre-screening and booking reminders. Tony Raz (Seattle tattoo artist) is first client for MVP validation. **Product goal:** Template we can sell to other tattoo artists.

**MVP Philosophy:**
- Assist, don't replace (Tony stays in control)
- DM pre-screening only (3 messages max, then Tony takes over)
- Manual booking (Tony picks time slots, system sends reminders)
- Test what works before automating more

### Tech Stack Summary

- **Primary Platform:** GoHighLevel (Workflows, Conversational AI, SMS, FB/Instagram Integration)
- **Database:** GHL Contacts (tags, custom fields)
- **Integrations:** Facebook Messenger, Instagram DM, Google Calendar, SMS (A2P)
- **Hosting:** GHL Cloud (SaaS platform)
- **Version Control:** GitHub (documentation and config templates)

**For full technical details:** See workflow-build-notes.md, conversational-ai-config.md

---

## Current Phase

- [x] 🎯 Discovery & Planning
- [x] 🏗️ MVP Development
- [x] 🚀 Feature Development
- [ ] 🧪 Testing & Validation (IN PROGRESS)
- [ ] ✅ Production Ready
- [ ] 📈 Live & Iterating

**Phase Description:** FB + Instagram workflows built and connected. Conversational AI refinement in progress. Booking workflow complete. Tony's calendar and socials connected (Dec 20). Waiting for A2P approval to enable SMS.

---

## This Week: Dec 22-29, 2025

**Week Focus:** Finalize Conversational AI using AI Agents, test all workflows end-to-end, evaluate Comment Responder. **ALL DUE: Monday Dec 29 EOD**

### In Progress

- [ ] **Test Booking Workflow End-to-End** `CU-ID: 86dyz5362`
  - **Description:** Test complete booking workflow now that Tony's calendar is connected
  - **Status:** Ready to test
  - **Priority:** High
  - **Due Date:** 2025-12-29 (Monday EOD)
  - **Blocker:** None (can test workflow logic before A2P approval)

- [ ] **Evaluate Comment Responder** `CU-ID: 86dyz536m`
  - **Description:** Research GHL's built-in Comment Responder feature for FB/Instagram posts. Possibly build simple version if worthwhile.
  - **Status:** Not started
  - **Priority:** High
  - **Due Date:** 2025-12-29 (Monday EOD)
  - **Blocker:** None
  - **Notes:** May add simple Comment Responder build if evaluation shows value

### Completed This Week

- [x] **Finalize Conversational AI for FB + Instagram** - Dec 27, 2025
  - **What Was Done:** Tested and refined Conv AI configuration in standalone AI Agent, then deployed to Facebook Messenger workflow
  - **Outcome:** Conversational AI working successfully for booking intent recognition and natural handoff behavior
  - **Time Savings:** 80% faster testing iterations using AI Agents feature
  - **Notes:** Applied same configuration to Instagram DM workflow. Both platforms ready for production use.

- [x] **Tony's Calendar + Socials Connected** - Dec 20, 2025
  - **What Was Done:** Connected Tony's Google Calendar, Facebook Page, and Instagram to GHL during Friday meeting
  - **Outcome:** All integrations ready for workflow testing
  - **Notes:** Used "Connected Assets" method in Meta Business Suite (documented in FB_Instagram_Integration_Process_DRAFT.md)

- [x] **Instagram DM "Allow Re-Entry" Discovery** - Dec 22, 2025
  - **What Was Done:** Troubleshot Instagram DM workflow trigger issue
  - **Outcome:** Discovered workflow setting "Allow Re-Entry" must be toggled ON for Conversational AI to handle multiple messages
  - **Learnings:** Default setting prevents workflow from triggering multiple times per contact
  - **Documented:** ClickUp task comment on 86dyw26eg

### Completed Previously

- [x] **A2P Registration Submitted** - Dec 17, 2025
  - **What Was Done:** Completed A2P sole proprietor registration for Tony
  - **Outcome:** Application submitted, identity verification link sent to Tony, waiting 3-7 days for approval
  - **Cost:** $40 upfront ($25 A2P + $15 domain: TonyRazTattoo.com)
  - **Learnings:** Privacy Policy + Terms of Service required, domain purchase mandatory for funnel pages

- [x] **Privacy Policy + Terms of Service Templates** - Dec 17, 2025
  - **What Was Done:** Created reusable templates with SMS-specific consent language
  - **Outcome:** Templates deployed to Tony's account, reusable for future clients
  - **Time Logged:** 52 min total

- [x] **FB Messenger Workflow** - Dec 16, 2025
  - **What Was Done:** Built and tested FB Messenger DM auto-responder with Conversational AI
  - **Outcome:** Working successfully, tested in Launch Maniac account
  - **Learnings:** Must use FB/Instagram Integration section (NOT Social Media section)
  - **Time Logged:** 12 min (after 9h troubleshooting in previous session)

- [x] **Booking Workflow** - Dec 16, 2025
  - **What Was Done:** Built simplified booking reminder workflow (5-day + 24-hour SMS reminders)
  - **Outcome:** Ready to activate once A2P approved
  - **Time Logged:** 1h 25min

### Blockers

**🚨 Critical Blockers:**
- **Waiting for A2P Approval** (Dec 17 submission)
  - **Impact:** Cannot activate SMS reminders or purchase phone number
  - **Needed to Unblock:** 3-7 day approval window (expected by Dec 24)
  - **Status:** Waiting

**No other blockers** ✅

---

## Backlog (Next Up)

**Priority order (top to bottom):**

1. [ ] **Purchase GHL Phone Number** `CU-ID: TBD`
   - **Why Critical:** Required after A2P approval to enable SMS functionality
   - **Estimated Effort:** 15 minutes
   - **Dependencies:** A2P approval
   - **Target Date:** Immediately after A2P approval

2. [ ] **Activate All Workflows in Tony's Account**
   - **Why Critical:** Deploy to production once A2P approved
   - **Estimated Effort:** 30 minutes
   - **Dependencies:** A2P approval, phone number purchased
   - **Target Date:** Same day as A2P approval

3. [ ] **Create 4 Group Calendars**
   - **Why Critical:** Per GHL support recommendation - separate booking links for different session durations
   - **Estimated Effort:** 30 minutes
   - **Target Date:** Before Tony starts using system
   - **Details:** Consultation (30min), 2hr, 4hr, 8hr sessions

4. [ ] **Monitor Tony's Usage for 2 Weeks**
   - **Why Critical:** Validate MVP assumptions, collect feedback for v2
   - **Estimated Effort:** Ongoing monitoring
   - **Target Date:** 2 weeks after activation

### Ideas Parking Lot

- Self-service booking (test demand after Tony uses system for a month)
- Deposit payment automation (Tony handles manually, revisit if requested)
- Multi-artist support (if tattoo shop has multiple artists)

---

## Decision Log

### Dec 27, 2025 - Constraint-Based Design Framework for Conversational AI

**Context:**
Building Conversational AI that stays within boundaries while remaining helpful. Traditional approach of telling AI "what to do" doesn't prevent overreach.

**Discovery:** Constraint-based design framework - tell AI what NOT to do more than what to do

**Framework Established:**
1. One question at a time (hard rule)
2. Explicit trigger phrases over AI inference
3. Stop after handoff requires explicit instruction
4. State timeline, don't ask open questions
5. Context awareness needs constant reinforcement
6. Returning clients need zero friction
7. Test reveals all failure modes

**Key Insight:** "Constrain first, optimize second. AI needs guardrails more than freedom."

**Implementation:**
- Tested all scenarios in AI Agents
- Added explicit constraints to Personality and Instructions sections
- Defined "STAY SILENT" conditions clearly
- Hardcoded "Tony" for MVP (variable replacement needed for scaling)

**Impact:**
- Cleaner handoffs (AI stops when it should)
- Better user experience (one question at a time)
- Faster qualification (timeline stated upfront)
- Template ready for scaling with Geoffrey's SDK

**For Geoffrey's SDK:**
- Variable replacement for artist name
- Proper stop-after-handoff enforcement
- Template exactly, just swap hardcoded values

**Documented:** Lessons_Learned_Conversational_AI_Constraint_Based_Design.md (comprehensive framework)

---

### Dec 22, 2025 - AI Agents for Testing (Workflow Optimization)

**Context:**
Testing Conversational AI in workflows requires creating full workflow, connecting FB/Instagram, and sending actual messages. Slow and cumbersome for refining AI responses.

**Discovery:** GHL has standalone "AI Agents" feature for testing Conv AI

**Options Considered:**
1. **Test in workflows** - Full integration but 15-20 min per iteration
2. **Use AI Agents** - Standalone testing, 2-3 min per iteration (CHOSEN)

**Decision Made:** Test Conv AI in AI Agents before deploying to workflows

**Rationale:**
- AI Agents allow testing Conv AI without workflows or platform connections
- Much faster iteration (80% time savings)
- NEW GHL FEATURE: AI Agents now support human handover with custom rules
- More control over testing edge cases

**Implementation:**
1. Create AI Agent in GHL (Settings → AI & Integrations → AI Agents)
2. Test and refine Conv AI configuration
3. Once satisfied, copy to FB Messenger + Instagram workflows
4. Documented testing workflow in conversational-ai-config.md

**Impact:** Significantly faster Conv AI refinement process for all future projects

**Documented:** conversational-ai-config.md, ClickUp task 86dyw2549

---

### Dec 22, 2025 - Instagram "Allow Re-Entry" Setting

**Context:**
Instagram DM workflow wasn't triggering correctly when customers sent messages.

**Decision Made:** Toggle ON "Allow Re-Entry" in workflow settings

**Rationale:**
- Without this setting, workflow only triggers once per contact
- Conversational AI needs to handle multiple message exchanges
- Default setting prevents proper conversation flow

**Implementation:** Updated workflow setting in GHL

**Impact:** Instagram DM workflow now functions correctly for multi-message conversations

**Documented:** ClickUp comment on task 86dyw26eg

---

### Dec 20, 2025 - Tony Onboarding Complete

**Context:**
Friday meeting to connect Tony's accounts and introduce system.

**Decision Made:** Connected calendar + socials, built website demo

**Rationale:**
- All integrations needed before workflow activation
- Website gives Tony something tangible to review

**Implementation:**
- Google Calendar connected via OAuth
- FB + Instagram connected via Meta Business Suite "Connected Assets"
- Website created using Claude

**Impact:** All technical prerequisites for activation complete

---

### Dec 17, 2025 - Domain Purchase Required for A2P

**Context:**
A2P funnel pages wouldn't go live after snapshot push. Discovered domain requirement.

**Options Considered:**
1. **Free GHL subdomain** - Doesn't exist (confirmed by GHL support)
2. **Purchase domain** - Required ($13-15/year)

**Decision Made:** Purchase domain for each client

**Rationale:**
- No free alternative exists
- Domain ownership good for client
- Can ask clients upfront if they already have domain (saves $15)

**Implementation:**
- Purchased TonyRazTattoo.com ($13)
- Add to onboarding checklist for future clients
- Include $40 upfront in pricing ($25 A2P + $15 domain)

**Impact:** All future clients need domain purchase budgeted

**Documented:** Session notes, ClickUp EPIC 2 comments

---

### Dec 16, 2025 - MVP Scope: Assist, Don't Replace

**Context:**
Tony currently 100% paper-based, concerned about losing personal touch.

**Options Considered:**
1. **Full automation (self-service booking)** - Maximum time savings but higher risk
2. **Assisted automation (DM pre-screening + manual booking)** - Tony stays in control (CHOSEN)

**Decision Made:** Assisted automation MVP

**Rationale:**
- Tony wants to transition online BUT stay in control
- DM pre-screening (3 messages max) filters tire-kickers
- Manual booking means Tony picks time slots
- Test system with real usage before adding complexity

**Implementation:**
- Conv AI responds max 3 messages, then Tony gets SMS alert
- Tony manually books in calendar, system sends reminders
- NO self-service booking in MVP
- NO deposit automation in MVP

**Impact:**
- Simplified workflows (1h 25min to build vs. 4+ hours)
- Tony gets SMS alerts to stay in loop
- Focus on time-saving, not full automation

**Documented:** PROJECT OVERVIEW (86dyx3nrq), workflow-build-notes.md

---

### Dec 16, 2025 - Calendar Structure: 4 Group Calendars

**Context:**
Tony needs different session lengths (consultation, 2hr, 4hr, 8hr). Unclear if GHL could handle with one calendar.

**Options Considered:**
1. **One calendar with multiple durations** - GHL support said not recommended
2. **4 separate Group Calendars** - Clean separation (CHOSEN)

**Decision Made:** Create 4 separate Group Calendars

**Rationale:**
- GHL support explicitly recommended this approach
- Each calendar gets unique booking link
- Tony sends appropriate link based on tattoo discussed
- All sync to his one Google Calendar

**Implementation:**
- Create during setup: Consultation (30min), 2hr, 4hr, 8hr
- Generate booking links for each
- All sync to Tony's Google Calendar

**Impact:** Tony can send specific booking link without manual duration selection

**Documented:** workflow-build-notes.md

---

## Session Context for AI

### Current Work Context

**Active Task:** Finalizing Conversational AI for FB + Instagram workflows

**Files Currently Modified:**
- conversational-ai-config.md - Refining prompts for natural handoff

**Recent Changes:**
- Dec 22: Instagram "Allow Re-Entry" toggle discovered and enabled
- Dec 20: Tony's calendar + socials connected
- Dec 17: A2P submitted, waiting for approval

### Open Questions

- [ ] Should Comment Responder be included in MVP or v2?
- [ ] What's the ideal Conv AI response tone? (testing in progress)

---

## Notes & Scratchpad

**Week Planning:**
- Mon-Wed: Finalize Conv AI
- Thu: Test booking workflow
- Fri-Sat: Evaluate Comment Responder
- Ongoing: Wait for A2P approval (expected by Dec 24)

**Success Metrics to Track After Launch:**
1. Tony manually responds to <30% of DMs
2. Zero no-shows after implementing booking reminders
3. Template reusable for 5+ other tattoo artists without major changes

---

## Metadata

**Document Information:**
- **Created:** 2025-12-14
- **Last Updated:** 2025-12-27
- **Updated By:** AI + User
- **Next Review:** Daily during active development

**Related Documents:**
- Session Notes: /session-notes/ folder
- Technical Configs: artist-config.md, conversational-ai-config.md, workflow-build-notes.md
- ClickUp MCP Reference: `C:\Users\Launch Maniac\.claude\ClickUp-MCP-Reference.md`

---

**Product of Launch Maniac LLC, Las Vegas, Nevada**
**(725) 444-8200 | support@launchmaniac.com**
