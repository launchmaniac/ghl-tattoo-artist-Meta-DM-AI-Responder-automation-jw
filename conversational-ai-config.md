# GHL Conversational AI Configuration - Tattoo Artist Meta (Instagram/Facebook) DM Automation

**Project Template:** Light conversation AI with artist handoff for tattoo booking inquiries
**Platforms:** Instagram DM + Facebook Messenger
**Goal:** Answer basic questions, gather qualifying info (2-3 messages), then hand off to artist for booking

**Artist-Specific Info:** See `artist-config.md` for client details

---

## Testing Workflow (IMPORTANT - Do This First!)

**Discovery (Dec 22, 2025):** GHL has standalone "AI Agents" feature for testing Conversational AI without creating workflows or connecting FB/Instagram.

### How to Test Conv AI Before Deploying to Workflows:

1. **Create AI Agent** (in GHL: Settings → AI & Integrations → AI Agents)
   - Name: "Tattoo Bot Test"
   - Add Conversational AI configuration (Personality, Instructions, Questions)
   - NEW: Set human handover rules (GHL recent update)

2. **Test Responses Directly in GHL**
   - No need to connect FB/Instagram
   - No need to create workflows
   - Test conversations in GHL interface
   - Iterate on prompts quickly (2-3 min per iteration vs. 15-20 min)

3. **Refine Until Satisfied**
   - Test booking intent recognition
   - Test handoff behavior
   - Test tone and personality
   - Test edge cases

4. **Deploy to Workflows**
   - Copy final configuration to FB Messenger workflow
   - Copy to Instagram DM workflow
   - Activate and test in real platform

**Time Savings:** 80% reduction in testing iterations

**NEW GHL FEATURE:**
- AI Agents now support human handover with custom rules
- Can set specific conditions for when to hand over to human
- More control than workflow-based handoff

---

## Conversational AI Settings

### Response Limit: **3 messages**
### Timeout: **24 hours**
### Wait Time: **10 seconds**

---

## Section 1: Personality (About You)

**Character count:** 289/300

```
You are a booking assistant for [ARTIST_NAME], a professional tattoo artist. You handle initial questions and gather basic info before connecting people with them.

YOUR ROLE:
- Answer simple questions about tattoo styles
- Ask qualifying questions (size, placement, reference images)
- Keep conversations brief (2-3 messages max)
- Stay silent when you have enough info for [ARTIST_NAME]

STAY SILENT (no response) WHEN:
- Customer wants to book or schedule
- You've gathered size + placement info
- After you've sent 3 messages
- Anything you're unsure about

[ARTIST_NAME] will be notified automatically and will jump in.
```

**Template Variables:**
- `[ARTIST_NAME]` - Replace with artist's first name

---

## Section 2: Additional Instructions

**Character count:** 298/300

```
Keep responses under 30 words. Friendly, casual tone (use :) when it feels right). One question at a time.

SILENT HANDOFF:
After 3 messages - stay silent.
Booking requests - stay silent immediately.
After gathering size + placement - stay silent.
Artist takes over automatically.

QUALIFYING QUESTIONS TO ASK:
"What size are you thinking?"
"Where do you want it placed?"
"Do you have any reference images or ideas in mind?"

DON'T:
Give specific prices. Book appointments. Promise dates. Discuss technical details. Send links. Say "I don't know."

TIME-WASTERS:
If timeline too far out: "No worries! Feel free to reach back out if anything changes."
```

---

## Section 3: Questions

**Character count:** 267/300

```
Q: What brings you in today?

Q: What kind of work do you do?
A: A bit of everything! Realism, color work, black and grey, traditional. Check out the page to get a better idea:)

Q: How far out are you booking?
A: We're currently booking for [AVAILABLE_MONTH]. If that still works, we can get an exact date set up.

Q: How much does it cost?
A: It depends on size and placement - can you tell me a bit more about what you're wanting and where?

Q: What size are you thinking?

Q: Where do you want it placed?

Q: Do you have reference images or a specific style in mind?
```

**Template Variables:**
- `[AVAILABLE_MONTH]` - Replace with current booking month (e.g., "March 2025")

---

## Branches Configuration

### Branch 1: No Condition Met
**Status:** Leave empty - AI continues conversation naturally

### Branch 2: Timeout (24 hours no response)
**Actions:**
1. Send Message: "Hey! Still interested in booking? Feel free to reach out anytime:)"
2. Add Tag: "Conversation Timeout"

---

## Workflow Structure

### Two Separate Workflows (Instagram + Facebook)

#### Workflow 1: Instagram DM Handler
```
[TRIGGER: Customer Replied - FB Messenger]
  ↓
[FILTER: Reply Channel = Instagram DM]
  ↓
[TAG: Instagram Lead]
  ↓
[CONVERSATIONAL AI]
  ├─ No condition met → Continue
  └─ Timeout → Check-in message + tag
  ↓
[WAIT: 10 seconds]
  ↓
[IF/ELSE: Keyword Detection - See below]
```

