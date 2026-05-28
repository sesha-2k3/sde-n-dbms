# Software Development & DBMS — Learning Roadmap

> **A structured, self-paced learning plan tailored for ML/DS engineers transitioning into software development.**
> Designed for ~1 hour/day over 7 days (SWE fundamentals) + an extended DBMS deep-dive track.

---

## About This Repo

This repository documents my journey from ML/Data Science into software development. Each day folder contains notes, code samples, and mini-projects that reinforce key concepts. The goal isn't to become an expert in a week — it's to build a strong mental model and a reference I can revisit.

**The Gap:** Software architecture, testing discipline, CI/CD workflows, system design thinking, and deeper DBMS internals.

---

## The Project — FitTrack: Diet & Workout Tracker

Instead of disconnected toy examples, the entire 7-day SWE track builds one real application end-to-end: a **client-facing Diet & Workout Tracking System** designed for personal trainers.

**The scenario:** You are a personal trainer. Your clients log in to the app, see a personalized dashboard with a welcome message, today's notes from you, and two main tabs — **Workout** and **Diet**. Under Workout, they pick from a checklist of three modes: **Strength**, **Cardio**, or **Rest**. Each day's progress is tracked, logged, and visible over time.

This project grows daily — from a raw API on Day 1, to a tested, Dockerized, CI/CD-enabled full-stack app by Day 7.

---

## Repository Structure

```
swe-fundamentals/
├── README.md
├── day-01-design-patterns/
│   ├── notes.md
│   ├── patterns/
│   │   ├── factory_example.py
│   │   ├── strategy_example.py
│   │   └── observer_example.py
│   └── refactor_log.md
├── day-02-backend-apis/
│   ├── notes.md
│   ├── fittrack-api/
│   │   ├── app/
│   │   │   ├── main.py
│   │   │   ├── routers/
│   │   │   │   ├── auth.py
│   │   │   │   ├── workouts.py
│   │   │   │   ├── diet.py
│   │   │   │   └── dashboard.py
│   │   │   ├── models/
│   │   │   │   ├── user.py
│   │   │   │   ├── workout.py
│   │   │   │   └── diet.py
│   │   │   ├── schemas/
│   │   │   ├── services/
│   │   │   └── auth/
│   │   ├── requirements.txt
│   │   └── README.md
│   └── rest-cheatsheet.md
├── day-03-databases/
│   ├── notes.md
│   ├── sql-exercises/
│   │   └── solutions.sql
│   ├── fittrack-api/  (extended from day 2)
│   │   ├── alembic/
│   │   ├── models/
│   │   └── db/
│   └── db-design-notes.md
├── day-04-testing/
│   ├── notes.md
│   ├── fittrack-api/  (extended)
│   │   ├── tests/
│   │   │   ├── test_auth.py
│   │   │   ├── test_workouts.py
│   │   │   ├── test_diet.py
│   │   │   ├── test_dashboard.py
│   │   │   └── conftest.py
│   │   ├── .pre-commit-config.yaml
│   │   └── pyproject.toml
│   └── tdd-reflection.md
├── day-05-cicd-docker/
│   ├── notes.md
│   ├── fittrack-api/  (extended)
│   │   ├── Dockerfile
│   │   ├── docker-compose.yml
│   │   ├── .github/workflows/ci.yml
│   │   └── .dockerignore
│   └── git-workflow-notes.md
├── day-06-system-design/
│   ├── notes.md
│   ├── fittrack-architecture/
│   │   ├── system-design.md
│   │   ├── diagrams/
│   │   └── README.md
│   └── system-design-flashcards.md
├── day-07-fullstack/
│   ├── notes.md
│   ├── fittrack-frontend/
│   │   ├── src/
│   │   │   ├── components/
│   │   │   │   ├── Login.jsx
│   │   │   │   ├── Dashboard.jsx
│   │   │   │   ├── WorkoutTab.jsx
│   │   │   │   └── DietTab.jsx
│   │   │   └── App.jsx
│   │   ├── package.json
│   │   └── README.md
│   ├── docker-compose.yml  (full stack)
│   └── WEEKLY-REFLECTION.md
├── dbms-mastery/
│   ├── 01-relational-model/
│   ├── 02-sql-advanced/
│   ├── 03-normalization/
│   ├── 04-indexing-and-storage/
│   ├── 05-transactions-and-concurrency/
│   ├── 06-query-processing/
│   ├── 07-nosql-and-newSQL/
│   ├── 08-distributed-databases/
│   └── projects/
└── resources.md
```

