# 🏈 OpenHudle – Video Analysis Platform for Teams

> An open-source video analysis and team collaboration platform inspired by Hudl — built for coaches, players, and analysts who want full control over their footage and data.

---

## 🧠 Project Vision

OpenHudle allows sports teams to **upload, analyze, and share practice and game footage** seamlessly. Coaches can draw over plays, tag players, share clips, and generate insights — all in a fast, intuitive interface designed with performance and collaboration in mind.

---

## ⚙️ Architecture Overview

### **Frontend**
- **Framework:** Next.js 16 (React 19 compiler, async caching, server actions)
- **Language:** TypeScript
- **UI:** Shadcn/UI + Tailwind CSS + Framer Motion
- **State Management:** Zustand or React Context + Server Components
- **Video Player:** Custom player using [Video.js](https://videojs.com/) or [Remotion Player]
- **Drawing Layer:** Fabric.js or Konva.js (Canvas-based annotations)

### **Backend**
- **Runtime:** Next.js Server Actions / Edge Runtime
- **ORM:** Prisma
- **Database:** PostgreSQL (with connection pooling via Prisma Accelerate or Supabase)
- **Auth:** NextAuth.js (Email + Google + Team invitation links)
- **File Storage:** AWS S3 (for raw + processed videos)
- **Transcoding:** AWS Lambda + FFmpeg (automated video optimization)
- **Real-Time:** WebSockets or Pusher (for comments, live drawing sync)
- **Background Jobs:** BullMQ (Redis-based) or Cloudflare Queues (for async video processing)
- **Analytics:** Clickhouse (optional) or PostgreSQL rollups for views/plays

### **Infrastructure**
- **CDN:** CloudFront or Cloudflare R2
- **Deployment:** Vercel (Frontend) + AWS Lambda (Processing) + Railway / Supabase (DB)
- **Monitoring:** Sentry + Logflare
- **CI/CD:** GitHub Actions (lint, test, deploy)

---

## 🧩 Core Features

| Category | Description |
|-----------|-------------|
| **Video Upload & Playback** | Upload game/practice videos, auto-transcoded to streamable formats |
| **Annotation Layer** | Draw arrows, circles, and text directly on top of videos |
| **Clip Creation** | Trim and save specific video moments as clips |
| **Team Management** | Add players, coaches, assign roles and permissions |
| **Comment System** | Timestamped comments under videos or clips |
| **Playbook Mode** | Save annotated clips into categorized playbooks |
| **Tagging System** | Tag players, plays, formations, and results |
| **Analytics Dashboard** | Stats on clips, tags, player engagement |
| **Sharing** | Generate private or team-only share links |
| **Offline Notes (optional)** | Download videos for offline review (future) |

---

## 🎯 User Stories

### **1. Authentication & Team Setup**
- As a coach, I want to create an account and start a new team.
- As a coach, I want to invite players and assistant coaches via email.
- As a player, I want to join a team from an invite link.
- As a user, I want to log in using Google or email.

### **2. Video Management**
- As a coach, I can upload raw game footage.
- As a player, I can view videos uploaded by my coach.
- As the system, I should transcode videos automatically to optimized formats.
- As a user, I can stream videos seamlessly on any device.
- As a coach, I can categorize videos (practice, game, special teams).

### **3. Video Analysis & Drawing**
- As a coach, I can pause the video and draw arrows, lines, and shapes.
- As a user, I can toggle annotations on/off.
- As a coach, I can save multiple drawings per frame.
- As a coach, I can replay drawings during playback.
- As a coach, I can scrub through the timeline and see annotations appear where relevant.
- As a coach, I can use colors to represent offense/defense.

### **4. Clip Creation & Tagging**
- As a coach, I can select a time range and create a “clip”.
- As a user, I can name and describe the clip.
- As a coach, I can tag players involved in the clip.
- As a coach, I can assign formations or situations to a clip.
- As a player, I can comment on clips for discussion.

### **5. Collaboration & Comments**
- As a player, I can comment at a specific timestamp.
- As a coach, I can reply to comments.
- As a user, I can like or pin important comments.
- As a coach, I can mark clips as “reviewed”.

### **6. Playbook Mode**
- As a coach, I can save clips to my playbook.
- As a user, I can browse categorized plays (Offense, Defense, Special Teams).
- As a coach, I can export a play as an image or short video with annotations.

### **7. Analytics**
- As a coach, I can see which players watched which videos.
- As a coach, I can track engagement per player (views, comments).
- As a team admin, I can see overall clip stats (tags, formations, outcomes).

### **8. Sharing & Permissions**
- As a coach, I can share a video link only accessible by my team.
- As a player, I can only access my team’s media.
- As a coach, I can revoke access to clips.
- As a coach, I can generate public share links (with expiration dates).

---

## 🚀 Development Roadmap (Sprints)

### **Sprint 1 – Foundation (Week 1–2)**
- [ ] Set up Next.js 16 + TypeScript + Tailwind + Shadcn
- [ ] Configure PostgreSQL + Prisma schema
- [ ] Implement NextAuth with Google & Email
- [ ] Set up AWS S3 for video uploads
- [ ] Implement simple video upload & playback

### **Sprint 2 – Teams & Permissions (Week 3–4)**
- [ ] Team creation + invitation system
- [ ] Role-based access (Coach / Player)
- [ ] Team dashboard layout
- [ ] Video categorization (Practice / Game)

### **Sprint 3 – Video Player & Annotations (Week 5–6)**
- [ ] Custom player (Video.js + Fabric.js / Konva.js)
- [ ] Draw tools (lines, arrows, text, circles)
- [ ] Annotation timeline syncing
- [ ] Save/load annotations from DB

### **Sprint 4 – Clips & Tagging (Week 7–8)**
- [ ] Create and manage clips
- [ ] Tag players and formations
- [ ] Comment system (timestamp-based)
- [ ] Real-time updates via WebSockets

### **Sprint 5 – Playbook & Analytics (Week 9–10)**
- [ ] Playbook creation (grouped clips)
- [ ] Export clips as shareable media
- [ ] Watch tracking (per-user)
- [ ] Analytics dashboard (views, clips, engagement)

### **Sprint 6 – Polish & Scale (Week 11–12)**
- [ ] Optimize video transcoding with FFmpeg Lambda
- [ ] Integrate CDN (CloudFront)
- [ ] Implement caching with Next.js 16 React compiler
- [ ] Add error logging & monitoring (Sentry)
- [ ] Final responsive polish + testing

---

## 🧰 Technologies Summary

| Area | Stack |
|------|-------|
| Frontend | Next.js 16, TypeScript, Tailwind, Shadcn, Zustand |
| Backend | Prisma, Next.js Server Actions, PostgreSQL |
| File Storage | AWS S3 |
| Video Transcoding | AWS Lambda + FFmpeg |
| Realtime | Pusher / WebSocket |
| Auth | NextAuth.js |
| Queue System | BullMQ / Cloudflare Queues |
| Deployment | Vercel + AWS |
| Analytics | PostgreSQL rollups / ClickHouse (optional) |

---

## 🧑‍💻 Future Ideas
- AI auto-tagging (detect formations or players using ML)
- Auto-clip detection based on motion or whistle detection
- Mobile app for fast video uploads
- Offline analysis mode

---

## 🏗️ Drawing Technologies

For reliable annotations across all screens:
- **Konva.js** → Canvas-based, scalable drawings with serialization (recommended)
- **Fabric.js** → Richer features, easier freehand tools, snapshot saving
- **SVG Overlay (custom)** → Perfect scaling on any device, ideal for static diagrams

Save drawings as **JSON state objects**, and replay using video timestamps. This guarantees the same drawings appear across all devices and resolutions.

---

## 📜 License
MIT License — free for teams, open-source for the community.

---

