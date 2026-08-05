# Proposed Architecture

## Prototype components

- **Mobile app:** React Native + Expo + TypeScript
- **Admin portal:** Next.js + TypeScript
- **Shared package:** routing types, validation schemas, and pure routing functions
- **Prototype backend:** PostgreSQL with a managed API and authentication layer

## Core design decision

Keep emergency-routing logic deterministic and testable. The client receives a signed/current configuration, evaluates the user's residence and time, and always provides a universal fallback. No generative AI should decide which emergency service a student contacts.

## Data flow

1. An administrator publishes an effective-dated contact configuration.
2. The mobile app synchronizes and caches the latest approved configuration.
3. The student requests help.
4. The routing engine evaluates urgency, residence, time, and availability.
5. The app displays the matched contact and safe fallback.
6. The native dialler opens after confirmation.

## Environments

- Local: fictional data only
- Development: synthetic accounts and contacts
- Staging: approved test accounts and non-production numbers
- Production: only after institutional privacy, security, and emergency-response approval

## Testing priorities

- Boundary times at service opening and closing
- Daylight-saving changes in America/Toronto
- Academic term transitions
- Expired and overlapping assignments
- Missing residence configuration
- Offline and stale-cache behavior
- Accessibility and large-text layouts

