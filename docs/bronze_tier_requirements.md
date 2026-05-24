# Prism Digital Mail FTE - Bronze Tier Requirements Documentation

## Product Overview

**Product Name:** Prism Digital Mail FTE

**Tagline:** Your AI Email Employee

**Description:** Prism Digital Mail FTE is an AI-powered email triage assistant that intelligently categorizes your inbox, routing emails to the right place so you focus only on what matters. Built on Claude Code and Obsidian, Prism Digital Mail FTE acts as your executive assistant, analyzing incoming emails and organizing them by priority and type.

## Overview
This document outlines the minimum viable deliverables for the Bronze Tier of the Personal AI Employee Hackathon. The Bronze Tier represents the foundational level of implementation that establishes the core functionality of Prism Digital Mail FTE.

## Project Philosophy

Prism Digital Mail FTE is being developed as a **product**, not just a hackathon submission. While implementing Bronze Tier requirements, we're building a foundation for a scalable, production-ready AI employee system with intelligent triage capabilities.

## Project Decisions & Clarifications

### Watcher Script Choice: Gmail
For the Bronze Tier requirement of "one working Watcher script (Gmail OR file system monitoring)", this project will implement the **Gmail watcher** approach.

### Intelligent Triage Architecture
Prism Digital Mail FTE implements an **intelligent triage layer** where Claude acts as an executive assistant, analyzing and routing emails rather than just detecting them. This goes beyond basic Bronze Tier requirements to create a more useful product.

**Three-Phase Architecture:**
1. **Detection** - Watcher detects emails and creates files in /Inbox
2. **Triage** - Claude analyzes and routes to appropriate folders
3. **Review** - User focuses on categorized items

### Vault Structure Status
The Obsidian vault structure has been successfully created with all required folders and documentation files. The vault is ready for use with the Gmail watcher script.

### PM2 Process Manager: NOT Required for Bronze Tier
**Important:** PM2 (or other process managers like supervisord) is **NOT required** for Bronze Tier completion.

**What IS Required:**
- A working Python watcher script that can be manually executed
- Script successfully monitors Gmail for new messages
- Script creates markdown files in the /Inbox folder (staging area)
- Demonstration that the watcher works when run

**When PM2 Would Be Needed:**
- Silver/Gold tiers where 24/7 autonomous operation is required
- Production deployment requiring auto-restart on crashes
- Continuous monitoring without manual intervention
- Advanced logging and process management features

**For Bronze Tier:** Simply running `python gmail_watcher.py` manually to demonstrate functionality is sufficient. The focus is on proving the watcher logic works, not on production-grade daemon management.

### Orchestrator & Automatic Claude Invocation: NOT Required for Bronze Tier
**Important:** Automatic triggering of Claude Code is **NOT required** for Bronze Tier.

**What IS Required:**
- Gmail watcher runs and creates files in /Inbox (staging area)
- You manually invoke Claude Code to triage and process the files
- Claude reads from and writes to the vault
- Claude routes emails to appropriate folders based on analysis

**What is NOT Required:**
- ❌ Orchestrator.py (master process that watches folders and triggers Claude)
- ❌ Automatic Claude Code invocation when files are created
- ❌ Ralph Wiggum loop (autonomous iteration until task complete)
- ❌ Cron jobs or Task Scheduler for automation

**When Automatic Invocation Would Be Needed:**
- Silver Tier adds: "Claude reasoning loop" and "Basic scheduling via cron or Task Scheduler"
- Gold Tier adds: Full autonomous operation with orchestrator
- Platinum Tier adds: 24/7 cloud deployment with health monitoring

**Bronze Tier Workflow:**
```
1. Run: python gmail_watcher.py (manually or in background)
2. Watcher detects email → Creates markdown file in /Inbox
3. You manually run: claude (in the vault directory)
4. Prism Digital Mail FTE (Claude) triages emails from /Inbox → Routes to /Needs_Action, /Summaries, or /Replies
5. Prism Digital Mail FTE updates Dashboard.md with triage summary
6. You review /Needs_Action for items requiring attention
7. Done - demonstrate Prism Digital Mail FTE's intelligent triage working
```

