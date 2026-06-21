# MASTER PROMPT — DocTIP Graduation Presentation (43 Slides, Reveal.js + GSAP)

You are an expert front-end developer. Build a **single-file `index.html`** Reveal.js presentation for the DocTIP graduation project. Follow every instruction below exactly. Do NOT skip any slide. Do NOT add comments in code unless asked.

---

## ASSETS YOU HAVE ACCESS TO

Scan and use all files in these directories:
- `C:\Users\MSI\OneDrive\Bureau\presentation\` — main project folder
- `C:\Users\MSI\OneDrive\Bureau\presentation\figures\` — diagrams, screenshots, LaTeX-exported figures
- `C:\Users\MSI\OneDrive\Bureau\presentation\figures\logos\` — technology logos (PNG/SVG)

Key image files (use relative paths from the HTML file):
```
figures/aderfia-logo.png
figures/pagedegarde.png
figures/amwell.png
figures/nhs.png
figures/medisafe.png
figures/doctolib.png
figures/Scrum Project Management Process Infographic Presentation (1).png
figures/diagrams/gantt-chart.png
figures/diagrams/uc-general.png
figures/diagrams/uc-patient-dashboard.png
figures/diagrams/uc-doctor-dashboard.png
figures/diagrams/uc-doctor-profile.png
figures/diagrams/uc-admin-manage-doctors.png
figures/diagrams/uc-admin-manage-patients.png
figures/diagrams/class-diagram.png
figures/diagrams/seq-auth.png
figures/diagrams/seq-triage.png
figures/diagrams/seq-clinical-ai.png
figures/diagrams/seq-anomaly.png
figures/diagrams/activity-auth.png
figures/diagrams/activity-book.png
figures/diagrams/activity-triage.png
figures/diagrams/activity-pri.png
figures/diagrams/ai-architecture.png
figures/diagrams/system-architecture.png
figures/diagrams/security-architecture.png
figures/screen-auth-flow.png
figures/screen-patient-home.png
figures/screen-triage.png
figures/discover1.png
figures/discover2.png
figures/discover3.png
figures/book2.png
figures/book3.png
figures/screen-medical-record.png
figures/screen-medications.png
figures/screen-lab-results.png
figures/screen-recovery-index.png
figures/screen-predictive-risk.png
figures/screen-sleep.png
figures/screen-doctor-onboarding.png
figures/screen-doctor-home.png
figures/screen-patient-detail.png
figures/screen-clinical-notes.png
figures/screen-admin-dashboard.png
figures/screen-admin-doctors.png
figures/screen-admin-analytics.png
figures/logos/vscode.png
figures/logos/android-studio.png
figures/logos/react-native.png
figures/logos/expo.png
figures/logos/vite.jpeg
figures/logos/tailwind.png
figures/logos/supabase.png
figures/logos/postgresql.png
figures/logos/deno.png
figures/logos/openai.png
figures/logos/openrouter.png
figures/logos/zustand.svg
```

---

## DESIGN SYSTEM

### Color Palette (CSS variables)
```css
--bg: #F0F4FF;
--navy: #0A1F5C;
--accent: #4A7BF7;
--card-bg: #FFFFFF;
--card-border: #D6E4FF;
--card-fill: #EAF1FF;
--body-text: #2D3A5A;
--teal: #38BDF8;
--danger: #EF4444;
```

### Typography
- Font: Inter (Google Fonts) `https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap`
- Slide title: `2.6rem; 800; #0A1F5C`
- Section divider title: `3.5rem; 800; white`
- Subtitle/label: `1.1rem; 600`
- Body: `1rem; 400; line-height: 1.6`
- Pill badge: `0.72rem; 700; letter-spacing: 0.08em; uppercase`

### Components

**Pill badge** (above every slide title):
```css
background: #EAF1FF; color: #4A7BF7; border-radius: 999px; padding: 4px 16px; font-size: 0.72rem; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; display: inline-block; margin-bottom: 12px;
```

**Card**:
```css
background: #FFFFFF; border: 1.5px solid #D6E4FF; border-radius: 16px; padding: 24px; box-shadow: 0 4px 24px rgba(74,123,247,0.08);
```

**Left-border highlight card**:
```css
border-left: 4px solid #4A7BF7; background: #EAF1FF; border-radius: 0 12px 12px 0; padding: 16px 20px;
```

**Numbered circle**:
```css
width: 40px; height: 40px; border-radius: 50%; background: #0A1F5C; color: white; font-weight: 800; font-size: 1rem; display: flex; align-items: center; justify-content: center;
```

**Section divider slide**:
```css
background: linear-gradient(135deg, #0A1F5C 0%, #1a3a8f 100%); width: 100vw; height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: center;
```
Plus animated SVG dot-grid overlay.

### Layout Rules
- Slide padding: `60px 80px`
- Card gap: `24px`
- Two-column: `grid-template-columns: 1fr 1fr; gap: 32px`
- Content: top-aligned (`center: false`)
- All icons: inline SVG only

---

## ANIMATION SYSTEM (GSAP 3)

