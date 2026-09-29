# Day 18: brain-dump-action-planner Skill

## What I Built
A custom Claude skill, `brain-dump-action-planner`, that turns messy notes, meeting transcripts, voice memos, and brainstorms into an interactive HTML dashboard. It never invents or infers missing information; gaps show as "Not specified".

## Skill Details
- **Name:** brain-dump-action-planner
- **Description:** Transform messy notes, meeting transcripts, voice memos, brainstorming sessions, and stream-of-consciousness thoughts into structured summaries, action plans, decisions, open questions, and task lists. Organize information clearly without inventing, assuming, or filling gaps. Preserve all names, dates, numbers, and terminology exactly as provided.
- **Modes:** Full Breakdown, Transcript Mode, Merge Mode
- **Status badges:** 🔴 High Priority, 🟠 Medium Priority, 🟢 Low Priority, ⚠️ Conflict, ❓ Open Question, ✅ Completed, ⏳ Pending

## Generated Dashboard: Project launch — meeting notes
**File:** `project-launch-dashboard.html` (self-contained, opens in any browser)
**Mode used:** Transcript Mode, 2 speakers (Raj, Ankit), 1 deadline identified

### Sections
| Section | Contents |
|---------|----------|
| Summary | Project sync between Raj and Ankit; landing page due July 5; backend API pending; marketing launch blocked by landing page |
| Key Takeaways | 4 color-coded highlight cards |
| Speaker Summary | Cards for Raj, Ankit, and Group |
| Action Items | Interactive table (Task, Owner, Deadline, Priority, Status); click a status badge to toggle Pending / Completed |
| Open Questions | Ankit's API completion date; owner of marketing launch; marketing launch date |
| Risks / Blockers | API delay risk; hard dependency on landing page |
| Conflicts | 2 conflicts flagged (missing API deadline vs. July 5 cutoff; dependency chain launch → landing page → API) |
| Additional Notes | Timeline dependency; no meeting date or project name specified |

### Action Items
| Task | Owner | Deadline | Priority | Status |
|------|-------|----------|----------|--------|
| Finish UI / landing page | Raj | July 5 | 🔴 High | ⏳ Pending |
| Finish backend APIs | Ankit | Not specified | 🔴 High | ⏳ Pending |
| Marketing campaign launch | Not specified | Not specified | 🟠 Medium | ⏳ Pending |

### Design Features
- Dark, Notion / Linear-style dashboard layout
- Cards, badges, hover effects, soft shadows
- Collapsible sections
- Mobile responsive

## How I Set Up the Skill
1. Opened Claude Settings > Capabilities (or Customize > Skills).
2. Created a new skill named `brain-dump-action-planner` (or uploaded the `.skill` file).
3. Added the description and pasted the instructions.
4. Saved the skill.



## Observations
- **Reusability:** the skill triggers from a plain prompt, with no need to re-enter the instructions.
- **Missing info:** "Not specified" appears instead of invented values (owner and deadline of the marketing launch, deadline of the API).
- **Caution:** a few lines in the first output (for example "Assigned to finish UI") go beyond what the notes state. Review outputs against the original notes.

