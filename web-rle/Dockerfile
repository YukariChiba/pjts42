# ---- Build stage ----
FROM node:alpine AS builder

RUN apk add --no-cache git
RUN npm install -g pnpm

WORKDIR /app

RUN git clone --recurse-submodules https://github.com/project-trans/RLE-wiki .

RUN pnpm install --frozen-lockfile
RUN pnpm update @project-trans/vitepress-theme-project-trans@prerelease

# RUN grep -rl 'fonts.project-trans.org' /app 2>/dev/null \
#     | grep -v '/.git/' \
#     | xargs -r sed -i 's|https://fonts.project-trans.org|http://fonts.pjts.dn42|g'

RUN pnpm build

# ---- Runtime stage ----
FROM nginx:alpine-slim AS runtime

COPY --from=builder /app/docs/.vitepress/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000