#### Workflow 2: Facebook Messenger Handler
```
[TRIGGER: Customer Replied - FB Messenger]
  ↓
[FILTER: Reply Channel = Facebook Messenger OR no filter]
  ↓
[TAG: Facebook Lead]
  ↓
[CONVERSATIONAL AI] (same config as Instagram)
  ↓
[WAIT: 10 seconds]
  ↓
[IF/ELSE: Keyword Detection - See below]
```

---

## If/Else Workflow Configuration (After Wait Action)

**Add Action:** IF/ELSE (Build My Own)

All conditions below are configured as separate branches within ONE If/Else action.

---

### Branch 1: Direct Booking Intent

**Condition Setup (OR logic):**
- Field: Contact → Last Message
- Operator: Contains
- Values (add as separate rows with OR):
  - `i want to book`
  - `can i book`
  - `book me`
  - `schedule me`
  - `set up appointment`
  - `get me in`
  - `when can i come in`
  - `set up a time`
  - `ready to book`
  - `let's book`

**Actions for This Branch:**
1. Send SMS to `[ARTIST_PHONE]`:
   ```
   🔔 BOOKING REQUEST

   From: {{contact.full_name}}
   Platform: [Instagram/Facebook]

   Message: "{{contact.last_message}}"

   Open [Instagram/Facebook] DMs NOW
   ```
2. Add Tag: `Artist Takeover - Booking`

---

### Branch 2: Design Details Provided

**Condition Setup (OR logic):**
- Field: Contact → Last Message
- Operator: Contains
- Values:
  - `full sleeve`
  - `half sleeve`
  - `quarter sleeve`
  - `full back`
  - `chest piece`
  - `forearm`
  - `upper arm`
  - `thigh`
  - `calf`
  - `reference image`
  - `reference pic`
  - `I can send`
  - `here's what`
  - `realistic style`
  - `traditional style`
  - `color work`
  - `black and grey`

**Actions for This Branch:**
1. Send SMS to `[ARTIST_PHONE]`:
   ```
   ✅ QUALIFIED LEAD

   From: {{contact.full_name}}
   Platform: [Instagram/Facebook]

   Details: "{{contact.last_message}}"

   Open [Instagram/Facebook] DMs - ready for quote
   ```
2. Add Tag: `Artist Takeover - Design Details`

---

### Branch 3: Availability Question

**Condition Setup (OR logic):**
- Field: Contact → Last Message
- Operator: Contains
- Values:
  - `when are you booking`
  - `how far out`
  - `what's your availability`
  - `when can you`
  - `do you have openings`
  - `how booked are you`

**Actions for This Branch:**
1. Add Tag: `Asked-Availability`
   - (No SMS - AI responds with calendar info)

---

### Branch 4: Confirmed After Availability

**Condition Setup (AND logic):**
- Row 1: Contact → Has Tag → `Asked-Availability`
- AND
- Row 2: Contact → Last Message → Contains (OR for multiple):
  - `yes`
  - `yeah`
  - `that works`
  - `sure`
  - `let's do it`
  - `sounds good`
  - `perfect`
  - `ok`
  - `okay`
  - `I'm down`
  - `interested`

**Actions for This Branch:**
1. Send SMS to `[ARTIST_PHONE]`:
   ```
   📅 BOOKING CONFIRMED

   From: {{contact.full_name}}
   Platform: [Instagram/Facebook]

   Timeline works: "{{contact.last_message}}"

   Open [Instagram/Facebook] DMs to schedule
   ```
2. Remove Tag: `Asked-Availability`
3. Add Tag: `Artist Takeover - Booking Confirmed`

---

### Branch 5: Pricing Question

**Condition Setup (OR logic):**
- Field: Contact → Last Message
- Operator: Contains
- Values:
  - `how much`
  - `what's the cost`
  - `price`
  - `pricing`
  - `what do you charge`
  - `cost for`
  - `how much would`

**Actions for This Branch:**
1. Add Tag: `Awaiting-Pricing-Details`
   - (No SMS - AI responds with qualifying questions)

---

### Branch 6: Replied After Pricing Question

**Condition Setup:**
- Field: Contact → Has Tag → `Awaiting-Pricing-Details`

**Actions for This Branch:**
1. Send SMS to `[ARTIST_PHONE]`:
   ```
   💰 PRICING FOLLOW-UP

   From: {{contact.full_name}}
   Platform: [Instagram/Facebook]

   Details: "{{contact.last_message}}"

   Open [Instagram/Facebook] DMs - ready for quote
   ```
2. Remove Tag: `Awaiting-Pricing-Details`
3. Add Tag: `Artist Takeover - Pricing`

---

### None Branch (Auto-Created)

**What This Means:** AI handled the conversation, no artist intervention needed.

**No actions required for this branch.**

---

## Template Variables Reference

