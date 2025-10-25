# 🏈 OpenHudle – Video Analysis Platform for Teams

> A distributed, high-performance video analysis and collaboration platform inspired by Hudl — designed for teams that want **full control**, **modularity**, and **scalability**.

---

## 🧠 Project Vision

OpenHudle empowers sports teams to **upload, analyze, and collaborate on practice and game footage** in real time.  
It’s open, extensible, and cloud-native — built with scalability, modularity, and maintainability in mind.

---

## ⚙️ Microservices Architecture Overview

Instead of a monolithic backend, OpenHudle is composed of **independent services** connected via **an event-driven architecture**.

Each service is containerized (Docker) and communicates through a lightweight message broker (e.g., **Redis Streams**, **NATS**, or **Kafka**).  
The frontend communicates with a **Gateway API** that routes and authenticates all requests.

---

### 🧩 Service Breakdown

#### **1. Frontend (Next.js 16)**
- **Stack:** Next.js 16, TypeScript, Shadcn/UI, Tailwind, Zustand
- **Responsibilities:**
  - UI, routing, and client interactions
  - Calls the API Gateway for all backend interactions
  - Manages real-time events via WebSockets
  - Video player, annotation layer, and dashboard rendering
- **Deployment:** Vercel or Docker container behind CDN

#### **2. API Gateway**
- **Stack:** Fastify + TypeScript or Next.js Edge API Routes
- **Responsibilities:**
  - Entry point for all client traffic
  - Auth validation via shared JWT
  - Routes traffic to internal microservices
  - Rate limiting, caching, and load balancing
- **Deployment:** AWS Lambda / Cloudflare Workers / Docker

#### **3. Auth Service**
- **Stack:** Node.js (Fastify) + PostgreSQL + Prisma
- **Responsibilities:**
  - User registration, login, OAuth (Google, email)
  - Team and role management
  - JWT / session issuing for other services
  - Invitation links
- **Communication:** REST + internal event bus
- **Storage:** PostgreSQL (Supabase / Railway)

#### **4. Media Service**
- **Stack:** Node.js + AWS SDK + FFmpeg + Prisma
- **Responsibilities:**
  - File uploads (to S3)
  - Video transcoding (via AWS Lambda)
  - Generate thumbnails and previews
  - Manage video metadata and storage lifecycle
- **Communication:** Message queue for processing
- **Storage:** AWS S3 + PostgreSQL

#### **5. Annotation Service**
- **Stack:** Node.js + WebSocket + Prisma
- **Responsibilities:**
  - Drawing and timeline sync via WebSocket
  - Save serialized annotation states (JSON)
  - Broadcast annotation updates in real-time
  - Replay system for annotation timelines

#### **6. Clip & Tag Service**
- **Stack:** Node.js + Prisma + PostgreSQL
- **Responsibilities:**
  - Create, tag, and categorize clips
  - Manage metadata (formations, outcomes)
  - Provide REST endpoints for clip search and filter

#### **7. Comment & Collaboration Service**
- **Stack:** Node.js + WebSocket + Prisma
- **Responsibilities:**
  - Timestamped comments and replies
  - Threading and notifications
  - Real-time collaboration sync

#### **8. Analytics Service**
- **Stack:** Node.js + ClickHouse or PostgreSQL
- **Responsibilities:**
  - Track views, engagement, and clip interactions
  - Generate per-player and team dashboards
  - Periodic rollups and summaries
- **Storage:** ClickHouse or PostgreSQL rollups

#### **9. Job Queue / Worker Service**
- **Stack:** BullMQ + Redis
- **Responsibilities:**
  - Background jobs (transcoding, analytics rollup)
  - Retry logic and job scheduling
  - Event relay between services

#### **10. Notification Service (Optional)**
- **Stack:** Node.js + WebSocket / Pusher / Firebase
- **Responsibilities:**
  - Send push and in-app notifications
  - Integrate with email or SMS (e.g., SendGrid)

---

## 🔗 Communication Model

| Type | Technology | Purpose |
|------|-------------|----------|
| **API Calls** | REST / GraphQL | Between Frontend and API Gateway |
| **Events** | Redis Streams / NATS / Kafka | Between internal services |
| **Real-Time** | WebSocket | Live annotations, comments, updates |
| **Queue Jobs** | BullMQ (Redis) | Background tasks like transcoding |
| **Auth Tokens** | JWT (signed by Auth service) | Secure inter-service communication |

