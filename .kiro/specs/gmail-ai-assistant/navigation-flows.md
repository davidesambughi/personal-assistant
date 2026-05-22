# Navigation Flows — Gmail AI Assistant MVP

All flows are derived directly from the wireframes. Screens not covered by a wireframe are listed as undefined.

---

## Global Layout Patterns

Most screens follow one of two structural patterns. The **Sidebar** is common to all screens (except Homepage) and is detailed in its own section.

### Pattern A: 4-Panel Layout (Complex)

Used for deep data interaction.

- **Top Header:** Global search, notifications, and profile.
- **Left Sidebar:** App navigation.
- **Main Content:** The primary information feed.
- **Right Panel:** AI Assistant context and actions.

### Pattern B: 2-Panel Layout (Simple)

Used for utility and overview screens.

- **Left Sidebar:** App navigation.
- **Main Content:** Centered single-column layout.

---

## Screens

| Screen              | Layout Pattern | Entry Point                           |
| ------------------- | -------------- | ------------------------------------- |
| Homepage            | Custom         | App root (unauthenticated)            |
| Dashboard (Inbox)   | 4-Panel        | After login / sidebar: Inbox          |
| Detailed Email View | 4-Panel        | Clicking an email card from Dashboard |
| Tasks               | 2-Panel        | Sidebar: Tasks                        |
| Daily Digest        | 2-Panel        | Sidebar: Daily Digest                 |
| Settings            | 2-Panel        | Sidebar: Settings                     |
| AI Summaries        | Undefined      | Sidebar: AI Summaries                 |
| Sent                | Undefined      | Sidebar: Sent                         |
| Trash               | Undefined      | Sidebar: Trash                        |

---

## Flow 1 — Authentication

**Entry point:** User opens the app and is not logged in

```
Homepage
  └── clicks "Continue with Google"
        └── Google OAuth flow
              └── success → Dashboard (Inbox)
```

**Already logged in:**

```
App opens → Dashboard (Inbox) directly
```

---

## Flow 2 — Dashboard (Inbox)

**Layout:** Pattern A (4-Panel)