All artist-specific information should be stored in `artist-config.md` file.

**Variables to replace when implementing:**
- `[ARTIST_NAME]` - Artist's first name (used in Personality section)
- `[ARTIST_PHONE]` - Artist's SMS number (used in all SMS actions)
- `[AVAILABLE_MONTH]` - Current booking month (used in Questions section)
- `[Instagram/Facebook]` - Platform name (used in SMS messages for clarity)

---

## Testing Scenarios

### Test 1: Basic Question
- Message: "What kind of work do you do?"
- Expected: AI responds with style list + directs to Instagram page
- Tag: Instagram Lead or Facebook Lead

### Test 2: Booking Request
- Message: "I want to book an appointment"
- Expected: AI stays silent, SMS sent to artist
- Tag: Artist Takeover - Booking

### Test 3: Design Question with Details
- Message: "Can you do a realistic half sleeve on my forearm?"
- Expected: AI may ask qualifying questions, then SMS sent to artist
- Tag: Artist Takeover - Design Details

### Test 4: Availability Question → Confirmation
- Message 1: "How far out are you booking?"
- Expected: AI responds with [AVAILABLE_MONTH], tag added
- Message 2: "That works for me"
- Expected: SMS sent to artist
- Tag: Artist Takeover - Booking Confirmed

### Test 5: Pricing Question → Details
- Message 1: "How much does a sleeve cost?"
- Expected: AI asks for size/placement details
- Message 2: "Full sleeve on my left arm"
- Expected: SMS sent to artist with both messages
- Tag: Artist Takeover - Pricing

### Test 6: Timeout
- Message AI, wait 24 hours without responding
- Expected: Check-in message sent automatically
- Tag: Conversation Timeout

---

## Implementation Checklist

1. ✅ Create `artist-config.md` with client-specific info
2. ✅ Replace all template variables in config sections
3. ⏳ Build Instagram workflow in GHL
4. ⏳ Build Facebook workflow in GHL (duplicate + change filters)
5. ⏳ Test all scenarios in Agency OS
6. ⏳ Deploy to artist sub-account when working

---

## GHL Support Documentation References

**Core Workflow Actions:**
- [If/Else Workflow Action](https://help.gohighlevel.com/support/solutions/articles/155000002471-workflow-action-if-else)
- [Send SMS Action](https://help.gohighlevel.com/support/solutions/articles/155000002474-workflow-action-send-sms)
- [Getting Started with Workflows](https://help.gohighlevel.com/support/solutions/articles/155000002288-getting-started-with-workflows)
- [Workflow Action List](https://help.gohighlevel.com/support/solutions/articles/155000002294-what-are-workflow-actions-complete-list-)

**Conversational AI:**
- [Setting Up Conversation AI](https://help.gohighlevel.com/support/solutions/articles/155000004401-setting-up-conversation-ai)
- [Conversation AI Action in Workflows](https://help.gohighlevel.com/support/solutions/articles/155000001358-workflow-x-conversation-ai-conversation-ai-action-beta)
- [Trigger a Workflow within Conversation AI](https://help.gohighlevel.com/support/solutions/articles/155000004098-trigger-a-workflow-within-conversation-ai)
- [AI Conversational Appointment Booking](https://help.gohighlevel.com/support/solutions/articles/48001216782-ai-conversational-appointment-booking-workflow-and-setup)

**Instagram/Facebook Automation:**
- [Instagram DM Workflow Action](https://help.gohighlevel.com/support/solutions/articles/155000003298-instagram-dm-workflow-action)
- [Instagram Interactive Messenger](https://help.gohighlevel.com/support/solutions/articles/155000004662-workflow-action-instagram-interactive-messenger)
- [Facebook Interactive Messenger](https://help.gohighlevel.com/support/solutions/articles/155000004661-workflow-action-facebook-interactive-messenger)
- [Facebook & Instagram Comment/DM Automation Guide](https://help.gohighlevel.com/support/solutions/articles/155000002055-guide-to-facebook-instagram-comment-automation-ai)
- [Comment Automation FAQs](https://help.gohighlevel.com/support/solutions/articles/155000002180-facebook-instagram-comment-automation-faqs)

**Workflow Triggers:**
- [Customer Replied Trigger](https://help.gohighlevel.com/support/solutions/articles/155000002677-workflow-trigger-customer-replied)
- [Understanding Workflow Behavior with SMS and Customer Replies](https://help.gohighlevel.com/support/solutions/articles/155000002475-understanding-workflow-behaviour-with-sms-and-customer-replies)

---

## Notes

- AI instructed to stay silent instead of verbal handoff for natural flow
- Artist too busy to manually follow up, so automated check-in after timeout
- 3-message limit filters tire-kickers while keeping artist in loop
- Separate workflows for Instagram vs Facebook for clarity and tracking
- Response limit (3 messages) is enforced by GHL Conversational AI automatically - no additional SMS trigger needed
