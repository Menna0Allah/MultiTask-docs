# Security

## Authentication Strategy
- JWT-based auth with short-lived access token and longer-lived refresh token.
- Access token lifetime: 60 minutes.
- Refresh token lifetime: 7 days.
- Refresh endpoint rotates/renews access for active sessions.

## Login Methods
- Email/username + password.
- Google OAuth (social login).

## Password Policy
- Minimum 8 characters.
- At least one uppercase letter.
- At least one number.

## Token Storage Decision
Current frontend stores tokens in `localStorage`.

Trade-offs:
- Pros: simple implementation and clear SPA session handling.
- Cons: higher XSS exposure than HttpOnly cookie strategy.
- Mitigations: strict input sanitization, dependency hygiene, and CSP hardening.

## Route and Data Protection
- Protected API routes require `Authorization: Bearer <token>`.
- Role and ownership checks enforce client/freelancer boundaries.
- Realtime channels validate authenticated identity and membership before subscription.

## Secrets Handling
- Secrets are injected via environment variables.
- Public docs expose only `.env.example` patterns, never real values.
- Keys to protect: Django secret, DB credentials, Stripe secrets, Gemini key, email credentials.

## PII Handling
- Profile and payment-related user data is treated as sensitive.
- Access is restricted to authenticated owners and authorized platform actions.
- Logs/analytics should avoid storing raw secrets and unnecessary personal fields.
