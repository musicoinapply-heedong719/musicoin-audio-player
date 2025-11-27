# Musicoin 3.0 – Web Audio Player (musicoin-audio-player)

## Overview

The **Musicoin 3.0 Web Audio Player** is a reference client for playing music and audio content
registered in the Musicoin ecosystem.

It demonstrates:

- How to link on-chain metadata with off-chain audio files  
- How to display artist and track information using the Musicoin 3.0 smart contracts  
- How to record or relay playback events for value distribution and analytics  

This project is **not** intended to be a full commercial streaming service,  
but a clear, minimal and extensible example for developers and ecosystem partners.

---

## Core Goals

- Provide a clean, browser-based player for Musicoin-registered tracks  
- Integrate with the Musicoin smart contracts and Artist ID system  
- Support lightweight playback logging for analytics and future reward models  
- Serve as a starter template for custom players (web, desktop, kiosk, etc.)

---

## Key Features

### 1. Track Browsing

- Track list view (title, artist, duration, tags)  
- Search / filter by:
  - Artist
  - Genre / tag
  - Recent / popular (via analytics backend)  

### 2. Playback

- HTML5-based audio playback:
  - Play / pause / seek
  - Next / previous track
  - Volume control & mute
- Playlist support:
  - Play queue
  - Repeat / shuffle (optional)

### 3. Metadata Display

- On-chain + off-chain metadata:
  - Track title, album, artist
  - Artist profile (from `musicoin-artist-id`)
  - Artwork (cover image from IPFS/URL)
  - Content hash and registration ID

### 4. Playback Logging (Optional)

- Send playback events to:
  - Analytics backend (`musicoin-analytics-dashboard`)
  - Future reward distribution modules
- Configurable strategy:
  - Log on “play start”
  - Log only if playback exceeds N seconds
  - Log on “completed”

### 5. Integration Hooks

- Use Artist ID to:
  - Link to artist homepage / Twitter/X  
  - Jump to artist detail or other dApps  
- Use Content Registry (future module) to:
  - Fetch base metadata  
- Use Analytics:
  - Show “most played” or “trending” sections  

---

## Architecture

The project is designed as a **frontend-first** application, with light backend helpers.

---

### 1. Frontend

Recommended stack:

- React / Next.js SPA or SSR  
- TailwindCSS or similar utility-first CSS  
- Audio via HTML5 `<audio>` element or lightweight library wrapper  

Main UI components:

- `PlayerBar` – play/pause/seek controls  
- `TrackList` – list or table of tracks  
- `TrackDetails` – metadata display  
- `NowPlaying` – compact view for current track  

---

### 2. Backend (Optional)

Responsibilities:

- Proxy to indexer/analytics APIs  
- Sign/verify messages (optional advanced flows)  
- Provide track lists:
  - New / trending / artist-specific / playlists  

Recommended stack:

- Node.js (Express / NestJS) or Python (FastAPI)  

Backend is optional if you directly query:

- Musicoin indexer API  
- IPFS / storage gateways  

---

### 3. Data Sources

- **On-chain:**
  - Track registration contract
  - Artist ID contract  
- **Off-chain:**
  - IPFS/HTTP storage for audio files
  - Analytics backend for popularity metrics  

---

## Example Data Flow

1. Player fetches a list of track IDs from the indexer/analytics API.  
2. For each track ID:
   - Calls Musicoin contract to get metadata references.  
   - Resolves IPFS/URL for audio and cover image.  
   - Loads artist info from Artist ID registry (via backend or direct call).  
3. User selects a track and presses Play.  
4. Player:
   - Loads audio URL into `<audio>` element.  
   - Starts playback and updates UI (Now Playing).  
5. When playback crosses a defined threshold:
   - A playback event is sent to the analytics service.  

---

## Installation

### 1. Clone Repository

```bash
git clone https://github.com/musicoin/musicoin-audio-player.git
cd musicoin-audio-player
```

### 2. Install Dependencies

```bash
npm install
```

(or `yarn`, `pnpm` based on preference)

### 3. Configure Environment

Copy the example environment file:

```bash
cp .env.example .env
```

Set:

- `NEXT_PUBLIC_INDEXER_API_URL`
- `NEXT_PUBLIC_ANALYTICS_API_URL`
- `NEXT_PUBLIC_CHAIN_ID`
- `NEXT_PUBLIC_RPC_URL`

### 4. Run Development Server

```bash
npm run dev
```

Then open:

- http://localhost:3000

---

## Folder Structure (Suggested)

```text
musicoin-audio-player/
  ├─ public/                # Static assets
  ├─ src/
  │   ├─ components/
  │   │   ├─ PlayerBar.tsx
  │   │   ├─ TrackList.tsx
  │   │   ├─ TrackDetails.tsx
  │   │   └─ NowPlaying.tsx
  │   ├─ pages/
  │   │   ├─ index.tsx      # Main player page
  │   │   └─ artist/[id].tsx
  │   ├─ lib/
  │   │   ├─ api.ts         # Client API helpers
  │   │   └─ audio.ts       # Optional audio logic wrapper
  │   └─ types/
  │       └─ index.ts       # Type definitions
  ├─ .env.example
  ├─ package.json
  └─ README.md
```

---

## Roadmap

### Phase 1 – MVP

- Basic track list & playback  
- Artist & track metadata from indexer  
- Simple Now Playing bar  

### Phase 2 – Enriched Experience

- Playlists & queue management  
- Trending / recommended sections  
- Artist pages with track lists  

### Phase 3 – Deep Ecosystem Integration

- Playback logging to analytics  
- Integration with Contract Proof and other modules (e.g., show license status)  
- Multi-device synchronization (future concept)  

### Phase 4 – Extended Features

- Waveform display (optional)  
- Equalizer or basic audio effects  
- Offline-friendly / PWA mode (future enhancement)  

---

## Contribution

Contributions are welcome:

- UI/UX improvements  
- Audio handling enhancements  
- New integration hooks (e.g., comments, sharing)  
- Performance optimizations  

Please open issues or PRs with details.

---

## License

TBD  
(MIT or Apache-2.0 recommended for quick ecosystem adoption.)
