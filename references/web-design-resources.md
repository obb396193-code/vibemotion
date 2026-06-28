# 前端设计资源 · 借鉴入口（做片时来这找参考）

> 🔴 **借鉴铁律(先懂这条)**：这些是**网页**资源。**外观 / 结构 / 审美方向能借;动效本身不能直接搬**——HF 视频是把暂停的 GSAP 时间轴逐帧 seek 截图,CSS transition/animation、framer-motion、滚动·hover 触发的动效**渲染时是死的**。要那个效果,就用 **GSAP timeline 重写**。
> 一句话:**借"长什么样"和"动效创意",不借"会自己动的代码"。**

## A. 组件库(借外观 + 借动效创意)
| 站 | 入口 | 借什么 / 注意 |
|---|---|---|
| **shadcn** | ui.shadcn.com · github.com/topics/shadcn | 无动效结构组件——做拟真界面抄它的 **HTML/CSS**(shadcn 是 React,HF 用不了 JSX,要把渲染出的 DOM/CSS 扒进合成) |
| **Aceternity UI** | ui.aceternity.com | 聚光/光束/卡片堆/文字特效等创意——借外观,动效用 GSAP 重写 |
| **React Bits** | reactbits.dev | 文字/背景动效创意库。本机有 `reactbits-animator` 技能 |
| **21st.dev** | 21st.dev | 精挑 React 组件/模板(非 AI 生成) |

> HF 取真界面 HTML/CSS 的具体手法(扒真字体+真图标+子合成)见 `realistic-ui-and-web.md` 的 **Route B**。

## B. 灵感库(定调:配色/版式/构图,**不是代码**)
| 站 | 入口 | 用法 |
|---|---|---|
| **Awwwards** | awwwards.com | 最佳网页设计趋势,定"高级感"方向 |
| **Land-book** | land-book.com | 落地页设计灵感库 |
| **Siteinspire** | siteinspire.com | 精选网站灵感 |
| **onepagelove** | onepagelove.com | 单页设计参考 |
| **landing.love** | landing.love | 落地页**动效**灵感(借节奏/点子) |
| **inja** | (见浏览器书签) | 落地页设计灵感 |

## 怎么用(两步)
1. **定调**：做片前去 B 挑 1-2 个方向,喂给 `taste-skill` / `impeccable` / `claude-design-spec.md` 落成规范。
2. **取件**：去 A 挑具体效果 → 用 Route B 把外观扒成 HTML/CSS → **动效用 GSAP 重写**。

> 是「灵感源/起点」,不是上限。挑中的效果重写好、渲染验证过,再进主题/范例库。