- **Sidebar:** Standard (see [Global Sidebar](#sidebar-navigation-global))
- **Right Panel:** AI Assistant active

### Top Header

```
Header
  ├── Search bar → "Search emails, people, topics..." input
  └── Right Actions
        ├── Notification Bell icon → (not defined in wireframes)
        └── User Profile dropdown ("John Doe") → (not defined in wireframes)
```

### Main panel

```
Dashboard
  ├── Urgent section (with counter, e.g., "3")
  │     ├── email card → "Open" button → Detailed Email View
  │     ├── email card → "Reply with AI" button → Detailed Email View (reply panel open)
  │     └── "View all" link → (not defined in wireframes)
  │
  └── Other Emails section (with counter, e.g., "8")
        ├── email card → "Open" button → Detailed Email View
        └── "View all" link → (not defined in wireframes)
```

### Right panel — AI Assistant

```
AI Assistant panel
  ├── Today's Summary card
  │     └── "View Full Digest →" link → Daily Digest
  │
  ├── Suggested Tasks section
  │     ├── task checklist items → (toggles status)
  │     └── "View All Tasks →" link → Tasks
  │
  └── Quick Actions card
        ├── "Summarize Unread Emails" → (not defined in wireframes)
        ├── "Draft New Email" → (not defined in wireframes)
        └── "Extract Tasks from Inbox" → Tasks
```

---

## Flow 3 — Detailed Email View

**Layout:** Pattern A (4-Panel)

- **Sidebar:** Standard (see [Global Sidebar](#sidebar-navigation-global))
- **Right Panel:** AI Assistant active (context-aware)

### Top Header

```
Header
  ├── "Back to Inbox" (top left) → Dashboard (Inbox)
  └── Right Actions
        ├── "Reply with AI" button → reply panel activates on right
        ├── "Mark as Done" button → marks email, stays on same screen
        └── Three-dots menu icon → (not defined in wireframes)
```

### Main Content

```
Email View
  ├── Subject Header: "<title>" + Priority Tags (Urgent, Work)
  │
  ├── Sender Info Row
  │     ├── Profile Image
  │     ├── Name & Email address → "to me" dropdown
  │     └── Action Icons (far right)
  │           ├── Star icon → (toggles star)
  │           ├── Clock icon (Snooze) → (not defined in wireframes)
  │           └── Three-dots menu icon → (not defined in wireframes)
  │
  ├── AI Insights Cards (Side-by-side)
  │     ├── AI Summary card (read-only)
  │     └── Extracted Tasks card
  │           └── task items with checkboxes and "Due: ..." labels
  │
  └── Email Thread section
        └── "Expand all" toggle → expands all thread messages
```

### Right panel — AI Assistant

```
AI Assistant panel
  ├── Suggested Replies
  │     ├── "Choose tone" dropdown → filters reply style
  │     ├── tone cards: Professional / Short / Casual → updates reply preview
  │     └── "Customize Reply" → reply becomes editable
  │
  ├── Action Items & Details (read-only)
  │     ├── Meeting (date/time)
  │     ├── Participants (list)
  │     └── Attachments (e.g., PDF cards)
  │
  └── Quick Actions
        ├── "Create Task" → Tasks
        └── "Add to Calendar" → (not defined in wireframes)
```

---

## Flow 4 — Tasks

**Layout:** Pattern B (2-Panel)

- **Sidebar:** Standard (see [Global Sidebar](#sidebar-navigation-global))
- **Right Panel:** Not present

### Main Content

```
Tasks screen
  ├── Tab: All → shows all tasks
  ├── Tab: Today → filters to today's tasks
  ├── Tab: Upcoming → filters to future tasks
  ├── Tab: Completed → shows completed tasks
  │
  ├── task items (grouped by Today/Tomorrow/Completed)
  │     └── checkbox → marks task as completed
  │
  └── "+ Add Task" button (top right) → (destination not defined in wireframes)
```

---

## Flow 5 — Daily Digest

**Layout:** Pattern B (2-Panel)

- **Sidebar:** Standard (see [Global Sidebar](#sidebar-navigation-global))
- **Right Panel:** Not present

### Main Content

```
Daily Digest screen
  ├── "Send Digest Email" button (top right) → sends digest to user's email
  │
  ├── Inbox Overview stats cards (Emails Received, Urgent, Action Required, Newsletters)
  │
  ├── Important Emails list
  │     └── email items with "Urgent" badge (navigation not defined in wireframe)
  │
  ├── Tasks Extracted section
  │     ├── task items with checkboxes and "Due: ..." labels
  │     ├── "+ X more tasks" indicator
  │     └── "View All →" link → Tasks screen
  │
  └── AI Recommendations section
        └── recommendation items with icons (read-only)
```

---

## Flow 6 — Settings

**Layout:** Pattern B (2-Panel)

- **Sidebar:** Standard (see [Global Sidebar](#sidebar-navigation-global))
- **Right Panel:** Not present

### Main Content

```
Settings screen
  ├── Connected Account
  │     └── "Disconnect" button → logs out / returns to Homepage
  │
  ├── AI Preferences
  │     ├── Summary Length dropdown → updates preference (Short / Medium / Long)
  │     └── Reply Tone dropdown → updates preference (Professional / etc.)
  │
  ├── Notifications
  │     ├── "Daily Digest Email" toggle → enables/disables
  │     └── "Urgent Email Alerts" toggle → enables/disables
  │
  └── Privacy
        ├── Data Encryption → read-only status indicator (Enabled)
        └── Data Retention → "Delete Stored Data" dropdown → (confirmation flow not defined in wireframes)
```

---

## Sidebar Navigation (Global)

Present on all Pattern A and Pattern B screens.

```
Sidebar
  ├── Inbox → Dashboard (Inbox)
  ├── Tasks → Tasks
  ├── AI Summaries → (wireframe not defined)
  ├── Daily Digest → Daily Digest
  ├── Sent → (wireframe not defined)
  ├── Trash → (wireframe not defined)
  └── Settings → Settings
  │
  └── User profile (bottom) → (no navigation defined)
```

---

## Undefined / Out of Scope for This Document

The following items are visible in the wireframes but have no defined destination screen:

- "View all" links in Urgent and Other inbox sections
- AI Summaries screen
- Sent screen
- Trash screen
- "+ Add Task" destination (action is defined, but destination screen is not)
- "Add to Calendar" quick action
- "Draft New Email" quick action
- "Delete Stored Data" confirmation
- Notification Bell destination
- Three-dots menu destination in Detailed View
