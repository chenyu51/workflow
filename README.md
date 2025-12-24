# Growth Workflow (Growth OS v2)

长期运行的个人成长系统，完全基于 GitHub Issues + Actions，按北京时间运转，每天只需 3-5 分钟即可完成记录。新增“Growth OS + 米尔顿语言模式学习系统（最终版）”，面向真实沟通训练，而非“催眠他人”。

## 核心功能
- **自动 Daily（工作日 09:00 北京时间）**：标题 `YYYY-MM-DD Daily`，基础三问+轮换训练模块（BASE / THINKING / RADAR / VALUE），每日练习不同侧重点，并附带“米尔顿语言微练习”区块。
- **自动 Weekly（周五 18:00 北京时间）**：标题 `YYYY-W## Weekly`，按 ISO 周序记录周复盘与价值总结，自动插入“米尔顿语言复盘”与可直接复制给 ChatGPT 的 Prompt。
- **米尔顿语言模式学习**：
  - 不按术语背诵，而是围绕三类能力：信息留白与抽象（A）、注意力引导与跟导（B）、意义与价值建构（C）。
  - 14 天游程的日常微练习，每天只额外多花 2-3 分钟，直接嵌入真实沟通。
  - Daily Issue 编辑后会自动根据你填写的真实场景/目标，从 `scenes.json` 匹配母类场景，并推荐主力/备选模式，生成“原句→改写”练习与风险提醒。
  - Weekly Issue 汇总本周 Daily 链接，附带 ChatGPT 复盘提示词，ChatGPT 负责点评、复盘与价值提炼（需要手动复制 Prompt）。
- **训练模块轮换**：以北京时间日期为种子，4 个模块循环：
  - BASE：基础三问 + 情绪能量
  - THINKING：14+ 天结构化思考题库，要求 5 句话内输出
  - RADAR：资讯雷达（AI/政策/全球/国内）+ 生意/职业随机样本
  - VALUE：价值提炼，提供多个视角与一句话模板
- **题库内置**：不依赖外部 API，数据存放在 `.github/data/*.json`。
- **防重复**：若同标题的 open issue 已存在则跳过创建。

### 米尔顿学习材料
- `.github/data/milton/patterns.json`：20+ 个模式卡，涵盖描述、使用建议、示例与风险。
- `.github/data/milton/drills_14d.json`：14 天游程，默认循环。
- `.github/data/milton/scenes.json`：真实沟通场景母类库，匹配信号+推荐模式，可手动扩展。
- `.github/data/milton/prompts.json`：ChatGPT 复盘提示词（每日/每周）。

## 使用步骤
1. **启用 Actions 权限**：到 `Settings > Actions > General > Workflow permissions` 选择 **Read and write permissions**，否则无法创建 Issue。
2. **准备标签**：
   - 手动在 Issues > Labels 创建：`daily`, `weekly`, `insight`, `thinking` 以及可选的 `skill:*`, `mindset:*`, `habit:*`。
   - 或运行可选 workflow `Bootstrap labels for Growth OS v2`（在 Actions 页手动触发 `labels_bootstrap.yml`）。
3. **确认定时任务**：
   - Daily：cron `0 1 * * 1-5`（UTC），对应 **北京时间=UTC+8** 的 09:00，全年无夏令时。
   - Weekly：cron `0 10 * * 5`（UTC），对应 **北京时间=UTC+8** 的周五 18:00。
   - GitHub Actions 只接受 UTC，需要人工换算并在注释中标明；北京没有夏令时。
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

## 米尔顿语言练习说明
- **不是催眠他人**：训练的是沟通与意义建构，让表达自然、低阻力。
- **场景自由输入**：Daily 中的“真实沟通场景/想达成的效果”完全自定义，越具体越好。
- **GitHub 负责结构**：自动生成日/周 Issue、匹配场景、推送练习框架。
- **ChatGPT 负责点评**：周复盘和每日反馈 Prompt 已在 `prompts.json`，需要时手动复制给 ChatGPT 获取点评。
- **扩展场景库**：
  1. 编辑 `.github/data/milton/scenes.json`，新增对象需包含 id/name/aliases/signals/recommended_pattern_ids；
  2. `signals` 用关键词数组，越贴合你常见场景越好；
  3. `recommended_pattern_ids` 使用 `patterns.json` 中的 id，顺序代表优先级；
  4. 保存后下次 Daily 编辑时会自动使用新的匹配逻辑。

## 调整 cron 示例
- 若希望 Daily 改为北京时间 08:30，需换算为 UTC（减 8 小时）得到 00:30，将 cron 调整为 `30 0 * * 1-5`，并更新 workflow 注释说明。中国不使用夏令时，全年偏移恒定。

## 提示
- 每天 3-5 分钟：回答基础三问 + 当日训练模块即可。
- 周复盘 10 分钟：回答框架、雷达与价值输出，便于周报/绩效复用。