### CDN
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
```

### Slide Trigger
```javascript
const animators = {};
Reveal.on('slidechanged', ({ currentSlide }) => {
  gsap.killTweensOf(currentSlide.querySelectorAll('*'));
  gsap.set(currentSlide.querySelectorAll('[data-anim]'), { clearProps: 'all' });
  if (animators[currentSlide.dataset.slideId]) animators[currentSlide.dataset.slideId](currentSlide);
});
Reveal.on('ready', ({ currentSlide }) => {
  if (animators[currentSlide.dataset.slideId]) animators[currentSlide.dataset.slideId](currentSlide);
});
```

### Slide Transition (GSAP, not Reveal default)
- Outgoing: `scale(1)→0.92, opacity 1→0, 0.35s, power2.in`
- Incoming: `scale(0.92)→1, opacity 0→1, 0.5s, power4.out`
- Reveal init: `transition: 'none'`

### Per-Element Rules (apply ALL of these)
- **Pill badge**: `from { opacity:0, y:-12, scale:0.8, 0.4s, back.out(2) }`
- **Slide title**: `from { opacity:0, x:-50, skewX:4, 0.55s, expo.out, delay:0.15 }`
- **Section divider title**: `from { opacity:0, scale:0.65, y:20, 0.75s, back.out(1.8) }`
- **Section divider sub-pills**: `from { opacity:0, y:30, scale:0.85, stagger:0.1, back.out(2), 0.4s, delay:0.4 }`
- **Cards (grid-aware)**: top-left `{ x:-40,y:-30,rotate:-2 }`, top-right `{ x:+40,y:-30,rotate:+2 }`, bottom-left `{ x:-40,y:+40,rotate:-1.5 }`, bottom-right `{ x:+40,y:+40,rotate:+1.5 }`, center `{ y:+50,scale:0.85 }`. All to `{ x:0,y:0,opacity:1,rotate:0,scale:1, back.out(1.6), 0.55s, stagger:0.1 }`
- **Left column**: `from { x:-60, opacity:0, 0.5s, power4.out, stagger:0.08 }`
- **Right column**: `from { x:+60, opacity:0, 0.5s, power4.out, stagger:0.08, delay:0.1 }`
- **Numbered circles**: `from { scale:0, opacity:0, 0.4s, elastic.out(1.2,0.4), stagger:0.12 }`
- **Checkmark/teal icons**: `from { scale:0, rotate:-90, 0.35s, back.out(3), stagger:0.08 }`
- **Warning icons**: `from { scale:0, rotate:-45, 0.4s, back.out(3), stagger:0.1 }` then pulse once `{ scale:1.08, 0.2s, yoyo:true, repeat:1, delay:0.8 }`
- **Phone frames**: `from { y:60, opacity:0, scale:0.85, back.out(1.5), 0.6s, stagger:0.15 }`, inner content `{ opacity:0, y:10, 0.4s, delay:0.3 }`
- **Browser frames**: `from { scaleY:0, opacity:0, transformOrigin:'bottom center', 0.6s, power4.out }`, inner content staggers 0.35s after
- **Bullet items**: `from { x:-25, opacity:0, 0.35s, power3.out, stagger:0.07, delay:0.2 }`
- **Tech logo cards**: `from { rotateY:90, opacity:0, perspective:600, 0.45s, back.out(1.5), stagger:0.07 }`
- **Sprint/timeline bars**: track `from { scaleX:0, transformOrigin:'left', 1.0s, power3.out }`, boxes `from { scaleY:0, opacity:0, transformOrigin:'bottom', back.out(2), 0.35s, stagger:0.1 }`
- **SVG diagrams**: box `from { scale:0.8, opacity:0, back.out(1.5), 0.4s }`, label `from { opacity:0, y:5, 0.25s, delay:0.1 }`, line `from { strokeDashoffset:totalLength, 0.6s, power2.inOut }`, arrow `from { scale:0, opacity:0, elastic.out(1,0.4), 0.3s }`
- **Conclusion cards**: card1 `{ y:60, rotate:-3 }`, card2 `{ y:80, scale:0.85, delay:0.12 }`, card3 `{ y:60, rotate:+3, delay:0.24 }`
- **Thank You text**: `from { scale:0.5, opacity:0, elastic.out(1,0.3), 0.8s, delay:0.6 }`

### Continuous Animations
- Dot-grid on dividers: `to { y:-8, 2s, yoyo:true, repeat:-1, sine.inOut, stagger:0.3 }`
- Gradient shift: `to { backgroundPosition:'100% 100%', 1.5s, power2.inOut }`

### Micro-Interactions (global, always active)
- Card hover: `to { y:-6, scale:1.02, boxShadow:'0 12px 40px rgba(74,123,247,0.18)', 0.25s }`, leave: `to { y:0, scale:1, boxShadow:'0 4px 24px rgba(74,123,247,0.07)', 0.3s }`
- SVG icons pulse after entrance: `to { scale:1.1, 0.2s, yoyo:true, repeat:1, delay:0.8, stagger:0.05 }`

---

## REVEAL.JS SETUP

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.6.1/reveal.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.6.1/theme/white.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/reveal.js/4.6.1/reveal.min.js"></script>
```

```javascript
Reveal.initialize({
  hash: true, transition: 'none', backgroundTransition: 'none',
  width: 1280, height: 720, margin: 0, controls: true, progress: true, center: false, plugins: []
});
```

---

## SLIDE-BY-SLIDE CONTENT (43 slides)

Below, `<!-- IMG: path -->` means use `<img src="path">` inside a phone/frame mockup or as a standalone image. All text content is provided verbatim. Use the component styles defined above.

