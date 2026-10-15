# nvim-edu-lzcapp

[nvim-edu](https://github.com/s3onghyun/nvim-edu) 的 LazyCat LPK 打包 —— 在浏览器里闯关练习 Vim/Neovim 与 tmux 按键的训练应用（纯静态站点，无后端服务）。

## 结构

- `package.yml` — LPK v2 包元数据（`community.lazycat.app.nvim-edu`）
- `lzc-manifest.yml` — 运行结构：静态文件直出（`file:///lzcapp/pkg/content/`）
- `lzc-build.yml` — 构建配置（`build.sh` + `contentdir: ./dist`）
- `build.sh` — 拉取上游 main 分支源码 → `npm ci && npm run build` → 拷贝 `dist/`
- `.github/lazycat-action.yml` — ca-x/lazycat-github-action 配置（git 版本源，node 工具链，仅私有商店）
- `.github/workflows/lazycat.yml` — 每日自动构建 + 发布喵喵商店

## 发布

推送到 `lazycat-contrib/nvim-edu-lzcapp` 后，GitHub Action 自动：

1. 计算下一个 patch 版本
2. 构建上游 main 最新 commit
3. 产出 `community.lazycat.app.nvim-edu-v<version>.lpk` Release 资产
4. 发布到喵喵商店（`APPSTORE_URL` / `APPSTORE_TOKEN`，可选 `APP_ID`、`PRIVATE_STORE_GROUP_CODES`）

需在仓库/组织配置 Secrets：`APPSTORE_URL`、`APPSTORE_TOKEN`。

## 本地验证

```bash
UPSTREAM_SOURCE_DIR=../nvim-edu lzc-cli project release -o nvim-edu.lpk
```
