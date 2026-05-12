# keycloak

Keycloak identity and access management server. Optimized build with PostgreSQL, metrics, and health endpoints enabled.

## Usage

```sh
docker pull ghcr.io/NovaMachina/keycloak:latest
docker run --rm \
  -e KC_DB_URL=jdbc:postgresql://db:5432/keycloak \
  -e KC_DB_USERNAME=keycloak \
  -e KC_DB_PASSWORD=secret \
  -e KC_HOSTNAME=auth.example.com \
  -e KC_BOOTSTRAP_ADMIN_USERNAME=admin \
  -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin \
  -p 8080:8080 -p 9000:9000 \
  ghcr.io/NovaMachina/keycloak:latest
```

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `KC_DB_URL` | required | JDBC URL, e.g. `jdbc:postgresql://db:5432/keycloak` |
| `KC_DB_USERNAME` | required | PostgreSQL username |
| `KC_DB_PASSWORD` | required | PostgreSQL password |
| `KC_HOSTNAME` | required | Public hostname Keycloak is reachable at, e.g. `auth.example.com` |
| `KC_BOOTSTRAP_ADMIN_USERNAME` | first-run | Admin username created on first start |
| `KC_BOOTSTRAP_ADMIN_PASSWORD` | first-run | Admin password created on first start |
| `KC_HOSTNAME_STRICT` | `true` | Set to `false` to skip hostname validation (dev only) |

## Ports

| Port | Description |
|------|-------------|
| `8080` | HTTP (main application) |
| `8443` | HTTPS (main application, if TLS configured) |
| `9000` | Management — health at `/health/ready`, metrics at `/metrics` |

## Tags

| Tag | Description |
|-----|-------------|
| `latest` | Latest build from `main` |
| `<sha>` | Pinned to a specific commit |
