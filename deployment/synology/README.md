# Immich on Synology (BlackholeNAS)

Live stack: `/volume2/docker-ssd/immich/`  
Web UI: http://10.0.0.19:2283

## Layout

| Path | Role |
|------|------|
| `/volume1/data/immich/library` | Immich uploads (HDD) |
| `/volume2/docker-ssd/immich/postgres` | Database (SSD) |
| `/volume1/homes/faizan/Photos` | Synology Photos → `/mnt/synology-photos` (ro) |

## Update

```bash
cd /volume2/docker-ssd/immich
# bump IMMICH_VERSION in .env, refresh compose from release if needed
sudo docker compose pull
sudo docker compose up -d
```

## Notes

- Synology Photos is an Immich **External Library** (PhotoLibrary + MobileBackup).
- Official images: `ghcr.io/immich-app/immich-server` (optional fork images via `build-custom-images` workflow on branch `mfa`).
