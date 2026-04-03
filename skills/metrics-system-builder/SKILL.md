---
name: metrics-system-builder
description: |
  帮助新项目从零开始快速搭建核心指标体系。根据游戏类型和商业模式，基于AARRR海盗模型自动生成分层指标体系；标注每个指标所需的事件和属性，识别当前可算/需补埋点的指标。

  触发条件：
  - 搭建指标体系、设计指标体系、指标体系规划
  - 新项目指标设计、核心指标梳理
  - AARRR模型、海盗模型指标
  - 埋点规划、埋点设计、事件设计
  - 游戏数据分析指标、运营指标体系

  支持的游戏类型：MMO、SLG、IAA、休闲游戏、中重度游戏、社交游戏、区块链游戏
  支持的商业模式：IAP(内购)、IAA(广告)、混合变现、订阅制
---

# 指标体系搭建助手

## 使用方式

```
/metrics-system-builder [游戏类型] [商业模式] [项目阶段]
```

**参数说明：**
- 游戏类型：MMO | SLG | IAA | 休闲 | 中重度 | 社交 | 链游
- 商业模式：IAP | IAA | 混合 | 订阅
- 项目阶段：研发期 | 测试期 | 公测期 | 稳定运营期

**示例：**
```
/metrics-system-builder SLG IAP 测试期
/metrics-system-builder IAA IAA 公测期
/metrics-system-builder MMO 混合 稳定运营期
```

---

## 核心框架：AARRR分层指标体系

### 一、Acquisition（获取用户）

#### 1.1 通用指标（所有游戏类型）

| 指标名称 | 计算公式 | 所需事件 | 所需属性 | 说明 |
|---------|---------|---------|---------|------|
| **新增用户数(DNU)** | COUNT(DISTINCT user_id) WHERE is_new_user = true | `app_install` | `user_id`, `channel`, `campaign`, `creative`, `device_type`, `os_version`, `country` | 每日新增用户绝对值 |
| **新增用户占比** | DNU / DAU | `app_install`, `app_launch` | 同上 | 衡量新用户流入速度 |
| **渠道新增用户数** | COUNT(DISTINCT user_id) WHERE channel = 'xxx' | `app_install` | `channel`, `campaign` | 分渠道统计新增 |
| **渠道CPA** | 渠道投放成本 / 渠道DNU | `app_install` + 成本数据 | `channel`, `cost` | 渠道获客成本 |
| **自然新增占比** | 自然新增DNU / 总DNU | `app_install` | `channel` (自然渠道标记) | 自然流量健康度 |
| **K因子(病毒系数)** | (总新增 - 付费新增) / 付费新增 | `app_install` | `channel`, `is_organic` | 用户传播能力 |

#### 1.2 IAA游戏特有指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **eCPM** | (广告收入 / 广告展示次数) × 1000 | `ad_impression` | `ad_type`, `revenue` |
| **填充率** | 广告展示次数 / 广告请求次数 | `ad_request`, `ad_impression` | `ad_type`, `ad_network` |
| **展示率** | 广告展示次数 / 广告填充次数 | `ad_impression`, `ad_fill` | `ad_type` |
| **归因ROI** | LTV / CPA | `app_install`, 付费事件 | `channel`, `revenue` |

#### 1.3 SLG游戏特有指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **有效新增用户** | 新增用户中完成核心教程的用户数 | `app_install`, `tutorial_complete` | `user_id`, `tutorial_id` |
| **新增用户首日留存** | 新增用户次日回访比例 | `app_install`, `app_launch` | `user_id`, `install_date` |

---

### 二、Activation（激活用户）

