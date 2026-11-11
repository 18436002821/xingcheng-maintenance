# 星橙里 · 物业维修工作台

React + TypeScript + Vite 手机/电脑适配的工单演示，可在 GitHub Pages 运行，不需要 ChatGPT 登录。

## 已实现

维修员、主管、财务、统计四个视角；新建、派单、接单、前后照片、费用填报、验收/退回、结算；搜索筛选、月份汇总、CSV 导出和预算提醒。

**当前为单浏览器演示版。角色切换不构成权限控制，数据和照片只保存在当前浏览器，不支持跨设备同步。示例工单不是实际业务记录。**

## GitHub Pages 发布

已包含构建后的 docs 文件夹：仓库 Settings → Pages → Deploy from a branch → main → /docs → Save。等待部署完成，使用 Pages 设置页面返回的网址。所有资源采用相对路径，支持仓库子目录。若账号套餐不支持私有仓库 Pages，可使用仅包含演示代码的公开仓库，或先私有保存源代码。

## 本地开发

需要 Node.js 22.13 或以上：

```bash
npm ci
npm run dev
npm run build
```

每次修改后重新构建，并将 src 和 docs 一起提交。无需在线构建。src/App.tsx 为业务逻辑，src/style.css 为样式，docs 为发布目录。

## 数据注意事项

清理浏览器网站数据会删除演示记录；不同浏览器、域名分别保存。CSV 不包含照片。预算提醒只显示在页面，不发送消息。示例月份为 2026 年 11 月。请勿录入真实业主资料、提交密钥或将上传照片存入 GitHub。

后续正式接入详见 DEPLOYMENT.md。
