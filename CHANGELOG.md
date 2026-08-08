# 更新日志

所有值得注意的变更都会记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

---

## [Unreleased]

### 新增

- MIT 许可证（`LICENSE`），作者 YesonWyld
- 站点图标（favicon.ico / favicon.png）
- GitHub Pages 自动部署工作流（`.github/workflows/pages.yml`）

### 变更

- 主应用文件由 `prompt-manager.html` 重命名为 `prompt-vault.html`
- 静态资源整理至 `assets/` 目录
- 补齐剩余按钮的内联 `onclick`/`onchange` 迁移，全部事件统一使用 `addEventListener`（完成 1.2.0 声明的事件迁移）
- README 项目结构与实际文件保持一致

## [1.2.0] - 2026-06-25

### 新增

- 多工具选择支持：提示词可关联多个适用工具（`tool` 字段支持逗号/顿号分隔的多值）
- 工具快速选择器：编辑弹窗内显示已有工具 chip，点击即可切换选中
- 工具自动补全下拉框：输入工具名时显示已有工具建议
- 默认工具种子（Claude Code、豆包、Codex、Workbuddy），确保常用工具始终可选
- 标签快速选择器：编辑弹窗内显示已有标签 chip，点击即可切换选中
- 标签自动补全下拉框：输入标签名时显示已有标签建议
- 默认标签种子（方案、开发），确保常用标签始终可选
- 正文 textarea 字数/行数实时计数器
- 卡片级别删除按钮（每个卡片右上角的垃圾桶图标）

### 修复

- XSS 防护：`escHtml()` 函数增加单引号转义（`'` → `&#39;`）
- localStorage 写入异常处理：`saveData()` 包裹 try/catch，QuotaExceededError 时给出中文提示
- 自动命名逻辑修复：修改 `autoName` 判据，编辑已有提示词时不再阻止自动命名更新
- 复制功能统一：`copyToClipboard()` 重构为回调模式，消除 `execCommand` 和 Clipboard API 返回值不一致问题
- Toast 定时器从 DOM 属性迁移为模块级变量 `_toastTimer`
- 搜索输入添加 200ms 防抖，减少大量数据时的频繁重渲染
- 编辑弹窗最大宽度从 640px 调整为 720px

### 变更

- 所有事件绑定从内联 `onclick`/`oninput`/`onpaste` 迁移为 `addEventListener` + 事件委托模式
- 标签筛选栏与卡片列表事件均使用事件委托处理，消除 XSS 风险
- `formBody` 的 `oninput`/`onpaste` 改用 `addEventListener` 绑定
- 备份文件整理至 `bakup/` 目录

---

## [1.1.0] - 2026-06-07

### 新增

- 深色模式支持：通过 `prefers-color-scheme: dark` 媒体查询自动切换
- 暗色主题下的所有组件样式适配（header 毛玻璃效果、卡片、表单、toast 等）
- 拖拽 JSON 文件导入：将 `.json` 文件拖到页面任意位置即可导入
- 空状态引导页：无数据或无匹配结果时展示友好的空状态提示
- 详情面板：右侧滑出式详情视图，展示提示词完整内容和元信息
- 响应式布局：移动端（≤640px）适配，卡片网格切换为单列
- Apple 风格 UI 系统（SF Pro 字体、圆角、阴影、毛玻璃效果）

### 变更

- 主布局从列表视图重构为卡片网格（`grid-template-columns: repeat(auto-fill, minmax(290px, 1fr))`）
- UI 组件全面升级：按钮、chip、modal、toast、表单控件统一 Apple 风格
- 标签改为 chip 样式，筛选栏从简单列表改为 chip 行
- 搜索框置于顶部 header 中，与导入/导出/新建按钮同行

---

## [1.0.0] - 2026-06-01

### 新增

- PromptVault 初始版本发布
- 核心 CRUD 功能：新建、编辑、删除、查看提示词
- localStorage 数据持久化（`promptvault_data` key）
- 基本卡片列表视图
- 标签筛选功能
- 全文搜索（名称、正文、标签）
- JSON 导入/导出功能
- 自动命名：从正文首行提取名称（前 50 字符）
- 单一工具选择（每提示词一个工具）
- 基本深色/浅色 CSS 变量体系
- 响应式卡片网格基础布局
- Toast 提示消息组件
- Modal 编辑弹窗