#### 2.1 通用指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 | 说明 |
|---------|---------|---------|---------|------|
| **DAU** | COUNT(DISTINCT user_id) WHERE date = today | `app_launch` | `user_id`, `login_time` | 日活跃用户数 |
| **WAU** | COUNT(DISTINCT user_id) WHERE week = current_week | `app_launch` | `user_id` | 周活跃用户数 |
| **MAU** | COUNT(DISTINCT user_id) WHERE month = current_month | `app_launch` | `user_id` | 月活跃用户数 |
| **DAU/MAU** | DAU / MAU | `app_launch` | `user_id` | 用户粘性指标 |
| **平均在线时长** | SUM(在线时长) / DAU | `session_start`, `session_end` | `user_id`, `duration` | 用户参与度 |
| **人均会话次数** | COUNT(session) / DAU | `session_start` | `user_id`, `session_id` | 用户活跃频次 |
| **核心功能渗透率** | 使用核心功能用户数 / DAU | `feature_use` | `user_id`, `feature_name` | 核心玩法参与度 |

#### 2.2 MMO游戏特有指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **角色创建率** | 创建角色用户数 / 新增用户数 | `app_install`, `character_create` | `user_id`, `character_id` |
| **首日等级分布** | 新用户首日达到等级分布 | `level_up` | `user_id`, `level`, `is_new_user` |
| **核心副本参与率** | 参与核心副本用户数 / DAU | `dungeon_enter` | `user_id`, `dungeon_id`, `dungeon_type` |
| **公会加入率** | 加入公会用户数 / DAU | `guild_join` | `user_id`, `guild_id` |
| **社交互动率** | 有社交行为用户数 / DAU | `chat_send`, `friend_add`, `trade` | `user_id`, `action_type` |

#### 2.3 SLG游戏特有指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **新手引导完成率** | 完成新手引导用户数 / 新增用户数 | `tutorial_start`, `tutorial_complete` | `user_id`, `tutorial_id`, `step_id` |
| **新手引导各步流失率** | 各步骤流失用户数 / 进入该步骤用户数 | `tutorial_step` | `user_id`, `step_id` |
| **大本营等级分布** | 用户大本营等级分布 | `base_upgrade` | `user_id`, `base_level` |
| **PVP参与率** | 参与PVP用户数 / DAU | `pvp_battle` | `user_id`, `battle_type` |
| **联盟加入率** | 加入联盟用户数 / DAU | `alliance_join` | `user_id`, `alliance_id` |

#### 2.4 社交游戏特有指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **好友添加率** | 添加好友用户数 / DAU | `friend_add` | `user_id`, `friend_id` |
| **人均好友数** | SUM(好友数) / DAU | `friend_add`, `friend_remove` | `user_id` |
| **消息发送率** | 发送消息用户数 / DAU | `message_send` | `user_id`, `message_type` |
| **社交互动深度** | 有N次以上社交互动用户数 / DAU | `social_interact` | `user_id`, `interact_count` |

---

### 三、Retention（留存用户）

#### 3.1 通用留存指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 | 说明 |
|---------|---------|---------|---------|------|
| **次日留存率** | 次日回访用户数 / 新增用户数 | `app_install`, `app_launch` | `user_id`, `install_date` | 核心留存指标 |
| **3日留存率** | 第3日回访用户数 / 新增用户数 | `app_install`, `app_launch` | `user_id`, `install_date` | 短期留存 |
| **7日留存率** | 第7日回访用户数 / 新增用户数 | `app_install`, `app_launch` | `user_id`, `install_date` | 中期留存 |
| **30日留存率** | 第30日回访用户数 / 新增用户数 | `app_install`, `app_launch` | `user_id`, `install_date` | 长期留存 |
| **留存曲线衰减率** | (N日留存 - N+1日留存) / N日留存 | `app_launch` | `user_id`, `install_date` | 留存健康度 |
| **分渠道留存率** | 分渠道统计留存 | `app_install`, `app_launch` | `user_id`, `channel` | 渠道质量评估 |

#### 3.2 分层留存指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **付费用户留存率** | 付费用户次日回访比例 | `purchase`, `app_launch` | `user_id`, `is_payer` |
| **高活跃用户留存率** | 高活跃用户留存比例 | `app_launch` | `user_id`, `active_level` |
| **核心玩法用户留存** | 参与核心玩法用户留存 | `core_gameplay`, `app_launch` | `user_id`, `gameplay_type` |

