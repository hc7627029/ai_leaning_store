# TE 字段名翻译对照表

本文档提供游戏行业常见的 TE 埋点字段名中英文翻译对照，供 `te-feasibility-analyzer` 和 `te-model-selector` skill 参考。

---

## 一、事件名翻译表

| 英文名 | 中文显示名 |
|-------|----------|
| app_start_up | 游戏启动 |
| purchase_complete | 付费完成 |
| purchase_succeed | 支付完成 |
| register | 用户注册 |
| login | 用户登录 |
| enter_level | 进入关卡 |
| leave_level | 离开关卡 |
| complete_level | 关卡完成 |
| fail_level | 关卡失败 |
| retry_level | 重试关卡 |
| spend_diamonds | 花费钻石 |
| obtain_diamonds | 获得钻石 |
| spend_gold | 花费金币 |
| obtain_gold | 获得金币 |
| spend_coin | 花费金币 |
| obtain_coin | 获得金币 |
| spend_stamina | 消耗体力 |
| obtain_stamina | 获得体力 |
| spend_energy | 消耗能量 |
| obtain_energy | 获得能量 |
| spend_item | 消耗道具 |
| obtain_item | 获得道具 |
| view_ads | 观看广告 |
| ad_complete | 广告完成 |
| ad_click | 广告点击 |
| tutorial_complete | 引导结束 |
| tutorial_start | 引导开始 |
| tutorial_skip | 跳过引导 |
| enter_shop | 进入商城 |
| browse_shop | 浏览商城 |
| buy_item | 购买商品 |
| get_equipment | 获得装备 |
| sell_equipment | 出售装备 |
| upgrade_equipment | 强化装备 |
| compose_equipment | 合成装备 |
| wear_equipment | 穿戴装备 |
| start_task | 开始任务 |
| complete_task | 完成任务 |
| abandon_task | 放弃任务 |
| start_battle | 开始战斗 |
| end_battle | 结束战斗 |
| enter_copy | 进入副本 |
| leave_copy | 离开副本 |
| join_guild | 加入公会 |
| leave_guild | 退出公会 |
| create_guild | 创建公会 |
| send_friend_request | 发送好友请求 |
| accept_friend_request | 接受好友请求 |
| remove_friend | 删除好友 |
| upgrade_role | 角色升级 |
| breakthrough_role | 角色突破 |
| awaken_role | 角色觉醒 |
| draw_card | 抽卡 |
| draw_result | 抽卡结果 |
| get_reward | 获得奖励 |
| get_sign_reward | 签到奖励 |
| get_mail_reward | 邮件奖励 |
| open_mail | 打开邮件 |
| claim_daily_reward | 领取每日奖励 |
| level_up | 升级 |
| online | 上线 |
| offline | 下线 |
| heartbeat | 心跳 |
| click_button | 点击按钮 |
| open_page | 打开页面 |
| close_page | 关闭页面 |
| share | 分享 |
| invite | 邀请 |
| bind_account | 绑定账号 |
| switch_account | 切换账号 |
| logout | 登出 |
| first_purchase | 首次付费 |
| recharge | 充值 |
| consume | 消耗 |
| exchange | 兑换 |
| gift_pack_purchase | 礼包购买 |
| lottery | 抽奖 |
| spin_wheel | 转盘抽奖 |
| enter_arena | 进入竞技场 |
| leave_arena | 离开竞技场 |
| start_match | 开始匹配 |
| match_success | 匹配成功 |
| match_fail | 匹配失败 |
| use_skill | 使用技能 |
| use_item | 使用道具 |
| unlock_feature | 解锁功能 |
| achievement_complete | 成就完成 |
| achievement_unlock | 成就解锁 |
| guide_step | 引导步骤 |
| popup_show | 弹窗展示 |
| popup_click | 弹窗点击 |

---

## 二、属性名翻译表

