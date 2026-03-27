# 流浪地球·种子编辑器

## 项目概述

这是一个基因编程小游戏，玩家需要设计能在极端外星环境下存活的植物。通过组合不同的基因片段（抗旱、抗辐射、发光等），在一个不断恶化的星球上种植它们，观察它们的进化或死亡。

**核心玩法**：
1. 在基因编辑器中选择基因片段（最多4个）
2. 点击种植按钮创建植物
3. 开始游戏，观察植物在环境中的生存情况
4. 触发环境事件（太阳耀斑、沙尘暴、冰河时期等）挑战植物适应性
5. 体验作为"星球绿化师"的责任感

**教育价值**：用游戏的方式学习基因工程和进化论

## 版本技术栈

- **Framework**: Next.js 16 (App Router)
- **Core**: React 19
- **Language**: TypeScript 5
- **UI 组件**: shadcn/ui (基于 Radix UI)
- **Styling**: Tailwind CSS 4
- **状态管理**: React Hooks (useState, useEffect, useCallback)
- **通知系统**: Sonner (toast notifications)

## 目录结构

```
├── public/                 # 静态资源
├── scripts/                # 构建与启动脚本
│   ├── build.sh            # 构建脚本
│   ├── dev.sh              # 开发环境启动脚本
│   ├── prepare.sh          # 预处理脚本
│   └── start.sh            # 生产环境启动脚本
├── src/
│   ├── app/                # 页面路由与布局
│   │   ├── page.tsx        # 主游戏页面
│   │   ├── layout.tsx      # 根布局
│   │   └── globals.css     # 全局样式（深空主题）
│   ├── components/         # 游戏组件
│   │   ├── ui/             # Shadcn UI 组件库
│   │   ├── GeneEditor.tsx  # 基因编辑器组件
│   │   ├── PlanetSimulation.tsx # 星球环境模拟组件
│   │   └── PlantGrowth.tsx # 植物生长区域组件
│   ├── hooks/              # 自定义 Hooks
│   ├── lib/                # 游戏逻辑与数据
│   │   ├── utils.ts        # 通用工具函数 (cn)
│   │   ├── gameData.ts     # 游戏数据定义（基因、环境、事件等）
│   │   └── gameLogic.ts    # 游戏逻辑（生存判定、进化、突变等）
│   └── server.ts           # 自定义服务端入口
├── next.config.ts          # Next.js 配置
├── package.json            # 项目依赖管理
└── tsconfig.json           # TypeScript 配置
```

- 项目文件（如 app 目录、pages 目录、components 等）默认初始化到 `src/` 目录下。

## 包管理规范

**仅允许使用 pnpm** 作为包管理器，**严禁使用 npm 或 yarn**。
**常用命令**：
- 安装依赖：`pnpm add <package>`
- 安装开发依赖：`pnpm add -D <package>`
- 安装所有依赖：`pnpm install`
- 移除依赖：`pnpm remove <package>`

## 开发规范

- **项目理解加速**：初始可以依赖项目下`package.json`文件理解项目类型，如果没有或无法理解退化成阅读其他文件。
- **Hydration 错误预防**：严禁在 JSX 渲染逻辑中直接使用 typeof window、Date.now()、Math.random() 等动态数据。必须使用 'use client' 并配合 useEffect + useState 确保动态内容仅在客户端挂载后渲染；同时严禁非法 HTML 嵌套（如 <p> 嵌套 <div>）。

## UI 设计与组件规范 (UI & Styling Standards)

- 模板默认预装核心组件库 `shadcn/ui`，位于`src/components/ui/`目录下
- Next.js 项目**必须默认**采用 shadcn/ui 组件、风格和规范，**除非用户指定用其他的组件和规范。**

## 游戏核心逻辑

### 基因系统
- **基因类型**：普通(common)、稀有(rare)、传说(legendary)
- **基因效果**：温度耐受、辐射抗性、水分需求、生长速度、寿命、发光、繁殖等
- **基因组合**：玩家可选择最多4个基因组合

### 环境系统
- **环境参数**：温度、辐射、水分、大气密度、阳光强度
- **环境事件**：太阳耀斑、沙尘暴、冰河时期、流星雨、酸雨等
- **环境恢复**：事件结束后环境会自然恢复

### 植物状态
- **生命阶段**：萌芽(🌱) → 幼苗(🌿) → 成长(🌳) → 成熟(🌲) → 繁盛(🌴)
- **生存状态**：繁荣(thriving)、生长中(growing)、挣扎(struggling)、濒死(dying)、死亡(dead)
- **适应性判定**：根据基因组效果和环境参数计算适应性分数，决定植物生死

### 游戏流程
1. 选择基因片段
2. 种植植物
3. 开始游戏（时间推进）
4. 观察植物状态变化
5. 触发环境事件增加挑战
6. 植物死亡则游戏结束



