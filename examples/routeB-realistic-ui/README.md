# 范例 · Route B 拟真界面动画（扒真字体 + 真图标 + 子合成组装）

**这不是第 4 个主题**，而是 `references/realistic-ui-and-web.md` 的 **Route B（真界面做成动画）** 的一条已渲染验证片。
外壳调性走的是 **warm / Claude Design**（暖橙 `#CC785C` + 米底 + 衬线感），整片用「真界面动画」技术做出来。

成片：`ai-report.mp4`（18s 竖屏 1080×1920，含音轨）。选题：**「跟 AI 说一句话，它就把周报写好了」**。

## 结构（这就是 Route B 的标准长相）
```
index.html              ← 总装：只引子合成 + 做接缝转场 + 挂音频轨
page1-input.html        ← 子合成①：输入页（光标打字 → 点发送）
page2-thinking.html     ← 子合成②：思考页（骨架屏微光 + 三点脉冲）
page3-result.html       ← 子合成③：结果页（周报卡逐条生成 → 点复制 → 已复制）
fonts/  HankenGrotesk-*.woff2   ← 扒来的「真字体」本地 woff2（Grok 真用的 Hanken Grotesk）
fonts.css                       ← 对应的本地 @font-face（已内联进每个子合成，这份是备份）
icons/  *.svg                   ← 扒来的「真图标」（Phosphor 真图标库，内联进页面）
audio/  bgm/click/type.mp3       ← 可选音效（ffmpeg 合成；点击声/打字声/BGM）
```

## 五个关键手法对应到代码
1. **扒真字体** → `fonts/` 里的本地 woff2 + 每个子合成 `<style>` 内联的 `@font-face`（中文走 Google Fonts 的 Noto Sans SC `<link>`，字体栈 `'Hanken Grotesk','Noto Sans SC'` 自动按字形回退）。
2. **真图标** → 每个页面里 inline 的 `<svg viewBox="0 0 256 256">`（直接来自 Phosphor，没自己画）。
3. **每页一个子合成** → 三个独立 `pageN-*.html`，各自 `<template id><div data-composition-id><script> 自己的时间轴 → window.__timelines["pN"]=tl</script>`。
4. **接缝转场组装** → `index.html` 的 `<div data-composition-src="pageN.html" data-start data-duration data-track-index>` + 顶层时间轴只控 section 的 opacity/scale/blur（crossfade、zoom-through）。section 之间**故意留 ~0.3s 重叠**才能交叉淡。
5. **假鼠标 + 音效（可选）** → 各页里的 `#cursor` SVG（GSAP 动 left/top + 点击缩弹）；`index.html` 的 `<audio data-start data-volume>` 分轨。

## 怎么复用
做新的拟真界面片：照这套改 —— 换真站(扒它的字体+图标)、换页面内容、换分场。渲染：
```bash
cd <目录> && npx hyperframes render . -o out.mp4 -w 1 --resolution portrait
```
⚠️ 子合成嵌套渲染在当前 HF 版本可用（本片已验证）；子合成里的资源路径相对**子合成文件**所在目录，所以 `fonts/`、`audio/` 与 `index.html` 同级即可。
