## 一、Event Analysis（事件分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Select Event | events[].eventName | 选择事件 | 事件名 |
| Calculation Method | events[].analysis | 计算方式 | 见下方聚合类型映射 |
| Property | events[].quota | 属性 | 数值属性名 |
| Group By | eventView.groupBy | 分组维度 | 属性列表 |
| Filter | eventView.filts | 筛选条件 | 筛选条件列表 |
| Time Granularity | eventView.timeParticleSize | 时间粒度 | T0/T1/T2/T3/T4/T5/T6/T7/T8/T9/T99 |
| Time Range | eventView.startTime/endTime | 时间范围 | yyyy-MM-dd HH:mm:ss |
| Chart Type | eventView.graphShape | 图表类型 | L0=折线图/L1=柱状图/L2=饼图/L3=累计图 |

### 聚合类型映射（Calculation Method）

| analysis值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| A100 | Total Count | 总次数 |
| A101 | Triggering User Count | 触发用户数 |
| A102 | Per User Count | 人均次数 |
| A103 | Sum | 总和 |
| A104 | Average | 均值 |
| A105 | Average Per User | 人均值 |
| A106 | Maximum | 最大值 |
| A107 | Minimum | 最小值 |
| A108 | Distinct Count | 去重数 |
| A109 | True Count | 为真数 |
| A110 | False Count | 为假数 |
| A111 | Non Empty Count | 不为空数 |
| A112 | Empty Count | 为空数 |
| A117 | Median | 中位数 |
| A119 | Percentile | 百分位数 |
| A120 | Variance | 方差 |
| A121 | Standard Deviation | 标准差 |

---

## 二、Retention（留存分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Analysis Subject | eventView.taIdMeasureVo | 分析主体 | #user_id等 |
| Initial Event | events[].type=0 | 初始事件 | 事件名 |
| Return Event | events[].type=1 | 回访事件 | 事件名 |
| Retention Period | eventView.unitNum | 留存周期数 | 数值 |
| Time Granularity | eventView.timeParticleSize | 时间粒度 | T1=日/T2=周/T3=月 |
| Retention Type | eventView.rtnRateOrNum | 留存显示类型 | R0=留存率/R1=留存人数 |
| Statistic Type | eventView.statType | 统计类型 | retention=留存分析/lost=流失分析 |
| Group By | eventView.groupBy | 分组维度 | 初始事件属性 |
| Filter | eventView.filts | 筛选条件 | 筛选条件列表 |
| Simultaneous Display | events[].type=2/3 | 同时展示 | 指标配置 |
| Time Range | eventView.startTime/endTime | 时间范围 | yyyy-MM-dd HH:mm:ss |

### 留存事件类型

| type值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| 0 | Initial Event | 初始事件 |
| 1 | Return Event | 回访事件 |
| 2 | Simultaneous Display Metric | 同时展示指标 |
| 3 | Initial Date Metric | 初始日期指标 |

---

## 三、Funnel（漏斗分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Analysis Subject | eventView.taIdMeasureVo | 分析主体 | #user_id等 |
| Funnel Step | events[].eventName | 漏斗步骤 | 事件名（按顺序） |
| Step Filter | events[].filts | 步骤筛选 | 步骤级筛选条件 |
| Window Period | eventView.windows_gap_ms + windows_gap_tu | 分析窗口 | 时间窗口 |
| Time Granularity | eventView.timeParticleSize | 时间粒度 | T1=天/T2=周/T3=月/T5=累计 |
| Display Type | eventView.displayType | 显示类型 | 0=转化率/1=流失率 |
| Chart Type | eventView.chartType | 图表类型 | 0=转化图/1=趋势图 |
| Filter | eventView.filts | 筛选条件 | 全局筛选条件 |
| Time Range | eventView.startTime/endTime | 时间范围 | yyyy-MM-dd HH:mm:ss |

### 漏斗窗口时间单位

| windows_gap_tu值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| second | Second | 秒 |
| minute | Minute | 分钟 |
| hour | Hour | 小时 |
| day | Day | 天 |
| week | Week | 周 |
| month | Month | 月 |

---

## 四、Distribution（分布分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Analysis Subject | eventView.taIdMeasureVo | 分析主体 | #user_id等 |
| Select Event | events[].eventName | 选择事件 | 事件名 |
| Calculation Method | events[].analysis | 计算方式 | 见聚合类型映射 |
| Property | events[].quota | 属性 | 属性名 |
| Interval Type | events[].intervalType | 区间类型 | discrete=离散值/def=默认区间/user_defined=自定义区间 |
| Interval Boundaries | events[].quotaIntervalArr | 区间边界 | 自定义区间数组 |
| Group By | eventView.groupBy | 分组维度 | 分组属性 |
| Filter | eventView.filts | 筛选条件 | 筛选条件列表 |
| Time Granularity | eventView.timeParticleSize | 时间粒度 | T1=天/T2=周/T3=月/T5=累计 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

