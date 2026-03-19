---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 304402201f35446709c4ef9d566af44235ce1025474525fdaa0e41f23cef5e018ab257b602203077b15c7a9abc2c11f7b2eb3113c5df0565e6f349f6f6aaf762a867b486d26a
    ReservedCode2: 304502205edf16e5dae90f98a341be0da9624721faafd2c2a304c8b282d75cfd28fd53da022100c3bc124a50ec82706ecf1a7742dfac32d124bd12c693a35e890d3a4734186631
---

# 项目概览 · 求职助手

> AI 驱动简历分析 + 猎聘职位列表 求职工具

---

## 项目信息

| 项目名 | 求职助手 |
|--------|----------|
| 版本 | v2.0 |
| 技术栈 | 纯前端（HTML + CSS + JS，无框架） |
| 部署方式 | GitHub Pages |
| GitHub 仓库 | `gqload@126.com/job-assistant` |
| 访问地址 | `https://[用户名].github.io/job-assistant/` |

---

## 页面架构

```
/
├── index.html          # 首页（职位列表，同 jobs.html）
├── jobs.html          # 职位列表页
│   └── 数据来源：liepin_job_list.csv（101条猎聘数据）
└── analyze.html       # 简历分析页
    ├── PDF 简历上传 → Coze API 分析
    └── 岗位匹配度分析
```

---

## 核心功能

### 功能一：职位列表浏览
- 展示 101 条猎聘真实职位数据
- 按匹配度由高到低排序
- 显示城市、薪资、公司名、岗位名、匹配度分
- 点击卡片跳转分析报告

### 功能二：简历上传与 AI 分析
- 支持 PDF、DOCX、DOC 格式简历上传
- 解析简历文本内容
- 调用 Coze API 对简历+岗位进行多维度分析
- 输出：综合匹配分 + 6项维度评分 + 改进建议 + 面试题

---

## 数据流

```
用户上传简历 (PDF/DOCX)
    ↓
JS 解析文件文本
    ↓
encodeURIComponent(JSON.stringify(job))
    ↓
?job=xxx 参数跳转 analyze.html
    ↓
analyze.html 读取 URL 参数
    ↓
提取岗位数据（公司/职位/描述/薪资）
    ↓
调用 Coze API: /v3/chat
    ↓
轮询 /v3/chat/retrieve + /v3/chat/message/list
    ↓
渲染分析结果（评分卡 + 维度雷达 + 建议 + 面试题）
```

---

## 已知限制与风险

| 风险 | 说明 | 建议 |
|------|------|------|
| Coze PAT Token 暴露 | Token 嵌在 JS 里，GitHub 公开后可被查看 | 可接受自用；公开分享需加后端保护 |
| 简历解析精度 | 前端纯 JS 解析 PDF/DOCX，大文件可能有兼容问题 | 建议 PDF 优先，文件 < 5MB |
| API 频率限制 | Coze API 有日调用限额 | 每天 < 100 次访问可满足 |

---

## 目录结构（待创建）

```
job-assistant/
├── index.html          # 职位列表
├── jobs.html           # 职位列表（别名）
├── analyze.html        # 简历分析页
├── assets/             # 静态资源（备用）
└── README.md
```
