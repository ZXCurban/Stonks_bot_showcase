# Scalability Notes

The system is designed with horizontal scalability as a core requirement.

## Stateless Bot Instances
Telegram bot handlers do not store any local or shared state.
Multiple bot instances can be deployed and run in parallel without coordination.

## Externalized State
All shared state is stored outside the application layer:
- Redis for volatile, time-sensitive, and coordination-related data
- PostgreSQL for persistent and transactional data

This separation allows bot processes to remain stateless and disposable.

## Background Tasks
Schedulers are isolated from request handlers and can be:
- executed in separate processes
- scaled independently from bot instances
- restarted without affecting active user sessions

Scheduler failures do not interrupt interactive bot operations.

## Bottleneck Awareness
Potential bottlenecks are explicitly identified:
- write-heavy database operations
- scheduled fan-out notifications

Mitigation strategies include:
- aggressive caching
- batching of write operations
- TTL-based expiration and cleanup logic
