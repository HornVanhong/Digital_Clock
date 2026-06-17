# 🎓 EduTrace — UI

### *Intelligent Learning Management & Real-Time Collaboration Platform*

<p align="center">
  <img src="public/images/logo/edutraceLogo.png" alt="EduTrace Logo" width="220px" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16.2-000000?style=for-the-badge&amp;logo=nextdotjs&amp;logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-19.0-20232A?style=for-the-badge&amp;logo=react&amp;logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/TypeScript-5.0-007ACC?style=for-the-badge&amp;logo=typescript&amp;logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Tailwind_v4-38B2AC?style=for-the-badge&amp;logo=tailwindcss&amp;logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-Compatible-2496ED?style=for-the-badge&amp;logo=docker&amp;logoColor=white" alt="Docker" />
</p>

EduTrace UI is a premium, highly responsive next-generation learning hub Dashboard built on Next.js 16 (App Router) and React 19. It integrates low-latency virtual classrooms via WebRTC, automated study tracking, structured assessment workflows, and interactive charts to deliver a comprehensive dashboard experience.

---

## 📡 Core Features

### 1. Live Virtual Classrooms
* **WebRTC Video/Audio:** Low-latency, peer-to-peer media streaming using PeerJS.
* **Screen Sharing:** Real-time presentation capabilities via browser display media streams.
* **Signaling & Collaboration:** Integrated Socket.IO for room chat, real-time hand-raising, push alerts, and active speaker visual indicators.
* **Virtual Backdrops:** Camera blur or custom backdrops driven by MediaPipe.

### ⏱️ 2. Automated Study Time Tracker
* **Automated Session Logging:** Automatically monitors and logs active study periods on student assessment pages.
* **Reliable Session Syncing:** Uses `navigator.sendBeacon` to sync progress to the server even if the browser tab is closed unexpectedly.
* **Daily Goal Targets:** Visual circular charts contrast current study progress with instructor-defined targets.

### 📝 3. Comprehensive Assessment Hub
* **Teacher Management Console:** Full CRUD tooling for tasks, classroom assigners, and a rich text workspace editor.
* **Interactive Submission Flow:** Student submission pipeline with Zod-validated attachment uploads, repository links, comments, and scoring panels for teachers.

### 📈 4. Advanced Analytics & AI Assistant
* **Visual Analytics:** Interactive charts (bar, donut, line charts) driven by MUI X-Charts for performance trends.
* **PDF Report Exporter:** Direct printing/saving of performance reports via Puppeteer-backed rendering.
* **AI Copilot Insight:** Scans tracking data and warns instructors about students at-risk of falling behind.

---

## 🛠️ Technology Stack

| Layer | Technologies & Libraries |
|---|---|
| **Framework & Engine** | Next.js 16 (App Router), React 19 (React Compiler), TypeScript |
| **Styles & Animations** | Tailwind CSS v4, PostCSS, Framer Motion |
| **Component Libraries** | HeroUI (formerly NextUI - Inputs, Selects, Tables), shadcn/ui (Sidebars, Popovers) |
| **WebRTC & Live Data** | PeerJS (Media Streams), Socket.IO (Signaling), SockJS/STOMP (Chat Protocol) |
| **Visuals & Exports** | MUI X-Charts, Puppeteer (PDF generator), HTML2Canvas |
| **Third-Party Services**| Knock SDK (Push/In-App Alerts), Cloudflare TURN (RTC Firewall Bypass) |

---

## 📂 Project Structure

```bash
src/
├── actions/       # Server actions (Next.js server-side operations)
├── app/           # App Router page structure & layout definitions
│   ├── (auth)/    # Authentication routes (Login, SignUp)
│   ├── (landing)/ # Marketing and landing pages
│   ├── (main)/    # Dashboard features (Assessment, Calendar, Reports)
│   └── api/       # API routes and backend handlers
├── components/    # Modular and reusable UI components
├── config/        # Environment configurations and global keys
├── context/       # Global React context providers
├── hooks/         # Custom React hooks (WebRTC, sockets, tracking)
├── lib/           # Configuration files and utility initializers (e.g. Knock)
├── schemas/       # Zod verification and validation models
├── services/      # Fetching logic and API services
├── stores/        # Zustand global state configurations
├── styles/        # Global style sheets (Tailwind/PostCSS configuration)
├── types/         # TypeScript type definitions and interfaces
└── utils/         # Helper functions and formatter modules
```

---

## ⚙️ Environment Configuration

To run the application, copy `.env.example` to `.env.local` in the project root:

```bash
cp .env.example .env.local
```

Open `.env.local` and configure the following variables:

```env
# APP AND SERVICE ROUTING
NEXT_PUBLIC_API_BASE_URL=https://api.example.com/api/v1  # External Spring Boot backend API
NEXTAUTH_URL=http://localhost:3000                     # URL of this Next.js app

# SECURITY
AUTH_SECRET=your_auth_secret_here                      # Secure key for session token encryption

# NOTIFICATIONS (KNOCK FEED)
NEXT_PUBLIC_KNOCK_API_KEY=                             # Public API key
NEXT_PUBLIC_KNOCK_FEED_CHANNEL_ID=                     # In-app feed Channel ID
NEXT_PUBLIC_KNOCK_PUSH_CHANNEL_ID=                     # Browser push Channel ID
NEXT_PUBLIC_VAPID_PUBLIC_KEY=                          # VAPID key for web push

# WEBRTC SIGNALING (CLOUDFLARE TURN)
CLOUDFLARE_TURN_KEY_ID=                                # CF Turn key ID
CLOUDFLARE_TURN_API_TOKEN=                             # CF Turn API token
```

> [!TIP]
> You can quickly generate a secure `AUTH_SECRET` key by running:
> ```bash
> npx auth secret
> ```

---

## 💻 Getting Started

### 📦 1. Installation
Clone the repository and install dependencies:

```bash
git clone https://github.com/14th-Gen-Basic-Course-Final-Project/EduTrace-UI.git
cd EduTrace-UI
npm install
```

### ⚡ 2. Start the Application

Choose the command matching your development setup:

#### Option A: Next.js Client Dev Mode (Standard)
*Use this option if you are connecting to a remote Socket.IO server.*
```bash
npm run dev
```

#### Option B: Next.js Client + Socket.IO Signaling Server
*Recommended for full local WebRTC testing.*
```bash
npx tsx server.ts
```

Once started, open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 📦 Available Scripts

Below is a reference of the available package commands:

| Command | Action |
|---|---|
| `npm run dev` | Runs the Next.js development server with hot-reload support on port `3000`. |
| `npx tsx server.ts` | Runs the dev server along with the custom Socket.IO signaling layer. |
| `npm run build` | Builds the production bundle inside the `.next` directory. |
| `npm run start` | Runs the built production bundle application. |
| `npm run lint` | Runs ESLint rules to identify syntax and style warnings. |

---

## 🐳 Containerization (Docker)

To deploy the production bundle in a standalone container locally, make sure Docker is running and run:

```bash
docker compose up --build
```

This builds the Docker image and exposes the dashboard UI on port `3000`.
