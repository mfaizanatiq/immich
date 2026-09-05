# Immich on BlackholeNAS (from your fork)

Source: https://github.com/mfaizanatiq/immich (`mfa` branch)  
Images: `ghcr.io/mfaizanatiq/immich-server:mfa` and `…/immich-machine-learning:mfa`

## Flow

1. Push changes to branch `mfa` → GitHub Actions builds & pushes images to GHCR  
2. On the NAS: `sudo docker compose pull && sudo docker compose up -d`  
3. Open http://10.0.0.19:2283

## First-time NAS setup

```bash
sudo mkdir -p /volume2/docker-ssd/immich/postgres /volume1/photo/immich
cd /volume2/docker-ssd/immich
# copy docker-compose.yml and .env here
cp .env.example .env   # then edit DB_PASSWORD
sudo docker compose up -d
```

If GHCR packages are private, log the NAS into GHCR once:

```bash
echo YOUR_GITHUB_PAT | sudo docker login ghcr.io -u mfaizanatiq --password-stdin
```

Prefer making the packages **public** after the first successful build (Packages → package → Package settings → Change visibility).

## Bootstrap without waiting for a custom build

Temporarily set images back to `ghcr.io/immich-app/immich-server:v3` (and matching ML) in compose, or set `IMMICH_VERSION=v3` only after switching image names to `immich-app`. Custom features require your `:mfa` images.
