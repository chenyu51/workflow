# Growth Workflow (Growth OS v2)

长期运行的个人成长系统，完全基于 GitHub Issues + Actions，按北京时间运转，每天只需 3-5 分钟即可完成记录。

## 核心功能
- **自动 Daily（工作日 09:00 北京时间）**：标题 `YYYY-MM-DD Daily`，基础三问+轮换训练模块（BASE / THINKING / RADAR / VALUE），每日练习不同侧重点。
- **自动 Weekly（周五 18:00 北京时间）**：标题 `YYYY-W## Weekly`，按 ISO 周序记录周复盘与价值总结。
- **训练模块轮换**：以北京时间日期为种子，4 个模块循环：
  - BASE：基础三问 + 情绪能量
  - THINKING：14+ 天结构化思考题库，要求 5 句话内输出
  - RADAR：资讯雷达（AI/政策/全球/国内）+ 生意/职业随机样本
  - VALUE：价值提炼，提供多个视角与一句话模板
- **题库内置**：不依赖外部 API，数据存放在 `.github/data/*.json`。
- **防重复**：若同标题的 open issue 已存在则跳过创建。

## 使用步骤
1. **启用 Actions 权限**：到 `Settings > Actions > General > Workflow permissions` 选择 **Read and write permissions**，否则无法创建 Issue。
2. **准备标签**：
   - 手动在 Issues > Labels 创建：`daily`, `weekly`, `insight`, `thinking` 以及可选的 `skill:*`, `mindset:*`, `habit:*`。
   - 或运行可选 workflow `Bootstrap labels for Growth OS v2`（在 Actions 页手动触发 `labels_bootstrap.yml`）。
3. **确认定时任务**：
   - Daily：cron `0 1 * * 1-5`（UTC），对应 **北京时间=UTC+8** 的 09:00，全年无夏令时。
   - Weekly：cron `0 10 * * 5`（UTC），对应 **北京时间=UTC+8** 的周五 18:00。
   - 如需调整本地时间，修改 workflow 内的 cron，并在注释中更新说明。
4. **手动触发**：所有 workflow 均支持 `workflow_dispatch`，可在 Actions 页面即时创建当日/当周 Issue。
5. **Issue 表单**：
   - `.github/ISSUE_TEMPLATE/daily.yml`：手动日记表单（含模块字段）。
   - `.github/ISSUE_TEMPLATE/weekly.yml`：手动周复盘表单（含新增问题）。
   - `.github/ISSUE_TEMPLATE/insight.yml`：捕获外部资讯/观察（可选）。
   - `.github/ISSUE_TEMPLATE/thinking.yml`：独立的思考练习记录（可选）。

## 文件概览
- `.github/workflows/daily_issue.yml`：自动创建 Daily Issue，按北京时间轮换训练模块。
- `.github/workflows/weekly_issue.yml`：自动创建 Weekly Issue（周五）。
- `.github/workflows/labels_bootstrap.yml`：可选，自动创建所需标签。
- `.github/data/thinking_prompts.json`：结构化思考题库。
- `.github/data/radar_topics.json`：资讯雷达主题题库。
- `.github/data/business_roles.json`：生意/职业样本题库。
- `.github/ISSUE_TEMPLATE/*.yml`：Issue Forms 模板。

## 调整 cron 示例
- 若希望 Daily 改为北京时间 08:30，需换算为 UTC（减 8 小时）得到 00:30，将 cron 调整为 `30 0 * * 1-5`，并更新 workflow 注释说明。中国不使用夏令时，全年偏移恒定。

## 提示
- 每天 3-5 分钟：回答基础三问 + 当日训练模块即可。
- 周复盘 10 分钟：回答框架、雷达与价值输出，便于周报/绩效复用。
