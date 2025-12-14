# GHL Workflow Build Notes - Meta DM Automation

**Last Updated:** December 14, 2024
**Status:** Building Facebook Messenger workflow in Agency OS

---

## Critical Discovery: Platform Separation Architecture

### Problem Identified
- **Issue:** Cannot determine message source (Instagram vs Facebook) in SMS notifications to artist
- **Initial Assumption:** One workflow with conditional branching could handle both platforms
- **Reality:** GHL doesn't expose platform detection variables (like `{{contact.reply_channel}}`) after trigger fires

### Solution: Two Separate Workflows

**Decision:** Build completely separate workflows for Instagram DM and Facebook Messenger

**Rationale:**
1. Reply Channel filter only available at trigger level
2. No runtime variables to detect platform in SMS actions
3. Hardcoded platform names in SMS required for artist clarity
4. Modular architecture cleaner than complex branching

### Build Order Strategy
1. ✅ Configure Conversational AI (platform-agnostic)
2. 🔄 Build Facebook Messenger workflow first (currently in progress)
3. ⏳ Test Facebook workflow thoroughly
4. ⏳ Duplicate workflow for Instagram
5. ⏳ Change Reply Channel filter to "Instagram DM"
6. ⏳ Update tags from "Facebook Lead" to "Instagram Lead"
7. ⏳ Update SMS platform references from "Facebook" to "Instagram"

---

## Current Build Progress (Facebook Messenger Workflow)

**Completed:**
- ✅ Trigger: Customer Replied - FB Messenger
- ✅ Conversational AI configuration deployed
- ✅ Planning and architecture design

**In Progress:**
- 🔄 Reply Channel Filter configuration
- 🔄 Tag Action setup
- 🔄 Wait action (10 seconds)
- 🔄 If/Else branch configuration

**Pending:**
- ⏳ 6 If/Else branches with keyword detection
- ⏳ SMS notification actions
- ⏳ Tag management actions
- ⏳ Testing and validation

---

## Frameworks Applied

### Adjacent Possible (Stuart Kauffman)
- Customer Replied trigger opens channel-specific automation
- No workflow duplication needed - leverage modular design
- Each platform workflow evolves independently if logic diverges

### Modular Architecture
- Two lean workflows > one complex branching workflow
- Separation beneficial when logic differs significantly by platform
- Maintenance trade-off: 2x workflows vs complex conditional logic

### Learning Loops
- Document which approach works better during testing
- Becomes part of reusable GHL playbook
- Capture lessons for future Meta automation projects

---

## Workflow Architecture

### Facebook Messenger Workflow
```
[TRIGGER: Customer Replied - FB Messenger]
  ↓
[FILTER: Reply Channel = Facebook Messenger OR no filter]
  ↓
[TAG: Facebook Lead]
  ↓
[CONVERSATIONAL AI]
  ├─ Branch 1: No condition met → Continue
  └─ Branch 2: Timeout (24h) → Check-in message + tag
  ↓
[WAIT: 10 seconds]
  ↓
[IF/ELSE: 6 Branches]
  ├─ Branch 1: Direct Booking Intent → SMS + Tag
  ├─ Branch 2: Design Details → SMS + Tag
  ├─ Branch 3: Availability Question → Tag only
  ├─ Branch 4: Confirmed After Availability → SMS + Tag swap
  ├─ Branch 5: Pricing Question → Tag only
  ├─ Branch 6: Replied After Pricing → SMS + Tag swap
  └─ None: AI handled, no intervention needed
```

### Instagram DM Workflow (Duplicate)
```
[TRIGGER: Customer Replied - FB Messenger]
  ↓
[FILTER: Reply Channel = Instagram DM]
  ↓
[TAG: Instagram Lead]
  ↓
[CONVERSATIONAL AI] (same config)
  ↓
[WAIT: 10 seconds]
  ↓
[IF/ELSE: 6 Branches] (same logic, different platform refs in SMS)
```

---

## Technical Validation Needed

**Assumptions requiring testing:**
1. ✅ Facebook + Instagram use same Meta API (confirmed: both use FB Messenger trigger)
2. ❓ Reply Channel filter correctly separates platforms at trigger level
3. ❓ Conversational AI response limit (3 messages) enforced automatically
4. ❓ Tag-based state management works across If/Else branches
5. ❓ SMS formatting displays correctly on mobile (emojis, line breaks)

**GHL Documentation Consulted:**
- Customer Replied Trigger behavior
- If/Else workflow action
- Reply Channel filter options
- FB/Instagram Interactive Messenger actions

---

## Next Steps

**Immediate (Today):**
1. Review screenshot of current workflow build
2. Complete If/Else branch configuration in Facebook workflow
3. Test keyword detection with sample messages
4. Verify SMS notifications send to artist phone
5. Document any GHL UI issues or workarounds

**Next Session:**
1. Duplicate Facebook workflow for Instagram
2. Update platform-specific elements
3. Test both workflows end-to-end
4. Deploy to artist sub-account if tests pass

---

## Notes & Lessons Learned

### Why Two Workflows Work Better
- Platform clarity in artist SMS notifications critical
- No runtime overhead from conditional logic
- Easier to debug platform-specific issues
- Can evolve workflows independently if needs diverge

### Conversational AI Insights
- 3-message limit enforced by AI automatically
- No need for separate "response limit reached" SMS trigger
- Silent handoff more natural than verbal transition
- Qualifying questions gather info before artist involvement

### Tag Strategy
- Platform tags: "Instagram Lead" vs "Facebook Lead"
- State tags: "Asked-Availability", "Awaiting-Pricing-Details"
- Handoff tags: "Artist Takeover - [Reason]"
- Timeout tag: "Conversation Timeout"

---

## References

**Artist Config:** `artist-config.md`
**Main Config:** `conversational-ai-config.md`
**ClickUp EPIC:** Meta DM Auto-Responder (Parent Task: 86dyv7z1x)
**Google Doc:** https://docs.google.com/document/d/1YiVnq9Uy5wDDi8VaBB0XwJgOIBxaZR--Cm8_CA6GfnY/edit?tab=t.m3ic8d3p6jd2