#### 3.3 SLG游戏留存指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **保护期留存率** | 新手保护期内留存 | `app_launch`, `protection_expire` | `user_id`, `protection_status` |
| **首周关键节点留存** | 达到关键节点用户留存 | `milestone_reach`, `app_launch` | `user_id`, `milestone_id` |

---

### 四、Revenue（获取收入）

#### 4.1 通用收入指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 | 说明 |
|---------|---------|---------|---------|------|
| **总收入(GMV)** | SUM(revenue) | `purchase` | `user_id`, `revenue`, `currency` | 总交易金额 |
| **日收入(DRU)** | SUM(revenue) WHERE date = today | `purchase` | `user_id`, `revenue` | 日收入 |
| **付费用户数(DPU)** | COUNT(DISTINCT user_id) WHERE has_purchase = true | `purchase` | `user_id` | 日付费用户数 |
| **付费率** | DPU / DAU | `purchase`, `app_launch` | `user_id` | 付费转化率 |
| **ARPU** | 日收入 / DAU | `purchase`, `app_launch` | `user_id`, `revenue` | 平均用户收入 |
| **ARPPU** | 日收入 / DPU | `purchase` | `user_id`, `revenue` | 付费用户平均收入 |
| **首次付费时间** | AVG(首次付费时间 - 安装时间) | `app_install`, `first_purchase` | `user_id`, `install_time`, `purchase_time` | 付费转化速度 |

#### 4.2 LTV指标体系

| 指标名称 | 计算公式 | 所需事件 | 所需属性 | 说明 |
|---------|---------|---------|---------|------|
| **LTV-N** | N日内累计收入 / N日前新增用户数 | `purchase`, `app_install` | `user_id`, `revenue`, `install_date` | N日生命周期价值 |
| **LTV90** | 90日LTV | `purchase`, `app_install` | `user_id`, `revenue`, `install_date` | 核心LTV指标 |
| **LTV/CAC** | LTV / CAC | `purchase`, `app_install` + 成本数据 | `channel`, `cost`, `revenue` | 回本周期评估 |
| **回本周期** | 首次达到LTV ≥ CPA的天数 | `purchase`, `app_install` | `user_id`, `revenue`, `channel` | 投放回本评估 |

#### 4.3 IAA游戏收入指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **广告收入** | SUM(ad_revenue) | `ad_impression` | `user_id`, `ad_revenue`, `ad_type` |
| **人均广告展示次数** | 广告展示次数 / DAU | `ad_impression` | `user_id` |
| **广告ARPU** | 广告收入 / DAU | `ad_impression` | `user_id`, `ad_revenue` |
| **激励视频完成率** | 激励视频完成次数 / 激励视频开始次数 | `ad_start`, `ad_complete` | `user_id`, `ad_type = 'rewarded'` |
| **插屏广告点击率** | 插屏点击次数 / 插屏展示次数 | `ad_impression`, `ad_click` | `user_id`, `ad_type = 'interstitial'` |

#### 4.4 付费深度指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **付费档位分布** | 各档位付费用户数分布 | `purchase` | `user_id`, `amount`, `sku_id` |
| **二次付费率** | 二次付费用户数 / 首次付费用户数 | `purchase` | `user_id`, `purchase_count` |
| **付费频次** | AVG(付费次数) | `purchase` | `user_id`, `purchase_count` |
| **大R识别阈值** | 累计付费 > N元的用户 | `purchase` | `user_id`, `total_revenue` |

---

### 五、Referral（传播推荐）

#### 5.1 传播指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 | 说明 |
|---------|---------|---------|---------|------|
| **分享率** | 分享用户数 / DAU | `share` | `user_id`, `share_type`, `share_channel` | 用户分享意愿 |
| **分享转化率** | 通过分享注册用户数 / 分享次数 | `share`, `app_install` | `user_id`, `invite_code` | 分享效果 |
| **邀请成功率** | 成功邀请用户数 / 发出邀请数 | `invite_send`, `invite_success` | `user_id`, `invite_id` | 邀请转化效果 |
| **K因子** | 平均每个用户带来的新用户数 | `app_install` | `user_id`, `referrer_id` | 病毒传播系数 |