### 分布专属聚合类型

| analysis值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| A200 | Count | 次数分布 |
| A201 | Days | 天数分布 |
| A202 | Hours | 小时分布 |

---

## 五、Path（路径分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Source Event | events.source_event.event_name | 起始事件 | 事件名 |
| Path Direction | events.source_type | 路径方向 | 0=前进路径/1=后退路径 |
| Participating Events | events.event_names | 参与事件 | 事件名列表 |
| Event Split | events.by_fields | 事件分叉 | 按属性拆分事件 |
| Session Interval | eventView.session_interval | 会话间隔 | 数值 |
| Session Unit | eventView.session_type | 会话单位 | second/minute/hour |
| User Filter | events.user_filter | 用户筛选 | 用户属性筛选 |
| Column Limit | eventView.col_limit | 列数限制 | 最大显示列数 |
| Row Limit | eventView.row_limit | 行数限制 | 最大显示行数 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

### 路径方向

| source_type值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| 0 | Forward Path | 前进路径 |
| 1 | Backward Path | 后退路径 |

---

## 六、Interval（间隔分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Analysis Subject | eventView.taIdMeasureVo | 分析主体 | #user_id等 |
| Start Event | events[].type=first | 起始事件 | 事件名 |
| End Event | events[].type=second | 结束事件 | 事件名 |
| Start Event Filter | events[].filts | 起始事件筛选 | 起始事件筛选条件 |
| End Event Filter | events[].filts | 结束事件筛选 | 结束事件筛选条件 |
| Interval Limit | eventView.windowsGapValue + windowsGapUnit | 间隔上限 | 时间窗口 |
| Relation Property | events[].relationProp | 关联属性 | 属性关联配置 |
| Group By | eventView.groupBy | 分组维度 | 分组属性 |
| Percentile Config | eventView.percentConfig | 百分位配置 | maxValue/threeQuarterValue/midValue/quarterValue/minValue/avgValue |
| Filter | eventView.filts | 筛选条件 | 全局筛选条件 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

### 间隔事件类型

| type值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| first | Initial Event | 起始事件 |
| second | Return Event | 结束事件 |

---

## 七、Attribution（归因分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Analysis Subject | eventView.taIdMeasureVo | 分析主体 | #user_id等 |
| Attribution Model | eventView.modelType | 归因模型 | first/last/linear |
| Attribution Window | eventView.attributionWindow | 归因窗口 | 时间窗口配置 |
| Target Event | events.targetEvent | 目标事件 | 转化事件 |
| Target Metric | events.targetEvent.analysis | 目标指标 | A100/A103等 |
| Target Property | events.targetEvent.quota | 目标属性 | 属性名 |
| Attribution Event | events.attributionEvents | 归因事件 | 触点事件列表 |
| Direct Conversion | eventView.directConversion | 直接转化 | true/false |
| Filter | eventView.filts | 筛选条件 | 全局筛选条件 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

### 归因模型

| modelType值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| first | First Touch | 首次触点归因 |
| last | Last Touch | 末次触点归因 |
| linear | Linear | 线性归因 |

### 归因窗口单位

| attributionWindow.unit值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| day | Day | 天 |
| hour | Hour | 小时 |
| minute | Minute | 分钟 |

---

## 八、Ranking（排行榜）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Ranking Dimension | events.rankProperty | 排行维度 | 属性名 |
| Ranking Metric | events.rankEvent | 排行指标 | 事件+聚合类型 |
| Ranking Method | events.rankType | 排行方式 | rank/dense_rank/row_rank |
| Metric Calculation | events.rankEvent.analysis | 指标计算方式 | A100/A101/A102/A103等 |
| Metric Property | events.rankEvent.quota | 指标属性 | 属性名 |
| Sort Direction | events.rankEvent.orderBy | 排序方向 | DESC/ASC |
| Additional Metric | events.meanwhileEvents | 同时显示指标 | 附加指标列表 |
| Filter | eventView.filts | 筛选条件 | 全局筛选条件 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

### 排行方式

| rankType值 | 英文名称 | 中文名称 | 说明 |
| :--- | :--- | :--- | :--- |
| rank | Standard Ranking | 标准排行 | 同值并列，跳跃排名 |
| dense_rank | Dense Ranking | 密集排行 | 同值并列，连续排名 |
| row_rank | Row Number | 行号排行 | 不重复，连续序号 |

