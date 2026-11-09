# image-gen-lab

本机生图方案的实验档案站。不是选型指南，也不是作品集：记录每套管线**怎么配、跑多快、吃多少显存、在什么图上翻车、为什么被换掉**。

同一台机器、同一批参考图、串行出图。所有耗时与显存都能回到台账、边车或实验日志；取不到的值写 `null`，结构上不存在的写 `"n/a"`，估算值单独标注。

## 页面清单

| 页面 | 内容 |
| --- | --- |
| `index.html` | 首页：方案总览卡片墙、总量指标、口径摘要 |
| `scheme-sdxl.html` | SDXL · Juggernaut-XL v9 —— 历史基线 |
| `scheme-zimage-turbo.html` | Z-Image Turbo —— 当前主力 |
| `scheme-zimage-base.html` | Z-Image Base —— 无独立产出，字段留 `null` |
| `scheme-double.html` | 双采 Base → Turbo —— 已放弃，附 OOM 与机理证据 |
| `scheme-latent.html` | latent 放大链 —— 4096×6144 单张交付 |
| `scheme-krea2.html` | Krea 2 —— 未实测，只列架构与既定参数 |
| `scheme-moss.html` | MOSS-Image —— 测试中，权重下载阶段 |
| `compare.html` | 横向对比：同 prompt / 同 seed 并排 + 对照表 |
| `gallery.html` | 案例库：按方案筛选的图墙，点开看大图与 prompt |

方法论不单独建页：判定口径、三态规则、硬件口径集中在首页 `#method`，各详情页按同一套写。

## 收录的方案

1. SDXL · Juggernaut-XL v9 —— 历史基线，「更锐但更蜡」，已被取代
2. Z-Image Turbo —— 当前主力，8 步 / cfg 1.0
3. Z-Image Base —— 30 步 / cfg 4.0，未单独留档
4. 双采（Base → Turbo 同架构续采）—— 已放弃，OOM 证据见详情页
5. latent 放大链 —— nearest-exact → refine → 4x-UltraSharp → lanczos
6. Krea 2 —— 权重已就位，本批 0 条产出，未实测
7. MOSS-Image —— 权重下载中，测试中

## 目录结构

```
.
├── index.html                  # 首页：方案卡片墙 + 口径摘要
├── scheme-sdxl.html            # 01 SDXL
├── scheme-zimage-turbo.html    # 02 Z-Image Turbo
├── scheme-zimage-base.html     # 03 Z-Image Base
├── scheme-double.html          # 04 双采（已放弃）
├── scheme-latent.html          # 05 latent 放大链
├── scheme-krea2.html           # 06 Krea 2（未实测）
├── scheme-moss.html            # 07 MOSS-Image（测试中）
├── compare.html                # 横向对比
├── gallery.html                # 案例库（筛选 + 灯箱）
├── assets/
│   ├── css/site.css            # 全站共用样式（系统字体，无 CDN）
│   └── img/                    # WebP，单张 ≤ 300 KB
└── README.md
```

页面内联的原生 JS 只用于案例库的筛选与灯箱，无外部依赖。

## 数据来源

- **生成台账**：142 行 × 26 列，字段字典 v1.2（Juggernaut 136 行 + Z-Image 6 行）
- **候选边车**：128 份 JSON，含 prompt、seed、denoise、耗时、显存最低空闲值
- **A/B 对照**：同一 prompt / 同 seed / 同画幅，10 张
- **8K 海报实验日志**：3 个 seed 的 raw 与终图耗时、峰值显存
- **单张耗时样例**：模型常驻后的真实出图成本

峰值显存 = ComfyUI 上报的 `vram_total`（57.84 GB）− 每 2 s 采样的最低 `vram_free`，属于**计算值**，页面上单独标注。

## 判定口径

- 只看服装版型、配色材质、配饰、发型轮廓、体型、义体位置；**不看脸**。
- 脸部只要求气质同档，五官偏差不作为否决项（2026-11-09 起）。
- 「✗」是模型能力边界，不作为调参可解项。

## 三态规则

| 写法 | 含义 |
| --- | --- |
| 真值 | 台账 / 边车 / 日志里实际记录 |
| `null` | 本该有值，但当时未采集 |
| `"n/a"` | 管线结构上不存在该环节（如 t2i 没有参考图） |

页面上的「—」一律表示未采集，不是 0。

## 隐私与收录

- 页面不出现本机绝对路径与用户名，路径统一脱敏。
- 不收录可能涉及成人向、露骨或明确版权角色的图；只用原创科幻角色的技术对照与静物样张。
- 不发布台账中的个人路径字段与本地数据库。

## 本地预览

无构建步骤。直接用浏览器打开 `index.html`，或在目录内起任意静态服务器：

```bash
python -m http.server 8000
```

## 设计与技术约束

- 无外部 CDN、无 Web 字体、无框架；只依赖系统字体与原生 HTML/CSS。
- 深色底、等宽数字、单一强调色（琥珀）。
- 图片统一 WebP，质量按体积梯度控制，单张 ≤ 300 KB。
- 响应式：桌面三列卡片墙，移动端单列，390 px 宽度无横向溢出。

## 许可

站点文案与排版：CC BY 4.0。图片为个人项目测试产物，仅用于技术展示，不授权商用或二次分发。