---

### SLIDE 1 — Cover (`data-slide-id="cover"`)

**Layout**: Full-screen centered, navy gradient background.

**Content**:
- EPI logo area (text: "EPI — Private International Higher School of Polytechnic")
- Ministry line: "Ministry of Higher Education and Scientific Research"
- Academic year: "ACADEMIC YEAR 2025/2026"
- Title: "Conception and Development of an AI Powered Intelligent Health Management Platform"
- Subtitle: "Graduation Project — Software Engineering"
- Company: <!-- IMG: figures/aderfia-logo.png --> ADERFIA Incorporation
- Authors: "Achieved by: Mouhamed Aziz Tounsi"
- Supervisors: "Supervised by: Mr. Ahmed Ben Ayed | Mr. Yassine Chaabane"

**Animation**: Title scales in from 0.5 with elastic ease, subtitle fades up, logos flip in.

---

### SLIDE 2 — Plan (`data-slide-id="plan"`)

**Layout**: Two-column with numbered circles on left.

**Content** — Table of contents with 6 sections:
```
01  General Context
02  Conceptual Design
03  Implementation
04  Conclusion
```

Each section has a numbered circle (navy bg, white text) + section title. Use pill badges for section numbers.

**Animation**: Numbered circles pop in with elastic ease, staggered left to right.

---

### SLIDE 3 — Divider: "01 — General Context" (`data-slide-id="div-context"`)

**Layout**: Full-screen navy gradient with dot-grid overlay.

**Content**:
- Large "01" number (white, 6rem)
- Title: "General Context"
- Sub-pills: "Problem Statement" | "Existing Solutions" | "Proposed Solution" | "Requirements"

**Animation**: Title scales in, sub-pills pop up staggered, dot-grid floats continuously.

---

### SLIDE 4 — Introduction (`data-slide-id="intro"`)

**Pill**: OVERVIEW
**Title**: Introduction

**Content** (two-column):
- **Left**: Text block — "The healthcare sector is undergoing a profound digital transformation, driven by the convergence of mobile technologies, cloud computing, and artificial intelligence. Yet, the management of medical practices remains fragmented: patient records are scattered across disconnected platforms, communication is limited, and intelligent tools for clinical decision support are largely absent."
- **Right**: Key points cards:
  - "Patients expect seamless digital experiences"
  - "Healthcare professionals face mounting administrative burdens"
  - "No integrated solution combines all features"

**Animation**: Left text slides in from left, right cards pop in from right.

---

### SLIDE 5 — Host Organization (`data-slide-id="org"`)

**Pill**: HOST ORGANIZATION
**Title**: Aderfia Incorporation

**Content** (two-column):
- **Left**: <!-- IMG: figures/aderfia-logo.png --> Logo + text: "A young Tunisian startup focused on integration of advanced technologies in the healthcare domain. Operates at the intersection of medical practice and digital innovation."
- **Right**: 4 cards with inline SVG icons:
  - "Medical Application Development"
  - "AI Integration"
  - "Telemedicine & Remote Monitoring"
  - "Health Data Security"

**Animation**: Logo fades in, cards stagger from right with rotate.

---

### SLIDE 6 — Problem Statement (`data-slide-id="problem"`)

**Pill**: PROBLEM STATEMENT
**Title**: Identified Gaps in Healthcare Systems

**Content**: 5 left-border highlight cards stacked vertically:
1. "Data Fragmentation — Medical info scattered across disconnected systems"
2. "Lack of Intelligent Monitoring — No composite recovery index"
3. "Insufficient Communication — No real-time messaging, video calls, or AI triage"
4. "Inadequate Security — Simple username/password doesn't meet medical standards"
5. "No Clinical Decision Support — Physicians lack AI tools for diagnosis"

**Animation**: Cards slide in from left, staggered, each with a warning icon that pulses.

---

### SLIDE 7 — Existing Solutions (`data-slide-id="existing"`)

**Pill**: EXISTING SOLUTIONS
**Title**: Analysis of Competing Platforms

**Content**: 4 cards in 2x2 grid:
- **Amwell**: <!-- IMG: figures/amwell.png --> "Online consultation, appointment management. Limitations: Unattractive UI, no AI, no recovery tracking."
- **NHS App**: <!-- IMG: figures/nhs.png --> "Medical records access. Limitations: No video, no messaging, no clinical AI."
- **Medisafe**: <!-- IMG: figures/medisafe.png --> "Medication tracking, reminders. Limitations: No consultations, no records, no doctor-patient communication."
- **Doctolib**: <!-- IMG: figures/doctolib.png --> "Appointment booking, teleconsultation. Limitations: No medical records, no recovery tracking, no clinical AI."

Each card has a small screenshot thumbnail and bullet points.

**Animation**: Cards animate grid-aware (top-left from -40,-30, etc.).

---

### SLIDE 8 — Comparative Study (`data-slide-id="comparative"`)

**Pill**: COMPARATIVE STUDY
**Title**: Feature Coverage Comparison

**Content**: A styled comparison table with checkmarks (teal SVG) and X marks (danger SVG):

