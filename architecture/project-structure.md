## Project Structure (Production)

This structure is not included verbatim in this repository. Entry points are omitted.

The production bot is organized as follows:
```bash
.
├── .env.example              # Example environment configuration (no secrets)
├── .gitignore                # Git ignore rules
├── FSMcontext/               # Finite State Machine definitions for user flows
│   └── fsm.py
├── aiogram_redis_utils/      # Redis-backed utilities for Telegram interaction
│   ├── message_tracker.py    # Message deduplication and lifecycle tracking
│   └── rate_limiter.py       # Rate limiting and anti-spam logic
├── core/                     # Cross-cutting infrastructure components
│   ├── logger.py             # Centralized logging setup
│   └── middleware.py         # Request/response middleware
├── handlers/                 # Telegram update handlers (thin layer)
│   └── handlers.py
├── support/                  # Auxiliary helpers and shared utilities
│   ├── bank_funcs.py         # Banking and balance-related helpers
│   ├── notify.py             # User notification helpers
│   └── promo.py              # Promotional and bonus mechanics
├── keyboards/                # Telegram keyboard layouts
│   └── keyboards.py
├── services/                 # Core business logic and game systems
│   ├── database/             # Persistence layer
│   │   ├── database.py       # Database connection and session management
│   │   └── models.py         # ORM models
│   ├── achievements/         # Achievement system and progression rules
│   │   ├── engine.py
│   │   ├── notifier.py
│   │   ├── repository.py
│   │   └── rules.py
│   ├── market/               # Market simulation and price visualization
│   │   └── chart.py
│   ├── quests/               # Dynamic quest system
│   │   ├── constants.py
│   │   ├── engine.py
│   │   ├── events.py
│   │   ├── generator.py
│   │   ├── payloads.py
│   │   ├── registry.py
│   │   ├── repository.py
│   │   ├── rules.py
│   │   └── texts.py
│   ├── redis_utils/           # Shared Redis helpers
│   │   └── utils.py
│   └── underground_market/   # High-risk, limited-time game mechanics
│       ├── game.py
│       └── scheduler.py
├── static/                   # Static and generated assets
│   ├── Photos/               # Game assets and images
│   └── tmp_charts/           # Generated market charts
```
