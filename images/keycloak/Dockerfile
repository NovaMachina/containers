FROM quay.io/keycloak/keycloak:26.6.1 AS builder

ENV KC_DB=postgres
ENV KC_METRICS_ENABLED=true
ENV KC_HEALTH_ENABLED=true

WORKDIR /opt/keycloak

RUN /opt/keycloak/bin/kc.sh build

FROM quay.io/keycloak/keycloak:26.6.1

LABEL org.opencontainers.image.source="https://github.com/novamachina/containers"
LABEL org.opencontainers.image.description="Keycloak identity and access management, optimized build with PostgreSQL, metrics, and health"

COPY --from=builder /opt/keycloak/ /opt/keycloak/

HEALTHCHECK --interval=30s --timeout=10s --start-period=90s --retries=3 \
  CMD curl -f http://localhost:9000/health/ready || exit 1

ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start", "--optimized"]
