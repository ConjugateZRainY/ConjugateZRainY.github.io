---
date: '2025-07-15T22:20:41+08:00'
draft: false
title: 'Building a Personal Blog on macOS with HUGO & PaperMod (Tips and Notes)'
---

Building a personal blog with HUGO is now quite mature. Hosting it on GitHub Pages is very convenient. This setup of my personal blog mainly referenced [SonnyCalcr's Blog](https://sonnycalcr.github.io/posts/build-a-blog-using-hugo-papermod-github-pages/) (the primary reference, for which I am deeply grateful), the [HUGO Official Website][2], and the [PaperMod Official Website][3], as well as related videos on YouTube, such as [Getting Started with HUGO](

# PaperMod's Official Documentation Recommends YAML Format
Official documentation: [We’ll be using yml/yaml format for all examples down below, it is recommend to use yaml over toml as it is easier to read.](https://adityatelange.github.io/hugo-PaperMod/posts/papermod-installation/), so the command to create a HUGO site is:
```bash
hugo new site MyFreshWebsite --format yaml
# replace MyFreshWebsite with name of your website
```

It doesn't matter if you didn't add --format yaml. In the folder created by HUGO (which is MyFreshWebsite in this official example), delete hugo.toml, create a new hugo.yaml, and add the content (of course, this can be modified; the key is switching to YAML syntax):
```yaml
baseURL: "https://examplesite.com/"
title: ExampleSite
languageCode: en-us
```

# 博客主目录的 layouts 结构应对应 themes 之中 layouts 的文件夹结构
HUGO 的逻辑是先找博客根目录的，如 layouts 内部的样式文件（*.html），然后再找 themes/PaperMod/layouts 之中的样式文件（这个例子里面主题是 PaperMod）。在自定义主题时，如果直接更改 themes/PaperMod/layouts 内部的主题，这部分内容会在主题（PaperMod）更新时被覆盖。因此，**不要直接更改 themes/PaperMod 之中的文件**。正确的操作是在和 `themes` 同级的 `layouts` 之中建立**同样结构**的文件夹，并从 `themes/PaperMod/layouts` 之中复制文件到和 `themes` 同级的，博客根目录的 `layouts` 内部对应的文件夹之中。

# The Structure of layouts in the Blog's Root Directory Should Correspond to the Folder Structure in themes/layouts
HUGO's logic is to first look for style files (*.html) in the blog's root directory, such as inside layouts, and then look for style files in themes/PaperMod/layouts (in this example, the theme is PaperMod). When customizing the theme, if you directly modify the theme inside themes/PaperMod/layouts, this content will be overwritten when the theme (PaperMod) is updated. Therefore, **do not directly modify files within themes/PaperMod**. The correct operation is to create folders of the same structure in the `layouts` directory at the same level as `themes`, and copy files from themes/PaperMod/layouts to the corresponding folders inside the `layouts` directory of the blog's root.

# MathJax Adding AMS Package Support
Most solutions circulating on the internet currently are early versions. In fact, the configuration for MathJax v3 has been updated in the HUGO Docs under [Mathematics in Markdown](https://gohugo.io/content-management/mathematics/#article) 。
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

Now that MathJax comes to the 4th edition, we can adjust the part of the link as
```html
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@4/tex-mml-chtml.js"></script> 
```

# Local Configuration Issues

1. When using the `hugo server` command locally on macOS, it defaults to the `http`protocol. You need to configure certificates; the specific method is to install `mkcert` using `brew`. The specific commands are as follows (remember to run the following commands in the blog directory):
```bash
brew install mkcert
mkcert -install
mkcert localhost
hugo server --tlsCertFile localhost.pem --tlsKeyFile localhost-key.pem
```
`mkcert localhost` will generate two files in the current directory: `localhost.pem` (certificate) and `localhost-key.pem` (private key)。Finally, remember to add the generated certificate files to `.gitignore`.

2. In local preview, Safari may not necessarily display the website icon correctly, while Chrome displays it perfectly. After actually deploying to GitHub Pages, the content viewed online is normal.

[2]: <https://gohugo.io> "HUGO"

[3]: <https://adityatelange.github.io/hugo-PaperMod/> "PaperMod Demo"