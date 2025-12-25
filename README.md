# Growth Workflow

基于 GitHub Actions 的自动化成长/练习系统（北京时间）。工作日每天自动生成两类 Issue，并同步写入仓库 Markdown 日志，所有内容均在仓库内留痕，可随时自查与回顾。

## 每日自动生成（周一至周五，Asia/Shanghai）
- **10:00 Milton Practice**（Issue + `journal/milton/YYYY-MM-DD-milton-practice.md`）
  - 14 天循环训练节奏，自动选取今日模式、任务与自检要点。
  - Issue 自动带上 `milton`、`practice` 标签，并附仓库内 Markdown 链接（主要填写在 md）。
- **19:00 Growth Daily**（Issue + `journal/daily/YYYY-MM-DD-daily.md`）
  - 轮换模块：BASE / THINKING / RADAR / VALUE，RADAR 使用内置题库与角色样本。
  - Issue 自动带上 `daily` 标签，并附仓库内 Markdown 链接（主要填写在 md）。

> GitHub cron 使用 UTC：`0 2 * * 1-5` = 北京时间 10:00；`0 11 * * 1-5` = 北京时间 19:00（全年无夏令时）。

## 仓库内置数据
- `.github/data/milton/patterns.json`：20+ 米尔顿模式卡（含描述/Do&Dont/示例/风险）。
- `.github/data/milton/drills_14d.json`：14 天游程，循环选取今日模式与任务。
- `.github/data/milton/scenes.json`：真实沟通场景母类库，可自定义扩展。
- `.github/data/milton/prompts.json`：每日/每周复盘 Prompt。
- `.github/data/radar_topics.json`：30+ RADAR 资讯题目。
- `.github/data/business_roles.json`：50+ 业务/职业角色样本。

## Markdown 填写规则与示例
- **Milton**：`journal/milton/YYYY-MM-DD-milton-practice.md`
  - 先展示“今日模式/任务/自检”，再给真实沟通与改写区块。
  - Issue 中会附上对应链接，例如：`https://github.com/<owner>/<repo>/blob/main/journal/milton/2024-12-31-milton-practice.md`。
- **Growth Daily**：`journal/daily/YYYY-MM-DD-daily.md`
  - 先写三问，再写“今日模块”提示（轮换）。
  - Issue 中会附上对应链接，例如：`https://github.com/<owner>/<repo>/blob/main/journal/daily/2024-12-31-daily.md`。

## 工作流说明
- `.github/workflows/milton_practice_10am.yml`：10:00 BJT 自动创建 Milton Practice Issue + md，幂等防重（Issue 标题重复直接跳过，md 已存在不覆盖）。
- `.github/workflows/growth_daily_7pm.yml`：19:00 BJT 自动创建 Growth Daily Issue + md，幂等防重（Issue 标题重复直接跳过，md 已存在不覆盖）。
- `.github/workflows/labels_bootstrap.yml`：手动触发，自动创建 `daily`、`weekly`、`milton`、`practice` 标签。

## 使用指南
1. **开启 Actions 写权限**：`Settings > Actions > General > Workflow permissions` 选择 **Read and write permissions**。
2. **初始化标签**：如仓库尚无必需标签，在 Actions 页面手动运行 `Bootstrap labels` 工作流。
3. **立即验证**：可在 Actions 页对 `Milton Practice Daily (BJT 10:00)` 或 `Growth Daily (BJT 19:00)` 选择 `Run workflow` 进行当日生成。
4. **填写位置**：Issue 仅作入口/索引，请在对应的 Markdown 文件中完成主要内容。

## 幂等与安全
- 若同标题的 open Issue 已存在，工作流自动跳过创建。
- 若对应日期的 Markdown 已存在，保留原文件不覆盖，但 Issue 仍按防重复逻辑处理。
- 完全使用仓库内置数据与默认 `GITHUB_TOKEN`，不依赖外部 API/Secrets。