### External Actions & MCP Servers: NOT Required for Bronze Tier
**Important:** Bronze Tier focuses on **PERCEPTION and TRIAGE only**, not external actions.

**What IS Required:**
- Gmail watcher reads/monitors emails (INPUT)
- Creates markdown files in vault (LOCAL FILE WRITE)
- Claude reads and writes to vault (LOCAL FILE READ/WRITE)
- Claude creates draft replies in /Replies folder (LOCAL FILE WRITE)

**What is NOT Required:**
- ❌ Sending emails (drafts only in /Replies)
- ❌ Replying to messages (drafts prepared but not sent)
- ❌ MCP servers for external actions
- ❌ Browser automation
- ❌ Any external API calls for actions (Gmail API read-only is fine)

**When External Actions Would Be Needed:**
- Silver Tier explicitly adds: "One working MCP server for external action (e.g., sending emails)"
- Gold Tier adds: "Multiple MCP servers for different action types"

**Bronze Tier is about building the "eyes" and "brain" (perception + triage), not the "hands" (actions).**

## Intelligent Triage Workflow

### Folder Structure (All inside Obsidian vault)

**Core Folders:**

- **`/Inbox`** - Untriaged watcher output (staging area)
  - Gmail watcher writes all detected emails here as markdown files
  - Raw, unprocessed items waiting for Claude triage
  - Format: `email-{sender}-{timestamp}.md`
  - Think of this as the "mail room" where everything arrives first

- **`/Needs_Action`** - Items requiring human attention (after Claude triage)
  - Claude moves urgent/important items here after analysis
  - User focuses on this folder for action items
  - Contains emails that need decisions, responses, or follow-up
  - Examples: Client inquiries, invoices, urgent requests

- **`/Summaries`** - FYI items that don't need action (markdown files)
  - Claude creates summary markdown files for informational emails
  - Newsletters, notifications, updates that don't require action
  - Format: `summary-{topic}-{timestamp}.md`
  - Keeps user informed without overwhelming with details
  - Examples: Newsletter summaries, system notifications, updates

- **`/Replies`** - Draft responses prepared by Claude (markdown files)
  - Claude writes draft reply markdown files here
  - Not sent in Bronze Tier (just prepared for review)
  - Format: `reply-{recipient}-{timestamp}.md`
  - Ready for Silver Tier when MCP email sending is added
  - User can review, edit, and approve drafts

- **`/Done`** - Completed/archived items
  - Processed items moved here for audit trail
  - Includes spam, irrelevant emails, and completed tasks
  - Maintains history of all processed items
  - Useful for reviewing what was handled

### Vault Status
The Obsidian vault has been successfully created with the complete folder structure:
- `/Inbox` - Empty, ready for watcher input
- `/Needs_Action` - Empty, ready for triage output
- `/Summaries` - Empty, ready for summary output
- `/Replies` - Empty, ready for draft output
- `/Done` - Empty, ready for archived items
- `Dashboard.md` - Empty, ready for triage statistics
- `Company_Handbook.md` - Empty, ready for triage criteria

### Complete Workflow Example

**Day 1: Setup**
1. Create Obsidian vault with folder structure: /Inbox, /Needs_Action, /Summaries, /Replies, /Done
2. Create Dashboard.md and Company_Handbook.md
3. Configure Gmail API credentials
4. Test watcher script

**Day 2: Detection Phase**
1. Run: `python gmail_watcher.py`
2. Watcher detects 5 unread emails
3. Creates 5 markdown files in /Inbox:
   - `email-client-a-2026-03-03-10-30.md` (client inquiry about pricing)
   - `email-newsletter-tech-2026-03-03-10-45.md` (weekly tech newsletter)
   - `email-supplier-b-2026-03-03-11-15.md` (invoice for payment)
   - `email-notification-github-2026-03-03-11-30.md` (GitHub PR notification)
   - `email-spam-promo-2026-03-03-12-00.md` (promotional spam)

