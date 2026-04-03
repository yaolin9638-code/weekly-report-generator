# Weekly Report Generator

自动从 Slack 获取工作内容，生成结构化周报并写入 Google Sheets。

## 功能
- 从 Slack 频道自动获取工作计划和工作总结
- 生成符合格式要求的周报
- 保留模板格式写入 Google Sheets
- 自动发送通知

## 配置步骤

### 1. Slack 配置
- 创建 Slack App: https://api.slack.com/apps
- 添加权限:
  - `channels:history`
  - `channels:read`
  - `chat:write`
  - `users:read`
  - `groups:history`
- 安装到 Workspace，获取 Token

### 2. Google Sheets 配置
- 创建 Google Cloud 项目
- 启用 Google Sheets API
- 创建 Service Account
- 下载 JSON 凭证
- 共享 Google Sheet 给 Service Account

### 3. 配置 Skill

在 `SKILL.md` 中替换以下占位符：

```markdown
## Slack 配置
- Token: YOUR_SLACK_TOKEN
- 频道 ID: YOUR_CHANNEL_ID_1, YOUR_CHANNEL_ID_2

## Google Sheets 配置
- 凭证路径: YOUR_GOOGLE_CREDENTIALS_PATH
- Service Account: YOUR_SERVICE_ACCOUNT_EMAIL
- Sheet ID: YOUR_SHEET_ID
- 模板分页: YOUR_TEMPLATE_SHEET_NAME

## 项目名称
- 项目名: YOUR_PROJECT_NAME
```

## 配置说明

| 配置项 | 说明 | 示例 |
|--------|------|------|
| YOUR_SLACK_TOKEN | Slack User Token (xoxp-开头) | xoxp-xxx... |
| YOUR_CHANNEL_ID_1 | 第一个 Slack 频道 ID | C0A1WM0GV44 |
| YOUR_CHANNEL_ID_2 | 第二个 Slack 频道 ID | C0991GCU11C |
| YOUR_GOOGLE_CREDENTIALS_PATH | Google 凭证 JSON 文件路径 | ~/.credentials/google-sheets.json |
| YOUR_SERVICE_ACCOUNT_EMAIL | Service Account 邮箱 | your-project@iam.gserviceaccount.com |
| YOUR_SHEET_ID | Google Sheet ID | 1Ndx9XeG2jKcYt36PUz8vyZbP6vz80rFiXdstsdCiCDE |
| YOUR_TEMPLATE_SHEET_NAME | 模板分页名称 | 周报(3/23-3/27) |
| YOUR_PROJECT_NAME | 项目/产品名称 | SESEGF |

## 周报格式要求

### 严禁事项
- ❌ 严禁写技术黑话堆砌报告
- ❌ 严禁写"已处理/已修复/已优化"但不写结果
- ❌ 不准用技术复杂性掩盖交付问题

### 必须写清楚
- ✅ 结果是什么
- ✅ 影响范围
- ✅ 责任人
- ✅ 时间点
- ✅ AI/自动化必须量化
- ✅ 风险项必须写明后果与备用方案

### 周报板块
1. 本周重要结论
2. 本周交付结果
3. 本周业务支撑与问题闭环
4. 本周AI提效
5. 本周技术债与风险排雷
6. 下周计划

## 使用方法

```bash
# 手动触发
触发"生成周报"
```

## 文件结构

```
weekly-report-generator/
├── SKILL.md          # 技能定义和配置
├── README.md         # 说明文档
└── .gitignore        # 忽略配置
```

## 注意事项

- Token 和凭证等敏感信息不要提交到代码仓库
- 确保 Slack Token 有足够权限读取频道消息
- Google Sheet 需要共享给 Service Account 才能写入
