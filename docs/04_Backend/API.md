# Eventora API Specification

**Version:** 1.0

**Architecture:** REST API

**Authentication:** Supabase JWT

---

# Base URL

```
/api/v1
```

Every authenticated request must include:

```
Authorization: Bearer <JWT_TOKEN>
```

---

# Authentication

## Register

```
POST /auth/register
```

Request

```json
{
  "full_name": "Ahmed Mohamed",
  "email": "ahmed@example.com",
  "password": "********"
}
```

Response

```json
{
  "success": true,
  "user_id": "uuid"
}
```

---

## Login

```
POST /auth/login
```

Request

```json
{
  "email": "ahmed@example.com",
  "password": "********"
}
```

Response

```json
{
  "access_token": "...",
  "refresh_token": "...",
  "user": {}
}
```

---

## Logout

```
POST /auth/logout
```

---

## Forgot Password

```
POST /auth/forgot-password
```

---

## Reset Password

```
POST /auth/reset-password
```

---

# Events

## Get All Events

```
GET /events
```

Returns all events owned by the logged-in user.

---

## Create Event

```
POST /events
```

Request

```json
{
  "title": "Ahmed & Sara Wedding",
  "type": "Wedding",
  "theme_id": "uuid",
  "layout_id": "uuid"
}
```

Response

```json
{
  "event_id": "uuid"
}
```

---

## Get Event

```
GET /events/{id}
```

---

## Update Event

```
PATCH /events/{id}
```

---

## Delete Event

```
DELETE /events/{id}
```

---

## Duplicate Event

```
POST /events/{id}/duplicate
```

---

## Publish Event

```
POST /events/{id}/publish
```

Response

```json
{
  "slug": "ahmed-sara",
  "url": "https://eventora.app/e/ahmed-sara"
}
```

---

# Themes

## Get Themes

```
GET /themes
```

---

## Get Theme Details

```
GET /themes/{id}
```

---

# Layouts

## Get Layouts

```
GET /layouts
```

---

## Get Layout Details

```
GET /layouts/{id}
```

---

# Components

## Get Components

```
GET /components
```

---

## Update Component Properties

```
PATCH /events/{id}/components/{componentId}
```

Example

```json
{
  "props": {
    "title": "Ahmed & Sara",
    "subtitle": "Forever Starts Here"
  }
}
```

---

# Assets

## Upload Image

```
POST /assets/upload
```

Multipart Form Data

Response

```json
{
  "url": "https://..."
}
```

---

## Delete Asset

```
DELETE /assets/{id}
```

---

# Guests

## Get Guests

```
GET /events/{id}/guests
```

---

## Add Guest

```
POST /events/{id}/guests
```

---

## Edit Guest

```
PATCH /guests/{id}
```

---

## Delete Guest

```
DELETE /guests/{id}
```

---

# RSVP

## Submit RSVP

```
POST /rsvp
```

Request

```json
{
  "guest_id": "uuid",
  "attendance": "accepted",
  "guests_count": 2,
  "meal_preference": "Chicken",
  "message": "Congratulations!"
}
```

---

## Get RSVP Responses

```
GET /events/{id}/rsvp
```

---

# Payments

## Create Checkout Session

```
POST /payments/checkout
```

---

## Verify Payment

```
POST /payments/verify
```

---

## Payment History

```
GET /payments
```

---

# Analytics

## Dashboard Analytics

```
GET /analytics/dashboard
```

Returns

* Total Events
* Published Events
* Views
* RSVP Count
* Revenue

---

## Event Analytics

```
GET /analytics/events/{id}
```

Returns

* Visitors
* Devices
* Countries
* QR Scans
* RSVP Statistics

---

# Public Website

## View Published Event

```
GET /public/{slug}
```

---

## QR Redirect

```
GET /qr/{slug}
```

---

# Notifications

## Send Email

```
POST /notifications/email
```

---

## Send WhatsApp

```
POST /notifications/whatsapp
```

---

## Send SMS

```
POST /notifications/sms
```

---

# Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Event title is required."
  }
}
```

---

# Success Response Format

```json
{
  "success": true,
  "data": {}
}
```

---

# HTTP Status Codes

| Code | Meaning               |
| ---- | --------------------- |
| 200  | Success               |
| 201  | Created               |
| 204  | Deleted               |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 409  | Conflict              |
| 422  | Validation Error      |
| 429  | Too Many Requests     |
| 500  | Internal Server Error |

---

# API Design Rules

* Use REST principles.
* All endpoints return JSON.
* Never expose private user data.
* Validate every request.
* Use UUIDs for all primary IDs.
* Use pagination for list endpoints.
* Support localization (Arabic & English).
* Version all APIs under `/api/v1`.

---

End of API Specification.
