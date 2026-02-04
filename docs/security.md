# Security Considerations

This project follows a defensive design approach focused on abuse prevention
and failure containment.

## Input Validation
All user input is validated at the service layer.
Handlers do not perform business-critical validation.

## Rate Limiting
Redis-based rate limiting is used to:
- prevent spam and flooding
- protect critical operations
- reduce automated abuse vectors

Rate limits are enforced using TTL-based counters and locks.

## Anti-Abuse Mechanisms
- FSM-based double-action protection
- Cooldown-enforced mechanics
- Time-limited and expiring game states

Abuse prevention logic is centralized at the service layer.

## Secrets Management
Sensitive configuration is injected via environment variables.
No secrets or credentials are stored in the repository.

## Failure Isolation
Redis or database failures do not crash the bot process.
The system degrades gracefully with reduced functionality
rather than failing hard.
