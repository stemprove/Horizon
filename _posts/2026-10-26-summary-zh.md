---
layout: default
title: "Horizon Summary: 2026-10-26 (ZH)"
date: 2026-10-26
lang: zh
---

> 从 29 条内容中筛选出 5 条重要资讯。

---

**科技新闻**
1. [Cerebras 详解万亿参数模型部署方案](#item-tech-news-1) ⭐️ 8.0/10
2. [Brotli 高危漏洞波及 Python 与 Node.js HTTP 组件](#item-tech-news-2) ⭐️ 8.0/10
3. [南北阁发布 Nanbeige4.3-33B，Apache 2.0 教师模型](#item-tech-news-3) ⭐️ 7.0/10
4. [苹果预计周三发布首款触屏 MacBook Pro](#item-tech-news-4) ⭐️ 7.0/10

**财经新闻**
1. [2025 年全国总人口减少 339 万](#item-finance-news-1) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Cerebras 详解万亿参数模型部署方案](https://www.cerebras.ai/blog/how-we-deploy-trillion-parameter-frontier-models-on-cerebras) ⭐️ 8.0/10

Cerebras 发布技术说明，介绍其如何在晶圆级硬件上部署万亿参数级前沿模型，面向关注大模型推理基础设施的开发者。该说明聚焦部署方法，并非新硬件发布；给定材料未提供具体模型清单、吞吐或延迟指标、上线日期及定价，因此相关能力仍属厂商描述，尚无独立测量结果。

hackernews · gmays · 10月25日 01:33 · [社区讨论](https://news.ycombinator.com/item?id=50227356)

**「背景」** Cerebras 的 WSE-3 采用权重流式架构：模型权重存放在可扩展至 PB 级的 DRAM 外部内存池，计算与存储因此解耦。这样，权重可以按需流入晶圆级芯片，单套系统便能承载远超片上内存的前沿模型。

**「对开发者的影响」** Cerebras 的万亿参数模型部署意味着这类模型可通过其托管推理 API 提供，开发者用 OpenAI 兼容接口接入，无需自建多卡集群。选型时仍需核对具体模型清单、价格和吞吐配额；Cerebras 宣称的 30 倍加速是厂商说法，并非独立实测。

**「社区讨论」** 评论者集中争论 Cerebras 的模型供给：有人称实际可用的是 GPT OSS 120B、Qwen 3.8 27B 等较小或较旧模型，速度虽快但准确性不适合其用途，并估计其模型上线比前沿落后约 6–9 个月。另一些评论认为其晶圆级硬件产能和资金限制导致难以满足需求，但也有人预计它会在数月内以更低成本提供接近前沿的模型。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://dev.to/hassanradwany/scaling-to-trillions-a-look-at-cerebras-weight-streaming-architecture-4meh">Scaling to Trillions : A Look at Cerebras ... - DEV Community</a></li>
<li><a href="https://www.cerebras.ai/inference">Fastest AI Inference Cloud and API | Cerebras</a></li>
<li><a href="https://www.cerebras.ai/pricing">Cerebras Inference Pricing | API and Enterprise Plans</a></li>

</ul>
</details>

**标签**: `#Cerebras`, `#AI hardware`, `#LLM deployment`, `#wafer-scale`, `#inference`

---

<a id="item-tech-news-2"></a>
### [Brotli 高危漏洞波及 Python 与 Node.js HTTP 组件](https://www.aikido.dev/blog/python-packages-vulnerable-node2shell-brotli-cve-2026-111497) ⭐️ 8.0/10

谷歌 Brotli 解码器漏洞 CVE-2026-111497 影响 1.0.3 至 1.2.0 版本，CVSS 4.0 评分为 9.2；远程未认证的攻击者可借特制压缩流造成内存损坏、敏感数据泄露、进程崩溃或可能的任意代码执行。该漏洞最初以 Node2Shell 之名披露，后被称为 HTTP2Shell，现确认波及 Python 与 Node.js 的 HTTP 相关组件。Python 侧需将 Brotli 升级至 1.2.1、brotlicffi 升级至 1.2.1.0；Node.js 的修复版本为 22.23.4、24.22.1 和 26.12.1。以上版本号与评分来自 Aikido Security 的转述，所给材料未提供独立验证。

telegram · zaihuapd · 10月25日 02:42

**「背景」** Brotli 是 HTTP 响应常用的压缩格式，解码器需要在应用处理请求正文前还原压缩流；因此，解码阶段的内存安全缺陷可能被远程输入直接触发。该漏洞最初以 Node2Shell 名称披露，后来也被称为 HTTP2Shell，来源还称 OpenAI 于今年 2 月发现了该问题。

**「影响与处置」** 使用受影响 Brotli 解码组件的 Python 与 Node.js 服务，需要按上述版本号升级才能消除该解码路径；在升级前，任何能向服务发送 HTTP 请求的外部客户端都可能触发这一内存损坏问题，因此暴露在公网的服务应优先排查依赖版本并安排升级。

**标签**: `#security vulnerability`, `#Brotli`, `#Python`, `#Node.js`, `#CVE`

---

<a id="item-tech-news-3"></a>
### [南北阁发布 Nanbeige4.3-33B，Apache 2.0 教师模型](https://www.reddit.com/r/MachineLearning/comments/1xf6x35/nanbeige_releases_nanbeige4333b_an_apache_20/) ⭐️ 7.0/10

南北阁（Nanbeige）发布 Nanbeige4.3-33B，采用 Apache 2.0 开放权重，模型卡标注 512K 上下文窗口，定位为其后续更小智能体（包括一款尚未发布的 3B 模型）的教师模型。团队自报的评测中，Terminal-Bench 2.1 得分为 80.9，对比 Qwen3.8-27B 的 73.0（各基准内使用相同评测框架与推理设置）；但在 SWE-Bench Pro 上为 60.3，低于对方的 61.7。上述分数均为发布方自己的评测，尚无独立复现。复现智能体结果的一个实际细节是：评测以 preserve\_thinking=true 保留先前推理内容，模型卡建议在多轮工具调用中启用该设置，但不建议用于普通聊天。

reddit · r/MachineLearning · /u/jatingargiitk · 10月25日 16:32

**「背景」** “教师模型”通常指在蒸馏流程中为更小模型提供训练信号或示范轨迹的较大模型，因此它的权重许可证、上下文长度和工具调用行为会直接影响小模型能否复用同一套数据与推理流程。Nanbeige 此次把 33B 模型定位为计划中更小 agent 的教师，而不是直接面向终端部署的旗舰模型。

**「对使用者的直接影响」** 计划采用该模型的团队需要注意，80.9 的 Terminal-Bench 2.1 分数来自厂商自行评测，且评测中启用了 preserve\_thinking=true，以保留此前的推理内容；模型卡只建议在多轮工具调用时使用该设置，不建议用于普通对话。因此，复现时应在固定该设置的前提下，比较任务成功率与总生成 token 数，而不是直接把厂商公布的高分当作部署排名依据；在 SWE-Bench Pro 上，该模型以 60.3 落后于 Qwen3.8-27B 的 61.7，也说明它并非在所有任务上都占优。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.marktechpost.com/2026/10/25/nanbeige-releases-nanbeige4-3-33b-open-agentic-coding-model/">Nanbeige Releases Nanbeige4.3-33B, a 33B Open Agentic Coding ...</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#agentic AI`, `#benchmark evaluation`, `#long context`, `#model release`

---

<a id="item-tech-news-4"></a>
### [苹果预计周三发布首款触屏 MacBook Pro](https://www.bloomberg.com/news/newsletters/2026-10-25/apple-to-unveil-touch-screen-macbook-pro-executive-promotions-in-box-checker) ⭐️ 7.0/10

据 Bloomberg 报道，苹果预计于本周三发布首款支持触屏的 MacBook Pro，14 英寸和 16 英寸机型将引入 OLED 屏幕与灵动岛。报道称其起售价将高于现款的 2499 美元，触控被定位为键盘和触控板的补充，而非替代。上述信息来自该 newsletter 的预期报道，发布前尚无苹果官方确认或独立验证。

telegram · zaihuapd · 10月25日 14:25

**「背景」** 多年来，苹果高管一直以人体工学为由反对在 Mac 笔记本上加入触摸屏，MacBook Pro 的交互长期以键盘和触控板为主；此次报道中的触屏与 OLED 将是 Mac 的首次。10 月初的报道已称苹果将在 10 月 27 日前后推出首款触屏 OLED MacBook Pro；另一篇报道则称苹果已确认 10 月 28 日在洛杉矶举行“Pro and tell”活动，Mark Gurman 预计触屏 Mac 会在该活动亮相，这与当前报道的“周三”发布时点相衔接。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.macrumors.com/2026/10/08/apple-october-27-macbook-pro/">Apple to Launch Touchscreen OLED MacBook Pro ... - MacRumors</a></li>
<li><a href="https://digg.com/tech/k053jiot">Apple ’s touch - screen MacBook Pro reportedly headed for October ...</a></li>

</ul>
</details>

**标签**: `#Apple`, `#MacBook Pro`, `#touchscreen`, `#OLED`, `#hardware`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [2025 年全国总人口减少 339 万](https://weibo.com/1796087453/5357878513767954) ⭐️ 7.0/10

据《中国统计年鉴 2026》数据，2025 年末全国总人口为 140489 万人（约 14.05 亿），比 2024 年末减少 339 万人；全年出生 792 万人，出生率 5.63‰，自然增长率-2.41‰。

telegram · zaihuapd · 10月25日 12:02

**「背景」** 自然增长率是指出生与死亡相抵后按每千人计算的人口变化率；-2.41‰意味着死亡人数多于出生人数。据《中国统计年鉴 2026》，2025 年出生率超过 7‰的 9 个省份和自然增长率为正的 7 个省份主要分布在西部和华南，黑龙江、吉林、辽宁的出生率最低。

**「影响」** 人口自然增长的区域分化意味着，出生率垫底的黑龙江、吉林、辽宁等省份将比其他地区更早面对劳动力收缩和养老支出上升的压力。

**标签**: `#China demographics`, `#population decline`, `#birth rate`, `#macroeconomic data`

---