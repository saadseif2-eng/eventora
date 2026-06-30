# Database Specification

**Project:** Eventora

**Version:** 1.0

**Database:** PostgreSQL (Supabase)

---

# Overview

Eventora stores all data inside PostgreSQL using Supabase.

Every Event belongs to one User.

Every Event can contain multiple Guests, Components, Assets and Analytics records.

The database is designed for scalability and future expansion.

---

# Entity Relationship

```
Users
   │
   ├────────────┐
   │            │
Events       Themes
   │            │
   │         Layouts
   │            │
   ├────────────┘
   │
Event Components
   │
Guests
   │
RSVP
   │
Payments
   │
Assets
   │
Analytics
```

---

# users

Stores user accounts.

| Column     | Type      |
| ---------- | --------- |
| id         | uuid      |
| full_name  | text      |
| email      | text      |
| phone      | text      |
| avatar     | text      |
| role       | text      |
| language   | text      |
| created_at | timestamp |
| updated_at | timestamp |

---

# events

Stores every created event.

| Column          | Type      |
| --------------- | --------- |
| id              | uuid      |
| user_id         | uuid      |
| title           | text      |
| slug            | text      |
| type            | text      |
| status          | text      |
| theme_id        | uuid      |
| layout_id       | uuid      |
| language        | text      |
| timezone        | text      |
| event_date      | timestamp |
| venue_name      | text      |
| venue_address   | text      |
| google_maps_url | text      |
| music_url       | text      |
| cover_image     | text      |
| published_at    | timestamp |
| created_at      | timestamp |
| updated_at      | timestamp |

---

# themes

Available themes.

| Column      | Type      |
| ----------- | --------- |
| id          | uuid      |
| name        | text      |
| category    | text      |
| preview     | text      |
| premium     | boolean   |
| config_json | jsonb     |
| created_at  | timestamp |

---

# layouts

Available layouts.

| Column      | Type      |
| ----------- | --------- |
| id          | uuid      |
| name        | text      |
| category    | text      |
| preview     | text      |
| premium     | boolean   |
| config_json | jsonb     |
| created_at  | timestamp |

---

# components

Master list of reusable components.

| Column      | Type      |
| ----------- | --------- |
| id          | uuid      |
| name        | text      |
| type        | text      |
| variant     | text      |
| preview     | text      |
| schema_json | jsonb     |
| premium     | boolean   |
| created_at  | timestamp |

---

# event_components

Components attached to an event.

| Column        | Type    |
| ------------- | ------- |
| id            | uuid    |
| event_id      | uuid    |
| component_id  | uuid    |
| display_order | integer |
| visible       | boolean |
| props_json    | jsonb   |

---

# guests

Guest list.

| Column       | Type      |
| ------------ | --------- |
| id           | uuid      |
| event_id     | uuid      |
| full_name    | text      |
| phone        | text      |
| email        | text      |
| guest_type   | text      |
| table_number | integer   |
| plus_one     | boolean   |
| qr_code      | text      |
| created_at   | timestamp |

---

# rsvp

Guest responses.

| Column          | Type      |
| --------------- | --------- |
| id              | uuid      |
| guest_id        | uuid      |
| attendance      | text      |
| guests_count    | integer   |
| meal_preference | text      |
| message         | text      |
| responded_at    | timestamp |

---

# assets

Uploaded files.

| Column     | Type      |
| ---------- | --------- |
| id         | uuid      |
| event_id   | uuid      |
| type       | text      |
| url        | text      |
| size       | bigint    |
| mime_type  | text      |
| created_at | timestamp |

---

# payments

Payment records.

| Column         | Type      |
| -------------- | --------- |
| id             | uuid      |
| event_id       | uuid      |
| provider       | text      |
| amount         | numeric   |
| currency       | text      |
| status         | text      |
| transaction_id | text      |
| invoice_url    | text      |
| paid_at        | timestamp |

---

# analytics

Website analytics.

| Column          | Type      |
| --------------- | --------- |
| id              | uuid      |
| event_id        | uuid      |
| page_views      | integer   |
| unique_visitors | integer   |
| qr_scans        | integer   |
| shares          | integer   |
| rsvp_count      | integer   |
| last_visit      | timestamp |

---

# Notifications

Stores scheduled notifications.

| Column       | Type      |
| ------------ | --------- |
| id           | uuid      |
| event_id     | uuid      |
| channel      | text      |
| recipient    | text      |
| status       | text      |
| scheduled_at | timestamp |
| sent_at      | timestamp |

---

# Event Status

* Draft
* Published
* Archived
* Deleted

---

# Supported Event Types

* Wedding
* Engagement
* Birthday
* Graduation
* Corporate
* Conference
* Baby Shower
* Private Party

---

# Indexes

```
events.slug
events.user_id
guests.phone
payments.status
analytics.event_id
```

---

# Storage Structure

```
storage/

events/

covers/

gallery/

music/

videos/

qr/

avatars/
```

---

# Security

* Row Level Security enabled
* User can only access their own events
* Guests cannot access dashboard data
* Public website only exposes published content
* Payment records are private
* Assets use signed URLs when required

---

# Future Tables

* vendors
* seating_plans
* event_staff
* chat_messages
* ai_history
* coupons
* subscriptions
* invoices
* audit_logs

---

End of Database Specification