**Day 3: Triage Phase**
1. User runs: `claude` (from vault directory)
2. Claude reads 5 files from /Inbox
3. Claude analyzes each email and routes:

   **Client inquiry** → `/Needs_Action/email-client-a-2026-03-03-10-30.md`
   - Reason: Requires response and decision on pricing
   - Also creates: `/Replies/reply-client-a-2026-03-03.md` (draft response)

   **Newsletter** → `/Summaries/summary-tech-newsletter-2026-03-03.md`
   - Reason: Informational only, no action needed
   - Summary includes: Key topics, interesting articles, trends

   **Invoice** → `/Needs_Action/email-supplier-b-2026-03-03-11-15.md`
   - Reason: Requires payment action
   - Flagged as: Payment due, amount, deadline

   **GitHub notification** → `/Summaries/summary-github-pr-2026-03-03.md`
   - Reason: FYI about PR status, can review later
   - Summary includes: PR title, status, reviewer comments

   **Spam** → `/Done/email-spam-promo-2026-03-03-12-00.md`
   - Reason: Irrelevant promotional content
   - Marked as: Spam, no action needed

4. Claude updates Dashboard.md with triage summary:
   ```markdown
   ## Latest Triage (2026-03-03 14:00)
   - Processed: 5 emails
   - Needs Action: 2 items
   - Summaries Created: 2 items
   - Draft Replies: 1 item
   - Archived: 1 item (spam)
   ```

**Day 4: Human Review**
1. User opens Obsidian vault
2. Reviews Dashboard.md for overview
3. Checks `/Needs_Action` (2 items requiring attention):
   - Reads client inquiry, reviews draft reply in `/Replies`
   - Notes invoice for payment processing
4. Reads `/Summaries` to stay informed:
   - Scans tech newsletter summary
   - Reviews GitHub PR summary
5. Takes action:
   - Approves draft reply (ready for Silver Tier to send)
   - Processes invoice payment
   - Moves completed items to `/Done`

**Success Criteria Met:**
- ✓ Watcher detects and creates files
- ✓ Prism Digital Mail FTE (Claude) reads and writes to vault
- ✓ Intelligent triage reduces cognitive load
- ✓ User focuses only on items needing attention
- ✓ All components work together
- ✓ Product-ready architecture for future tiers

## Bronze Tier Deliverables (Minimum Viable Product)

Based on the hackathon guidelines and Prism Digital Mail FTE's enhanced architecture, the following items constitute the Bronze Tier requirements:

### Vault Structure Verification
The Obsidian vault structure has been successfully created with all required folders:
- `/Inbox` - Untriaged emails from watcher (staging area)
- `/Needs_Action` - Items requiring human attention (after Prism Digital Mail FTE triage)
- `/Summaries` - FYI items that don't need action (markdown summaries)
- `/Replies` - Draft responses prepared by Prism Digital Mail FTE (markdown files, not sent)
- `/Done` - Completed/archived items
- `Dashboard.md` - Main dashboard with triage statistics and recent activity
- `Company_Handbook.md` - Rules of engagement and triage criteria

All folders have been verified to exist and are ready for use.

1. **Obsidian Vault with Dashboard.md and Company_Handbook.md**
   - Create an Obsidian vault structure
   - Implement a Dashboard.md file showing triage statistics and recent activity
   - Create a Company_Handbook.md file with rules of engagement and triage criteria

2. **One working Gmail Watcher script**
   - Implement a Python watcher script that monitors Gmail
   - Detect unread emails using Gmail API
   - Create markdown files in the /Inbox folder for each detected email
   - Mark emails as processed to avoid duplicates
   - Include email metadata (sender, subject, timestamp, body)

3. **Prism Digital Mail FTE (Claude Code) successfully reading from and writing to the vault**
   - Configure Claude Code to work with the Obsidian vault
   - Verify reading capability from vault files
   - Verify writing capability to vault files
   - Demonstrate intelligent triage and routing