---

## 🧰 Infrastructure Overview

| Component | Provider / Tech |
|------------|----------------|
| **Frontend Hosting** | Vercel / Cloudflare Pages |
| **API Gateway** | AWS Lambda / Cloudflare Workers |
| **Microservices** | Docker containers on AWS ECS / Railway |
| **Database** | PostgreSQL (RDS / Supabase) |
| **Analytics DB** | ClickHouse |
| **Object Storage** | AWS S3 (videos, thumbnails, exports) |
| **CDN** | CloudFront / Cloudflare R2 |
| **Job Queue** | Redis (Elasticache / Upstash) |
| **Monitoring** | Sentry + Grafana + Loki |
| **CI/CD** | GitHub Actions |

---

## 🧱 Directory Structure

```
/openhudle
├── /apps
│   ├── /frontend             # Next.js app
│   ├── /gateway              # API Gateway
│   └── /admin-dashboard      # (Optional) Management interface
│
├── /services
│   ├── auth-service
│   ├── media-service
│   ├── annotation-service
│   ├── clip-tag-service
│   ├── comment-service
│   ├── analytics-service
│   ├── job-service
│   └── notification-service
│
├── /packages
│   ├── prisma-schema         # Shared DB schema
│   ├── types                 # Shared TypeScript interfaces
│   ├── utils                 # Common utilities
│   ├── config                # Shared configs (env, constants)
│
├── /infra
│   ├── docker-compose.yml
│   ├── terraform/            # IaC for AWS setup
│   ├── k8s/                  # Optional Kubernetes configs
│
└── README.md
```

---

## 🚀 Development Sprints

| Sprint | Focus | Services |
|--------|--------|-----------|
| **Sprint 1** | Foundation | Frontend setup, API Gateway, Auth service |
| **Sprint 2** | Video upload pipeline | Media service, S3, transcoding |
| **Sprint 3** | Annotations + Real-time | Annotation service + WebSocket infra |
| **Sprint 4** | Clips & Tags | Clip-tag service + frontend integration |
| **Sprint 5** | Collaboration | Comment + Notification services |
| **Sprint 6** | Analytics + Optimization | Analytics + caching + observability |
| **Sprint 7** | Polish & Release | UX refinements, monitoring, docs |

---

## 🧠 Drawing Layer Technology

| Component | Library | Description |
|------------|----------|-------------|
| **Canvas Layer** | Konva.js | Vector-based drawing and animations |
| **Serialization** | JSON | Stores drawings as objects for replay |
| **Reproduction** | Time-synced re-rendering | Ensures consistent drawing playback |
| **Future Option** | Fabric.js / SVG Overlay | Scalable, resolution-independent rendering |

---

## 🧑‍💻 Future Expansion

- AI-assisted tagging (pose & player detection)
- Voice annotations
- Mobile upload companion app
- Offline annotation playback
- Live game streaming + instant review

---

## ⚡ Why Microservices?

✅ **Scalable:** Each service can scale independently.  
✅ **Maintainable:** Clear ownership and smaller deployable units.  
✅ **Performant:** Decouple video processing from the main app.  
✅ **Future-proof:** Easier to integrate ML and analytics down the line.  
✅ **Flexible:** Choose the best tools per service (e.g., Go for video if needed).  

---

## 🧩 Technologies Summary

| Area | Tech Stack |
|------|-------------|
| **Frontend** | Next.js 16, TypeScript, Tailwind, Shadcn, Zustand |
| **Auth** | Fastify, Prisma, PostgreSQL |
| **Media** | AWS S3, FFmpeg, Lambda |
| **Annotations** | Konva.js, WebSocket, Prisma |
| **Clips/Tags** | Node.js, Prisma |
| **Analytics** | ClickHouse / PostgreSQL |
| **Infra** | Docker, Redis, GitHub Actions, AWS ECS, Terraform |
| **Monitoring** | Sentry, Grafana, Loki |

---

## 🧱 Summary

OpenHudle is a **modular, distributed video analysis platform** that brings Hudl-level power to teams everywhere.  
Designed with **Next.js 16**, **microservices**, and **modern cloud-native principles**, it’s scalable, hackable, and built for the long run.

---

> 🧑‍💻 Built by developers, for athletes.
>  
> ⚙️ _“Control your footage. Own your analysis.”_
