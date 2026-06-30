# Eventora Rendering Engine Specification

**Version:** 1.0

**Status:** Production Ready

---

# Overview

The Rendering Engine is responsible for transforming structured event data into a complete interactive website.

The renderer **never generates HTML using AI**.

Instead, it renders predefined React components using structured JSON data.

This approach guarantees:

* High performance
* Consistent design
* Easy maintenance
* Better SEO
* Component reusability

---

# Rendering Pipeline

```
User

↓

Create Event

↓

Save Event Data

↓

Choose Theme

↓

Choose Layout

↓

Load Components

↓

Merge Data

↓

Validate

↓

Render React Components

↓

Published Website
```

---

# Rendering Principles

The renderer must:

* Never generate HTML with AI
* Never generate CSS with AI
* Never create unknown components
* Render only registered components
* Support RTL and LTR
* Support Dark Mode
* Support responsive layouts

---

# Input

The renderer receives one JSON object.

Example:

```json
{
  "event": {
    "title": "Ahmed & Sara Wedding",
    "type": "Wedding",
    "language": "ar"
  },

  "theme": "luxury-black",

  "layout": "royal-01",

  "components": [
    {
      "type": "Hero",
      "variant": "hero-01"
    },
    {
      "type": "Countdown",
      "variant": "countdown-01"
    },
    {
      "type": "Venue",
      "variant": "venue-01"
    },
    {
      "type": "Gallery",
      "variant": "gallery-01"
    },
    {
      "type": "RSVP",
      "variant": "rsvp-01"
    }
  ]
}
```

---

# Component Registry

Every component must exist inside the registry.

Example

```
Hero

Countdown

Gallery

Venue

RSVP

Timeline

Story

Footer
```

If a component is missing

Rendering stops.

---

# Component Props

Every component receives props.

Example

```ts
Hero

title

subtitle

backgroundImage

eventDate

buttonText

buttonLink
```

Example

```ts
Countdown

eventDate

labels

timezone
```

---

# Theme Resolution

The renderer loads:

* Colors
* Typography
* Radius
* Shadows
* Buttons
* Cards
* Icons

from Theme Tokens.

Components never define colors directly.

---

# Layout Resolution

Layout determines:

* Section order
* Section spacing
* Width
* Alignment
* Hero position
* Gallery style

Layouts never contain event data.

---

# Rendering Flow

```
Load Theme

↓

Load Layout

↓

Load Components

↓

Inject Event Data

↓

Validate Props

↓

Render

↓

Hydrate

↓

Publish
```

---

# Validation Rules

Before rendering

Validate

* Event title
* Event date
* Theme exists
* Layout exists
* Required components exist
* Required props exist

If validation fails

Rendering must stop.

---

# Fallback Strategy

If Gallery has no images

↓

Hide Gallery

If Music URL is empty

↓

Hide Music Player

If RSVP disabled

↓

Remove RSVP Component

---

# Component Visibility

Each component supports

```
visible = true

visible = false
```

Hidden components are ignored.

---

# Responsive Rendering

Breakpoints

```
Mobile

Tablet

Laptop

Desktop
```

Components adapt automatically.

---

# RTL Support

Arabic

↓

RTL

English

↓

LTR

The renderer automatically changes:

* Alignment
* Direction
* Icons
* Margins
* Navigation

---

# Dark Mode

Every theme supports

* Light
* Dark

No component should implement its own dark mode.

---

# SEO

Generate automatically

* Title
* Description
* Open Graph Image
* Twitter Card
* Canonical URL
* Structured Data

---

# Performance

Use

* Lazy Loading
* Dynamic Imports
* Image Optimization
* Font Optimization
* Route Caching
* CDN Assets

---

# Security

Escape all user input.

Sanitize HTML.

Validate URLs.

Reject unsupported file types.

Prevent XSS.

---

# Renderer Output

The renderer returns

```
Interactive React Website
```

containing

* Hero
* Countdown
* Story
* Venue
* Gallery
* RSVP
* Footer

depending on the selected layout.

---

# Error Handling

Missing Theme

↓

404 Theme

Missing Layout

↓

404 Layout

Missing Component

↓

Component Error

Invalid Props

↓

Validation Error

---

# Future Support

Planned features

* AI Theme Generator
* AI Layout Generator
* Live Preview
* Real-time Collaboration
* Multi-page Events
* Marketplace Components
* White Label Rendering

---

# Development Rules

* Stateless Renderer
* No Business Logic
* No Database Access
* No Authentication Logic
* Render Only
* Fully Typed
* Testable
* Modular
* Reusable

---

# Rendering Lifecycle

```
Request

↓

Load Event

↓

Load Theme

↓

Load Layout

↓

Load Components

↓

Merge Props

↓

Validate

↓

Render

↓

Return HTML + Hydration

↓

Client Interactive
```

---

# Success Criteria

The renderer is considered successful when:

* Every component renders correctly.
* Layout matches the selected design.
* Theme is applied consistently.
* Responsive behavior works.
* SEO metadata is generated.
* No runtime rendering errors occur.

---

End of Renderer Specification.