| 英文名 | 中文显示名 | 类型 |
|-------|----------|-----|
| start_time | 启动时间 | 时间 |
| end_time | 结束时间 | 时间 |
| duration | 持续时长 | 数值 |
| play_time | 游玩时长 | 数值 |
| online_time | 在线时长 | 数值 |
| offline_time | 离线时长 | 数值 |
| pay_amount | 付费金额 | 数值 |
| total_payment_amount | 付费金额 | 数值 |
| total_payment_times | 付费次数 | 数值 |
| first_pay_time | 首次付费时间 | 时间 |
| last_pay_time | 最后付费时间 | 时间 |
| player_level | 玩家等级 | 数值 |
| vip_level | VIP等级 | 数值 |
| vip_points | VIP积分 | 数值 |
| diamond | 持有钻石 | 数值 |
| diamonds | 持有钻石 | 数值 |
| golden_coin | 持有金币 | 数值 |
| gold_coin | 持有金币 | 数值 |
| gold | 持有金币 | 数值 |
| coin | 持有金币 | 数值 |
| stamina | 体力值 | 数值 |
| energy | 能量值 | 数值 |
| coupon | 点券 | 数值 |
| tickets | 券数量 | 数值 |
| level_id | 关卡ID | 文本 |
| level_name | 关卡名称 | 文本 |
| level_difficulty | 关卡难度 | 文本 |
| level_star | 关卡星级 | 数值 |
| level_score | 关卡得分 | 数值 |
| level_duration | 关卡耗时 | 数值 |
| level_status | 关卡状态 | 文本 |
| product_id | 商品ID | 文本 |
| product_name | 商品名称 | 文本 |
| product_type | 商品类型 | 文本 |
| product_price | 商品价格 | 数值 |
| buy_count | 购买数量 | 数值 |
| item_id | 道具ID | 文本 |
| item_name | 道具名称 | 文本 |
| item_type | 道具类型 | 文本 |
| item_count | 道具数量 | 数值 |
| item_quality | 道具品质 | 文本 |
| equipment_id | 装备ID | 文本 |
| equipment_name | 装备名称 | 文本 |
| equipment_level | 装备等级 | 数值 |
| equipment_quality | 装备品质 | 文本 |
| equipment_type | 装备类型 | 文本 |
| task_id | 任务ID | 文本 |
| task_name | 任务名称 | 文本 |
| task_type | 任务类型 | 文本 |
| task_status | 任务状态 | 文本 |
| task_progress | 任务进度 | 数值 |
| guild_id | 公会ID | 文本 |
| guild_name | 公会名称 | 文本 |
| guild_level | 公会等级 | 数值 |
| guild_member_count | 公会成员数 | 数值 |
| friend_count | 好友数量 | 数值 |
| friend_id | 好友ID | 文本 |
| role_id | 角色ID | 文本 |
| role_name | 角色名称 | 文本 |
| role_level | 角色等级 | 数值 |
| role_type | 角色类型 | 文本 |
| role_career | 角色职业 | 文本 |
| role_power | 角色战力 | 数值 |
| battle_result | 战斗结果 | 文本 |
| battle_type | 战斗类型 | 文本 |
| damage_value | 伤害值 | 数值 |
| kill_count | 击杀数 | 数值 |
| death_count | 死亡数 | 数值 |
| ad_type | 广告类型 | 文本 |
| ad_position | 广告位置 | 文本 |
| ad_duration | 广告时长 | 数值 |
| ad_reward | 广告奖励 | 文本 |
| draw_type | 抽卡类型 | 文本 |
| draw_count | 抽卡次数 | 数值 |
| draw_result_type | 抽卡结果类型 | 文本 |
| draw_cost | 抽卡消耗 | 数值 |
| reward_type | 奖励类型 | 文本 |
| reward_amount | 奖励数量 | 数值 |
| reward_id | 奖励ID | 文本 |
| copy_id | 副本ID | 文本 |
| copy_name | 副本名称 | 文本 |
| copy_type | 副本类型 | 文本 |
| copy_difficulty | 副本难度 | 文本 |
| copy_star | 副本星级 | 数值 |
| match_time | 匹配时长 | 数值 |
| match_rank | 匹配段位 | 文本 |
| arena_rank | 竞技场排名 | 数值 |
| arena_score | 竞技场积分 | 数值 |
| skill_id | 技能ID | 文本 |
| skill_name | 技能名称 | 文本 |
| skill_level | 技能等级 | 数值 |
| feature_id | 功能ID | 文本 |
| feature_name | 功能名称 | 文本 |
| achievement_id | 成就ID | 文本 |
| achievement_name | 成就名称 | 文本 |
| achievement_type | 成就类型 | 文本 |
| achievement_progress | 成就进度 | 数值 |
| guide_step_id | 引导步骤ID | 文本 |
| popup_id | 弹窗ID | 文本 |
| popup_type | 弹窗类型 | 文本 |
| button_id | 按钮ID | 文本 |
| button_name | 按钮名称 | 文本 |
| page_id | 页面ID | 文本 |
| page_name | 页面名称 | 文本 |
| page_type | 页面类型 | 文本 |
| channel | 渠道 | 文本 |
| channel_id | 渠道ID | 文本 |
| channel_name | 渠道名称 | 文本 |
| device_id | 设备ID | 文本 |
| device_type | 设备类型 | 文本 |
| device_model | 设备型号 | 文本 |
| os_type | 系统类型 | 文本 |
| os_version | 系统版本 | 文本 |
| app_version | 应用版本 | 文本 |
| app_id | 应用ID | 文本 |
| game_id | 游戏ID | 文本 |
| game_name | 游戏名称 | 文本 |
| server_id | 服务器ID | 文本 |
| server_name | 服务器名称 | 文本 |
| region | 地区 | 文本 |
| country | 国家 | 文本 |
| language | 语言 | 文本 |
| ip | IP地址 | 文本 |
| network_type | 网络类型 | 文本 |
| login_type | 登录类型 | 文本 |
| register_time | 注册时间 | 时间 |
| register_channel | 注册渠道 | 文本 |
| register_device | 注册设备 | 文本 |
| first_login_time | 首次登录时间 | 时间 |
| last_login_time | 最后登录时间 | 时间 |
| total_online_days | 总在线天数 | 数值 |
| total_play_days | 总游玩天数 | 数值 |
| days_since_register | 注册距今天数 | 数值 |
| days_since_last_login | 距上次登录天数 | 数值 |
| is_new_user | 是否新用户 | 布尔 |
| is_vip | 是否VIP | 布尔 |
| is_first_pay | 是否首充 | 布尔 |
| has_paid | 是否付费 | 布尔 |
| is_online | 是否在线 | 布尔 |
| gender | 性别 | 文本 |
| age | 年龄 | 数值 |
| birthday | 生日 | 时间 |
| nickname | 昵称 | 文本 |
| avatar | 头像 | 文本 |
| signature | 签名 | 文本 |
| invite_code | 邀请码 | 文本 |
| inviter_id | 邀请人ID | 文本 |
| share_platform | 分享平台 | 文本 |
| share_count | 分享次数 | 数值 |
| invite_count | 邀请次数 | 数值 |
| gift_pack_id | 礼包ID | 文本 |
| gift_pack_name | 礼包名称 | 文本 |
| gift_pack_type | 礼包类型 | 文本 |
| lottery_id | 抽奖ID | 文本 |
| lottery_type | 抽奖类型 | 文本 |
| wheel_result | 转盘结果 | 文本 |
| wheel_reward | 转盘奖励 | 文本 |
| mail_id | 邮件ID | 文本 |
| mail_type | 邮件类型 | 文本 |
| mail_status | 邮件状态 | 文本 |
| sign_day | 签到天数 | 数值 |
| sign_status | 签到状态 | 文本 |
| daily_reward_type | 每日奖励类型 | 文本 |
| daily_reward_amount | 每日奖励数量 | 数值 |
| upgrade_from_level | 升级前等级 | 数值 |
| upgrade_to_level | 升级后等级 | 数值 |
| upgrade_cost | 升级消耗 | 数值 |
| breakthrough_level | 突破等级 | 数值 |
| awaken_level | 觉醒等级 | 数值 |
| compose_material | 合成材料 | 文本 |
| compose_result | 合成结果 | 文本 |
| compose_cost | 合成消耗 | 数值 |
| exchange_type | 兑换类型 | 文本 |
| exchange_from | 兑换来源 | 文本 |
| exchange_to | 兑换目标 | 文本 |
| exchange_amount | 兑换数量 | 数值 |
| consume_type | 消耗类型 | 文本 |
| consume_amount | 消耗数量 | 数值 |
| consume_reason | 消耗原因 | 文本 |
| balance_before | 变动前余额 | 数值 |
| balance_after | 变动后余额 | 数值 |
| balance_change | 余额变动 | 数值 |

