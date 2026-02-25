# ReachHFX — Real-Time Transit ETA Platform (Overview)

This repository is **informational only**. It contains product/architecture documentation and diagrams for ReachHFX.

- **Mobile app repo:** (private) / (link here)
- **Backend repo:** (private) / (link here)
- **Status:** Active development (2025–present)

---

## What ReachHFX Does

ReachHFX provides real-time transit ETAs by ingesting **GTFS-Realtime (protobuf)** updates, merging them with **static GTFS schedules**, and serving low-latency queries to a React Native client.

**Scope:** 80-route network, 2,317 stops (Halifax)

---

## Architecture

> Paste your architecture diagram image into `docs/` and update the path below.

![ReachHFX Architecture Diagram](docs/reachhfx-architecture.png)

### High-Level Components
- **React Native Mobile Client**
  - Stop search + arrivals/ETAs (edit to match your UI)
  - Calls backend endpoints for stop/route ETA data
- **Backend API (Node.js)**
  - Serves ETA queries from an in-memory state model
  - Exposes endpoints for stop search and arrival predictions (edit)
- **Ingestion + State Updater**
  - Pulls GTFS-RT protobuf feed on ~5s cadence
  - Merges real-time updates with static GTFS schedules
  - Maintains current “transit state” in memory for low-latency responses
- **Deployment**
  - Runs on AWS Lightsail (Ubuntu)
  - Scheduled ingestion jobs + repeatable deployments (edit details if you want)

---

## Key Engineering Decisions

### Performance
- **Precomputed stop → trip mappings** to avoid repeated scans and recomputation.
- In-memory indexing/state designed for fast per-stop ETA queries.

### Freshness
- Targeted ~**5-second** update cadence driven by GTFS-RT ingestion.

### Delivery & Quality
- GitHub Actions CI validates iOS builds for App Store/TestFlight compatibility (edit: how).

---

## Metrics (Add/Update)
- **ETA lookup performance:** ~70% improvement via precomputed mappings
- **Update cadence:** 5 seconds
- **TestFlight:** 25+ active testers

---

- System Sequence Diagram:  
  ![](docs/reachhfx-sequence.png)

- Data Model / State Diagram:  
  ![](docs/reachhfx-state-model.png)

---

## Screenshots (Optional)
| Screen | Preview |
|-------|---------|
| Home/Search | ![](docs/reachhfx-home.png) |
| Stop/Arrivals | ![](docs/reachhfx-stop.png) |

---

## Contact
Riley Devitt — rileydevitt@dal.ca
