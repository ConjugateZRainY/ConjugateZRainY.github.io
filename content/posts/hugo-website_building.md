---
date: '2025-07-15T22:20:41+08:00'
draft: false
title: 'HUGO + GitHub Pages 搭建个人博客'
---

HUGO 搭建个人博客已经相当成熟了。挂载到 GitHub Pages 相当方便。这里面还是有几点值得注意的地方。

# 阅读 HUGO 和 PaperMod 的官方文档

HUGO 和 PaperMod 的具体安装操作在其各自的网站上都有详细的说明。HUGO 是有一些并不广为人知的更新的。例如 MathJax v3 的配置已经更新在 HUGO 的 Docs 之中了，然而目前网络上流传的都还是几年以前的信息。

# 不要直接更改 themes/PaperMod 之中的文件

例如，并不是直接更改 `themes/PaperMod/layouts` 之中的文件，正确的操作是在和 `themes` 同级的 `layouts` 之中建立同样结构的文件夹，并从 `themes/PaperMod/layouts` 之中复制文件到 和 `themes` 同级的 `layouts` 对应的文件夹之中。

# MathJax 的配置

```html
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
<script>
  MathJax = {
    tex: {
      displayMath: [['\\[', '\\]'], ['$$', '$$']],  // block
      inlineMath: [['\\(', '\\)']],                  // inline
      packages: {"[+]": ["ams"]}
    },
    loader:{
      load: ['ui/safe']
    },
  };
</script>
```

# 显示问题

本地显示中，Safari 无法显示网页的 icon，而 Chrome 则完整显示。这一部分目前更改不了。