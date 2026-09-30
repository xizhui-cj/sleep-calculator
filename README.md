# 睡眠时间计算器

手机和桌面均可使用的静态睡眠时间计算器。柔和多彩配色、睡觉小狗涂鸦、无外部字体或前端依赖。

- 默认「现在睡」：读取设备本地时间，给出建议起床时间，自动随分钟更新。
- 「定时起床」：输入起床时间，倒推出建议上床时间；目标为下一次该时间。
- 起床时间保存在当前浏览器的 localStorage 中，下次保留。每次打开仍默认「现在睡」。
- 每个周期按90分钟计算，另预留30分钟入睡。显示1–6个周期：共2、3.5、5、6.5、8和9.5小时卧床时间。
- 跨午夜显示今天、明天或昨天；已过的上床时间会明确标注。
- 全部计算在本机完成，没有账户、数据上传或第三方追踪脚本。

## GitHub → Cloudflare Workers 自动发布

1. 在GitHub创建仓库 `sleep-calculator`。上传本目录的文件，确保 `wrangler.jsonc` 在仓库根目录，`public/index.html` 与 `public/sleep-doodle.webp` 在 `public/` 内。
2. 在Cloudflare控制台进入 **Workers & Pages → Create application → Import a repository**，选择GitHub和该仓库。已有Cloudflare GitHub连接时可直接选择仓库。
3. Worker名称填 `sleep-calculator`，生产分支选择 `main`。
4. 构建命令留空（无需构建）；部署命令填 `npx wrangler@4 deploy`；根目录保持仓库根目录。
5. 点击部署。成功后访问控制台显示的 `workers.dev` 网址。
6. 以后提交到 `main` 后，Cloudflare会自动发布。

无需配置API token、数据库或付费服务。Cloudflare若要求给GitHub应用增加新仓库权限，只授权这个仓库即可。

## 本地打开

直接双击 `public/index.html` 可使用；图片文件需保留在旁边。为获得最可靠的偏好保存行为，建议用静态服务器或部署后的HTTPS网址。

## 计算说明

90分钟周期与30分钟入睡是计算假设，真实周期及入睡时间会变化，不能保证醒来恰好处于浅睡阶段。成年人通常需要每晚7–9小时实际睡眠，因此优先显示5、6个周期，其余仅供参考。

参考：[NHLBI睡眠时长建议](https://www.nhlbi.nih.gov/health/sleep/how-much-sleep)。
