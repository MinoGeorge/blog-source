+++
date = '2025-02-24T21:20:49+08:00'
draft = false
title = '在博客文章中使用LaTeX'
tags = ['Learning','Blog','LaTeX']
weight=1
+++

最近需要整理一些学习资料，理科又不可避免的要用到一些数学公式，生成公式的图片太过麻烦并且不好整理文件，不如为Papermod添加公式显示功能。  

像是这样（块状公式）
`$$\boldsymbol{x}_{i+1}+\boldsymbol{x}_{i+2}=\boldsymbol{x}_{i+3}$$`

那么，对于行内公式：`$\boldsymbol{x}_{i+1}+\boldsymbol{x}_{i+2}=\boldsymbol{x}_{i+3}$`


# 添加mathjax

定位到`themes\PaperMod\layouts\partials`，然后在该目录下创建文件`mathjax.html`，该文件内容见下：  

```html
<script type="text/javascript"
        async
        src="https://cdn.bootcss.com/mathjax/2.7.3/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[\[','\]\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});

MathJax.Hub.Queue(function() {
    // Fix <code> tags after MathJax finishes running. This is a
    // hack to overcome a shortcoming of Markdown. Discussion at
    // https://github.com/mojombo/jekyll/issues/199
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>

<style>
code.has-jax {
    font: inherit;
    font-size: 100%;
    background: inherit;
    border: inherit;
    color: #515151;
}
</style>

<script src="//yihui.org/js/math-code.js" defer></script>
<!-- Just one possible MathJax CDN below. You may use others. -->
<script defer
  src="//mathjax.rstudio.com/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

```  

# 编辑`extend_head.html`  

在该文件最后添加：

```
{{ partial "mathjax.html" . }}

```

保存即可。

# 使用方法  

以`$a > b,b > c \Rightarrow a > c $`为例子。

首先，根据LaTeX语法，写出表达式`a > b,b > c \Rightarrow a > c `，使用\$符号包裹（前后都有该符号），然后使用反引号包裹即可。





### 参考文章：  

1.The Best Way to Support LaTeX Math in Markdown with MathJax <a href="https://yihui.org/en/2018/07/latex-math-markdown/" target="_blank" rel="noopener">https://yihui.org/en/2018/07/latex-math-markdown/</a>  

2.Hugo博客添加LaTeX语法支持 <a href="https://www.shaohanyun.top/posts/env/hugo_mathjax/" target="_blank" rel="noopener">https://www.shaohanyun.top/posts/env/hugo_mathjax/</a>