4. **Enhanced folder structure with intelligent triage**
   - Create folder structure inside the Obsidian vault
   - /Inbox - Untriaged emails from watcher (staging area)
   - /Needs_Action - Items requiring human attention (after Prism Digital Mail FTE triage)
   - /Summaries - FYI items that don't need action (markdown summaries)
   - /Replies - Draft responses prepared by Prism Digital Mail FTE (markdown files, not sent)
   - /Done - Completed/archived items

5. **All AI functionality implemented as Agent Skills**
   - **CRITICAL:** All email-related AI functionality MUST be implemented as Claude Code Agent Skills
   - Email triage logic → Agent Skill
   - Email analysis and categorization → Agent Skill
   - Summary generation → Agent Skill
   - Draft reply creation → Agent Skill
   - Routing decisions → Agent Skill
   - Dashboard updates → Agent Skill
   - Follow the Agent Skills framework as specified in the guidelines
   - Skills should be reusable, well-documented, and independently testable

### Why Agent Skills?

The hackathon explicitly requires all AI functionality to be implemented as Agent Skills. This approach provides:

- **Reusability:** Skills can be invoked across different contexts
- **Modularity:** Each skill has a single, well-defined purpose
- **Testability:** Skills can be tested independently
- **Scalability:** Easy to add new skills for Silver/Gold tiers
- **Maintainability:** Clear separation of concerns

**Example Skills for Prism Digital Mail FTE:**
- `/triage-email` - Analyzes an email and determines routing
- `/create-summary` - Generates a summary from email content
- `/draft-reply` - Creates a draft response to an email
- `/update-dashboard` - Updates Dashboard.md with triage statistics

## Implementation Approach

### Phase 1: Vault Setup
- Create Obsidian vault structure
- Implement core documentation files (Dashboard.md, Company_Handbook.md)
- Set up folder hierarchy (/Inbox, /Needs_Action, /Summaries, /Replies, /Done)
- Define triage criteria in Company_Handbook.md

### Phase 2: Watcher Implementation
- Set up Gmail API credentials
- Develop Python watcher script
- Implement email detection and markdown file creation
- Test watcher creates files in /Inbox correctly

### Phase 3: Prism Digital Mail FTE Integration & Triage Logic
- Configure Claude Code for vault access
- Design Prism Digital Mail FTE triage logic as Agent Skills (not inline code)
- Test reading from /Inbox and writing to appropriate folders
- Validate summary creation and draft reply generation
- Test Dashboard.md updates
- **Note:** All logic must be implemented as Agent Skills in Phase 4

### Phase 4: Agent Skills Implementation
- **CRITICAL PHASE:** Convert all email-related AI functionality to Agent Skills
- Design skill architecture:
  - Email triage skill
  - Summary generation skill
  - Draft reply skill
  - Dashboard update skill
- Implement each skill following Agent Skills framework
- Test skills work correctly with Claude Code
- Document skill usage and invocation patterns
- Ensure skills are reusable and modular

## Technical Requirements

### Vault Structure
All folders inside the Obsidian vault:
- /Inbox - Untriaged watcher output
- /Needs_Action - Items requiring human attention
- /Summaries - FYI summaries (markdown files)
- /Replies - Draft responses (markdown files)
- /Done - Completed/archived items

### Files to Create
- Dashboard.md - Main dashboard with triage statistics and recent activity
- Company_Handbook.md - Rules of engagement and triage criteria
- gmail_watcher.py - Gmail monitoring script

### Python Dependencies
- google-auth
- google-auth-oauthlib
- google-auth-httplib2
- google-api-python-client

### Gmail API Setup
- Google Cloud project with Gmail API enabled
- OAuth 2.0 credentials configured
- Read-only scope: `https://www.googleapis.com/auth/gmail.readonly`

## Success Criteria
- All Bronze Tier deliverables are implemented
- Working demonstration of Prism Digital Mail FTE's intelligent triage workflow
- Gmail watcher successfully detects and creates files
- Prism Digital Mail FTE successfully triages and routes emails
- User can focus on /Needs_Action folder for items requiring attention
- Proper documentation of implementation
- Compliance with the specified requirements
- Product-ready architecture that scales to Silver/Gold tiers
