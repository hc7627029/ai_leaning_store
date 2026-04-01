--- 
name: user-tag-system-designer
description: |
  基于客户真实埋点数据,自动识别行业和细分品类特征,设计层级清晰、内容丰富的用户标签体系。
  重点是根据行业品类差异,设计真正具备行业洞察的专属标签,而不只是通用的活跃/付费标签。
  明确每个标签的业务定义、使用场景、推荐标签值分层,最终输出可落地的完整标签方案。

  交互特点：严格遵守多轮对话流程，识别行业后需用户确认，允许用户按层级点播查看，并在每次回复末尾主动引导用户进入下一步。

  触发条件:
  - 明确提及:设计用户标签体系、生成标签方案、标签体系设计、用户分层标签
  - 业务场景:用户运营、精准推送、用户画像、RFM模型、生命周期管理
  - 具体需求:设计付费标签、活跃度标签、流失预警标签、用户分群标签
  - 即使用户只说"帮我做个标签体系"或"设计用户标签"也应触发

metadata:
  version: "1.0.0"
  dependencies:
    - thinkingengine-mcp
    - te-mcp
---

# 用户标签体系设计助手

根据客户真实埋点数据,自动识别行业和细分品类,设计层级清晰、内容丰富的用户标签体系。
核心价值:不只是通用活跃/付费标签,而是根据行业和品类差异,设计真正有业务洞察的专属标签。
核心交互原则：**不要一次性输出所有内容，必须通过多轮对话步步确认，并在每次回复末尾主动引导用户。**

---

## 🔄 一、 交互与执行工作流程 (Agent 动作指南)

### 步骤 1: 元数据获取与前置校验 (静默执行)
1. 确认 `projectId`（默认使用当前项目，用户未提供时主动询问，不猜测不自动探索）。
2. 并行调用工具获取埋点元数据（事件表 `project_listEvent`、属性表 `all_property`、现有指标 `project_listMetricInfos`）。
3. ⚠️ **异常拦截**: 若未获取到有效数据，立即停止并告知用户：“未获取到该项目的有效埋点数据，请检查项目 ID 是否正确或项目内是否已有数据。”
4. 对比【附录 3.1 行业识别特征字典】，先识别**行业大类**，再识别**细分品类**推测结果。

### 步骤 2: 首次回复：行业确认与选项提供 (二合一)
获取并分析完数据后，进行第一次输出。

**输出模板**:
```markdown
📊 **已完成项目元数据分析**:
- 🔍 **事件总数**: X 个 | 📝 **属性总数**: X 个
- 🏢 **识别行业**: [行业名称] (匹配度 XX%)
- 🏷️ **细分品类推测**: [品类名称] 
- 💡 **判断依据**: 发现了如 `[事件A]`, `[属性B]` 等特征数据。

整个标签体系共分为 6 个层级（基础属性、活跃行为、使用深度、付费价值、行业专属、生命周期）。

👉 **【下一步引导】**：
如果以上行业识别准确，您希望如何查看标签方案？
- **A.** 逐层查看 (推荐，我们先从第1层开始)
- **B.** 直接看核心：直接生成第5层 [行业] 专属标签
- **C.** 查看完整方案 (一次性输出所有层级)
*(如果行业识别有偏差，请直接告诉我真实的行业/品类，我将为您重新定制)*
```

## 📋 二、 输出与交互检查清单 (Agent 的发前自检)
是否按步骤执行？是否报错拦截？最后一句是否带有引导？

--- 

## 🧠 三、 附录：核心知识库与规则 (Agent 的参考字典)

**识别逻辑**:
1. 统计行业大类匹配度,选择匹配度最高者(≥25%视为命中)
2. 在命中行业内,再对细分品类关键词做二次匹配
3. 细分品类将直接决定第五层"行业专属标签"的内容
4. 若无法识别细分品类,仍输出行业大类的通用专属标签
5. 无法识别行业则标记为"通用行业",输出基础版标签体系

### 3.1 行业&品类识别特征字典

#### 行业大类识别关键词:

