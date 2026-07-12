# pjts42

用于在 dn42 网络一键部署 [Project Trans](https://github.com/project-trans) 的若干网络服务。

## 服务列表

| 服务 | 镜像 | 说明 |
| --- | --- | --- |
| `pjts-caddy` | `caddy:2-alpine` | Web 出口代理 |
| `pjts-coredns` | `coredns/coredns` | 提供 `pjts.dn42` / `fd42:706a:7473::/64` 区域权威 DNS |
| `pjts-web-mtf` | `node:alpine` (构建) / `nginx:alpine-slim`（服务）| [Next-MtF-wiki](https://github.com/project-trans/Next-MtF-wiki) |
| `pjts-web-rle` | `node:alpine` (构建) / `nginx:alpine-slim`（服务）| [RLE-wiki](https://github.com/project-trans/RLE-wiki) |
| `pjts-web-fonts` | `nixos/nix` (构建) / `nginx:alpine-slim`（服务）| [fonts](https://github.com/project-trans/fonts) 静态字体资源 |

## 域名

| 域名 | 后端 |
| --- | --- |
| `mtf.pjts.dn42` | `pjts-web-mtf:3000` |
| `rle.pjts.dn42` | `pjts-web-rle:3000` |
| `fonts.pjts.dn42` | `pjts-web-fonts:3000` |
| `mtf.dn42` | `pjts-web-mtf:3000` |

## 快速开始

```bash
docker compose up -d
# 或者
podman compose up -d
```

这会创建一个通向容器的接口，请将 `fd42:706a:7473::/64` 路由至该接口。

## LICENSE

APGL-3.0
