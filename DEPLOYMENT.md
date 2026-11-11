# 后续正式部署与企业微信接入

现在无需购买服务器或域名。GitHub Pages 提供前端演示托管；企业微信免登、数据库、消息推送均尚未实现。

## 改造步骤

1. 用后端 API 替换 App.tsx 的 localStorage 读写，数据库保存工单、材料、人员、项目授权、照片元信息和操作日志。
2. 企业微信 OAuth 回调校验 state，以 code 获取 UserId，再映射服务端角色和所属项目。Secret、access_token 只保存在服务端。
3. 服务端强制角色和项目权限：维修员仅本人任务、主管仅授权项目、财务仅已验收工单、统计只读。不能信任前端角色切换。
4. 服务端校验状态流转、维修前后照片、费用；金额以整数分保存，结算使用事务及幂等机制。
5. 照片存入受控对象存储，验证类型和大小，签发有时效且经过权限校验的访问地址。
6. 按企业微信后台要求配置应用主页、员工可见范围、可信域名、校验文件和服务器出口可信 IP；如用 JS-SDK，由后端生成签名。
7. 消息通知经后端发送，记录发送结果和重试。页面操作成功不等于通知送达。
8. 用三类员工账号测试跨设备同步、越权拦截、验收退回、重复提交、重复结算、备份恢复，再正式启用。

## API 规划（未实现）

GET /api/me：员工及授权项目。
GET/POST /api/orders：列表/新建。
GET /api/orders/:id：详情。
POST /api/orders/:id/assign：指派。
POST /api/orders/:id/accept：接单。
PUT /api/orders/:id/costs：材料及人工费。
POST /api/orders/:id/photos：上传前后照片。
POST /api/orders/:id/submit：提交验收。
POST /api/orders/:id/review：验收通过或退回。
POST /api/orders/:id/settle：财务结算。
GET /api/reports：按权限和日期汇总。

## 参考

- https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- https://developer.work.weixin.qq.com/document/path/91022
- https://work.weixin.qq.com/
