# Scalability Notes

The system is designed with horizontal scalability in mind.

## Stateless Bot Instances
Telegram bot handlers do not store any local state.
Multiple bot instances can be run in parallel.

## Externalized State
All shared state is stored outside the application:
- Redis for volatile and time-sensitive data
- PostgreSQL for persistent data

## Background Tasks
Schedulers are isolated from request handlers and can be:
- run in separate processes
- scaled independently
- restarted without affecting user sessions

## Bottleneck Awareness
Potential bottlenecks are well understood:
- database write-heavy operations
- scheduled fan-out notifications

Mitigations include:
- caching
- batching
- TTL-based logic
