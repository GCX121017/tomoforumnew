# 明天后 (Tomoforum)

一个现代化中文社区论坛，基于 Next.js 16 + Supabase + Tailwind CSS 4 构建。

## ✨ 功能特性

### 核心功能
- 📝 **帖子系统** — 发帖 / 编辑 / 删除 / 置顶 / Markdown 支持（GFM）
- 💬 **评论系统** — 嵌套回复 / 点赞 / 表情
- 👍 **互动** — 帖子点赞 / 收藏 / 浏览计数（服务端去重）
- 🔍 **搜索** — 全文搜索 / 分类筛选 / 作者筛选 / 标签过滤
- 🏷️ **分类与标签** — 6 个预设分类板块 / 自由标签系统
- 📊 **积分与等级** — 7 级成长体系（冒泡→SVIP）/ 实时积分计算

### 用户系统
- 🔐 **认证** — 用户名 + 头像 + 密码登录，Cookie 持久化
- 👤 **个人主页** — 头像 / 签名 / 等级徽章 / 积分详情 / 发帖列表 / 收藏列表
- 🔔 **通知系统** — 点赞 / 评论 / 关注 / 好友 / 私信等多类型通知
- 👥 **关注系统** — 关注 / 粉丝列表 / 关注动态 Feed
- 🤝 **好友系统** — 好友申请 / 接受 / 拒绝 / 删除
- 💬 **私信系统** — 全页面聊天 / 消息编辑（2分钟内）/ 消息撤回（2分钟内）
- 🛡️ **管理后台** — 官方账号专属管理面板（帖子 / 评论 / 用户管理 / 发官方帖）

### UI / UX
- 🌙 **深色模式** — 一键切换，全局适配
- 📱 **响应式设计** — 桌面端双栏 / 移动端单栏 + 底部导航
- 🎨 **黑白极简风格** — V2EX 风格帖子列表，shadcn/ui 组件库
- ⚡ **SPA 体验** — Zustand 路由 + Framer Motion 页面过渡动画
- 📝 **Markdown 编辑器** — 格式化工具栏（12 个按钮）/ 实时预览
- 🖼️ **图片系统** — 上传 / 拖拽 / 灯箱 / 缩略图网格

## 🛠️ 技术栈

| 类别 | 技术 |
|------|------|
| 框架 | Next.js 16 (App Router) |
| 语言 | TypeScript 5 |
| 样式 | Tailwind CSS 4 + shadcn/ui |
| 数据库 | Supabase (PostgreSQL) + Prisma ORM |
| 状态管理 | Zustand + TanStack Query |
| 动画 | Framer Motion |
| 认证 | Cookie-based 认证 + bcrypt 密码哈希 |
| 图标 | Lucide React |
| Markdown | react-markdown + remark-gfm + highlight.js |
| 通知 | Sonner (Toast) |

## 📦 快速开始

### 环境要求
- Node.js 20+ 或 Bun 1.x
- Supabase 项目（需要提前创建）

### 安装步骤

```bash
# 1. 克隆仓库
git clone https://github.com/your-username/tomoforum.git
cd tomoforum

# 2. 安装依赖
bun install
# 或 npm install

# 3. 配置环境变量
cp .env.example .env
# 编辑 .env，填入你的 Supabase 凭据

# 4. 同步数据库
bun run db:push
# 或 npx prisma db push

# 5. 初始化种子数据（创建官方账号和社区公约帖子）
# 访问 GET /api/seed

# 6. 启动开发服务器
bun run dev
# 或 npm run dev

# 7. 打开浏览器访问 http://localhost:3000
```

### 环境变量说明

| 变量名 | 说明 | 获取方式 |
|--------|------|---------|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase 项目 URL | Supabase Dashboard → Settings → API |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase 匿名密钥 | Supabase Dashboard → Settings → API |

## 📁 项目结构

```
tomoforum/
├── prisma/
│   └── schema.prisma          # 数据库模型定义（13 个模型）
├── public/
│   ├── logo.svg               # 社区 Logo
│   └── robots.txt
├── src/
│   ├── app/
│   │   ├── layout.tsx         # 根布局
│   │   ├── page.tsx           # SPA 入口（Zustand 路由）
│   │   ├── globals.css        # 全局样式
│   │   └── api/
│   │       ├── auth/          # 认证（登录/注册/登出）
│   │       ├── admin/         # 管理后台 API
│   │       ├── posts/         # 帖子 CRUD + 点赞/收藏/置顶/浏览
│   │       ├── comments/      # 评论 CRUD + 点赞
│   │       ├── users/         # 用户 + 关注
│   │       ├── friends/       # 好友系统
│   │       ├── messages/      # 私信系统 + 编辑/撤回
│   │       ├── notifications/ # 通知系统
│   │       ├── search/        # 搜索
│   │       ├── categories/    # 分类
│   │       ├── follows/       # 关注状态批量查询
│   │       └── seed/          # 种子数据
│   ├── components/
│   │   ├── forum/             # 业务组件（23 个）
│   │   └── ui/                # shadcn/ui 基础组件
│   ├── lib/
│   │   ├── supabase.ts        # Supabase 客户端
│   │   ├── normalizeUser.ts   # 用户名编解码（Base64URL）
│   │   ├── levels.ts          # 积分等级体系
│   │   ├── password.ts        # 密码工具（bcrypt）
│   │   └── utils.ts           # 通用工具
│   ├── store/
│   │   └── forum.ts           # Zustand 全局状态
│   └── hooks/                 # 自定义 Hooks
├── .env.example               # 环境变量模板
├── LICENSE                    # MIT 许可证
└── package.json
```

## 📊 数据模型

共 **13 个数据模型**：

| 模型 | 说明 |
|------|------|
| `User` | 用户（含密码/角色/等级/积分） |
| `Post` | 帖子 |
| `Comment` | 评论（支持嵌套回复） |
| `Tag` | 标签 |
| `PostTag` | 帖子-标签关联 |
| `Category` | 分类 |
| `Notification` | 通知 |
| `PostLike` | 帖子点赞 |
| `PostBookmark` | 帖子收藏 |
| `PostView` | 浏览记录（去重） |
| `CommentLike` | 评论点赞 |
| `Follow` | 关注关系 |
| `FriendRequest` | 好友关系 |
| `PrivateMessage` | 私信 |

## 🔑 管理员账号

种子数据会自动创建管理员账号「明天过后」。首次部署后请通过注册流程创建管理员并手动在数据库中设置 `role = 'official'`。

## 📝 常用脚本

```bash
bun run dev          # 启动开发服务器
bun run build        # 构建生产版本
bun run start        # 启动生产服务器
bun run lint         # ESLint 代码检查
bun run db:push      # 同步数据库 Schema
bun run db:generate  # 生成 Prisma Client
```

## 📄 许可证

本项目采用 [MIT License](./LICENSE) 开源。

## 📧 联系方式

- **邮箱**（推荐）：zl199518@outlook.com
- **备用邮箱**：guanqpcx@outlook.com
- **社区**：在论坛内 @ 官方账号「明天过后」
