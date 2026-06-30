# Eventora Architecture

**Version:** 1.0

---

# Overview

Eventora is a modular SaaS platform for creating interactive event websites.

The platform is built using reusable modules instead of static templates.

Each published website is generated dynamically based on:

* Event Data
* Theme
* Layout
* Components

---

# System Architecture

```
User

↓

Authentication

↓

Dashboard

↓

Event Wizard

↓

Theme Selection

↓

Layout Selection

↓

Event Data

↓

Rendering Engine

↓

Published Website
```

---

# Core Modules

## Authentication

Handles:

* Login
* Register
* Google Login
* Apple Login
* Password Reset
* Session Management

---

## Dashboard

Users can:

* Create Events
* Edit Events
* Delete Events
* Duplicate Events
* Publish Events
* View Analytics

---

## Event Wizard

Responsible for collecting all event information.

Steps:

1. Event Type
2. Theme
3. Layout
4. Event Details
5. Preview
6. Publish

---

## Theme Engine

Responsible for:

* Colors
* Typography
* Buttons
* Cards
* Shadows
* Animations

A Theme never contains event data.

---

## Layout Engine

Responsible for page structure.

Examples:

* Luxury
* Minimal
* Modern
* Classic
* Royal
* Floral

---

## Component Engine

Every page is built from reusable components.

Examples:

* Hero
* Countdown
* Story
* Gallery
* RSVP
* Venue
* Footer

Each component accepts data through props.

---

## Rendering Engine

Receives:

* Theme
* Layout
* Components
* Event Data

Produces:

Interactive Event Website

The renderer never generates HTML using AI.

It renders React Components dynamically.

---

## Publishing Engine

Responsible for:

* Slug Generation
* Website Publishing
* QR Code Generation
* SEO Metadata
* Sitemap Update

---

## Analytics Engine

Tracks:

* Views
* Visitors
* RSVP Count
* QR Scans
* Shares

---

# Data Flow

```
User

↓

Dashboard

↓

Event Wizard

↓

Database

↓

Renderer

↓

Website

↓

Analytics
```

---

# Frontend Stack

* Next.js 15
* React
* TypeScript
* Tailwind CSS
* shadcn/ui
* Framer Motion

---

# Backend Stack

* Supabase
* PostgreSQL
* Edge Functions

---

# Storage

Supabase Storage

Folders:

* covers
* gallery
* music
* qr
* avatars

---

# Authentication

Supabase Auth

Supports:

* Email
* Google
* Apple
* OTP

---

# Payments

Supported Providers:

* Stripe
* Paymob

---

# Localization

Languages:

* Arabic
* English

Supports:

* RTL
* LTR

---

# Performance Strategy

* Lazy Loading
* Image Optimization
* CDN Assets
* Incremental Rendering
* Code Splitting

---

# Security

* Row Level Security
* Protected API Routes
* Signed URLs
* Input Validation
* Rate Limiting

---

# Scalability

The platform is designed to support:

* Thousands of users
* Millions of published event pages
* Thousands of concurrent visitors

---

# Future Expansion

* Vendor Marketplace
* AI Invitation Generator
* AI Video Invitations
* Seating Planner
* WhatsApp Invitations
* Email Campaigns
* Mobile App
* White Label Platform

---

# Development Principles

* Modular Architecture
* Reusable Components
* Clean Code
* Type Safety
* Accessibility
* Responsive Design
* No Hardcoded Data
* Production Ready

---

End of Architecture Specification
