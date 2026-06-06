<div align="center">

<img src="https://capsule-render.vercel.app/api?type=cylinder&color=5865F2,7289DA,4752C4,36393F&height=200&section=header&text=Discord%20Clone&fontSize=58&fontColor=ffffff&fontAlignY=50&desc=Real-time%20%E2%80%A2%20Full-Stack%20%E2%80%A2%20Production-Grade&descAlignY=70&descSize=15&descColor=B9BBBE&animation=blinking" width="100%"/>

<br/>

<p>
<img src="https://img.shields.io/badge/Next.js-14-000000?style=for-the-badge&logo=nextdotjs&logoColor=white"/>
<img src="https://img.shields.io/badge/Prisma-ORM-2D3748?style=for-the-badge&logo=prisma&logoColor=white"/>
<img src="https://img.shields.io/badge/Clerk-Auth-6C47FF?style=for-the-badge&logo=clerk&logoColor=white"/>
<img src="https://img.shields.io/badge/Tailwind-CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white"/>
<img src="https://img.shields.io/badge/Deployed-Koyeb-121212?style=for-the-badge&logo=koyeb&logoColor=white"/>
<img src="https://img.shields.io/badge/License-MIT-5865F2?style=for-the-badge"/>
</p>

<br/>

<a href="https://discord-clone.koyeb.app">
<img src="https://img.shields.io/badge/LIVE%20DEMO%20%E2%86%92%20discord--clone.koyeb.app-5865F2?style=for-the-badge&logo=googlechrome&logoColor=white"/>
</a>

<br/><br/>

<table>
<tr>
<td align="center" width="180">
<img src="https://img.shields.io/badge/Real--time-Messaging-5865F2?style=flat-square"/><br/>
<sub>Socket.io powered chat</sub>
</td>
<td align="center" width="180">
<img src="https://img.shields.io/badge/Server-Management-7289DA?style=flat-square"/><br/>
<sub>Create and customize servers</sub>
</td>
<td align="center" width="180">
<img src="https://img.shields.io/badge/Channel-System-4752C4?style=flat-square"/><br/>
<sub>Text and voice channels</sub>
</td>
<td align="center" width="180">
<img src="https://img.shields.io/badge/Google-Auth-36393F?style=flat-square"/><br/>
<sub>Clerk authentication</sub>
</td>
</tr>
</table>

</div>

---

## What is this

A production-grade Discord clone — not a tutorial project, not a UI mockup. Real servers. Real channels. Real-time messaging with fallback polling. Google OAuth. Image uploads. Built on Next.js 14 App Router with Prisma ORM and deployed live on Koyeb.

```
┌─────────────────────────────────────────────────────────────────────┐
│                     How it works end-to-end                         │
│                                                                     │
│  User signs in via Google (Clerk)                                   │
│          │                                                          │
│          ▼                                                          │
│  Creates or joins a server                                          │
│          │                                                          │
│          ├──▶  Creates channels inside the server                   │
│          ├──▶  Invites members via invite link                      │
│          ├──▶  Sends messages in real-time                          │
│          └──▶  Messages persist in database via Prisma              │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Live Demo

**Production URL:** [discord-clone.koyeb.app](https://discord-clone.koyeb.app)

Sign in with Google, create a server, add channels, and start messaging. No setup required.

---

## Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Framework | Next.js 14 (App Router) | Full-stack React framework |
| Styling | Tailwind CSS | Utility-first CSS |
| Auth | Clerk | Google OAuth + session management |
| Database ORM | Prisma | Type-safe database client |
| Real-time | Socket.io + Polling fallback | Live messaging |
| File Uploads | UploadThing | Server image and attachment uploads |
| Deployment | Koyeb | Production hosting |
| Language | TypeScript | Type safety across the codebase |

---

## Architecture

<div align="center">

```
╔══════════════════════════════════════════════════════════════════════╗
║                Discord Clone — System Architecture                   ║
╠══════════════════════════════════════════════════════════════════════╣
║                                                                      ║
║   CLIENT (Browser)                                                   ║
║   ┌──────────────────────────────────────────────────────────────┐  ║
║   │  Next.js 14 App Router                                       │  ║
║   │  ├── /                    Landing / Auth redirect            │  ║
║   │  ├── /servers/[id]        Server view with sidebar           │  ║
║   │  ├── /servers/[id]/channels/[id]   Channel + messages        │  ║
║   │  └── Tailwind UI components                                  │  ║
║   └───────────────────────┬──────────────────────────────────────┘  ║
║                           │  API Routes + Server Actions             ║
║                           ▼                                          ║
║   SERVER (Next.js API)                                               ║
║   ┌──────────────────────────────────────────────────────────────┐  ║
║   │  /api/servers          Server CRUD                           │  ║
║   │  /api/channels         Channel CRUD                          │  ║
║   │  /api/messages         Message read/write                    │  ║
║   │  /api/socket           Socket.io real-time handler           │  ║
║   │  /api/uploadthing      File upload handler                   │  ║
║   └───────────────────────┬──────────────────────────────────────┘  ║
║                           │  Prisma ORM                              ║
║                           ▼                                          ║
║   DATABASE                                                           ║
║   ┌──────────────────────────────────────────────────────────────┐  ║
║   │  Users → Servers → Channels → Messages                       │  ║
║   │  Members → Profiles → Conversations                          │  ║
║   └──────────────────────────────────────────────────────────────┘  ║
╚══════════════════════════════════════════════════════════════════════╝
```

</div>

---

## Database Schema

```
Profile
  └── id, userId, name, imageUrl, email
  └── has many: servers, members, channels

