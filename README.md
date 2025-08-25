# Real-Time Fleet/Asset Tracker (Maps + WebSockets)

A zero-setup learning project for your HCCDA Huawei Tech Essential students. Runs locally on Windows 10 with Docker Desktop.

**Tech stack**
- Backend: FastAPI + WebSockets (Uvicorn)
- Frontend: Leaflet (interactive map) + vanilla JS
- Packaging: Docker + docker-compose

## Quick Start (Windows 10)

1) Install **Docker Desktop** and ensure it is running.
2) Download and unzip this project (or clone your repo if you upload it).
3) Open **PowerShell** in the project folder and run:

```powershell
docker compose up --build -d
```

4) Open your browser: **http://localhost:8000**  
   - You'll see a live map of moving assets around Lahore by default.
   - WebSocket updates stream every second.

5) To view logs (optional):
```powershell
docker compose logs -f tracker
```

6) To stop:
```powershell
docker compose down
```

## Customize (optional)

- **Number of assets**: edit `ASSET_COUNT` in `docker-compose.yml`.
- **City center**: edit `CITY_CENTER_LAT`, `CITY_CENTER_LNG` in `docker-compose.yml`.
- **Update interval (ms)**: edit `TICK_MS` in `docker-compose.yml`.

## REST Endpoints (for exercises)

- `GET /api/assets` – list current assets.
- `POST /api/assets` – create a new asset. Example body:
  ```json
  {"id":"van-99","name":"Training Van 99","lat":31.50,"lng":74.35}
  ```
- `PATCH /api/assets/{id}` – update an asset's location/status manually.
- `GET /health` – health check.

## WebSocket

- `ws://localhost:8000/ws`
- Messages:
  - Snapshot on connect:
    ```json
    {"type":"snapshot","data":[{asset}, ...]}
    ```
  - Incremental update for a single asset:
    ```json
    {"type":"asset_update","data":{asset}}
    ```

## Teaching ideas
- Ask students to add a **/api/telemetry** POST endpoint and push real GPS points.
- Add per-asset **polylines** to show tracks.
- Add **geofencing** alerts and toast notifications.
- Store data in **Redis** or **PostgreSQL** instead of memory.
"# -Real-Time-Fleet-Asset-Tracker" 
