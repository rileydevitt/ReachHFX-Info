# ReachHFX — Real-Time Transit ETA Platform

Real-time transit ETAs for Halifax built on GTFS + GTFS-Realtime. Mobile app (React Native) + backend service (Node.js) that ingests GTFS-RT protobuf feeds, merges with static schedules, and serves low-latency ETA queries.

> Status: Active development (2025–present)  
> Platforms: iOS (TestFlight), (Edit: Android if applicable)

---

## Architecture (High Level)

> Replace `docs/architecture.png` with your diagram path.

![ReachHFX Architecture Diagram](docs/architecture.png)

### Key Components
- **Mobile App (React Native)**: UI for stop search, arrivals/ETAs, and route browsing (edit to match).
- **Backend API (Node.js)**: Provides ETA endpoints backed by an in-memory transit state.
- **Ingestion Jobs**: Scheduled jobs that pull GTFS-Realtime (protobuf) and refresh state.
- **Static GTFS Data**: Routes/trips/stops/calendars used to ground real-time updates.
- **Deployment**: AWS Lightsail (Ubuntu) + scheduled ingestion (cron/systemd/etc. — edit to match).

---

## Data Sources
- **GTFS (Static)**: routes, trips, stop_times, calendar, etc.
- **GTFS-Realtime (protobuf)**: trip updates / vehicle positions (edit which you use).

---

## How ETAs Work (Implementation Notes)
- **Precomputed stop → trip mappings** to avoid repeated scans and improve query performance.
- **State model**: In-memory representation of real-time updates merged with static schedule data.
- **Freshness**: Updates target ~5s refresh cycles (edit if different).

---

## Screenshots (Optional)

> Drop screenshots in `docs/` and update paths.

| Screen | Preview |
|-------|---------|
| Home / Search | ![](docs/screen_home.png) |
| Stop Detail / Arrivals | ![](docs/screen_stop.png) |

---

## Tech Stack
- **Mobile**: React Native, TypeScript (edit)
- **Backend**: Node.js (Express/Fastify — edit), TypeScript/JavaScript (edit)
- **Data**: GTFS, GTFS-Realtime protobuf
- **Infra**: AWS Lightsail (Ubuntu), GitHub Actions CI

---

## Repository Structure (Edit to match)

/mobile # React Native app
/server # Backend API + ingestion logic
/docs # Diagrams + screenshots
/scripts # One-off tooling (optional)


---

## Getting Started

### Prerequisites
- Node.js (version: edit)
- (Optional) Yarn / pnpm / npm
- Xcode for iOS builds (if running iOS locally)
- (Edit) Any required API keys or feed URLs

### 1) Clone
```bash
git clone https://github.com/<your-username>/ReachHFX.git
cd ReachHFX
2) Backend Setup
cd server
npm install

Create .env:

cp .env.example .env

.env (example — edit keys/values):

PORT=3000
GTFS_STATIC_PATH=./data/gtfs
GTFS_RT_URL=https://<your-gtfs-rt-feed>
UPDATE_INTERVAL_SECONDS=5

Run backend:

npm run dev
3) Mobile Setup
cd ../mobile
npm install

Configure API base URL (edit how you do it):

EXPO_PUBLIC_API_BASE_URL=http://localhost:3000

Run:

npm start
API (Edit)

List your real endpoints. Example format:

GET /health

Returns service health and last update time.

GET /stops/search?q=<query>

Search stops by name.

GET /stops/:stopId/etas

Returns upcoming ETAs for a stop.

CI/CD

GitHub Actions validates builds on PRs/merges (edit details).

Deployment to Lightsail is repeatable (edit: scripts/commands).
