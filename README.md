# Google OAuth 品牌页 三个链接怎么填

用途：Google Cloud 的 **Google Auth Platform → 品牌（Branding）** 页要求填
Application home page / privacy policy / terms of service 三个公开链接，
否则「发布应用」是灰的、创建 OAuth 客户端也可能被拦。

本目录是给这个用途准备的三个静态页（内容极简，只说明「本人自用的
rclone Google Drive 只读客户端，不收集任何数据」）：

- `index.html`   → Application home page
- `privacy.html` → Application privacy policy link
- `tos.html`     → Application terms of service link

## 方案 A：GitHub Pages（社区通行做法，免费）

1. 建一个**公开**仓库，名字必须正好是 `<你的GitHub用户名>.github.io`。
2. 把本目录三个文件传到仓库根目录（网页端 Add file → Upload files 即可）。
3. 仓库 Settings → Pages → Source 选 `Deploy from a branch`，
   Branch 选 `main`、目录选 `/(root)`，Save。
4. 等 1–2 分钟，用浏览器确认这两个地址能打开（必须公开可访问、不需要登录）：
   - `https://<用户名>.github.io/`
   - `https://<用户名>.github.io/privacy.html`
5. 回到品牌页填：

   | 字段 | 填什么 |
   | --- | --- |
   | Application home page | `https://<用户名>.github.io/` |
   | Application privacy policy link | `https://<用户名>.github.io/privacy.html` |
   | Application terms of service link | `https://<用户名>.github.io/tos.html` |
   | Authorized domains | `<用户名>.github.io`（**只填域名**，不带 https:// 和路径） |

6. 保存。若报「域名未验证 / 需要验证所有权」，说明 Google 要求对该域名做
   所有权验证（Search Console 的 DNS TXT 方式），`github.io` 做不到 →
   改用方案 B 或 C。

## 方案 B：你已经有自己的域名 / 博客 / 实验室主页

直接用现成地址，但注意：
- 首页与隐私政策页必须**公开可访问**；
- Authorized domains 填该域名本身（不带协议、路径）；
- 若域名所有权未验证，同样要求做 Search Console 验证。

## 方案 C：不发布，留在测试状态

品牌页这几个 URL 可以不管，但代价是：应用处于「测试」状态时，
refresh token 按**签发时间** 7 天过期（用不用都过期），等于每周要重新授权
一次，每次都还需要 SSH 隧道 + 浏览器。

## 注意

- 这三页只是给 Google 与用户看的门面，内容不必复杂；关键是**公开可访问**。
- 隐私政策页建议保留「不收集数据、不共享给第三方、凭据只存本机」这几句。
- 若 Google 要求填 ToS 但你没标星提示，可留空；填上更省事。
