# UW Residence Response

An early-stage mobile application concept that helps University of Waterloo residence students quickly identify and contact the correct emergency or after-hours support service.

> This project is a student-led prototype. It is not affiliated with, endorsed by, or a replacement for University of Waterloo emergency services or 911.

## Product goal

Make the correct help option obvious in a stressful moment. The app will use a student's residence, the current term, the time, and approved service hours to display the appropriate contact route.

## Initial MVP

- Student onboarding and residence registration
- Residence- and term-aware contact directory
- Time-aware availability for services such as CRT and Duty Dons
- One-tap native calling
- A short “Not sure who to call?” decision guide
- Residence address card for communicating a location to 911
- Offline access to critical contact information
- Web admin portal for approved contact and schedule updates

## Repository layout

```text
apps/
  mobile/           Student-facing iOS/Android app (planned)
  admin/            Campus Housing admin portal (planned)
packages/
  shared/           Shared types, validation, and routing logic (planned)
docs/
  product-plan.md   Product requirements and roadmap
  architecture.md   Proposed technical architecture
```

## Proposed stack

- Mobile: React Native with Expo and TypeScript
- Admin portal: Next.js and TypeScript
- Backend: Supabase/PostgreSQL for the prototype
- Validation: Zod
- Tests: Vitest/Jest and React Native Testing Library

The production identity and hosting approach must be reviewed with the University before using Waterloo credentials or real student data.

## Collaboration workflow

1. Create an issue describing the change.
2. Create a branch such as `feature/contact-routing`.
3. Keep commits small and descriptive.
4. Open a pull request into `main`.
5. Have the other contributor review it before merging.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## Safety rule

The product must never delay access to 911. Any uncertain or high-risk situation should make the 911 option immediately available.