| Criterion | Amwell | NHS | Medisafe | Doctolib |
|---|---|---|---|---|
| Video consultation | ✓ | ✗ | ✗ | ✓ |
| Appointment management | ✓ | ✓ | ✗ | ✓ |
| Integrated medical record | ✓ | ✓ | ✗ | ✗ |
| Instant messaging | ✗ | ✗ | ✗ | ✗ |
| Medication tracking | ✗ | ✗ | ✓ | ✗ |
| AI symptom triage | ✗ | ✗ | ✗ | ✗ |
| AI diagnostic assistance | ✗ | ✗ | ✗ | ✗ |
| Laboratory results | ✗ | Partial | ✗ | ✗ |
| Recovery index | ✗ | ✗ | ✗ | ✗ |
| Admin dashboard | ✗ | ✗ | ✗ | Partial |
| Zero Trust security | ✗ | ✗ | ✗ | ✗ |

Below: Bar chart showing "Features Supported (out of 12)" — Amwell: 4, NHS: 5, Medisafe: 1, Doctolib: 5.

**Animation**: Table rows slide in staggered, checkmarks pop with elastic ease.

---

### SLIDE 9 — Proposed Solution (`data-slide-id="solution"`)

**Pill**: PROPOSED SOLUTION
**Title**: DocTIP — AI Powered Health Management Platform

**Content**: Center card with 3 connected portal icons:
- **Patient Mobile App** (phone icon): "Cross-platform iOS/Android. Appointment booking, medical records, AI triage, medications, messaging, video calls."
- **Doctor Mobile App** (stethoscope icon): "Patient management, clinical AI tools, SOAP notes, differential diagnosis, ORION assistant."
- **Web Admin Dashboard** (monitor icon): "Platform supervision, doctor verification, analytics, AI monitoring."

Connected by lines to a central "Supabase Backend" node.

**Animation**: Central node scales in, then portal cards pop out from it, connection lines draw.

---

### SLIDE 10 — Project Objectives (`data-slide-id="objectives"`)

**Pill**: OBJECTIVES
**Title**: Project Goals

**Content**: 8 numbered items in 2x4 grid, each with a numbered circle + text:
1. "Centralize medical data in secure PostgreSQL database"
2. "Cross-platform mobile app (iOS & Android)"
3. "Web administration dashboard"
4. "AI modules: triage, diagnosis, SOAP notes, risk prediction"
5. "Telemedicine: real-time video & audio calls"
6. "Zero Trust security model with anomaly detection"
7. "Patient Recovery Index (PRI) — weighted composite 0-100"
8. "Internationalization: 3 languages, 3 currencies"

**Animation**: Numbered circles pop with elastic ease, staggered.

---

### SLIDE 11 — Actor Identification (`data-slide-id="actors"`)

**Pill**: ACTORS
**Title**: System Actors

**Content**: 3 large cards side by side:
- **Patient** (person icon): "Browse doctors, book appointments, access medical record, track medications, use AI triage, chat & video calls, emergency mode"
- **Doctor** (doctor icon): "Manage patients, diagnoses, prescriptions, lab requests, AI clinical tools, ORION assistant, voice scribe"
- **Admin** (shield icon): "Platform supervision, doctor verification, patient management, analytics, AI monitoring, complaint moderation"

**Animation**: Cards pop in from bottom, staggered.

---

### SLIDE 12 — Functional Requirements: Patient (`data-slide-id="req-patient"`)

**Pill**: REQUIREMENTS
**Title**: Functional Requirements — Patient

**Content**: Left column list with checkmark icons:
- Browse doctors by specialty, map view
- Book appointments (clinic/home/video)
- Manage appointments (cancel, reschedule, video call)
- Medical record (blood type, allergies, conditions, history)
- Lab results with trend charts
- Medication tracking with adherence ring
- AI symptom triage
- Real-time messaging (text, images, files)
- Video/audio teleconsultation
- Predictive risk scores
- Emergency SOS mode

**Animation**: Items slide in from left, checkmarks pop in 0.05s before text.

---

### SLIDE 13 — Functional Requirements: Doctor (`data-slide-id="req-doctor"`)

**Pill**: REQUIREMENTS
**Title**: Functional Requirements — Doctor

**Content**: Left column list with checkmark icons:
- Manage patient list with detailed profiles
- Multi-medication prescriptions
- Interactive calendar with heat map
- Diagnosis with ICD codes
- AI differential diagnosis
- Lab analysis requests
- Operation planning
- AI SOAP note generation
- Voice Scribe (4 templates)
- ORION AI clinical assistant
- Risk Radar dashboard
- Per-patient AI analytics

**Animation**: Same as slide 12.

---

### SLIDE 14 — Functional Requirements: Admin (`data-slide-id="req-admin"`)

**Pill**: REQUIREMENTS
**Title**: Functional Requirements — Administrator

**Content**: Left column list with checkmark icons:
- Real-time KPI dashboard
- Doctor management (approve/reject/suspend)
- Patient management with enriched profiles
- Appointment filtering and status management
- Prescription tracking
- Laboratory results with anomaly flags
- Review moderation
- Messaging supervision (read-only)
- Notification management (broadcast)
- Complaint pipeline (open→review→resolved)
- Platform analytics
- AI usage monitoring
- Platform configuration

**Animation**: Same pattern.

---

### SLIDE 15 — Non-Functional Requirements (`data-slide-id="nfr"`)

**Pill**: NON-FUNCTIONAL
**Title**: Non-Functional Requirements

