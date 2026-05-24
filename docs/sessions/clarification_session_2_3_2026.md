# Bronze Tier Implementation Clarifications

## Session Date: 2026-03-02

### Question 1: Watcher Script Implementation
**Question:** For the Bronze Tier requirements, which type of Watcher script should we implement - Gmail or file system monitoring? Both are acceptable according to the guidelines.

**Answer:** Either type is acceptable for Bronze Tier. The choice depends on what's more practical for the current setup.

### Question 2: Vault Structure Scope
**Question:** Regarding the Obsidian vault structure requirements, should we implement the full folder structure as outlined in the documentation (Inbox, Needs_Action, Done, Plans, Logs, Pending_Approval, Approved, Rejected) or just the minimal required folders (Inbox, Needs_Action, Done)?

**Answer:** Only required for bronze tier. Plans and Logs and Accepted and Rejected and Pending_Approval are out the scope.

### Question 3: Documentation Detail Level
**Question:** For the key documentation files (Dashboard.md and Company_Handbook.md), what level of detail should we implement for the Bronze Tier? Should we create basic templates or more detailed content?

**Answer:** Later - we'll implement basic templates for now and expand later.

## Key Bronze Tier Requirements (Based on Clarifications)

1. **Obsidian Vault Structure**
   - Required folders: Inbox, Needs_Action, Done
   - Optional folders (not for Bronze): Plans, Logs, Pending_Approval, Approved, Rejected

2. **Documentation Files**
   - Dashboard.md (basic template)
   - Company_Handbook.md (basic template)

3. **Watcher Script**
   - One working watcher script (either Gmail or file system monitoring)

4. **Claude Code Integration**
   - Verify reading from and writing to the vault

5. **Agent Skills**
   - All AI functionality should be implemented as Agent Skills