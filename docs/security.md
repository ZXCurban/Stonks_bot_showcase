# Security Considerations

This project follows a defensive design approach.

## Input Validation
All user input is validated at the service layer.

## Rate Limiting
Redis-based rate limiting is used to:
- prevent spam
- protect critical operations
- reduce abuse vectors

## Anti-Abuse Mechanisms
- Double-action protection
- Cooldown-based mechanics
- Time-limited game states

## Secrets Management
Sensitive configuration is injected via environment variables.
No secrets are stored in the repository.

## Failure Isolation
Redis or database failures do not crash the bot.
The system degrades gracefully.
