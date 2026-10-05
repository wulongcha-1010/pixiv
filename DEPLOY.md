# 部署说明

## Cloudflare Pages（自动部署）

- 项目名：`pixiv`
- 线上地址：https://pixiv-dvr.pages.dev/
- 生产分支：`main`
- 构建命令：`npx --yes pnpm@11.19.0 install --frozen-lockfile && npx --yes pnpm@11.19.0 run build`
- 输出目录：`dist`
- 环境变量：`NODE_VERSION=22`

推送到 `main` 分支后 Cloudflare 会自动构建并发布。

## 手动部署

```bash
pnpm install
pnpm build
npx wrangler pages deploy dist --project-name=pixiv --branch=main
```

## 说明

- 接口和图床由浏览器直连（默认 `api.cocomi.eu.org` + `i.pixiv.re`），可用 `.env` 覆盖，见 `.env.example`。
- `pnpm-workspace.yaml` 承载 pnpm 10+ 的 `patchedDependencies` / `allowBuilds` 配置。
- `.gitattributes` 固定 LF 并让 `*.patch` 保持原始字节，否则 pnpm 补丁 hash 校验会失败。
