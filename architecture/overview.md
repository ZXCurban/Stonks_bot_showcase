# Architecture Overview

This project is a production-ready Telegram game backend built with an
event-driven, asynchronous architecture.

The system is designed to handle:
- concurrent users
- background schedulers
- time-based game mechanics
- dynamic market simulation

All critical state is externalized. Bot instances remain stateless and can be
scaled horizontally.

## Logical Layers

### Telegram Interface Layer
- Receives updates from Telegram
- Stateless handlers
- Minimal business logic
- Delegates work to the service layer
- User interaction flows are controlled via FSM

### Application / Service Layer
- Core game mechanics
- Market simulation
- Achievements and quest systems
- Risk-based and time-limited game mechanics
- Validation, orchestration, and enforcement of game rules

### Infrastructure Layer
- PostgreSQL for persistent state
- Redis for:
  - cooldowns and temporary state
  - rate limiting and anti-abuse
  - locks and TTL-based mechanics
- Isolated background schedulers

## Background Tasks

The system relies on background schedulers for non-interactive workloads:

- Market price updates (hourly)
- Trend recalculation
- Limited-time events (e.g. underground market)
- Cleanup and expiration jobs
- Message lifecycle management

Schedulers are isolated from request handlers and can be restarted
without affecting active user sessions.

## Reliability & Anti-Abuse

- Redis-based rate limiting
- FSM-based double-action protection
- Cooldown and TTL-enforced mechanics
- Idempotent service operations
- Graceful degradation in case of Redis or database failures
