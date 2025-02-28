# Keycloak

```bash
docker run --name keycloak_unoptimized -p 8080:8080 \
        -e KC_BOOTSTRAP_ADMIN_USERNAME=admin \
        -e KC_BOOTSTRAP_ADMIN_PASSWORD=change_me \
        -v /path/to/realm/data:/opt/keycloak/data/import \
        quay.io/keycloak/keycloak:latest \
        start-dev --import-realm
```