**Content**: 5 cards in layout:
- **Security**: "JWT auth, Row Level Security, Zero Trust architecture, device fingerprinting, audit logging"
- **Performance**: "Serverless auto-scaling, optimized indexes, real-time subscriptions, offline cache"
- **Maintainability**: "Strict TypeScript, modular architecture, reusable components, Zustand stores"
- **Usability**: "Premium UI with animations, haptic feedback, RTL support, rich visual components"
- **Availability**: "Managed infrastructure, partial offline mode, cross-platform (iOS, Android, Web)"

**Animation**: Cards stagger from different directions.

---

### SLIDE 16 — Work Methodology (`data-slide-id="methodology"`)

**Pill**: METHODOLOGY
**Title**: Agile Scrum Methodology

**Content**: Two-column:
- **Left**: Text — "Adopted Scrum for rapid iterations, adaptability, value-based prioritization, and continuous delivery. 2-week sprints, each delivering a testable functional increment."
- **Right**: <!-- IMG: figures/Scrum Project Management Process Infographic Presentation (1).png --> Scrum cycle diagram

**Animation**: Text slides in left, image fades in right.

---

### SLIDE 17 — Sprint Planning & Gantt (`data-slide-id="planning"`)

**Pill**: PLANNING
**Title**: Sprint Planning & Gantt Chart

**Content**: Two-column:
- **Left**: Sprint table:
  | Sprint | Module | Deliverables |
  |---|---|---|
  | 0 | Analysis | Requirements, UML diagrams |
  | 1 | Core Foundation | PostgreSQL, Auth, RLS |
  | 2 | Mobile Foundations | Onboarding, profiles, records |
  | 3 | Scheduling & Meds | Appointments, medications |
  | 4 | Labs & Messaging | Lab results, real-time chat |
  | 5 | Clinical AI | AI triage, SOAP, video calls |
  | 6 | Admin & Analytics | Web dashboard, monitoring |
  | 7 | Advanced Features | PRI, emergency, deployment |

- **Right**: <!-- IMG: figures/diagrams/gantt-chart.png --> Gantt chart

**Animation**: Table rows slide in staggered, Gantt chart draws from left.

---

### SLIDE 18 — Divider: "02 — Conceptual Design" (`data-slide-id="div-design"`)

**Layout**: Full-screen navy gradient with dot-grid overlay.

**Content**:
- "02"
- "Conceptual Design"
- Sub-pills: "Use Case Diagrams" | "Class Diagram" | "Sequence Diagrams" | "Activity Diagrams" | "AI Architecture"

**Animation**: Same as divider pattern.

---

### SLIDE 19 — General Use Case Diagram (`data-slide-id="uc-general"`)

**Pill**: USE CASES
**Title**: General Use Case Diagram

**Content**: <!-- IMG: figures/diagrams/uc-general.png --> Full-width image of the general use case diagram. Below: 3 actor badges (Patient, Doctor, Admin) with key use cases listed.

**Animation**: Image scales in from 0.85, actor badges pop up below.

---

### SLIDE 20 — Refined UC: Patient Profile (`data-slide-id="uc-patient-profile"`)

**Pill**: USE CASE REFINEMENT
**Title**: Manage Patient Profile

**Content**: Two-column:
- **Left**: <!-- IMG: figures/diagrams/uc-patient-detail.png --> Use case diagram image
- **Right**: Key scenarios card:
  - "Edit personal info, emergency contact"
  - "Manage health profile (allergies, conditions)"
  - "Manage insurance and payment"
  - "Manage medical record and settings"
  - "Contact support"

**Animation**: Diagram slides in from left, scenario cards from right.

---

### SLIDE 21 — Refined UC: Patient Dashboard (`data-slide-id="uc-patient-dash"`)

**Pill**: USE CASE REFINEMENT
**Title**: Consult Patient Dashboard

**Content**: Two-column:
- **Left**: <!-- IMG: figures/diagrams/uc-patient-dashboard.png --> Use case diagram
- **Right**: Key scenarios:
  - "Consult schedule, recovery index, health insights"
  - "Manage services (sleep, activity, lab results)"
  - "Manage medications (add, edit, mark taken)"
  - "Interact with AI health assistant"
  - "Predict health risks"

**Animation**: Same pattern.

---

### SLIDE 22 — Refined UC: Doctor Dashboard (`data-slide-id="uc-doctor-dash"`)

**Pill**: USE CASE REFINEMENT
**Title**: Consult Doctor Dashboard

**Content**: Two-column:
- **Left**: <!-- IMG: figures/diagrams/uc-doctor-dashboard.png --> Use case diagram
- **Right**: Key scenarios:
  - "Consult schedule, risk radar, critical alerts"
  - "Manage clinical tools (differential, SOAP, voice scribe)"
  - "Interact with AI clinical assistant"
  - "Generate population health insights"

**Animation**: Same pattern.

---

### SLIDE 23 — Refined UC: Manage Doctors (`data-slide-id="uc-manage-docs"`)

**Pill**: USE CASE REFINEMENT
**Title**: Manage Doctors (Admin)

**Content**: Two-column:
- **Left**: <!-- IMG: figures/diagrams/uc-admin-manage-doctors.png --> Use case diagram
- **Right**: Key scenarios:
  - "Consult doctors list with filters"
  - "View doctor info and credentials"
  - "Approve / Reject / Suspend / Delete"

