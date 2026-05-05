# 不动点定理 · Fixed Point Theorems in Economics

> 经济学中三大不动点定理的交互式教学网页 — Brouwer · Kakutani · Banach
>
> *Continuity gives existence — contraction gives an algorithm.*

一个单文件 HTML 教学项目,用三个交互式可视化讲解经济学中最基础的三个不动点定理,并附带完整的中英双语证明与经济学应用。

A single-file HTML educational project explaining the three fundamental fixed-point theorems in economics — with interactive visualizations, formal proofs, and economic applications, all bilingual.

---

## 概述 · Overview

| 定理 Theorem | 经济学核心应用 Core Application |
|---|---|
| **Brouwer** 布劳威尔 | Walrasian 一般均衡的存在性 (Arrow–Debreu, 1954) |
| **Kakutani** 角谷 | Nash 均衡的存在性 (Nash, 1950) |
| **Banach** 巴拿赫 / 压缩映射 | 动态规划中 Bellman 方程的可解性与值迭代算法 |

每个定理都包含一个**可调参的可视化**、**中英双语直觉解释**,以及**完整的形式化证明**(中英两种证法)和**经济学应用**(含 intuition)。

Each theorem includes an interactive visualization, bilingual intuition, complete formal proofs in both English and Chinese (often via different methods), and a fully developed economic application with intuition.

---

## 特性 · Features

- **纯白主题 + 暗色模式** — 默认跟随系统 `prefers-color-scheme`,右上角按钮可手动切换;选择通过 `localStorage` 持久化
- **MathJax 3 公式渲染** — 所有公式用 LaTeX 编写,academic-grade 排版
- **三个交互可视化** — 纯 Canvas 2D 实现,无外部图形库
- **响应式布局** — 桌面 / 平板 / 移动端均良好适配
- **零构建** — 单文件 HTML,直接打开即可使用

---

## 快速开始 · Quick Start

**本地打开:**

```bash
open fixed_point_theorems.html
# 或双击文件用浏览器打开
```

**部署到静态托管**(GitHub Pages / Netlify / Vercel 等):

```bash
git add fixed_point_theorems.html
git commit -m "Deploy fixed-point theorems page"
git push
```

需要联网以加载 MathJax(从 jsDelivr CDN)。如需离线使用,见下方"离线部署"。

---

## 内容详解 · Content Walkthrough

### 1. Brouwer 布劳威尔不动点定理

**交互:** 拖动红色不动点改变其位置;sliders 控制收缩系数 $\alpha$ 与旋转角 $\theta$。箭头表示位移 $f(x) - x$,在不动点处消失。

**证明方法:**
- *English* — via the no-retraction theorem(借助代数拓扑中"球不可缩到球面")
- *中文* — 基于 Sperner 引理的组合证明

**经济学应用:** 在价格单纯形上构造连续的"价格调整映射",Brouwer 定理保证 Walrasian 均衡的存在。

### 2. Kakutani 角谷不动点定理

**交互:** 调节跳跃位置 $a$、上下分支高度 $b_1, b_2$;勾选"退化为单值函数"可观察 Brouwer 失效——竖直填充消失后,函数与对角线 $y=x$ 不再相交。

**证明:** 经 Brouwer 定理 + simplicial approximation,通过 closed graph 与 convex values 完成极限论证。

**经济学应用:** 有限博弈中,玩家"无差异时混合"使最佳反应成为集合值映射,Kakutani 给出 Nash 均衡的存在性。

### 3. Banach 巴拿赫(压缩映射)不动点定理

**交互:** 点击画布任意位置选择起点 $x_0$,自动播放迭代轨迹 $x_n = T^n(x_0)$ 收敛到唯一不动点;实时显示 $\|x_n - x^*\|$。$L$ 控制压缩强度,$\theta$ 加入旋转产生螺旋收敛。

**证明:** Cauchy 列 + 完备性 + Lipschitz 连续性的标准三步证明,附显式误差界 $d(x_n, x^*) \le \frac{L^n}{1-L} d(x_1, x_0)$。

**经济学应用:** Bellman 算子是压缩常数为 $\beta$(贴现率)的压缩映射,故 Bellman 方程有唯一解,值迭代以几何速率收敛——这是几乎所有动态规划与强化学习算法的理论基石。

