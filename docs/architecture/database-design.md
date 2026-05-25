# Database Design — Team Up

---

# 1. Overview

The Team Up database is designed using a **relational database architecture** powered by **PostgreSQL** and managed through **Prisma ORM**.

The database is optimized for:

- Realtime collaboration
- High scalability
- Relationship-driven data modeling
- Mobile-first API performance
- Secure authentication handling
- Efficient querying and pagination
- Modular feature expansion

The system follows:

- Normalized relational design
- Domain-driven schema separation
- Type-safe ORM integration
- Scalable indexing strategies

---

# 2. Database Technology Stack

| Layer | Technology |
|---|---|
| Database | PostgreSQL |
| ORM | Prisma ORM |
| Authentication | Supabase Auth |
| Realtime | Supabase Realtime |
| Storage | Supabase Storage |
| Query Language | SQL |
| Backend Integration | NestJS |

---

# 3. High Level Database Architecture

```text
                   ┌─────────────────────┐
                   │   Mobile / Web App  │
                   └──────────┬──────────┘
                              │
                              ▼
                     ┌────────────────┐
                     │   NestJS APIs  │
                     └────────┬───────┘
                              │
                              ▼
                     ┌────────────────┐
                     │   Prisma ORM   │
                     └────────┬───────┘
                              │
                              ▼
                     ┌────────────────┐
                     │ PostgreSQL DB  │
                     └────────┬───────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
      Tables             Relations            Indexes
```

---

# 4. Database Design Principles

The database follows these principles:

1. Relational normalization
2. Domain-based entity separation
3. Scalable indexing
4. Transaction safety
5. Realtime compatibility
6. Efficient joins and querying
7. Type-safe schema management
8. Future-ready extensibility

---

# 5. Core Database Domains

The database is divided into multiple logical domains.

---

## Main Domains

```text
Users
Profiles
Ideas
Teams
KingsCourt
Chats
Messages
Notifications
Skills
Interests
JoinRequests
ActivityLogs
MediaUploads
```

---

# 6. Entity Relationship Overview

```text
User
 ├── Profile
 ├── Ideas
 ├── TeamMemberships
 ├── Notifications
 ├── Skills
 ├── Interests
 └── Messages

Idea
 ├── Team
 ├── JoinRequests
 ├── Media
 └── ActivityLogs

Team
 ├── Leaders
 ├── KingsCourt
 ├── Chats
 └── Notifications
```

---

# 7. Users Table

Stores authentication-linked user information.

---

## users

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| email | String | Unique email |
| username | String | Unique username |
| full_name | String | User full name |
| avatar_url | String | Profile image |
| bio | Text | User biography |
| profile_completion | Integer | Completion percentage |
| created_at | Timestamp | Creation time |
| updated_at | Timestamp | Last update |

---

## Relationships

- One user can create many ideas
- One user can join many teams
- One user can have many notifications
- One user can send many messages

---

# 8. Ideas Table

Stores startup or project ideas created by users.

---

## ideas

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| owner_id | UUID | References users.id |
| title | String | Idea title |
| description | Text | Full idea description |
| category | String | Idea category |
| status | Enum | Draft / Published / Closed |
| visibility | Enum | Public / Private |
| likes_count | Integer | Engagement metric |
| created_at | Timestamp | Creation time |
| updated_at | Timestamp | Last update |

---

## Relationships

- One idea belongs to one user
- One idea can have one team
- One idea can have many join requests
- One idea can have many media uploads

---

# 9. Teams Table

Represents collaborative groups built around ideas.

---

## teams

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| idea_id | UUID | References ideas.id |
| king_id | UUID | Team owner |
| team_name | String | Team name |
| description | Text | Team description |
| max_members | Integer | Member limit |
| created_at | Timestamp | Creation time |

---

## Relationships

- One team belongs to one idea
- One team has many members
- One team has one Kings Court
- One team has many chats

---

# 10. Team Members Table

Handles many-to-many relationship between users and teams.

---

## team_members

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| team_id | UUID | References teams.id |
| user_id | UUID | References users.id |
| role | Enum | King / Leader |
| joined_at | Timestamp | Join time |

---

## Purpose

This table enables:

- Multiple users joining teams
- Role management
- Team permissions
- Team membership tracking

---

# 11. Join Requests Table

Stores requests from users wanting to join teams.

---

