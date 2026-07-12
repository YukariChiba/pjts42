# ---- Build stage ----
FROM node:alpine AS builder

RUN apk add --no-cache git
RUN npm install -g pnpm

WORKDIR /app

RUN git clone --recurse-submodules https://github.com/project-trans/Next-MtF-wiki.git .

# RUN grep -rl 'fonts.project-trans.org' /app 2>/dev/null \
#     | xargs -r sed -i 's|https://fonts.project-trans.org|http://fonts.pjts.dn42|g'

RUN pnpm install --frozen-lockfile

ARG NEXT_PUBLIC_SITE_URL=http://mtf.pjts.dn42/
ARG NEXT_PUBLIC_ROBOTS_ALLOW=true
ARG NEXT_PUBLIC_INCLUDE_SITEMAP=true
ARG NEXT_PUBLIC_SERVER_BUILD_INDEX=true
ARG NEXT_PUBLIC_BANNER_TEXT=banner-text-disclaimer
ARG NEXT_PUBLIC_EDIT_LINK_GITHUB_URL=https://github.com/project-trans/MtF-wiki/tree/master/
ARG NEXT_PUBLIC_OG_BASE_URL=http://mtf.pjts.dn42/

ENV NEXT_PUBLIC_SITE_URL=${NEXT_PUBLIC_SITE_URL} \
    NEXT_PUBLIC_ROBOTS_ALLOW=${NEXT_PUBLIC_ROBOTS_ALLOW} \
    NEXT_PUBLIC_INCLUDE_SITEMAP=${NEXT_PUBLIC_INCLUDE_SITEMAP} \
    NEXT_PUBLIC_SERVER_BUILD_INDEX=${NEXT_PUBLIC_SERVER_BUILD_INDEX} \
    NEXT_PUBLIC_BANNER_TEXT=${NEXT_PUBLIC_BANNER_TEXT} \
    NEXT_PUBLIC_EDIT_LINK_GITHUB_URL=${NEXT_PUBLIC_EDIT_LINK_GITHUB_URL} \
    NEXT_PUBLIC_OG_BASE_URL=${NEXT_PUBLIC_OG_BASE_URL}

RUN NEXT_PUBLIC_DEPLOY_TIME=$(date -u +'%Y-%m-%dT%H:%M:%SZ') pnpm build

# ---- Runtime stage ----
FROM nginx:alpine-slim AS runtime

COPY --from=builder /app/apps/wiki/out /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000