#### 5.2 社交裂变指标

| 指标名称 | 计算公式 | 所需事件 | 所需属性 |
|---------|---------|---------|---------|
| **裂变层级** | 用户传播链平均深度 | `app_install` | `user_id`, `referrer_id`, `referrer_level` |
| **裂变系数** | 各层级新增用户数 / 上一层级用户数 | `app_install` | `user_id`, `referrer_level` |

---

## 游戏类型指标模板

### MMO游戏指标体系

```
核心关注指标：
├── 获取层
│   ├── 新增用户数(DNU)
│   ├── 渠道CPA
│   └── 自然新增占比
├── 激活层
│   ├── DAU/MAU (粘性)
│   ├── 核心副本参与率
│   ├── 公会加入率
│   └── 社交互动率
├── 留存层
│   ├── 次日留存率
│   ├── 7日留存率
│   └── 30日留存率
├── 收入层
│   ├── ARPU
│   ├── 付费率
│   ├── LTV90
│   └── 付费档位分布
└── 传播层
    ├── 分享率
    └── K因子

关键埋点事件：
- character_create: 角色创建
- level_up: 升级
- dungeon_enter/complete: 副本进入/完成
- guild_join/create: 公会加入/创建
- pvp_battle: PVP战斗
- trade: 交易
- chat_send: 聊天
```

### SLG游戏指标体系

```
核心关注指标：
├── 获取层
│   ├── 有效新增用户(过教程)
│   ├── 渠道CPA
│   └── 新增用户首日留存
├── 激活层
│   ├── 新手引导完成率
│   ├── 大本营等级分布
│   ├── PVP参与率
│   └── 联盟加入率
├── 留存层
│   ├── 次日留存率
│   ├── 保护期留存率
│   └── 首周关键节点留存
├── 收入层
│   ├── ARPU
│   ├── LTV/CAC
│   ├── 回本周期
│   └── 付费档位分布
└── 传播层
    ├── 联盟邀请率
    └── 联盟邀请转化率

关键埋点事件：
- tutorial_start/step/complete: 新手引导
- base_upgrade: 大本营升级
- building_build/upgrade: 建筑建造/升级
- troop_train: 部队训练
- pvp_battle: PVP战斗
- pve_battle: PVE战斗
- alliance_join/create: 联盟加入/创建
- resource_gather: 资源采集
```

### IAA休闲游戏指标体系

```
核心关注指标：
├── 获取层
│   ├── 新增用户数(DNU)
│   ├── eCPM
│   └── 归因ROI
├── 激活层
│   ├── DAU
│   ├── 平均在线时长
│   ├── 人均会话次数
│   └── 人均广告展示次数
├── 留存层
│   ├── 次日留存率
│   ├── 7日留存率
│   └── 30日留存率
├── 收入层
│   ├── 广告ARPU
│   ├── 填充率
│   ├── 激励视频完成率
│   └── 展示率
└── 传播层
    ├── 分享率
    └── 分享转化率

关键埋点事件：
- level_start/complete/fail: 关卡开始/完成/失败
- ad_request/fill/impression/click: 广告请求/填充/展示/点击
- ad_complete: 广告完成(激励视频)
- reward_claim: 奖励领取
- item_use: 道具使用
```

---

## 埋点规划模板

### 事件设计规范

```
事件命名规范：
- 格式：{对象}_{动作}
- 示例：level_complete, item_purchase, guild_join

事件属性规范：
- 必备属性：user_id, timestamp, platform, version
- 业务属性：根据具体事件定义

公共属性：
- user_id: 用户唯一标识
- device_id: 设备唯一标识
- platform: 平台(iOS/Android)
- os_version: 系统版本
- app_version: 应用版本
- channel: 渠道
- country: 国家/地区
- language: 语言
```

### 核心事件清单

