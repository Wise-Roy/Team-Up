# Team Up - User Flows Documentation

## Core Terminology

| Term | Meaning |
|------|---------|
| King | Owner/creator of an Idea |
| Leader | A participant selected by the King to join the Idea |
| King's Court | Dedicated collaboration room created for a King and accepted Leaders |
| Idea | Startup/project/business/problem-solving concept created by a user |

---

# 1. User Onboarding Flows

## 1.1 User Registration Flow

### Primary Flow
1. User opens app
2. User selects:
   - Sign up with Email
   - Sign up with Google
   - Sign up with GitHub (optional future feature)
3. User enters account details
4. System verifies account
5. User account is created
6. User is redirected to profile setup

### Edge Cases
- Email already exists
- Invalid verification token
- OAuth cancellation
- Weak password validation

---

## 1.2 Profile Setup Flow

### Primary Flow
1. User uploads:
   - Profile picture
   - Bio
   - Skills
   - Interests
   - Experience
   - Social links
   - Portfolio/GitHub/LinkedIn
2. System calculates profile completion percentage
3. User can continue using app

### Business Rule
- User profile must be **80% complete** before:
  - Creating Ideas
  - Publishing Ideas

### Missing Flow You Should Add
#### Skill Verification (Future)
- Add badges or verification for:
  - GitHub activity
  - LinkedIn
  - Portfolio projects

This improves trust between Kings and Leaders.

---

# 2. Idea Lifecycle Flows

## 2.1 Create Idea Draft Flow

### Primary Flow
1. User clicks "Create Idea"
2. System checks profile completion >= 80%
3. User fills:
   - Idea title
   - Description
   - Problem statement
   - Vision
   - Required skills
   - Team size needed
   - Tags/categories
4. User saves draft

### Edge Cases
- Profile completion below 80%
- Missing required fields
- Invalid team size

---

## 2.2 Publish Idea Flow

### Primary Flow
1. User opens draft
2. User clicks "Publish"
3. Idea becomes visible in:
   - Feed
   - Search
   - Recommendations
4. Other users can now apply

### Suggested Additional Logic
You should include:
- Visibility types:
  - Public Idea
  - Invite-only Idea
  - Hidden Draft

This gives Kings better control.

---

## 2.3 Browse & Discover Ideas Flow

### Primary Flow
1. User visits Ideas Feed
2. User can:
   - Search Ideas
   - Filter by skills
   - Filter by domain
   - Filter by stage
   - Filter by remote/local
3. User opens Idea details
4. User decides whether to apply

### Missing Flows You Should Add
- Recommended Ideas based on user interests
- Trending Ideas
- Recently funded/popular Ideas
- Similar Ideas suggestions

---

# 3. Idea Application & Recruitment Flows

## 3.1 Apply to Join Idea Flow

### Primary Flow
1. User opens Idea page
2. User clicks "Apply"
3. User submits:
   - Reason for joining
   - What value they bring
   - Relevant experience
4. Application is sent to King

### Suggested Improvements
Add:
- Resume/portfolio attachment
- Availability selection
- Role preference

---

## 3.2 King Reviews Applications Flow

### Primary Flow
1. King receives application notifications
2. King views applicant profiles
3. King reviews:
   - Skills
   - Interests
   - Experience
   - Application note
4. King chooses:
   - Accept
   - Reject
   - Shortlist

### Missing Important Flow
#### Interview / Discussion Stage
Before accepting:
- King may initiate temporary chat/interview
- Schedule call/discussion
- Ask follow-up questions

This is important for real collaboration quality.

---

## 3.3 Leader Acceptance Flow

### Primary Flow
1. Applicant receives acceptance notification
2. Applicant accepts invitation
3. User officially becomes Leader

### Alternative Flow
- Leader may decline invitation

---

# 4. King's Court (Project Room) Flows

## 4.1 Court Creation Flow

### Primary Flow
1. King accepts one or more Leaders
2. System automatically creates King's Court
3. Court includes:
   - Shared chat
   - Member list
   - Tasks (future)
   - Shared files (future)
   - Idea roadmap (future)

### Suggested Improvement
Court should not form immediately after first acceptance.

Better flow:
1. King manually clicks:
   - "Start Project"
2. Then Court is created

This gives flexibility during recruitment.

---

## 4.2 Court Collaboration Flow

### Primary Flow
Inside King's Court members can:
- Chat
- Share files
- Discuss roadmap
- Share links/resources
- Create milestones
- Assign responsibilities

### Future Flows
- Voting/poll system
- Sprint planning
- Kanban/task board
- Meeting scheduling
- Notes/wiki/documentation

---

## 4.3 Member Exit Flow

### Flow Variants
A Leader may:
- Leave voluntarily
- Be removed by King
- Become inactive

### System Actions
- Notify remaining members
- Preserve message history
- Update member count

---

## 4.4 Court Closure Flow

### Primary Flow
1. King marks project as:
   - Completed
   - Archived
   - Discontinued
2. Court becomes read-only

---

# 5. Direct Messaging Flows