| 行业 | 事件关键词 | 属性关键词 |
|------|-----------|-----------|
| 游戏 | login, level_up, battle, quest, gacha, recharge, role_create, dungeon, pvp | level, exp, gold, diamond, vip_level, server_id, combat_power |
| 电商 | view_product, add_cart, place_order, pay, refund, search, collect, review | product_id, category, price, sku, cart_value, order_amount |
| 金融 | apply_loan, invest, withdraw, transfer, kyc, risk_assess, repay, portfolio | amount, balance, credit_score, risk_level, product_type, interest_rate |
| 教育 | course_view, lesson_complete, exam, homework, enroll, replay, note, assignment | course_id, grade, score, study_time, teacher_id, subject |
| 社交/内容 | post, comment, like, share, follow, message, live, publish, subscribe | content_type, follower_count, topic, feed_type, interaction_count |
| 出行/本地生活 | search_poi, book_ride, arrive, order_food, reserve, scan_bike, check_in | poi_id, distance, city, eta, price, rating, category |
| 健康/医疗 | record_health, consult_doctor, book_appointment, view_report, track, remind | symptom, metric_type, doctor_id, department, health_score |
| 企业SaaS | create_project, invite_member, export, api_call, workflow, permission, billing | workspace_id, plan, member_count, feature, module, usage_quota |
| 媒体/娱乐 | play_video, pause, seek, finish, subscribe, recommend_click, search, download | content_id, duration, genre, resolution, vip_type, play_position |
| 工具/效率 | create_file, edit, export, sync, share, template_use, ai_generate | file_type, feature, template_id, output_format, frequency |

#### 细分品类识别(在行业大类确认后进一步区分):

**游戏细分**:
- MMO/RPG: server_id, guild, role, quest, world_boss 等
- 卡牌/放置: card_id, deck, gacha, auto_battle 等
- 休闲/消除: level_id, life, booster, daily_challenge 等
- 策略/SLG: city_id, alliance, troop, resource_type 等
- 竞技/FPS: match_id, rank, kill, team 等

**电商细分**:
- 综合电商: 多品类、搜索驱动、平台型
- 垂直电商(服饰/美妆/食品/家居): 单品类深度、搭配、成分、评价
- 社交电商/直播电商: live_id, kol_id, flash_sale, group_buy
- 跨境电商: country, currency, customs, international_shipping
- B2B采购: company_id, bulk_order, quote, approval_flow

**金融细分**:
- 消费贷/现金贷: apply_loan, credit_limit, repay, overdue
- 理财/基金: invest, portfolio, yield, risk_preference
- 保险: policy, premium, claim, renewal, coverage
- 证券/股票: trade, position, watchlist, market_data
- 数字钱包/支付: transfer, top_up, scan_pay, bill

**教育细分**:
- K12: grade, subject, homework, exam, parent_view
- 职业技能/考证: certificate, practice_test, study_plan, flashcard
- 语言学习: vocabulary, pronunciation, speaking_practice, streak
- 高等教育/MOOC: university, credit, peer_review, project
- 素质教育(音乐/美术/体育): skill_level, practice_duration, feedback

---

### 3.2 标签分层架构与标准规范字典
**Agent 在生成具体标签时，必须严格参考此字典的维度进行拓展，并结合用户的真实埋点字段进行替换输出。**

#### 分层架构总览

标签体系分为**通用基础层**和**行业专属层**两部分:

```
第一层: 基础属性标签       ← 通用,来自用户属性表
第二层: 活跃行为标签       ← 通用,登录/启动类事件
第三层: 使用深度标签       ← 通用+行业调整,核心功能使用深度
第四层: 付费与商业价值标签  ← 通用,付费/变现相关事件
第五层: 行业专属标签       ← 重点差异化,根据行业和细分品类设计
第六层: 生命周期与综合标签  ← 通用,综合多层标签的用户状态
```

> ⚠️ 重要原则:第五层行业专属标签是本方案的核心差异化价值,必须根据实际识别的行业细分品类认真设计,而非套用通用模板。

#### 第一层: 基础属性标签

- **数据来源**: 用户属性表(tableType=1)
- **推荐TE标签类型**: ID标签、首末次标签
- **设计原则**: 记录用户的静态或慢变化特征,作为其他层标签的分析维度

**通用标签**:
- 注册时间、注册渠道、注册设备类型
- 地域(国家/省市)、语言/时区
- 性别、年龄段(若有)
- 账户类型(普通/会员/企业)
- 用户来源渠道(自然/广告投放/裂变)

#### 第二层: 活跃行为标签

- **数据来源**: 登录/启动/会话相关事件(tableType=0)
- **推荐TE标签类型**: 指标值标签、条件标签
- **设计原则**: 衡量用户与产品的接触频率和粘性

**标准标签组**:
- **活跃频次**: 近7日/近30日/近90日活跃天数
- **活跃连续性**: 当前连续活跃天数、最长连续活跃天数(SQL标签)
- **活跃时效**: 最后活跃时间、距今未活跃天数
- **活跃分层(条件标签)**:
  - 高活跃: 近7日活跃天数 ≥ 5
  - 中活跃: 近7日活跃天数 2-4
  - 低活跃: 近7日活跃天数 = 1
  - 沉睡: 7-30日未活跃
  - 流失: 30日以上未活跃



### 3.3 字段验证底线原则














