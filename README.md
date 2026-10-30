# stitchbook-compose

Starts the StitchBook services together in Docker. PostgreSQL stays in the existing `stitchbook-postgres` container so local accounts are kept.

Clone every service as a sibling of this folder:

```
Projects/
  stitchbook-compose/
  stitchbook-core/
  stitchbook-payments/
  stitchbook-notifications/
  stitchbook-admin/
  stitchbook-customer/
  stitchbook-tailor/
  stitchbook-gateway/
```

Copy each service's `.env.example` to `.env` and use the same `JWT_SECRET` and `INTERNAL_TOKEN`. The database host inside Docker is set by this file to `stitchbook-postgres`.

The gateway listens on port **8090** because 8080 is often already taken.

## Run

```bash
docker start stitchbook-postgres
docker network create stitchbook
docker network connect stitchbook stitchbook-postgres
docker compose up -d --build
```

`docker network create` and `docker network connect` only need to happen once. Open http://127.0.0.1:8090
