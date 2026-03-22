---
name: A-Share Quant Tools
description: 定义 A 股量化监控 Agent 可调用的底层工具链、API 接口及核心执行逻辑。
---

## Available Tools (可用工具集)

Agent 拥有以下五大核心工具箱，用于完成从数据采集到交易决策的全链路闭环：

### 1. `fetch_ths_news(tags: list, pages: int) -> list[dict]`
- **描述**: 调用同花顺 7x24 小时新闻 API，获取最新的市场异动、政策发布和个股利好。
- **参数**:
  - `tags`: 筛选标签（如 `''` 全部, `'-21101'` 重大事件, `'21109'` 机会挖掘）。
  - `pages`: 抓取的页数（默认 4 页，保证信息覆盖面）。
- **返回值**: 包含清洗去重后、带有时间戳 (ctime) 的 A 股新闻字典列表。

### 2. `fetch_tencent_market_data(symbols: list, data_type: str) -> dict`
- **描述**: 批量调用腾讯财经 API，获取股票的实时盘口数据或历史 K 线。
- **参数**:
  - `symbols`: 股票代码列表，自动进行前缀转换（如 688498 -> sh688498）。
  - `data_type`: 请求类型（`'quote'` 实时行情, `'kline'` 前复权日 K 线）。
- **机制**: 采用批处理模式（每批最多 30 只），提取涨跌幅、最新价、封单资金量及连板状态。

### 3. `calculate_quant_score(stock_data: dict, news_sentiment: float) -> dict`
- **描述**: 核心量化决策引擎。将新闻情绪与盘面数据结合，输出一致性评分及交易策略。
- **输入**: 包含个股基础行情和对应新闻的情绪得分 (Impact Level: S/A/B/C)。
- **输出**: 
  - `consistency_score`: 0-100 分（结合情绪、板块、龙头、资金、量价、封单 6 大维度）。
  - `action`: 交易指令（如 `强烈买入`、`观望`）。
  - `risk_control`: 止盈/止损价格（基于当前价计算的 +5%/+10% 止盈，-3% 止损）。
  - `position_advice`: 仓位建议（如 `≤30%`）。

### 4. `generate_dashboard_html(data_context: dict) -> str`
- **描述**: 将结构化数据注入 TailwindCSS + ECharts 的 `template.html` 模板中。
- **参数**: 包含 Hot7 榜单、实时利好精选、看涨预测 Top 5 的汇总数据字典。
- **机制**: 替换 `__PLACEHOLDER__` 占位符，配置自动刷新时间间隔（默认 3 分钟），生成单页暗黑风监控面板。

### 5. `push_alerts(targets: list, payload: dict)`
- **描述**: 执行多渠道信息分发，将关键异动和决策推送到用户终端。
- **参数**:
  - `targets`: 推送目标（`['telegram', 'feishu']`）。
  - `payload`: 结构化的消息内容（包括标的、异动原因、打分和图表/链接）。
- **机制**:
  - **飞书**: 自动构建交互式卡片 (Interactive Card)，带有红色 Header 和 Markdown 排版。
  - **Telegram**: 采用 HTML parse_mode 发送，若内容超长 (≥4000 字符) 自动触发分块发送防截断。

## Usage Constraints (调用约束)
- **频率限制**: 请求 THS API 时必须增加合理的延时（如 1.5s），避免触发反爬策略。
- **交易时间校验**: 在调用 `push_alerts` 的自动轮询模式时，必须前置调用 `is_market_hours()`（基于东八区 UTC+8 校验 9:15-15:00），休市期间必须静默或仅刷新面板。