## 5.1 User Discovery Flow

### Primary Flow
1. User opens Chat page
2. User sees:
   - Suggested users
   - Online users
   - Recently active users
3. User opens another user's profile

---

## 5.2 Connection Request Flow

### Primary Flow
1. User sends short introduction note
2. Receiver gets request notification
3. Receiver chooses:
   - Accept
   - Reject

### If Accepted
- Direct messaging becomes available

### Missing Important Feature
You should include:
- Spam protection
- Daily request limits
- Block/report user

Very important for platform safety.

---

## 5.3 Direct Messaging Flow

### Features
Users can:
- Send messages
- Share files
- Share Idea links
- Send voice notes (future)
- Start audio/video call (future)

### Additional States
- Seen/unseen messages
- Typing indicator
- Online status

---

# 6. Community & Feed Flows

## 6.1 Feed Interaction Flow

### Users Can
- Post discussions
- Ask questions
- Share updates
- Comment
- Like/react
- Share posts

### Suggested Additions
- Save/bookmark posts
- Follow users
- Follow topics/tags

---

## 6.2 Community Groups Flow

### Primary Flow
1. User discovers groups
2. User joins group
3. User participates in:
   - Group chat
   - Discussions
   - Resource sharing

### Group Types
- Public groups
- Private groups
- Skill-specific groups
- Startup-domain groups

---

## 6.3 Group Moderation Flow

### Required Missing Flow
You should add moderation:
- Report content
- Remove spam
- Ban abusive users
- Admin/moderator roles

This becomes critical as community grows.

---

# 7. Notifications Flows

## Notification Types
Users should receive notifications for:
- New applications
- Application accepted/rejected
- Court creation
- New messages
- Mentions
- Group invites
- Idea updates
- Comments/replies

### Suggested Improvement
Allow notification preferences:
- Push
- Email
- In-app

---

# 8. Search & Discovery Flows

## Search Targets
Users should be able to search:
- Ideas
- Users
- Skills
- Groups
- Posts

### Suggested Filters
- Skill match
- Availability
- Experience level
- Remote/in-person
- Domain/category

---

# 9. Reputation & Trust Flows (Strongly Recommended)

This is a missing but important system.

## Possible Features
- Leader ratings
- King ratings
- Completed project badges
- Reliability score
- Contribution score

This improves trust and collaboration quality.

---

# 10. Reporting & Safety Flows

## Required Safety Flows

### Users Can
- Report abuse
- Report spam
- Block users
- Mute users
- Leave groups

### Admin Can
- Suspend users
- Remove content
- Review reports

This is essential for scaling safely.

---

# 11. Admin Flows

## Admin Dashboard

### Admin Can
- Manage users
- Manage reports
- Moderate communities
- Review flagged content
- Monitor platform activity

---

# 12. Future Advanced Flows

## Suggested Future Features

### Collaboration
- Task management
- Shared whiteboards
- Document collaboration
- AI teammate suggestions

### Growth
- Startup showcase pages
- Investor profiles
- Hackathon events
- Team matching AI

### Monetization
- Premium profiles
- Featured Ideas
- Subscription plans

---

# 13. Recommended State Transitions

## Idea States

Draft
-> Published
-> Recruiting
-> Active Project
-> Completed
-> Archived

---

## Application States

Applied
-> Shortlisted
-> Accepted
-> Declined

---

## Court States

Created
-> Active
-> Dormant
-> Archived

---

# 14. Important Missing Architectural Concepts

## 14.1 Roles & Permissions

Need role-based permissions:
- User
- King
- Leader
- Moderator
- Admin

---

## 14.2 Privacy Controls

Users should control:
- Who can message them
- Profile visibility
- Group visibility
- Online status

---

## 14.3 Trust & Anti-Spam

Should include:
- Fake account detection
- Rate limiting
- Duplicate application prevention
- Spam filtering

---

# 15. Recommended Core User Journey

## Example Complete Journey

1. User signs up
2. Completes profile
3. Browses feed
4. Joins communities
5. Creates Idea
6. Publishes Idea
7. Receives applications
8. Reviews candidates
9. Accepts Leaders
10. Creates King's Court
11. Collaborates with team
12. Completes project
13. Gains reputation

---

# 16. Most Important Product Decisions You Should Clarify

These are still undefined and very important:

## Collaboration Rules
- Can a user join multiple Ideas?
- Can a King have multiple active Courts?
- Can Leaders invite others?
- Can Ideas be transferred to another King?

## Team Rules
- Maximum team size?
- Can Leaders leave anytime?
- What happens if King becomes inactive?

## Community Rules
- Public vs private groups?
- Group ownership transfer?
- Anonymous posting allowed?

---

# Final Recommendation

The strongest missing areas in your current thinking are:

1. Moderation & safety
2. Reputation/trust system
3. Notifications
4. State transitions
5. Privacy controls
6. Recruitment workflow depth
7. Collaboration tooling
8. Spam prevention
9. Role permissions
10. Court lifecycle management

Without these, the app works functionally but becomes difficult to scale properly.