Server
  └── id, name, imageUrl, inviteCode, profileId
  └── has many: members, channels

Channel
  └── id, name, type (TEXT/AUDIO/VIDEO), profileId, serverId
  └── has many: messages

Member
  └── id, role (ADMIN/MODERATOR/GUEST), profileId, serverId
  └── has many: messages, conversationsInitiated

Message
  └── id, content, fileUrl, deleted
  └── belongs to: member, channel
```

---

## Features

**Authentication**
- Google OAuth via Clerk
- Protected routes with middleware
- Persistent sessions

**Server System**
- Create servers with custom name and image
- Unique invite code generation per server
- Join servers via invite link
- Member role management: Admin, Moderator, Guest

**Channel System**
- Create text channels inside servers
- Channel types: Text, Audio, Video
- Channel-level permissions by member role

**Messaging**
- Real-time message delivery via Socket.io
- Automatic fallback to polling every 1s if WebSocket unavailable
- Message persistence in database
- File and image attachments via UploadThing
- Message edit and delete

**UI**
- Discord-accurate dark theme
- Responsive sidebar with server and channel navigation
- Search across servers and channels
- Light/dark mode toggle

---

## UI Layout

```
┌─────┬────────────────────┬──────────────────────────────────────────┐
│     │                    │  # general                               │
│  S  │  Server Name    ▾  ├──────────────────────────────────────────┤
│  e  │  ─────────────     │                                          │
│  r  │  Search      ⌘K   │                                          │
│  v  │                    │         Welcome to #general              │
│  e  │  TEXT CHANNELS  +  │         This is the start of the         │
│  r  │  # general    lock │         channel.                         │
│  s  │  # announcements   │                                          │
│     │                    │                                          │
│  i  │                    ├──────────────────────────────────────────┤
│  c  │                    │  + Message #general                      │
│  o  │  + Add New Task    └──────────────────────────────────────────┘
│  n  │  Help
│  s  │  Logout
└─────┴────────────────────┘
```

---

## Project Structure

```
discord-clone-main/
│
├── .github/                    # GitHub workflows
│
├── prisma/
│   └── schema.prisma           # Full database schema
│
├── src/
│   ├── app/
│   │   ├── (auth)/             # Clerk auth pages
│   │   ├── (main)/             # Main app layout
│   │   │   └── servers/[serverId]/channels/[channelId]/
│   │   └── api/
│   │       ├── channels/       # Channel API routes
│   │       ├── messages/       # Message API routes
│   │       ├── servers/        # Server API routes
│   │       ├── socket/         # Socket.io handler
│   │       └── uploadthing/    # File upload handler
│   │
│   ├── components/
│   │   ├── chat/               # Message components
│   │   ├── modals/             # Server, channel, invite modals
│   │   ├── navigation/         # Sidebar and server list
│   │   └── server/             # Server sidebar components
│   │
│   ├── hooks/                  # Custom React hooks
│   ├── lib/                    # Prisma client, utilities
│   └── types/                  # TypeScript types
│
├── .env.example                # Environment variable template
├── components.json             # shadcn/ui config
├── next.config.mjs             # Next.js config
├── tailwind.config.ts          # Tailwind config
├── docker-compose.yml          # Docker setup
├── Dockerfile
└── package.json
```

---

## Installation

### Prerequisites

- Node.js 18+
- PostgreSQL database (or any Prisma-supported DB)
- Clerk account
- UploadThing account

### Setup

```bash
# Clone the repository
git clone https://github.com/aly-abbas11/Discord-Clone-Next.git
cd Discord-Clone-Next

# Install dependencies
npm install --legacy-peer-deps

# Copy environment variables
cp .env.example .env
```

### Environment Variables

Fill in your `.env` file:

```env
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_xxxxxxxxxx
CLERK_SECRET_KEY=sk_test_xxxxxxxxxx
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/discord_clone

# UploadThing
UPLOADTHING_SECRET=sk_live_xxxxxxxxxx
UPLOADTHING_APP_ID=xxxxxxxxxx

# App
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### Run

```bash
# Push database schema
npx prisma db push

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## Docker

```bash
docker-compose up --build
```

---

## Deployment

This project is deployed on **Koyeb** with zero-downtime deployment via GitHub integration.

To deploy your own instance:

1. Push to GitHub
2. Connect repo to Koyeb
3. Set all environment variables in Koyeb dashboard
4. Deploy

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=cylinder&color=5865F2,7289DA,4752C4,36393F&height=120&section=footer&animation=blinking" width="100%"/>

<sub>Built with Next.js 14 — Web Technologies Lab Project — Air University Lahore, Spring 2026</sub>

</div>