**Animation**: Same pattern.

---

### SLIDE 24 — Refined UC: Manage Patients (`data-slide-id="uc-manage-patients"`)

**Pill**: USE CASE REFINEMENT
**Title**: Manage Patients (Admin)

**Content**: Two-column:
- **Left**: <!-- IMG: figures/diagrams/uc-admin-manage-patients.png --> Use case diagram
- **Right**: Key scenarios:
  - "Consult patient list"
  - "View patient profiles with PRI score"
  - "Suspend / Delete patient accounts"

**Animation**: Same pattern.

---

### SLIDE 25 — Class Diagram (`data-slide-id="class-diagram"`)

**Pill**: STATIC MODEL
**Title**: System Class Diagram

**Content**: <!-- IMG: figures/diagrams/class-diagram.png --> Full-width class diagram image. Below: key classes listed as pill badges: "User", "Patient", "Doctor", "Admin", "Appointment", "Prescription", "Diagnosis", "MedicalRecord", "RecoveryScore", "TriageSession"

**Animation**: Diagram draws in (scaleY from 0), class badges pop staggered.

---

### SLIDE 26 — Sequence: Authentication (`data-slide-id="seq-auth"`)

**Pill**: SEQUENCE DIAGRAM
**Title**: Authentication Flow

**Content**: <!-- IMG: figures/diagrams/seq-auth.png --> Sequence diagram image. Right side: numbered steps:
1. "User enters email & password"
2. "Supabase Auth validates credentials"
3. "JWT token generated"
4. "User redirected to role-specific portal"

**Animation**: Diagram slides in from left, steps appear staggered from right.

---

### SLIDE 27 — Sequence: AI Triage (`data-slide-id="seq-triage"`)

**Pill**: SEQUENCE DIAGRAM
**Title**: AI Symptom Triage

**Content**: <!-- IMG: figures/diagrams/seq-triage.png --> Sequence diagram. Right side: numbered steps:
1. "Patient describes symptoms"
2. "Edge Function builds clinical prompt"
3. "GPT-4 returns urgency, conditions, specialty"
4. "Session persisted to database"
5. "Emergency flag triggers alert if critical"

**Animation**: Same pattern.

---

### SLIDE 28 — Sequence: AI Clinical Assistance (`data-slide-id="seq-clinical"`)

**Pill**: SEQUENCE DIAGRAM
**Title**: AI Clinical Diagnostic Assistance

**Content**: <!-- IMG: figures/diagrams/seq-clinical-ai.png --> Sequence diagram. Right side: numbered steps:
1. "Doctor selects patient, enters symptoms"
2. "System fetches patient context (allergies, conditions)"
3. "GPT-4 returns ranked diagnoses + ICD-10 + red flags"
4. "Doctor writes SOAP note, saves to database"

**Animation**: Same pattern.

---

### SLIDE 29 — Activity: Appointment Booking (`data-slide-id="activity-book"`)

**Pill**: ACTIVITY DIAGRAM
**Title**: Appointment Booking Workflow

**Content**: <!-- IMG: figures/diagrams/activity-book.png --> Activity diagram. Right side: key decision points highlighted.

**Animation**: Diagram scales in, decision nodes pulse.

---

### SLIDE 30 — Activity: AI Triage (`data-slide-id="activity-triage"`)

**Pill**: ACTIVITY DIAGRAM
**Title**: AI Symptom Triage Workflow

**Content**: <!-- IMG: figures/diagrams/activity-triage.png --> Activity diagram. Right side: flow steps.

**Animation**: Same pattern.

---

### SLIDE 31 — AI Module Architecture (`data-slide-id="ai-arch"`)

**Pill**: AI ARCHITECTURE
**Title**: Artificial Intelligence Module Architecture

**Content**: Two-column:
- **Left**: <!-- IMG: figures/diagrams/ai-architecture.png --> Architecture diagram
- **Right**: Module inventory table:
  | # | Module | Location |
  |---|---|---|
  | 1 | ai-triage | Edge (GPT-4) |
  | 2 | ai-clinical-support | Edge (GPT-4) |
  | 3 | compute-pri | Edge (algo) |
  | 4 | generateSOAPNote | Client (nano) |
  | 5 | getDifferentialDiagnosis | Client (nano) |
  | 6 | predictHealthRisks | Client (nano) |
  | 7 | analyzeBehavioralHealth | Client (nano) |
  | 8 | analyzeVoice | Client (nano) |

**Animation**: Diagram draws in, table rows slide in staggered.

---

### SLIDE 32 — Divider: "03 — Implementation" (`data-slide-id="div-impl"`)

**Layout**: Full-screen navy gradient with dot-grid overlay.

**Content**:
- "03"
- "Implementation"
- Sub-pills: "System Architecture" | "Technologies" | "Patient Portal" | "Doctor Portal" | "Admin Dashboard"

**Animation**: Divider pattern.

---

### SLIDE 33 — System Architecture (`data-slide-id="sys-arch"`)

**Pill**: ARCHITECTURE
**Title**: DocTIP System Architecture

**Content**: <!-- IMG: figures/diagrams/system-architecture.png --> Full-width architecture diagram. Below: 3 layer badges:
- "Presentation Layer: React Native + Expo | React + Vite"
- "Business Logic: Edge Functions + Client AI"
- "Data Layer: PostgreSQL + RLS + Realtime + Storage"