## join_requests

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| team_id | UUID | References teams.id |
| user_id | UUID | References users.id |
| reason | Text | User motivation |
| status | Enum | Pending / Accepted / Rejected |
| created_at | Timestamp | Request time |

---

# 12. Kings Court Table

Represents the private collaboration room for a team.

---

## kings_court

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| team_id | UUID | References teams.id |
| created_at | Timestamp | Creation time |

---

# 13. Chats Table

Represents communication channels.

---

## chats

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| team_id | UUID | References teams.id |
| type | Enum | Group / Direct |
| created_at | Timestamp | Creation time |

---

# 14. Messages Table

Stores realtime communication messages.

---

## messages

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| chat_id | UUID | References chats.id |
| sender_id | UUID | References users.id |
| content | Text | Message body |
| media_url | String | Optional attachment |
| created_at | Timestamp | Sent time |

---

# 15. Notifications Table

Stores platform notifications.

---

## notifications

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| user_id | UUID | References users.id |
| type | Enum | Notification type |
| title | String | Notification title |
| message | Text | Notification body |
| is_read | Boolean | Read state |
| created_at | Timestamp | Creation time |

---

# 16. Skills System

Users can attach multiple skills.

---

## skills

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| name | String | Skill name |

---

## user_skills

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| user_id | UUID | References users.id |
| skill_id | UUID | References skills.id |

---

# 17. Interests System

Users can select multiple interests.

---

## interests

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| name | String | Interest name |

---

## user_interests

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| user_id | UUID | References users.id |
| interest_id | UUID | References interests.id |

---

# 18. Activity Logs Table

Tracks major platform activity.

---

## activity_logs

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| user_id | UUID | Actor |
| action | String | Event type |
| entity_type | String | Related entity |
| entity_id | UUID | Related record |
| created_at | Timestamp | Event timestamp |

---

# 19. Media Uploads Table

Stores uploaded media references.

---

## media_uploads

| Column | Type | Description |
|---|---|---|
| id | UUID | Primary key |
| owner_id | UUID | References users.id |
| entity_type | String | Related module |
| entity_id | UUID | Related entity |
| media_url | String | File URL |
| created_at | Timestamp | Upload time |

---

# 20. Database Relationships

## One-to-One Relationships

```text
User → Profile
Team → KingsCourt
```

---

## One-to-Many Relationships

```text
User → Ideas
User → Notifications
Chat → Messages
Idea → JoinRequests
```

---

## Many-to-Many Relationships

```text
Users ↔ Teams
Users ↔ Skills
Users ↔ Interests
```

---

# 21. Indexing Strategy

Indexes are added for high-frequency queries.

---

## Indexed Fields

| Table | Indexed Column |
|---|---|
| users | email |
| users | username |
| ideas | category |
| ideas | created_at |
| messages | chat_id |
| notifications | user_id |
| join_requests | team_id |

---

# 22. Pagination Strategy

Pagination is optimized using:

- Cursor pagination
- Indexed ordering
- Infinite scrolling support

---

## Example Query

```sql
SELECT *
FROM ideas
WHERE created_at < cursor
ORDER BY created_at DESC
LIMIT 20;
```

---

# 23. Realtime Database Strategy

Supabase Realtime listens to:

- Message inserts
- Notification inserts
- Team updates
- Join request changes

---

## Realtime Flow

```text
Database Change
       │
       ▼
Supabase Realtime
       │
       ▼
Frontend Subscription
       │
       ▼
Live UI Update
```

---

# 24. Data Integrity Strategy

Data consistency is maintained using:

- Foreign keys
- Transactions
- Constraints
- Unique indexes
- Cascading deletes where appropriate

---

# 25. Soft Delete Strategy

Important entities use soft deletes.

---

## Example

```text
deleted_at TIMESTAMP NULL
```

Benefits:

- Recovery support
- Audit safety
- Historical preservation

---

# 26. Backup & Recovery Strategy

Database protection includes:

- Automated backups
- Point-in-time recovery
- Transaction logs
- Disaster recovery planning

---

# 27. Future Database Scaling

Planned future improvements:

- Read replicas
- Distributed caching
- Search indexing
- Event-driven architecture
- Dedicated analytics database
- AI recommendation indexing

---

# 28. Conclusion

The Team Up database architecture is designed as a:

- Relational
- Scalable
- Realtime-ready
- Secure
- Modular
- Performance-optimized system

leveraging:

- PostgreSQL
- Prisma ORM
- Supabase
- TypeScript

to support collaborative team building, realtime communication, and scalable platform growth.