---
date: '2025-07-15T22:20:41+08:00'
draft: false
title: 'HUGO & PaperMod 在 macOS 搭建个人博客（注意事项向）'
---

HUGO 搭建个人博客已经相当成熟了。挂载到 GitHub Pages 相当方便。本次搭建个人博客，主要参考了 [SonnyCalcr's Blog](https://sonnycalcr.github.io/posts/build-a-blog-using-hugo-papermod-github-pages/) （最主要参考文献，深表感谢），[HUGO 官方网页][2] 和 [PaperMod 官方网页][3]，在 YouTube 上相关视频，如 [Getting Started with HUGO](https://youtu.be/hjD9jTi_DQ4?si=X0IAU6-BeV3Ezcv9)。本文档的动机在于说明笔者配置过程之中遇到的问题。

# PaperMod 的官方文档建议 yaml 格式
官方文档：[We’ll be using yml/yaml format for all examples down below, it is recommend to use yaml over toml as it is easier to read.](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/)，所以 HUGO 建站命令是
```bash
hugo new site MyFreshWebsite --format yaml
# replace MyFreshWebsite with name of your website
```
没有添加 `--format yaml`也没关系，在 HUGO 建立的文件夹（在这个官方例子里就是 MyFreshWebsite）中把 HUGO.toml 删除，新建 HUGO.yaml 并添加内容（当然是可以改动的，关键是换成 yaml 语法）
```yaml
baseURL: "https://examplesite.com/"
title: ExampleSite
languageCode: en-us
```

# 博客主目录的 layouts 结构应对应 themes 之中 layouts 的文件夹结构
HUGO 的逻辑是先找博客根目录的，如 layouts 内部的样式文件（*.html），然后再找 themes/PaperMod/layouts 之中的样式文件（这个例子里面主题是 PaperMod）。在自定义主题时，如果直接更改 themes/PaperMod/layouts 内部的主题，这部分内容会在主题（PaperMod）更新时被覆盖。因此，**不要直接更改 themes/PaperMod 之中的文件**。正确的操作是在和 `themes` 同级的 `layouts` 之中建立**同样结构**的文件夹，并从 `themes/PaperMod/layouts` 之中复制文件到和 `themes` 同级的，博客根目录的 `layouts` 内部对应的文件夹之中。

# MathJax 添加 AMS 宏包支持
目前网络上流传的大部分是早期的解决方案。实际上，MathJax v3 的配置已经更新在 HUGO Docs 之中的 [Mathematics in Markdown](https://gohugo.io/content-management/mathematics/#article) 。
```html
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
<script>
  MathJax = {
    tex: {
      displayMath: [['\\[', '\\]'], ['$$', '$$']],  // 行间显示
      inlineMath: [['\\(', '\\)']],                 // 行内显示
      packages: {"[+]": ["ams"]}                    // 添加 AMS 支持
    },
    loader:{
      load: ['ui/safe']                             // 为了安全性，保持默认设置即可
    },
  };
</script>
```

# 本地配置问题

1. 在 macOS 本地使用 `hugo server` 命令时，默认使用 `http` 协议。需要配置证书，具体操作就是使用 brew 安装 mkcert。具体命令如下（记得在博客的目录中运行以下命令）
```bash
brew install mkcert
mkcert -install
mkcert localhost
hugo server --tlsCertFile localhost.pem --tlsKeyFile localhost-key.pem
```
`mkcert localhost`会在当前目录下生成两个文件：localhost.pem (证书) 和 localhost-key.pem (私钥)。最后要记得将生成的证书文件添加到 .gitignore。

2. 本地显示中，Safari 不一定能够正常显示网页 icon，而 Chrome 则完整显示。实际挂载到 GitHub Pages 以后，在线浏览的内容都是正常的。

[2]: <https://gohugo.io> "HUGO"

[3]: <https://adityatelange.github.io/hugo-PaperMod/> "PaperMod Demo"