---

## 技术栈 · Tech Stack

| 组件 | 用途 |
|------|------|
| HTML / CSS / Vanilla JS | 主体结构、样式、交互 |
| Canvas 2D | 三个可视化的图形绘制 |
| [MathJax 3](https://www.mathjax.org/) (CHTML) | LaTeX 公式渲染 |
| CSS Custom Properties | 主题颜色变量与暗色模式 |
| `localStorage` | 主题偏好持久化 |

**唯一外部依赖** 是 MathJax,通过 CDN 加载:

```html
<script async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
```

---

## 浏览器兼容性 · Browser Support

需要支持以下现代特性:
- ES6+ (箭头函数、模板字符串、`const`/`let`)
- CSS 自定义属性
- `prefers-color-scheme` 媒体查询
- Canvas 2D Context
- `localStorage`

经测试可用版本:Chrome 88+ · Firefox 85+ · Safari 14+ · Edge 88+

---

## 文件结构 · File Structure

```
fixed_point_theorems.html
│
├── <head>
│   ├── MathJax 配置 + CDN 加载
│   └── <style>
│       ├── CSS variables (light + dark + manual override)
│       ├── 排版与布局
│       ├── 公式 / 证明区样式
│       └── 主题切换按钮样式
│
├── <body>
│   ├── 右上角主题切换按钮
│   ├── <header> 项目标题
│   ├── ×3 <section class="theorem">
│   │   ├── 标题(中英 + 编号)
│   │   ├── 交互区:canvas + controls
│   │   ├── 直觉简介(CN + EN 双栏)
│   │   └── 形式化区:Theorem · Proof · Application
│   ├── <footer> 署名
│   └── <script>
│       ├── 主题切换逻辑
│       └── 三个可视化模块(IIFE)
└── (end)
```

---

## 自定义 · Customization

### 修改配色

所有颜色集中在 `<style>` 顶部的 `:root` 与 `[data-theme="dark"]` 块:

```css
:root {
  --bg: #ffffff;
  --accent: #1a3a8f;
  --ochre: #b07d2b;
  --crimson: #b91c1c;     /* 不动点颜色 */
  --teal: #1f6e63;        /* Banach 轨迹颜色 */
  /* ... */
}
```

### 修改可视化默认参数

每个可视化封装在独立 IIFE 中,默认值在顶部定义。例如 Banach:

```js
let L = 0.75;            // 压缩常数
let theta = Math.PI / 4; // 旋转角
const fixedPoint = { x: 0.5, y: 0.5 };
```

### 离线部署

下载 MathJax 至本地并替换 CDN 链接:

```bash
npm install mathjax
# 或直接下载 release 包并解压到 ./mathjax/
```

```html
<!-- 替换为本地路径 -->
<script async src="./mathjax/es5/tex-chtml.js"></script>
```

---

## 配套文档 · Companion Document

仓库中还包含一份 Markdown 版本的完整证明文档 (`fixed_point_theorems.md`),用 LaTeX 数学公式排版,适合作为讲义、笔记或导出 PDF。

A companion Markdown document (`fixed_point_theorems.md`) provides the same proofs and applications in a print-friendly format with LaTeX math, suitable for lecture notes or PDF export.

---

## 致谢 · Acknowledgements

数学内容主要基于以下经典文献:

- L. E. J. Brouwer (1911). *Über Abbildungen von Mannigfaltigkeiten*. Math. Ann.
- S. Banach (1922). *Sur les opérations dans les ensembles abstraits et leur application aux équations intégrales*. Fund. Math.
- S. Kakutani (1941). *A generalization of Brouwer's fixed point theorem*. Duke Math. J.
- J. F. Nash (1950). *Equilibrium points in n-person games*. PNAS.
- K. J. Arrow & G. Debreu (1954). *Existence of an equilibrium for a competitive economy*. Econometrica.

---

## License · 许可

本项目仅供学习与教学使用。If you use this in a course or publication, attribution is appreciated but not required.

---

## 作者 · Author

由 **Karcen Zheng** 制作 · [联系我](https://karcen.github.io/zhengjiacheng.github.io/)

Made by **Karcen Zheng** · [Get in touch](https://karcen.github.io/zhengjiacheng.github.io/)