**Animation**: Architecture draws in, layer badges pop below.

---

### SLIDE 34 — Technologies Used (`data-slide-id="tech"`)

**Pill**: TECHNOLOGIES
**Title**: Technology Stack

**Content**: Tech logo cards in 4x3 grid (flip-in animation):
<!-- IMG: figures/logos/vscode.png --> VS Code
<!-- IMG: figures/logos/android-studio.png --> Android Studio
<!-- IMG: figures/logos/react-native.png --> React Native
<!-- IMG: figures/logos/expo.png --> Expo
<!-- IMG: figures/logos/vite.jpeg --> Vite
<!-- IMG: figures/logos/tailwind.png --> Tailwind CSS
<!-- IMG: figures/logos/supabase.png --> Supabase
<!-- IMG: figures/logos/postgresql.png --> PostgreSQL
<!-- IMG: figures/logos/deno.png --> Deno
<!-- IMG: figures/logos/openai.png --> OpenAI
<!-- IMG: figures/logos/openrouter.png --> OpenRouter
<!-- IMG: figures/logos/zustand.svg --> Zustand

Each card: logo image + name below.

**Animation**: Cards flip in from rotateY(90), staggered left-to-right, row-by-row.

---

### SLIDE 35 — Patient Portal: Auth & Onboarding (`data-slide-id="pp-auth"`)

**Pill**: PATIENT PORTAL
**Title**: Authentication & Onboarding

**Content**: Phone frame mockups showing:
<!-- IMG: figures/screen-auth-flow.png -->
<!-- IMG: figures/roledoct1.png -->
<!-- IMG: figures/patientlogin.png -->
<!-- IMG: figures/patientregistre.png -->

Text: "Role selection → Login → Registration → 4-step onboarding wizard (personal, medical, allergies, lifestyle)"

**Animation**: Phone frames rise from bottom, staggered.

---

### SLIDE 36 — Patient Portal: Home Dashboard (`data-slide-id="pp-home"`)

**Pill**: PATIENT PORTAL
**Title**: Home Dashboard

**Content**: Phone frame mockup:
<!-- IMG: figures/screen-patient-home.png -->

Feature bullets:
- "Weekly calendar strip with interactive day pills"
- "AI-powered health insight card (10min cache)"
- "Quick actions: appointments, records, medications, triage"
- "Upcoming appointments with doctor avatar"
- "Medication reminders with adherence ring"

**Animation**: Phone frame rises, bullets slide in from right.

---

### SLIDE 37 — Patient Portal: AI Triage (`data-slide-id="pp-triage"`)

**Pill**: PATIENT PORTAL
**Title**: AI Symptom Triage

**Content**: Phone frame mockup:
<!-- IMG: figures/screen-triage.png -->

Feature bullets:
- "Conversational AI interface (GPT-4)"
- "Urgency assessment: low/moderate/high/emergency"
- "Possible conditions ranked by likelihood"
- "Recommended specialty + follow-up questions"
- "Action plan: immediate, short-term, long-term"

**Animation**: Phone frame rises, bullets slide in.

---

### SLIDE 38 — Patient Portal: Appointments (`data-slide-id="pp-appt"`)

**Pill**: PATIENT PORTAL
**Title**: Appointment Booking

**Content**: Phone frame mockups (3 images in row):
<!-- IMG: figures/discover1.png -->
<!-- IMG: figures/discover2.png -->
<!-- IMG: figures/book2.png -->

Feature bullets:
- "Browse doctors by specialty (16 categories)"
- "Interactive Leaflet map view"
- "Visit type: clinic, home, video"
- "AI-optimized time slot suggestions"

**Animation**: Phone frames stagger up, bullets from right.

---

### SLIDE 39 — Patient Portal: Medical Record & Meds (`data-slide-id="pp-record"`)

**Pill**: PATIENT PORTAL
**Title**: Medical Record & Medications

**Content**: Phone frame mockups side by side:
<!-- IMG: figures/screen-medical-record.png -->
<!-- IMG: figures/screen-medications.png -->

Feature bullets:
- "Complete health profile: blood type, allergies, conditions, history"
- "Daily dose-by-dose tracking"
- "Adherence progress ring"
- "15-minute cron reminders via FCM"

**Animation**: Phone frames rise, bullets slide in.

---

### SLIDE 40 — Patient Portal: Lab Results & PRI (`data-slide-id="pp-labs"`)

**Pill**: PATIENT PORTAL
**Title**: Lab Results & Recovery Index

**Content**: Phone frame mockups side by side:
<!-- IMG: figures/screen-lab-results.png -->
<!-- IMG: figures/screen-recovery-index.png -->

Feature bullets:
- "Per-biomarker values with reference ranges"
- "Trend charts with cubic Bézier smoothing"
- "OCR upload: GPT-4o Vision parses paper reports"
- "PRI: weighted composite 0-100 (adherence, labs, activity, evaluation)"
- "Radar chart + 7-day history + recovery drivers"

**Animation**: Same pattern.

---

### SLIDE 41 — Doctor Portal: Dashboard (`data-slide-id="dp-home"`)

**Pill**: DOCTOR PORTAL
**Title**: Doctor Dashboard