---

## 九、Heatmap（热力图）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Heat Event | events.hotEvent | 热力事件 | 事件名 |
| Heat Metric | events.hotQuota | 热力指标 | 聚合类型配置 |
| X Coordinate | events.coordinate.xProp | X坐标 | 坐标属性 |
| Y Coordinate | events.coordinate.yProp | Y坐标 | 坐标属性 |
| Coordinate Property | events.coordinate.xProp/yProp.columnName | 坐标属性 | screen_width/screen_height等 |
| Metric Calculation | events.hotQuota.analysis | 指标计算方式 | A100/A101/A102/A103等 |
| Metric Property | events.hotQuota.quota | 指标属性 | 属性名 |
| Comparison Group | events.comparedGroup | 对比组 | 分组对比配置 |
| Group Name | events.comparedGroup.groupName | 组名 | 分组名称 |
| Group Filter | events.comparedGroup.filts | 组筛选 | 分组筛选条件 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

---

## 十、Prop_analysis（属性分析）

| 英文配置项 | QP字段名 | 中文名称（TE前端） | 可选值/说明 |
| :--- | :--- | :--- | :--- |
| Analysis Type | events[].analysis | 分析类型 | A101/A108/A103等 |
| Property | events[].quota | 属性 | 属性名 |
| Group By | eventView.groupBy | 分组维度 | 分组属性 |
| User Crowd | eventView.userCrowds | 用户人群 | 人群对比配置 |
| Crowd Name | eventView.userCrowds.crowdName | 人群名称 | 人群名称 |
| Crowd Filter | eventView.userCrowds.filts | 人群筛选 | 人群筛选条件 |
| Filter | events[].filts | 筛选条件 | 筛选条件列表 |
| Time Range | eventView.startTime/endTime 或 recentDay | 时间范围 | yyyy-MM-dd HH:mm:ss 或 0-7 |

### 属性分析专属聚合类型

| analysis值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| A101 | User Count | 用户数 |
| A108 | Distinct Count | 去重数 |

---

## 通用映射表

### 过滤操作符（CalcType）

| calcuSymbol值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| C00 | Equals | 等于 |
| C000 | Equals Empty String | 为空字符串 |
| C01 | Not Equals | 不等于 |
| C010 | Not Equals Empty String | 不为空字符串 |
| C02 | Less Than | 小于 |
| C020 | Less Than or Equal | 小于等于 |
| C03 | Greater Than | 大于 |
| C030 | Greater Than or Equal | 大于等于 |
| C04 | Has Value | 有值 |
| C05 | No Value | 无值 |
| C06 | Range | 区间 |
| C060 | Date Range | 日期区间 |
| C07 | Contains | 包括 |
| C08 | Does Not Contain | 不包括 |
| C09 | True | 为真 |
| C10 | False | 为假 |
| C11 | Regex Match | 正则匹配 |
| C12 | Regex Does Not Match | 正则不匹配 |
| C13 | Relative to Current Time | 相对当前时间 |
| C14 | Relative to Event Time | 相对事件时间 |
| C20 | Belongs to Cluster | 属于群组 |
| C21 | Does Not Belong to Cluster | 不属于群组 |

### 表格字段类型（TableType）

| tableType值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- |
| 0 | Event Property | 事件属性 |
| 1 | User Property | 用户属性 |
| 2 | User Cluster Property | 用户群组属性 |

### 时间粒度（timeParticleSize）

| 模型 | 值 | 英文名称 | 中文名称 |
| :--- | :--- | :--- | :--- |
| Event/Interval | T0 | By Hour | 按小时 |
| Event/Interval | T1 | By Day | 按天 |
| Event/Retention/Distribution/Interval | T2 | By Week | 按周 |
| Event/Retention/Distribution/Interval | T3 | By Month | 按月 |
| Event/Interval | T4 | By 1 Minute | 按分钟 |
| Event/Distribution | T5 | Total | 累计 |
| Event/Interval | T6 | By 5 Minutes | 按5分钟 |
| Event/Interval | T7 | By 10 Minutes | 按10分钟 |
| Event/Interval | T8 | By Quarter | 按季度 |
| Event/Interval | T9 | By Year | 按年 |
| Event | T99 | No Aggregation | 不聚合 |
| Retention/Funnel | T1 | By Day | 按天 |
| Retention/Funnel | T2 | By Week | 按周 |
| Retention/Funnel | T3 | By Month | 按月 |
| Funnel | T5 | Total | 累计 |

---
