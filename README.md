# Child Medical Screening (ChildScan Health)

A comprehensive mobile-first tool for pediatric health screenings. Medical professionals register children under 10, conduct health screenings, manage referrals to clinics or specialists, and coordinate field registrations — with a role-based team, parent notes, and AI-assisted screening advice.

## Features

- **Child registry** — register children with demographics, guardian contact, school, and bus/transport logistics (departure & estimated arrival at the IBO center).
- **Health screenings** — record height, weight, temperature, vision/hearing, general appearance, clinical findings, and a screening status (healthy / needs follow-up / referred / high risk).
- **Referrals** — create referrals to clinics, hospitals, or specialists with priority (routine / urgent / emergency) and lifecycle status (pending / scheduled / completed / cancelled).
- **High-risk automation** — high-risk screenings auto-create an urgent referral and email the examining clinician (backend function `handleHighRiskScreening`).
- **Referral follow-up** — scheduled workflow checks pending referrals and nudges them along (`checkReferralFollowup`).
- **AI exam advice** — per-child AI-generated screening recommendations based on clinical history.
- **Team & invitations** — invite doctors / charity admins; role-based access; doctor profiles with specialty, license number, age, background.
- **Charity admin field registration** — pre-screening registration with transport relay to the IBO center.
- **Notes & comments** — shared team notes board with urgent / non-urgent flags.
- **Instagram publishing** — post updates to a linked Instagram Business account (`postToInstagram`).

## Tech stack

- **Frontend:** React 18 + Vite, Tailwind CSS, shadcn/ui, lucide-react, react-router-dom, recharts, react-leaflet, framer-motion.
- **Backend / BaaS:** Base44 (auth, entities/database, integrations, scheduled workflows, hosting).
- **Integrations:** GitHub (connector), Google Calendar, Instagram Graph API, built-in LLM / email / file uploads.

## Project structure

```
src/
  pages/          # Dashboard, Children, ChildDetail, Screenings, Referrals,
                  # Users (team), DoctorProfile, InstagramPost, TeamChat (notes)
  components/     # Layout, dialogs, status badges, exam advice card, ui/ (shadcn)
  lib/            # Auth context, utils, query client
  api/            # base44Client (pre-initialized SDK)
base44/
  entities/       # Child, Screening, Referral, Note, User (JSON schemas + RLS)
  functions/      # handleHighRiskScreening, checkReferralFollowup, postToInstagram
  workflows/      # High-Risk Screening Followup (scheduled + entity triggers)
```

## Data model

- **Child** — full name, DOB, gender, guardian, address, school, registration number, registration status, bus departure / estimated arrival times.
- **Screening** — child link, examiner, vitals, vision/hearing, findings, status.
- **Referral** — child + screening link, facility, type, reason, specialty, priority, status.
- **Note** — content, author, priority (urgent / normal).
- **User** — role (admin / doctor / charity_admin), specialty, license number, profile fields.

Row-level security restricts Child / Screening / Referral / Note updates and deletes to the record creator or admins.

## Getting started (local development)

```bash
npm install
npm run dev
```

The app expects the Base44 environment to be configured (app id + service credentials provided by the Base44 platform). Frontend code talks to Base44 through the pre-initialized SDK at `@/api/base44Client`.

## Deployment

This project is hosted and deployed on the **Base44** platform.

1. Open the app in the Base44 builder.
2. Use **Settings → GitHub** to sync this repository (2-way sync) so source stays in sync.
3. Publish from the builder — Base44 builds and hosts the web app and ships the same code to iOS/Android.

Build outputs are standard Vite static assets; you can also self-host the `dist/` folder on any static host if you wire up the Base44 SDK env vars.

## License

Provided as-is for the ChildScan Health project.
