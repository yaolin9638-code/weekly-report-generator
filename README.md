# Weekly Report Generator

自动从 Slack 获取工作内容，生成结构化周报并写入 Google Sheets。

## 这是什么

一个自动化技能，每周自动从 Slack 频道读取团队成员的工作计划和工作总结，按照预设格式生成周报，并写入 Google Sheets 表格保存。

## 解决了什么问题

- 手动整理周报费时费力
- 周报格式不统一
- 容易遗漏信息
- 复制粘贴容易出错

## 适合谁用

- 需要定期写周报的团队
- 使用 Slack 进行工作汇报的团队
- 使用 Google Sheets 管理周报的团队

## 功能特点

- ✅ 自动从 Slack 读取工作消息
- ✅ 智能提取工作计划和工作总结
- ✅ 生成符合格式要求的周报
- ✅ 保留模板格式写入 Google Sheets
- ✅ 支持自定义配置

## 配置步骤（小白教程）

### 第一步：创建 Slack Token

1. 打开 https://api.slack.com/apps 点击 "Create New App"
2. 选择 "From scratch"，输入名字如 "周报机器人"
3. 点击 "OAuth & Permissions"
4. 在 "Scopes" 添加权限：
   - `channels:history` - 读取频道历史
   - `channels:read` - 读取频道列表
   - `chat:write` - 发送消息
   - `users:read` - 读取用户信息
   - `groups:history` - 读取群组消息
5. 点击 "Install to Workspace"
6. 复制显示的 Token（以 xoxp- 开头）

### 第二步：获取 Slack 频道 ID

1. 在 Slack 频道右键 → 复制链接
2. 链接中的 `C` 开头就是频道 ID
   - 例如：https://app.slack.com/client/T0001/B0001/C0A1WM0GV44
   - 频道 ID 就是 `C0A1WM0GV44`

### 第三步：创建 Google Sheets 凭证

1. 打开 https://console.cloud.google.com/
2. 创建新项目
3. 启用 "Google Sheets API" 和 "Google Drive API"
4. 创建 Service Account：
   - IAM 和管理员 → 服务账号 → 创建服务账号
   - 填写名称，角色选择 "编辑者"
   - 创建密钥 → 选择 JSON
5. 下载 JSON 文件保存

### 第四步：配置 Google Sheet

1. 创建一个 Google Sheet
2. 创建好模板分页（如"周报模板"）
3. 分享给 Service Account 邮箱：
   - 邮箱地址在下载的 JSON 文件中 `client_email` 字段
   - 权限选择"编辑者"

### 第五步：配置技能

编辑 `SKILL.md`，替换以下占位符：

```markdown
## Slack 配置
- Token: 你的Slack Token
- 频道: 你的频道ID

## Google Sheets 配置
- 凭证路径: ~/.credentials/google-sheets.json
- Service Account: 你的Service Account邮箱
- Sheet ID: 你的Sheet ID
- 模板分页: 你的模板分页名
```

## 配置项说明

| 占位符 | 怎么填 | 在哪里找 |
|--------|--------|----------|
| YOUR_SLACK_TOKEN | Slack Token (xoxp-开头) | Slack App 的 OAuth 页面 |
| YOUR_CHANNEL_ID | Slack 频道 ID (C开头) | 频道链接中获取 |
| YOUR_GOOGLE_CREDENTIALS_PATH | 凭证文件路径 | 下载的 JSON 文件 |
| YOUR_SERVICE_ACCOUNT_EMAIL | Service Account 邮箱 | JSON 文件中 client_email 字段 |
| YOUR_SHEET_ID | Google Sheet ID | 表格链接中 d/ 后面的部分 |
| YOUR_TEMPLATE_SHEET_NAME | 模板分页名称 | Google Sheet 分页名称 |
| YOUR_PROJECT_NAME | 项目名称 | 如 SESEGF、77AI 等 |

## 如何使用

1. **手动触发**：告诉助手"生成周报"
2. **自动触发**：按配置的触发时间自动运行

## 周报格式要求

### 禁止这样写 ❌
- "已处理" → 不写结果是什么
- "已修复" → 不写影响范围
- 技术术语堆砌 → 不写业务结果

### 应该这样写 ✅
- "完成了用户登录功能，测试通过已上线"
- "修复了支付失败问题，影响 100+ 用户"
- "开发效率提升 50%"

### 周报板块
1. 本周重要结论（P0/P1事故、资源情况）
2. 本周交付结果（交付盘、稳定性盘、效率盘）
3. 本周业务支撑与问题闭环（红榜、黑榜、闭环动作）
4. 本周AI提效（自动化、提效证明、工具沉淀）
5. 本周技术债与风险排雷
6. 下周计划

## 文件结构

```
weekly-report-generator/
├── SKILL.md          # 技能定义（需要配置）
├── README.md         # 说明文档
└── .gitignore        # 忽略配置
```

## 常见问题

**Q: Token 权限不够怎么办？**
A: 确保添加了 `groups:history` 权限，并重新安装 App

**Q: Google Sheet 写入失败？**
A: 确保已把 Service Account 邮箱添加到表格共享中

**Q: 如何测试？**
A: 手动触发"生成周报"查看输出