---

## Part 1: 7-Day SWE Fundamentals

### Day 1 — Software Architecture & Design Patterns

**Why this matters:** You've built ML pipelines and REST APIs — now learn how production software is actually structured. This is the biggest gap between "ML engineer who can code" and "software developer."

**Concepts to cover:**

- SOLID Principles — Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
- Design Patterns — Factory, Singleton, Observer, Strategy, Decorator
- MVC / MVP / MVVM architecture patterns
- Separation of Concerns & Dependency Injection
- Clean Code principles — naming conventions, function design, comments, formatting

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [Refactoring Guru — Design Patterns](https://refactoring.guru/design-patterns) | Interactive | Best visual guide to all GoF patterns with Python/Java examples |
| [roadmap.sh — Software Design & Architecture](https://roadmap.sh/software-design-architecture) | Roadmap | Interactive roadmap to track your progress |
| [ArjanCodes — SOLID & Design Patterns in Python](https://www.youtube.com/c/ArjanCodes) | [Video](https://www.youtube.com/watch?v=pTB30aXS77U) | Python-focused, perfect for your background |
| [Clean Code Summary (GitHub Gist)](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29) | Reading | Community summary of the key Clean Code principles |

**Practice Project:** Plan the FitTrack application architecture on paper. Identify which design patterns apply — Strategy pattern for workout types (Strength, Cardio, Rest), Factory pattern for creating workout/diet entries, Repository pattern for data access. Sketch the class diagram and document which SOLID principles each decision follows. Commit this as your `refactor-log.md`.

---

### Day 2 — Backend Development & RESTful APIs

**Why this matters:** You've used FastAPI before — now go deeper. Understand REST conventions, middleware, authentication, error handling, and how to structure a production backend properly.

**Concepts to cover:**

- REST principles — resources, HTTP methods, status codes, idempotency
- API versioning, pagination, filtering, and error handling standards
- Middleware, authentication (JWT, OAuth2), and authorization
- Request validation with Pydantic (go beyond basics — nested models, custom validators)
- Project structure — routers, services, repositories pattern

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [FastAPI Official Docs — Tutorial](https://fastapi.tiangolo.com/tutorial/) | Docs | Go through the advanced sections you may have skipped |
| [roadmap.sh — API Design Roadmap](https://roadmap.sh/api-design) | Roadmap | Comprehensive overview of API design best practices |
| [Microsoft — RESTful Web API Design](https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design) | Reading | Industry-standard guide to REST API design patterns |
| [freeCodeCamp — Back End Dev & APIs](https://www.freecodecamp.org/learn/back-end-development-and-apis/) | Course | Free hands-on projects with Node.js (good to see both ecosystems) |

**Practice Project:** Build the FitTrack API with FastAPI. Implement:
- **Auth routes** — register, login (JWT), get current user
- **Dashboard route** — returns welcome message ("Welcome back, {name}!"), today's personal note from trainer, and today's workout/diet summary
- **Workout routes** — log a workout entry (type: Strength | Cardio | Rest, with checklist items), get workout history, get today's workout
- **Diet routes** — log a meal entry, get diet history, get today's meals

Structure the project with routers → services → schemas (Pydantic). Push to your repo with a working README and example curl commands.

---

### Day 3 — Databases: SQL Deep Dive & ORM

**Why this matters:** You know SQL and MongoDB from your projects, but software development demands deeper DB skills — migrations, ORMs, indexing strategy, and understanding query performance.

**Concepts to cover:**

- Relational DB design — normalization (1NF through 3NF), entity relationships
- Indexes, query optimization, and reading EXPLAIN/ANALYZE output
- ORM patterns with SQLAlchemy + Alembic migrations
- ACID properties and transaction management
- SQL vs NoSQL — when to use what and the real tradeoffs

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [SQLBolt — Interactive SQL Lessons](https://sqlbolt.com/) | Interactive | Quick refresher with hands-on exercises |
| [SQLAlchemy 2.0 Official Tutorial](https://docs.sqlalchemy.org/en/20/tutorial/) | Docs | The ORM that pairs perfectly with FastAPI |
| [CMU 15-445 Lectures (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Andy Pavlo's legendary DB course — watch indexing & transactions lectures |
| [Use The Index, Luke](https://use-the-index-luke.com/) | Reading | The best free resource on SQL indexing and query performance |

**Practice Project:** Add PostgreSQL + SQLAlchemy to FitTrack. Design the schema:
- `users` — id, name, email, hashed_password, trainer_id, created_at
- `trainer_notes` — id, trainer_id, client_id, note_text, date, created_at
- `workouts` — id, user_id, date, type (strength/cardio/rest), completed, details (JSONB for flexible checklist items)
- `meals` — id, user_id, date, meal_type (breakfast/lunch/dinner/snack), description, calories, protein, carbs, fat

Implement Alembic migrations, add indexes on (user_id, date) for fast dashboard lookups, and write queries demonstrating JOINs (user + today's note + today's workouts), GROUP BY (weekly workout summary), and subqueries (clients who missed workouts this week).

---

### Day 4 — Testing & Code Quality

**Why this matters:** Your resume mentions "QA checks and automated regression tests" — now formalize that knowledge. Testing is what separates hobby projects from production software.

**Concepts to cover:**

- Testing pyramid — unit tests, integration tests, end-to-end tests
- pytest — fixtures, parametrize, mocking with `unittest.mock`, conftest patterns
- Test-Driven Development (TDD) workflow
- Code coverage — when it matters and when it doesn't
- Linting (ruff/flake8), type checking (mypy), and pre-commit hooks

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [pytest Official Docs](https://docs.pytest.org/en/stable/) | Docs | The standard Python testing framework |
| [RealPython — Testing in Python](https://realpython.com/python-testing/) | Tutorial | Comprehensive guide covering unittest, pytest, and mocking |
| [ArjanCodes — TDD in Python](https://www.youtube.com/watch?v=B1j6k2j2eJg) | Video | Practical TDD walkthrough in Python |
| [roadmap.sh — QA Roadmap](https://roadmap.sh/qa) | Roadmap | Broader view of quality assurance practices |

**Practice Project:** Write a full test suite for FitTrack:
- **Unit tests** — workout service logic (can't log two workout types for the same day, calorie validation on meals, etc.) with mocked DB
- **Integration tests** — auth flow (register → login → access protected route), workout logging via API endpoints using `TestClient`
- **Edge cases** — logging a workout for a future date (should fail), unauthorized access to another client's data, empty diet entries
- Add a `.pre-commit-config.yaml` with ruff + mypy. Aim for >80% coverage.

---

### Day 5 — Git Workflows, CI/CD & Docker

**Why this matters:** You list Git and Docker on your resume. Now learn the professional workflows — branching strategies, GitHub Actions, multi-stage Docker builds, and automated pipelines.

**Concepts to cover:**

- Git branching strategies — Git Flow vs trunk-based development
- Writing good commit messages (Conventional Commits) and PR descriptions
- GitHub Actions — CI pipeline (lint → test → build → report)
- Docker — multi-stage builds, docker-compose for local dev, .dockerignore
- Environment management — `.env` files, secrets handling, 12-factor app config

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [GitHub Skills — Interactive Courses](https://skills.github.com/) | Interactive | Free hands-on courses directly in GitHub repos |
| [GitHub Actions Official Docs](https://docs.github.com/en/actions) | Docs | Learn to automate CI/CD pipelines |
| [Docker Official Getting Started](https://docs.docker.com/get-started/) | Tutorial | Multi-stage builds and compose deep dive |
| [roadmap.sh — DevOps Roadmap](https://roadmap.sh/devops) | Roadmap | Broader context for CI/CD, infrastructure, and deployment |

**Practice Project:** Dockerize FitTrack with a multi-stage build. Write a `docker-compose.yml` with three services:
- `api` — the FastAPI app (multi-stage: build deps → slim runtime image)
- `db` — PostgreSQL with a health check and persistent volume
- `redis` — for session caching (prep for Day 6)

Add a GitHub Actions workflow (`ci.yml`) that runs on every push and PR: install deps → ruff lint → mypy check → pytest with coverage report. Add proper `.dockerignore` and `.env.example` files.

---

### Day 6 — System Design Fundamentals

**Why this matters:** You've deployed systems handling 5,000+ interactions/month. Now understand the principles behind designing systems that handle millions — load balancing, caching, queues, and more.

**Concepts to cover:**

- Scalability — horizontal vs vertical scaling and when to use each
- Load balancers, reverse proxies (Nginx), CDNs
- Caching strategies — Redis, in-memory caching, cache invalidation patterns
- Message queues — RabbitMQ, Redis Pub/Sub, Celery for async tasks
- CAP theorem, database sharding, replication basics

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [System Design Primer (GitHub, 280K+ stars)](https://github.com/donnemartin/system-design-primer) | Reading | The single best free system design resource on the internet |
| [ByteByteGo YouTube Channel](https://www.youtube.com/@ByteByteGo) | Video | Visual system design explanations by Alex Xu |
| [roadmap.sh — System Design Roadmap](https://roadmap.sh/system-design) | Roadmap | Interactive roadmap with linked resources for each topic |
| [roadmap.sh — Backend Projects](https://roadmap.sh/backend/projects) | Projects | Practice projects — URL shortener, caching proxy, broadcast server |

**Practice Project:** Design FitTrack at scale. Create `fittrack-architecture/system-design.md` that covers:
- **Architecture diagram** (Mermaid or Excalidraw) — client app → API gateway → auth service → workout service → diet service → DB
- **Caching layer** — implement Redis caching for the dashboard endpoint (today's note + workout + diet are fetched on every login; cache per user with TTL, invalidate on new log entry)
- **Scaling analysis** — if 10,000 trainers each have 50 clients, and each client logs in once daily, what's the read/write ratio? Where are the bottlenecks? How would you shard the `workouts` table?
- **Async processing** — design a notification system (e.g., "Your trainer left you a new note") using Celery + Redis as broker

---

### Day 7 — Putting It All Together & Frontend Basics

**Why this matters:** Tie everything together. Learn enough frontend (React basics) to build full-stack awareness, connect it to your backend, review the week, and plan your continued learning path.

**Concepts to cover:**

- Frontend basics — HTML/CSS/JS refresher, DOM manipulation
- React fundamentals — components, state, props, hooks (useState, useEffect)
- Connecting frontend to backend API (fetch/axios, CORS handling)
- Full-stack architecture — how frontend and backend communicate in production
- Code review practices, writing good documentation (README, API docs with Swagger)

**Curated Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [React Official Tutorial (tic-tac-toe)](https://react.dev/learn/tutorial-tic-tac-toe) | Tutorial | Official hands-on intro, well-paced for beginners |
| [roadmap.sh — Frontend Roadmap](https://roadmap.sh/frontend) | Roadmap | See the full frontend landscape and pick what to learn next |
| [The Odin Project — Foundations](https://www.theodinproject.com/paths/foundations) | Course | Free, project-based full-stack curriculum |
| [Full Stack Open (Univ. of Helsinki)](https://fullstackopen.com/en/) | Course | Deep university-level: React, Node, GraphQL, TypeScript — all free |

**Practice Project:** Build the FitTrack client dashboard in React:
- **Login page** — email/password form, call the auth API, store JWT
- **Dashboard** — "Welcome back, {name}!" header, today's date, trainer's personal note for today displayed as a card
- **Workout tab** — checklist UI with three options: Strength, Cardio, Rest. Client taps one to mark today's workout type as complete. Show a weekly history grid (Mon–Sun, color-coded by type)
- **Diet tab** — simple meal log form (meal type dropdown, description, calories). List of today's logged meals below the form

Deploy the full stack with Docker Compose (frontend + API + PostgreSQL + Redis). Write a comprehensive project README that someone could clone and run.

---

## Part 2: DBMS Mastery

> A deeper, self-paced track for mastering database management systems — from relational theory to distributed architectures. This complements Day 3 of the SWE roadmap and goes far beyond it.

### Module 1 — Relational Model & Relational Algebra

**Concepts:**

- The relational model — relations, tuples, attributes, domains, schemas
- Keys — superkey, candidate key, primary key, foreign key, composite key
- Relational algebra operations — select (σ), project (π), union (∪), set difference (−), Cartesian product (×), rename (ρ)
- Extended operations — natural join (⋈), theta join, semijoin, division, outer joins
- Equivalence of relational algebra expressions (query optimization foundations)

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [CMU 15-445 — Lecture 1: Relational Model (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Andy Pavlo's course — the gold standard for DBMS education |
| [Stanford Databases: Modeling and Theory (edX)](https://www.edx.org/learn/databases/stanford-university-databases-modeling-and-theory) | Course | Jennifer Widom's classic Stanford course — free to audit |
| [Database System Concepts (Silberschatz) — Ch. 2, 6](https://db-book.com/) | Textbook | The standard DBMS textbook used in most university courses |
| [Scaler — DBMS Fundamentals Course (Free)](https://www.scaler.com/topics/course/dbms/) | Course | Free course with certificate covering fundamentals through advanced |

**Practice:** Translate 10 English-language queries into relational algebra, then into SQL. Use FitTrack's schema as your dataset — e.g., "Find all clients whose trainer left a note today but who haven't logged a workout" expressed in both relational algebra and SQL.

---

### Module 2 — Advanced SQL

**Concepts:**

- Subqueries — correlated vs uncorrelated, EXISTS, IN, ANY/ALL
- Window functions — ROW_NUMBER, RANK, DENSE_RANK, LEAD/LAG, NTILE, running aggregates
- Common Table Expressions (CTEs) — recursive and non-recursive
- Set operations — UNION, INTERSECT, EXCEPT with proper usage
- Advanced aggregation — GROUPING SETS, CUBE, ROLLUP for OLAP-style queries
- JSON/JSONB operations in PostgreSQL (bridging SQL and NoSQL)

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [SQLBolt — Interactive SQL Lessons](https://sqlbolt.com/) | Interactive | Start here for a structured refresher |
| [PostgreSQL Official Docs — Window Functions](https://www.postgresql.org/docs/current/tutorial-window.html) | Docs | Authoritative reference with clear examples |
| [Mode Analytics SQL Tutorial](https://mode.com/sql-tutorial) | Tutorial | Real datasets and progressively harder exercises |
| [LeetCode — Database Problems (Top 50)](https://leetcode.com/studyplan/top-sql-50/) | Practice | Interview-style SQL problems for drilling speed |
| [Khan Academy — Intro to SQL](https://www.khanacademy.org/computing/computer-programming/sql) | Interactive | Video tutorials paired with coding challenges |

**Practice:** Write queries against FitTrack data:
- Window functions — rank clients by workout consistency this month, calculate each client's running calorie average using LAG, 7-day rolling workout streak
- CTEs — recursive query to find a trainer's full client tree (if trainers can have sub-trainers), weekly summary CTE feeding into a monthly report
- JSONB — query the workout `details` field to find all strength workouts that included "bench press" in the checklist

---

### Module 3 — Database Design & Normalization

**Concepts:**

- Entity-Relationship (ER) modeling — entities, attributes, relationships, cardinality
- ER to relational schema translation rules
- Functional dependencies — Armstrong's axioms, closure of attribute sets
- Normal forms — 1NF, 2NF, 3NF, BCNF, 4NF (multivalued dependencies)
- Denormalization — when and why to break normal forms for performance
- Schema design patterns for common applications (e-commerce, social media, SaaS)

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [Stanford Databases: Modeling and Theory (edX)](https://www.edx.org/learn/databases/stanford-university-databases-modeling-and-theory) | Course | Covers relational design theory comprehensively |
| [CMU 15-445 — Database Storage (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Understanding how schema choices impact physical storage |
| [Vertabelo Database Modeler (Free Tier)](https://vertabelo.com/) | Tool | Visual ER diagram tool for practicing schema design |
| [Database System Concepts — Ch. 7, 8](https://db-book.com/) | Textbook | Normalization theory with worked examples |

**Practice:** Redesign FitTrack's schema with rigor:
- Draw a full ER diagram (entities: User, Trainer, Workout, WorkoutDetail, Meal, TrainerNote, WorkoutPlan/Template)
- Normalize to 3NF — document each functional dependency
- Identify where denormalization helps: e.g., storing `total_daily_calories` on a `daily_summary` table instead of computing via aggregation on every dashboard load
- Add a `workout_templates` table so trainers can assign reusable workout plans to clients — model the many-to-many relationship

---

### Module 4 — Indexing & Storage Internals

**Concepts:**

- How data is physically stored — pages, tuples, slotted pages, heap files
- B+ Trees — structure, search, insertion, deletion, and why they dominate
- Hash indexes — static vs dynamic (extendible, linear hashing)
- Clustered vs non-clustered indexes, covering indexes, partial indexes
- Index selection strategy — reading EXPLAIN ANALYZE output, identifying sequential vs index scans
- Storage models — N-ary (row store) vs Decomposition (column store) and when to use each

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [Use The Index, Luke](https://use-the-index-luke.com/) | Reading | The best free resource on SQL indexing — practical and thorough |
| [CMU 15-445 — Index Lectures (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Deep dive into B+ Trees, hash indexes, and storage |
| [PostgreSQL Docs — Index Types](https://www.postgresql.org/docs/current/indexes-types.html) | Docs | Understand GIN, GiST, BRIN, and B-Tree indexes in practice |
| [pgMustard — EXPLAIN Analyzer](https://www.pgmustard.com/docs/explain) | Tool | Learn to read and interpret PostgreSQL query plans |

**Practice:** Seed FitTrack with 1M+ rows of synthetic workout and meal data across 500 users over 2 years. Benchmark:
- Dashboard query (today's workouts + meals + note for a user) with and without a composite index on `(user_id, date)`
- GIN index on the JSONB `details` column for workout checklist searches
- Partial index on `workouts WHERE type = 'rest'` for a "rest day report" query
- Document EXPLAIN ANALYZE output before and after each optimization

---

### Module 5 — Transactions & Concurrency Control

**Concepts:**

- ACID properties — Atomicity, Consistency, Isolation, Durability (what each really means)
- Transaction isolation levels — Read Uncommitted, Read Committed, Repeatable Read, Serializable
- Concurrency anomalies — dirty reads, non-repeatable reads, phantom reads, write skew
- Locking protocols — Two-Phase Locking (2PL), deadlock detection and prevention
- Multi-Version Concurrency Control (MVCC) — how PostgreSQL actually handles concurrency
- Write-Ahead Logging (WAL) and crash recovery

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [CMU 15-445 — Transaction Lectures (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Best explanation of 2PL, MVCC, and isolation levels |
| [PostgreSQL Docs — Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html) | Docs | How PostgreSQL implements isolation levels in practice |
| [Designing Data-Intensive Applications — Ch. 7](https://dataintensive.net/) | Textbook | Martin Kleppmann's masterful explanation of transactions |
| [Jepsen.io — Consistency Models](https://jepsen.io/consistency) | Reading | Kyle Kingsbury's analysis of consistency in real-world databases |

**Practice:** Using FitTrack's database, write Python scripts that demonstrate:
- **Dirty read scenario** — trainer updates a client's note while the client is reading the dashboard
- **Lost update** — two requests try to update the same workout entry simultaneously (e.g., client marks "complete" from phone and laptop at the same time)
- **Phantom read** — a trainer counts how many clients worked out today while a new workout log is being inserted
- Test each scenario under Read Committed vs Serializable. Document the behavior.

---

### Module 6 — Query Processing & Optimization

**Concepts:**

- Query processing pipeline — parsing → optimization → execution
- Query plan operators — sequential scan, index scan, nested loop join, hash join, merge join, sort
- Cost-based optimization — selectivity estimation, cardinality estimation, cost models
- Join ordering and join algorithm selection
- Query rewriting rules — predicate pushdown, projection pushdown, subquery unnesting
- Materialized views and query caching strategies

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [CMU 15-445 — Query Processing Lectures (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Covers query execution, join algorithms, and optimization |
| [PostgreSQL Docs — Performance Tips](https://www.postgresql.org/docs/current/performance-tips.html) | Docs | Practical guide to optimizing PostgreSQL queries |
| [pganalyze — Query Optimization Guide](https://pganalyze.com/docs/explain/query-optimization) | Tutorial | Real-world PostgreSQL query optimization patterns |
| [Database System Concepts — Ch. 15, 16](https://db-book.com/) | Textbook | Academic foundation for query processing and optimization |

**Practice:** Optimize these FitTrack queries:
1. "Show a trainer's full client dashboard with each client's workout count, average daily calories, and last active date this month" — involves multi-table JOINs and aggregation
2. "Find all clients who have been on a rest day for 3+ consecutive days" — requires window functions or self-joins
3. "Monthly leaderboard: rank all clients by workout consistency (percentage of days with a logged workout)" — heavy aggregation
4. Create a materialized view for the trainer dashboard that refreshes daily. Compare query times vs. live computation.
5. For each query, document the original EXPLAIN ANALYZE, what you changed, and the resulting improvement.

---

### Module 7 — NoSQL & NewSQL Systems

**Concepts:**

- Document stores — MongoDB (you know this — now understand the internals: WiredTiger, BSON, aggregation pipeline)
- Key-value stores — Redis data structures, persistence options (RDB vs AOF), use cases beyond caching
- Wide-column stores — Cassandra/HBase data model, partition keys, compaction strategies
- Graph databases — Neo4j, property graph model, Cypher query language
- NewSQL — CockroachDB, TiDB, Vitess — distributed SQL with strong consistency
- Polyglot persistence — choosing the right database for each part of your system

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [MongoDB University (Free Courses)](https://learn.mongodb.com/) | Course | Official, free courses with certification |
| [Redis University (Free)](https://university.redis.io/) | Course | Learn Redis data structures and use patterns |
| [Designing Data-Intensive Applications — Ch. 2, 3](https://dataintensive.net/) | Textbook | Best comparison of different data models and storage engines |
| [roadmap.sh — PostgreSQL DBA Roadmap](https://roadmap.sh/postgresql-dba) | Roadmap | Comprehensive guide to PostgreSQL administration |

**Practice:** Extend FitTrack with polyglot persistence:
- **Redis** — cache today's dashboard per user (hash), implement a workout streak counter (sorted set), and store active session tokens
- **MongoDB** — store flexible workout templates (different exercises, sets, reps, variations) that don't fit neatly into a relational schema
- **PostgreSQL** — remains the source of truth for users, workouts, meals, and notes
- Write a comparison doc: for each data type in FitTrack, explain which store you chose and why

---

### Module 8 — Distributed Databases

**Concepts:**

- Distributed system fundamentals — network partitions, consistency models, consensus protocols
- CAP theorem and the PACELC extension — what the tradeoffs really mean in practice
- Replication strategies — single-leader, multi-leader, leaderless (Dynamo-style)
- Partitioning/sharding strategies — range-based, hash-based, consistent hashing
- Distributed transactions — two-phase commit (2PC), Saga pattern, eventual consistency
- Real-world architectures — how Amazon DynamoDB, Google Spanner, and CockroachDB work

**Resources:**

| Resource | Type | Why It's Good |
|----------|------|---------------|
| [CMU 15-445 — Distributed DB Lectures (YouTube)](https://www.youtube.com/@CMUDatabaseGroup) | Video | Andy Pavlo covers distributed architectures and consensus |
| [Designing Data-Intensive Applications — Ch. 5-9](https://dataintensive.net/) | Textbook | The definitive resource on replication, partitioning, and consistency |
| [Jepsen.io — Analysis of Distributed Databases](https://jepsen.io/analyses) | Reading | Real-world testing of consistency claims by database vendors |
| [The Amazon DynamoDB Paper (2022)](https://www.usenix.org/conference/atc22/presentation/elhemali) | Paper | Understand the design of a planet-scale distributed database |

**Practice:** Scale FitTrack conceptually and practically:
- Set up a 3-node PostgreSQL cluster with streaming replication (Docker). Simulate a node failure and observe failover.
- Design a sharding strategy for FitTrack: shard by `trainer_id`? by `user_id`? Analyze the query patterns and justify your choice.
- Write a design doc for FitTrack at 1M users: which tables get sharded, which stay replicated, what consistency guarantees do you need for workouts vs. dashboard reads?

---

## DBMS Mastery Projects

These projects tie together multiple modules and give you portfolio-worthy work:

**Project 1 — Build a Mini Query Engine (Modules 1, 2, 6)**
Write a simple SQL parser and executor in Python that supports SELECT, WHERE, JOIN, and GROUP BY on CSV files. Implement a basic cost-based optimizer that chooses between nested-loop and hash join based on table size. Test it on exported FitTrack data.

**Project 2 — FitTrack Performance Benchmarker (Modules 4, 5, 6)**
Create a benchmarking tool that simulates FitTrack's access patterns: dashboard reads (high frequency), workout inserts (medium), trainer bulk queries (low frequency, heavy). Measure throughput/latency across different index configurations and isolation levels. Output results as charts.

**Project 3 — Multi-Model FitTrack (Modules 3, 7)**
Implement the full polyglot persistence version of FitTrack — PostgreSQL for structured data, Redis for caching/sessions/streaks, MongoDB for flexible workout templates. Build a unified data access layer that abstracts the storage choice from the API layer. Benchmark each store for its respective query patterns.

---

## Recommended Learning Order

```
Week 1:  Day 1 → Day 2 → Day 3 → Day 4 → Day 5 → Day 6 → Day 7
         (SWE Fundamentals — 1 hour/day)

Week 2+: DBMS Module 1 → Module 2 → Module 3
         (Relational foundations — take your time)

Week 4+: DBMS Module 4 → Module 5 → Module 6
         (Internals & performance — this is where depth comes from)

Week 6+: DBMS Module 7 → Module 8 → Projects
         (Distributed & NoSQL — the modern landscape)
```

---

## Key Reference Resources (Bookmarks)

**Roadmaps & Tracks:**
- [roadmap.sh — Backend Developer](https://roadmap.sh/backend) — Interactive roadmap for backend development
- [roadmap.sh — System Design](https://roadmap.sh/system-design) — System design concepts and interview prep
- [roadmap.sh — PostgreSQL DBA](https://roadmap.sh/postgresql-dba) — Database administration track

**University Courses (Free):**
- [CMU 15-445 — Database Systems](https://15445.courses.cs.cmu.edu/) — Andy Pavlo's legendary course (lectures on YouTube)
- [Stanford Databases (edX)](https://www.edx.org/learn/databases/stanford-university-databases-modeling-and-theory) — Jennifer Widom's foundational database course
- [Full Stack Open (Univ. of Helsinki)](https://fullstackopen.com/en/) — Modern full-stack development: React, Node, GraphQL, TypeScript
- [freeCodeCamp — Back End Dev & APIs](https://www.freecodecamp.org/learn/back-end-development-and-apis/) — Free hands-on backend certification

**Books (The Essential Three):**
- *Designing Data-Intensive Applications* by Martin Kleppmann — The Bible of modern data systems
- *Database System Concepts* by Silberschatz, Korth, Sudarshan — Standard academic DBMS textbook
- *Clean Code* by Robert C. Martin — Software craftsmanship fundamentals

**Practice Platforms:**
- [SQLBolt](https://sqlbolt.com/) — Interactive SQL exercises
- [LeetCode — Top SQL 50](https://leetcode.com/studyplan/top-sql-50/) — Interview-style SQL problems
- [Use The Index, Luke](https://use-the-index-luke.com/) — SQL indexing and performance
- [HackerRank — SQL Track](https://www.hackerrank.com/domains/sql) — SQL challenges by difficulty

---

## How I Use This Repo

Each folder has a `notes.md` where I document what I learned in my own words — not just what, but *why* and *when to use it*. The code samples are minimal, focused examples I can revisit quickly. The projects are meant to be pushed, broken, and improved over time.

The goal: if someone reads this repo, they should understand not just what I learned, but how I think about software systems.

---

*Last updated: May 2026*