---

## 三、字段名推断规则

当字段名不在上述翻译表中时，可按以下规则推断：

### 3.1 中文显示名推断

| 关键词 | 推断显示名 |
|-------|----------|
| amount | 金额 |
| count | 次数 |
| time | 时间 |
| id | ID |
| level | 等级/关卡 |
| diamond / diamonds | 钻石 |
| coin / coins / gold | 金币 |
| stamina | 体力 |
| energy | 能量 |
| item | 道具 |
| equipment | 装备 |
| skill | 技能 |
| task | 任务 |
| guild | 公会 |
| friend | 好友 |
| role | 角色 |
| battle | 战斗 |
| copy | 副本 |
| ad | 广告 |
| draw | 抽卡 |
| reward | 奖励 |
| product | 商品 |
| shop | 商城 |
| guide / tutorial | 引导 |
| popup | 弹窗 |
| button | 按钮 |
| page | 页面 |
| channel | 渠道 |
| server | 服务器 |
| device | 设备 |
| upgrade | 升级 |
| breakthrough | 突破 |
| awaken | 觉醒 |
| compose | 合成 |
| exchange | 兑换 |
| consume | 消耗 |
| balance | 余额 |
| mail | 邮件 |
| sign | 签到 |
| gift_pack | 礼包 |
| lottery | 抽奖 |
| wheel | 转盘 |
| arena | 竞技场 |
| match | 匹配 |
| achievement | 成就 |
| vip | VIP |
| player | 玩家 |
| user | 用户 |
| online | 在线 |
| offline | 离线 |
| login | 登录 |
| register | 注册 |
| pay | 付费 |
| purchase / buy | 购买 |
| spend | 花费 |
| obtain / get | 获得 |
| start | 开始 |
| end | 结束 |
| enter | 进入 |
| leave | 离开 |
| complete | 完成 |
| fail | 失败 |
| success | 成功 |
| win | 胜利 |
| lose | 失败 |
| result | 结果 |
| status | 状态 |
| type | 类型 |
| name | 名称 |
| duration | 时长 |
| score | 得分 |
| rank | 排名/段位 |
| power | 战力 |
| damage | 伤害 |
| kill | 击杀 |
| death | 死亡 |
| share | 分享 |
| invite | 邀请 |

### 3.2 属性类型推断

| 关键词 | 推断类型 |
|-------|---------|
| amount / count / price / score / power / damage / rank / level / duration / days | 数值型 |
| time / date | 时间型 |
| is_ / has_ / can_ | 布尔型 |
| _id / id | 文本型（ID类） |
| _name / name | 文本型（名称类） |
| _type / type | 文本型（类型类） |
| _status / status | 文本型（状态类） |
| （默认） | 文本型 |

---

## 使用说明

1. **精确匹配优先**：先在翻译表中查找精确匹配
2. **推断规则补充**：找不到时按关键词推断
3. **保留原文**：无法推断的字段名保留英文原名
4. **一致性原则**：同一字段在不同地方使用相同翻译
