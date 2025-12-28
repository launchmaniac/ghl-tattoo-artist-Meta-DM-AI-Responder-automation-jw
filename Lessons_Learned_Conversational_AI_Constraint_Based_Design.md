# Lessons Learned - Conversational AI Constraint-Based Design

**Project:** GHL Tattoo Artist Meta DM Automation
**Date Discovered:** 2025-12-27
**Component:** Conversational AI configuration (FB Messenger + Instagram DM)
**Discovery Type:** Design Framework
**Reusability:** High - Applicable to all conversational AI implementations

---

## Problem Statement

Building Conversational AI that stays within defined boundaries while remaining helpful. AIs naturally default to being "helpful" which causes overreach - responding when they shouldn't, asking multiple questions at once, repeating questions, and failing to hand off cleanly to humans.

---

## Root Cause

**AI Default Behavior:** Conversational AI models are trained to be maximally helpful, which conflicts with constrained use cases like pre-screening assistants that should:
- Ask minimal questions
- Hand off quickly
- Not overreach into artist's domain

**Traditional approach fails:** Telling AI "what to do" doesn't prevent overreach. Must explicitly define "what NOT to do."

---

## Discovery Process

**Testing Method:** AI Agents feature in GHL (standalone testing without workflows)

**Iteration Process:**
1. Built initial "helpful" AI configuration
2. Tested with real conversation scenarios
3. Identified specific failure patterns
4. Added explicit constraints
5. Re-tested until behavior matched requirements

**Key Insight:** Every refinement came from actual conversations showing AI breaking rules. Testing revealed all failure modes.

---

## Framework: Constraint-Based Design

**Core Principle:** Tell AI what NOT to do more than what to do. Constrain first, optimize second. AI needs guardrails more than freedom.

---

## Key Refinements (9 Discoveries)

### 1. One Question at a Time (Hard Rule)

**Problem:** AI naturally asks compound questions
- Example: "What size are you thinking and where do you want it placed?"

**Why It Fails:** Humans hate compound questions. Causes decision paralysis or incomplete answers.

**Solution:** Explicit instruction: "One question at a time. Never ask multiple things in one message."

**Impact:** Cleaner conversation flow, better response quality

---

### 2. Explicit Trigger Phrases Over AI Inference

**Problem:** AI tries to guess when user wants to book or connect with artist

**Why It Fails:** AI inference is unreliable. Creates false positives/negatives.

**Solution:** Tell users explicit trigger phrases
- "Say 'get Tony' to connect with the artist"
- "Reply 'book' when ready to schedule"

**Why It Works:** User-initiated actions > AI guessing intent. Users have control.

**Impact:** Zero false handoffs, users know exactly how to escalate

---

### 3. Stop After Handoff Is Hard (Requires Explicit Instruction)

**Problem:** AI wants to respond to polite messages after handoff
- User: "Thank you!"
- AI: "You're welcome! Let me know if you need anything else!" (WRONG - already handed off)

**Why It Fails:** Politeness is deeply trained into AI behavior

**Solution:** Explicit instruction: "Do not respond after handoff. Stay completely silent after artist takeover."

**Implementation:** Added to "STAY SILENT WHEN" section in Personality

**Impact:** Clean handoff with no AI interference after artist takes over

---

### 4. State Timeline, Don't Ask

**Problem:** Open-ended questions waste time
- Bad: "When do you want to come in?"
- Users give vague answers: "Soon," "Next month," "ASAP"

**Solution:** State timeline upfront with yes/no confirmation
- Good: "We're booked 6-8 weeks out, does that work?"

**Why It Works:** Filters early. Tire-kickers self-select out. Serious clients confirm immediately.

**Impact:** Reduced back-and-forth, faster qualification

---

### 5. Context Awareness Is Fragile (Needs Constant Reinforcement)

**Problem:** AI forgets what user already said
- User: "I want a dragon on my right arm"
- AI: "What are you thinking about getting?" (Already answered)
- AI: "Where do you want it placed?" (Already answered)

**Solution:** Explicit instruction: "If they said 'dragon on right arm' you know WHAT and WHERE - don't ask again."

**Why It's Hard:** AI context window is limited, needs explicit reminders not to repeat questions

**Impact:** Less frustrating user experience, faster conversations

---

### 6. Returning Clients Need Zero Friction

**Problem:** Returning clients forced through same screening questions as new clients

**Why It Fails:** Kills experience. Loyal clients expect VIP treatment, not interrogation.

**Solution:** Immediate handoff for returning clients (non-negotiable)
- Check contact history
- If previous booking exists → silent handoff immediately
- Add tag: "Returning Client - Priority"

**Impact:** Preserves relationship with existing clients, shows respect for loyalty

**Note:** Requires contact history tracking in GHL

---

### 7. GHL Custom Values Broken for Multi-Tenant Use

**Problem:** Tried to use custom values for artist name (e.g., `{{custom_values.artist_name}}`)

**Why It Fails:** GHL custom values don't work as expected for dynamic artist names in templates

**Workaround for MVP:** Hardcoded "Tony" for pilot launch

**Long-term Solution:** Geoffrey's SDK will handle variable replacement for artist name when deploying template to multiple clients

**Action Items:**
- Document for Geoffrey: Need variable replacement for artist name
- Must work across multiple sub-accounts
- Template should swap hardcoded values automatically

---

### 8. Test Reveals All (No Shortcuts)

