# ---- Build stage ----
FROM nixos/nix:latest AS builder

ENV NIXPKGS_ALLOW_UNFREE=1

WORKDIR /app

RUN nix --extra-experimental-features 'nix-command flakes' \
        --option sandbox false \
        --accept-flake-config \
        build github:project-trans/fonts

# ---- Runtime stage ----
FROM nginx:alpine-slim AS runtime

COPY --from=builder /app/result/ /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000
