# Architecture Overview

This project is a production-ready Telegram game backend built with an
event-driven and asynchronous architecture.

The system is designed to handle:
- concurrent users
- background schedulers
- time-based game mechanics
- dynamic market simulation

All critical state is externalized and the bot instances remain stateless.

## Logical Layers

### Telegram Interface Layer
- Receives updates from Telegram
- Stateless handlers
- Minimal business logic
- Delegates work to service layer

### Application / Service Layer
- Core game mechanics
- Market simulation
- Achievements and quests
- Risk-based mini-games
- Validation and orchestration

### Infrastructure Layer
- PostgreSQL for persistent state
- Redis for:
  - cooldowns
  - temporary game state
  - rate limiting
  - locks and TTL-based mechanics
- Background schedulers

## Background Tasks

The system relies heavily on background schedulers:

- Market price updates (hourly)
- Trend recalculation
- Limited-time events (black market)
- Cleanup jobs
- Message lifecycle management

Schedulers are isolated from request handlers and protected from crashes.

## Reliability & Anti-Abuse

- Redis-based rate limiting
- Silent spam mitigation
- Double-action protection
- TTL-based locks
- Idempotent operations
- Graceful degradation when Redis is unavailable