**Discovery:** Every refinement came from actual conversations showing AI breaking rules

**What This Means:**
- Can't design Conversational AI from theory alone
- Must test with real scenarios
- Each test reveals new failure modes
- Iterate until behavior matches requirements

**Testing Workflow:**
1. Use AI Agents for fast iteration (2-3 min per test)
2. Test edge cases: polite users, impatient users, returning clients, tire-kickers
3. Document each failure pattern
4. Add explicit constraint
5. Re-test to confirm fix

**Time Savings:** AI Agents testing = 80% faster than workflow testing

---

### 9. Human Handoff Action Requires Scenario Toggle (GHL Configuration)

**Problem:** Added human handoff action to workflow but it wasn't triggering

**Why It Fails:** GHL requires explicit scenario toggle to activate human handoff action. Not obvious in UI.

**Solution:** Toggle ON the scenario for human handoff action in workflow settings

**How to Fix:**
1. Open workflow with human handoff action
2. Find the human handoff action node
3. Toggle ON the scenario (enable the handoff scenario)
4. Save workflow

**Why This Matters:** Human handoff won't work at all without this toggle. Silent failure - workflow runs but handoff never triggers.

**Impact:** Critical for testing and deployment. Easy to miss during workflow build.

**Prevention:** Add to workflow deployment checklist - always verify scenario toggle is ON for human handoff actions.

---

## Implementation Checklist

**For Current Project (Tony Raz MVP):**
- [x] Add "one question at a time" rule
- [x] Define explicit trigger phrases for handoff
- [x] Add "stay silent after handoff" instruction
- [x] State timeline upfront (6-8 weeks)
- [x] Add context awareness reminders
- [x] Implement returning client check (if GHL supports)
- [x] Hardcode "Tony" for pilot (artist name must be hardcoded)
- [x] Toggle ON scenario for human handoff action
- [x] Test all scenarios in AI Agents before deployment

---

## Constraint-Based Design Framework (Reusable)

**When building any Conversational AI:**

1. **Define boundaries first**
   - What should AI NOT do?
   - When should AI stay silent?
   - What's outside AI's domain?

2. **Add explicit constraints**
   - One question per message
   - Stay silent after handoff
   - Don't repeat questions
   - State facts, don't ask open questions

3. **Test with real scenarios**
   - Use AI Agents for fast iteration
   - Test edge cases
   - Document every failure
   - Add constraints as needed

4. **User-initiated actions > AI inference**
   - Give users explicit trigger phrases
   - Don't guess intent
   - Let users escalate when ready

5. **Constrain first, optimize second**
   - Start with strict rules
   - Loosen only if needed
   - AI needs guardrails more than freedom

---

## Technical Implementation Details

**Files Modified:**
- conversational-ai-config.md (Personality, Instructions, Questions sections)

**GHL Configuration:**
- Response Limit: 3 messages (enforced by GHL)
- Timeout: 24 hours
- Wait Time: 10 seconds

**Personality Section Changes:**
```
STAY SILENT (no response) WHEN:
- Customer wants to book or schedule
- You've gathered size + placement info
- After you've sent 3 messages
- Anything you're unsure about
```

**Instructions Section Changes:**
```
Keep responses under 30 words. One question at a time.

SILENT HANDOFF:
After 3 messages - stay silent.
Booking requests - stay silent immediately.
After gathering size + placement - stay silent.
```

---

## Impact & Results

**Time Savings:**
- AI Agents testing: 80% reduction in iteration time (15-20 min → 2-3 min)
- Faster deployment to production

**Conversation Quality:**
- Cleaner handoffs (AI stops when it should)
- Less user frustration (one question at a time)
- Better qualification (timeline stated upfront)
- Fewer repeated questions (context awareness)

**Scalability:**
- Framework applicable to all future Conv AI implementations
- Template ready for multi-artist deployment (pending SDK work)

---

## Prevention (How to Avoid This in Future)

**For Future Conversational AI Projects:**

1. **Start with Constraint-Based Framework**
   - Use this document as template
   - Define "what NOT to do" before "what to do"
   - Copy constraint list from this implementation

2. **Always Test in AI Agents First**
   - Never deploy to workflows without AI Agents testing
   - Test all edge cases before going live
   - Document failures as you find them

3. **Add to Template Checklist**
   - Include constraint-based design in AI-Context-Workspace-Template
   - Make it standard practice for all Conv AI work

---

## GHL Custom Values Limitation

**Technical Constraint:** GHL Agent builder only allows for business name to be included in custom values (CV's). Artist name has to be hardcoded to get system operational.

**Current Implementation:** Hardcoded "Tony" in Personality and Instructions sections.

**Impact:** Each artist deployment requires manual find/replace of artist name in configuration.

---

## Tags

`[discovery]` `[framework]` `[conversational-ai]` `[constraint-based-design]` `[reusable]` `[high-impact]` `[template]` `[ghl-limitation]`

---

## Related Documentation

- **Workspace:** GHL-Tattoo-Automation-WORKSPACE.md (Decision Log, Dec 27 entry)
- **Technical Config:** conversational-ai-config.md (implementation details)
- **Session Notes:** Session_Notes_20251222_Template_System_and_AI_Agents_Discovery.md
- **Template:** Lessons-Learned-Template.md (format used)

---

**Product of Launch Maniac LLC, Las Vegas, Nevada**
**(725) 444-8200 | support@launchmaniac.com**
