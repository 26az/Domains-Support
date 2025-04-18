![Domain-Support](https://look.pics.cloudns.ch/img/cover2.png)

<div align="center">

# Domains-Support

</div>



一个基于 Cloudflare Pages 的域名管理系统，帮助您轻松管理和监控多个域名的状态、到期时间等信息。

## 功能特点

- 域名管理：添加、编辑、删除域名信息
- 状态监控：自动检查域名在线状态
- 到期提醒：设置域名到期提醒时间
- 多注册商支持：支持多个域名注册商的信息记录
- Telegram 通知：支持通过 Telegram 发送到期提醒
- 响应式设计：支持移动端和桌面端访问
- 安全认证：基于用户名密码的访问控制

## 快速开始

### 前置要求

- GitHub 账号
- Cloudflare 账号

### 安装步骤

1. Fork 本仓库到您的 GitHub 账号

2. 在 Cloudflare Pages 中创建新项目
   - 登录 Cloudflare Dashboard
   - 进入 Pages 页面
   - 点击 "Create a project"
   - 选择 "Connect to Git"
   - 选择您 fork 的仓库

3. 配置构建设置
   - 构建命令：`npm run build`
   - 构建输出目录：`dist`
   - 环境变量：
     ```
     USER=your_username
     PASS=your_password
     API_TOKEN=your_api_token
     ```

4. 创建 D1 数据库
   - 在 Cloudflare Dashboard 中进入 D1 页面
   - 创建新数据库，命名为 `domains-db`
   - 复制数据库 ID

5. 配置数据库
   - 在 Cloudflare Pages 项目设置中添加 D1 数据库绑定
   - 绑定名称：`DB`
   - 数据库 ID：粘贴之前复制的 ID

6. 初始化数据库
   - 在 Cloudflare Dashboard 中进入 D1 页面
   - 选择您的数据库
   - 执行 `schema.sql` 中的 SQL 语句

7. 部署
   - 点击 "Save and Deploy"
   - 等待部署完成

部署完成后，您可以通过 Cloudflare Pages 提供的域名访问系统。

## API 文档

### 1. 域名检查 API

**端点**: `/api/check`
**方法**: GET 或 POST
**认证**: 需要 API Token（通过 URL 参数或 Bearer Token）

认证方式（二选一）：
1. URL 参数：`/api/check?token=your_token`
2. Bearer Token：`Authorization: Bearer your_token`

响应：
```json
{
    "status": 200,
    "message": "检查完成",
    "data": {
        "total_domains": 10,
        "notified_domains": [
            {
                "domain": "example.com",
                "remainingDays": 15,
                "expiry_date": "2024-03-01"
            }
        ]
    }
}
```

### 2. 域名列表 API

**端点**: `/api/addrec`
**方法**: POST
**认证**: 需要 Bearer Token

响应：
```json
{
    "status": 200,
    "message": "获取成功",
    "data": [
        {
            "id": 1,
            "domain": "example.com",
            "registrar": "Cloudflare",
            "registrar_link": "https://cloudflare.com",
            "registrar_date": "2023-01-01",
            "expiry_date": "2024-01-01",
            "service_type": "网站",
            "status": "在线",
            "memo": "主站"
        }
    ]
}
```

## 配置说明

### 环境变量

- `USER`: 管理员用户名
- `PASS`: 管理员密码
- `API_TOKEN`: API 访问令牌

## 贡献指南

欢迎提交 Issue 和 Pull Request！

## 许可证

本项目基于 MIT 许可证开源 - 查看 [LICENSE](LICENSE) 文件了解更多详情。

## 作者

饭奇骏 ([@frankiejun](https://github.com/frankiejun))