**Content**: Phone frame mockups:
<!-- IMG: figures/screen-doctor-home.png -->
<!-- IMG: figures/screen-doctor-onboarding.png -->

Feature bullets:
- "Daily schedule calendar"
- "Real-time stats: appointments, patients, rating"
- "AI clinical intelligence card"
- "Critical lab result alerts"
- "4-step onboarding wizard with verification"

**Animation**: Phone frames rise, bullets from right.

---

### SLIDE 42 — Doctor Portal: Clinical AI Tools (`data-slide-id="dp-ai"`)

**Pill**: DOCTOR PORTAL
**Title**: Clinical AI Tools

**Content**: Phone frame mockups:
<!-- IMG: figures/screen-clinical-notes.png -->
<!-- IMG: figures/screen-patient-detail.png -->

Feature bullets:
- "AI SOAP note generation (24 complaints, 18 findings)"
- "Differential diagnosis: ranked by confidence + ICD-10 + red flags"
- "ORION: persistent AI chatbot (drug interactions, guidelines, dosage)"
- "Voice Scribe: 4 templates, AI polish"
- "Risk Radar: all patients by risk score"

**Animation**: Same pattern.

---

### SLIDE 43 — Web Admin Dashboard (`data-slide-id="admin"`)

**Pill**: ADMIN DASHBOARD
**Title**: Web Administration Dashboard

**Content**: Browser frame mockups:
<!-- IMG: figures/screen-admin-dashboard.png -->
<!-- IMG: figures/screen-admin-doctors.png -->
<!-- IMG: figures/screen-admin-analytics.png -->

Feature bullets:
- "Real-time KPIs: patients, doctors, appointments, PRI"
- "Doctor management: approve/reject/suspend"
- "Patient profiles with enriched data"
- "Analytics: user growth, specialty rankings, triage distribution"
- "22 pages with sidebar navigation"

**Animation**: Browser frames scale from bottom, bullets stagger.

---

### SLIDE 44 — Difficulties & Solutions (`data-slide-id="difficulties"`)

**Pill**: CHALLENGES
**Title**: Difficulties Encountered & Solutions

**Content**: 6 cards in 2x3 grid, each with problem → solution:

1. "WebView ES6 compatibility → Rewritten in ES5 syntax"
2. "Overpass API reliability → Multi-endpoint cascade + Nominatim fallback"
3. "AI JSON parsing → aiJSON() with markdown stripping, brace matching"
4. "Medical data authorization → doctor_patient_relationships table in RLS"
5. "Real-time message sync → Client-side dedup + reconnection logic"
6. "Push notification targeting → Scheduled Edge Function + FCM dispatch"

**Animation**: Cards pop in grid-aware, problem icons pulse.

---

### SLIDE 45 — Divider: "04 — Conclusion" (`data-slide-id="div-conclusion"`)

**Layout**: Full-screen navy gradient with dot-grid overlay.

**Content**:
- "04"
- "Conclusion & Perspectives"

**Animation**: Divider pattern.

---

### SLIDE 46 — Conclusion & Perspectives (`data-slide-id="conclusion"`)

**Pill**: CONCLUSION
**Title**: Project Outcomes & Future Perspectives

**Content**: Two-column:
- **Left** — Achievements (3 cards stacked):
  1. "Coherent system: patient app + doctor app + admin dashboard"
  2. "AI-powered triage, diagnosis support, clinical documentation"
  3. "Zero Trust security with anomaly detection"
- **Right** — Future Perspectives (bullet list):
  - "Offline capabilities for constrained connectivity"
  - "Wearable health data integration"
  - "Enhanced AI for voice & image workflows"
  - "Pharmacy & clinical workflow integration"
  - "Multi-clinic administration"
  - "Compliance alignment (HIPAA, NIST)"

**Animation**: Achievement cards slide in from left with slight rotate, perspective bullets from right.

---

### SLIDE 47 — Thank You (`data-slide-id="thankyou"`)

**Layout**: Full-screen centered, navy gradient.

**Content**:
- Large "Thank You" text (white, 4rem, 800 weight)
- "Mouhamed Aziz Tounsi"
- "DocTIP — AI Powered Intelligent Health Management Platform"
- "ADERFIA Incorporation"
- <!-- IMG: figures/aderfia-logo.png -->
- Academic year: "2025/2026"

**Animation**: "Thank You" scales in with elastic ease, other elements fade up staggered.

---

## IMPORTANT IMPLEMENTATION NOTES

1. **Single HTML file**: Everything in one `index.html`. Inline `<style>` for all CSS, inline `<script>` for all JS.
2. **No comments in code** unless explicitly asked.
3. **43 `<section>` tags**, each with `data-slide-id` attribute.
4. **Section dividers** use `data-background` with the navy gradient.
5. **Phone mockups**: Use `<div class="phone-frame">` with rounded corners, shadow, and the screenshot inside.
6. **Browser mockups**: Use `<div class="browser-frame">` with title bar dots and screenshot.
7. **All images**: Use `max-width: 100%; height: auto;` to fit containers.
8. **Responsive**: The presentation is fixed at 1280x720.
9. **Each slide must have its animator entry** in the `animators` object.
10. **Test all animations** — every element on every slide must animate in.

Build the complete `index.html` now. Every slide. Every animation. Every image reference. No shortcuts.