| 事件名称 | 事件说明 | 必备属性 | 扩展属性 |
|---------|---------|---------|---------|
| `app_install` | 应用安装 | user_id, channel | campaign, creative, referrer_id |
| `app_launch` | 应用启动 | user_id | session_id, launch_type |
| `app_close` | 应用关闭 | user_id, session_id | duration |
| `tutorial_start` | 新手引导开始 | user_id, tutorial_id | - |
| `tutorial_step` | 新手引导步骤 | user_id, tutorial_id, step_id | step_name |
| `tutorial_complete` | 新手引导完成 | user_id, tutorial_id | duration |
| `level_up` | 等级提升 | user_id, level_old, level_new | - |
| `purchase` | 付费 | user_id, sku_id, amount, currency | item_id, item_name |
| `ad_impression` | 广告展示 | user_id, ad_type, ad_network | ad_id, revenue |
| `ad_click` | 广告点击 | user_id, ad_type, ad_network | ad_id |
| `share` | 分享 | user_id, share_type, share_channel | content_id |

---

## 埋点评估模板

### 当前可算指标识别

```
评估流程：
1. 获取当前已埋点事件列表
2. 对比指标所需事件
3. 标记可算/需补埋点状态

输出格式：
| 指标名称 | 所需事件 | 当前状态 | 缺失事件 |
|---------|---------|---------|---------|
| 次日留存率 | app_install, app_launch | ✅ 可算 | - |
| 付费率 | purchase, app_launch | ⚠️ 部分可算 | purchase |
| LTV90 | app_install, purchase | ❌ 不可算 | purchase |
```

### 埋点优先级排序

```
优先级规则：
P0 - 核心指标所需事件（留存、付费相关）
P1 - 重要指标所需事件（激活、核心玩法）
P2 - 辅助指标所需事件（社交、传播）
P3 - 优化指标所需事件（细节玩法）
```

---

## Skill 执行流程

```
输入：游戏类型、商业模式、项目阶段

Step 1: 选择指标模板
        └── 根据游戏类型加载对应指标模板

Step 2: 生成指标体系
        ├── 获取层指标（Acquisition）
        ├── 激活层指标（Activation）
        ├── 留存层指标（Retention）
        ├── 收入层指标（Revenue）
        └── 传播层指标（Referral）

Step 3: 标注埋点需求
        └── 为每个指标标注所需事件和属性

Step 4: 埋点评估（可选）
        ├── 输入当前已埋点事件列表
        ├── 识别可算指标
        ├── 识别需补埋点指标
        └── 输出埋点优先级

Step 5: 输出结果
        ├── 指标体系文档
        ├── 埋点设计文档
        └── 埋点评估报告
```

---

## 输出示例

### 指标体系文档结构

```markdown
# [游戏名称] 指标体系文档

## 1. 项目概述
- 游戏类型：SLG
- 商业模式：IAP
- 项目阶段：测试期

## 2. AARRR指标体系

### 2.1 获取层(Acquisition)
| 指标 | 公式 | 所需事件 | 优先级 |
|-----|------|---------|-------|
| ... | ... | ... | ... |

### 2.2 激活层(Activation)
...

### 2.3 留存层(Retention)
...

### 2.4 收入层(Revenue)
...

### 2.5 传播层(Referral)
...

## 3. 埋点设计

### 3.1 事件清单
...

### 3.2 属性清单
...

## 4. 埋点评估

### 4.1 可算指标
...

### 4.2 需补埋点指标
...

### 4.3 埋点优先级
...
```

---

## 注意事项

1. **指标选择原则**
   - 聚焦核心指标，避免指标过多
   - 指标可量化、可追踪
   - 指标与业务目标对齐

2. **埋点设计原则**
   - 事件命名统一规范
   - 属性设计完整
   - 避免冗余埋点

3. **数据质量保障**
   - 埋点测试验证
   - 数据监控告警
   - 定期数据审计

---

**Skill 作者：** Claude
**版本：** 1.0.0
**更新日期：** 2026-04-03
