# AI.TRACK · AI 发展监控台

> **在线站点**：<https://blackinkvc.github.io/image-gen-lab/>  
> **实例 01 · 生图实验**：<https://blackinkvc.github.io/image-gen-lab/lab/>  
> **H3 实测看板**：<https://blackinkvc.github.io/image-gen-lab/lab/bench-h3.html>

把 AI 的进展拆成九块可以核对的台账：基模、Agent、公司、硬件、应用、原理、历史、本地部署、实测实例。人工维护的快照，不自动抓取，不追热度排行。

原来的生图实验档案整体迁到 `/lab/`，作为**实例 01**；根目录改为监控门户。后续实例在 `/lab/` 之外平级新开目录，编号不跳号。

## 页面清单（根目录 · 门户）

| 页面 | 内容 |
| --- | --- |
| `index.html` | 门户：九板块入口、近期信号、读法、实例入口 |
| `models.html` | 基模：闭源旗舰 / 开放权重 / 推理模型台账，三条技术主线 |
| `agents.html` | Agent：能力栈、MCP / A2A 协议、8 个产品、评测与风险 |
| `companies.html` | 公司：产业链五层、20 家台账、合作与资本、观察指标 |
| `hardware.html` | 硬件：prefill / decode 两类瓶颈、12 个型号、显存估算 |
| `apps.html` | 应用：六类产品、19 个条目、形态变化与选型 |
| `principles.html` | 原理：推理账、注意力、训练、推理模型、MoE、扩散、量化、评估 |
| `history.html` | 历史：1943–2025 五个阶段的关键节点 |
| `local.html` | 本地部署：推理栈、显存档位、硬件路线、常见坑、本机实践 |
| `cases.html` | 实例索引：01 已上线，02–06 占位与字段规范 |

## 页面清单（`/lab/` · 实例 01）

| 页面 | 内容 |
| --- | --- |
| `lab/index.html` | 实验档案首页：方案总览、总量指标、口径摘要 |
| `lab/scheme-sdxl.html` | SDXL · Juggernaut-XL v9 —— 历史基线 |
| `lab/scheme-zimage-turbo.html` | Z-Image Turbo —— 当前主力 |
| `lab/scheme-zimage-base.html` | Z-Image Base —— 无独立产出，字段留 `null` |
| `lab/scheme-double.html` | 双采 Base → Turbo —— 已放弃，附 OOM 与机理证据 |
| `lab/scheme-latent.html` | latent 放大链 —— 4096×6144 单张交付 |
| `lab/scheme-krea2.html` | Krea 2 —— 未实测，只列架构与既定参数 |
| `lab/scheme-moss.html` | MOSS-Image —— 测试中，权重下载阶段 |
| `lab/compare.html` | 横向对比：同 prompt / 同 seed 并排 + 对照表 |
| `lab/gallery.html` | 案例库：按方案筛选的图墙，点开看大图与 prompt |
| `lab/bench-h3.html` | H3 实测看板：内存分工、H3-Image、视频样片耗时、GGUF 判定 |

根目录下旧的 `scheme-*.html`、`compare.html`、`gallery.html`、`bench-h3.html` 保留为轻量跳转页，避免外链失效。

## 数据口径

- **快照而不是实时**：知识基线 2025-11，2026 年进展统一标「待补充」，不预填。
- **三态写法**：真值直接写；本该有值但未采集写 `—` / `null`；结构上不存在写 `n/a`。
- **不抄跑分**：没有出处的 benchmark 分数不收录；能力只描述到「面向什么场景」。
- **带 `*` 的条目**表示细节待核实，不作为选型依据。

## 实例 01 摘要

同一台机器、同一批参考图、串行出图。所有耗时与显存都能回到台账、边车或实验日志。

- **生成台账**：142 行 × 26 列（Juggernaut 136 行 + Z-Image 6 行）
- **候选边车**：128 份 JSON，含 prompt、seed、denoise、耗时、显存最低空闲值
- **A/B 对照**：同 prompt / 同 seed / 同画幅，10 张
- **8K 海报实验**：3 个 seed 的 raw 与终图耗时、峰值显存
- **环境备忘**：48+16 → 32+32 内存重分配；H3 生图与生视频实测；GGUF 最小验证

峰值显存 = ComfyUI 上报的 `vram_total`（57.84 GB）− 每 2 s 采样的最低 `vram_free`，属于**计算值**，页面上单独标注。

### 判定口径

- 只看服装版型、配色材质、配饰、发型轮廓、体型、义体位置；**不看脸**。
- 脸部只要求气质同档，五官偏差不作为否决项（2026-11-09 起）。
- 「✗」是模型能力边界，不作为调参可解项。

## 目录结构

```
.
├── index.html                  # 门户：九板块 + 信号 + 读法
├── models.html                 # 01 基模
├── agents.html                 # 02 Agent
├── companies.html              # 03 公司
├── hardware.html               # 04 硬件
├── apps.html                   # 05 应用
├── principles.html             # 06 原理
├── history.html                # 07 历史
├── local.html                  # 08 本地部署
├── cases.html                  # 09 实例索引
├── scheme-*.html / compare.html / gallery.html / bench-h3.html   # 旧路径跳转
├── lab/                        # 实例 01 · 生图实验（自成一套）
│   ├── index.html
│   ├── scheme-*.html
│   ├── compare.html
│   ├── gallery.html
│   └── bench-h3.html
├── assets/
│   ├── css/site.css            # 全站共用样式（系统字体，无 CDN）
│   ├── css/bench.css           # H3 看板样式
│   └── img/                    # WebP，单张 ≤ 300 KB
└── README.md
```

页面内联的原生 JS 只用于案例库的筛选与灯箱，无外部依赖。

## 本地预览

无构建步骤。直接用浏览器打开 `index.html`，或在目录内起任意静态服务器：

```bash
python -m http.server 8000
```

## 设计与技术约束

- 无外部 CDN、无 Web 字体、无框架；只依赖系统字体与原生 HTML/CSS。
- 全站浅色监控台风格：浅灰底、白卡、细线、等宽数字；强调色只用于状态与关键数字。
- 统一顶部导航（九板块）、二级锚点导航、面包屑、翻页与页脚。
- 图片统一 WebP，质量按体积梯度控制，单张 ≤ 300 KB。
- 响应式：桌面三列卡片墙，移动端单列，390 px 宽度无横向溢出。

## 隐私与收录

- 页面不出现本机绝对路径与用户名，路径统一脱敏。
- 不收录可能涉及成人向、露骨或明确版权角色的图；只用原创科幻角色的技术对照与静物样张。
- 不发布台账中的个人路径字段与本地数据库。

## 许可

站点文案与排版：CC BY 4.0。图片为个人项目测试产物，仅用于技术展示，不授权商用或二次分发。
