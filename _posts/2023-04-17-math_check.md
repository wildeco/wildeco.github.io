---
title: "Math test"
date: 2023-04-15T15:34:30-04:00
math: true
---

### Latex code is not displaying properly in GitHub pages###



\\(p(\theta) = \mathbf{\prod}_{i,c}p(\mathbf{\theta}^i(c))\\) inline formula  yay
$ f(x) = x^2$ 


$$r = \frac{1}{2}$


$$x = y^2$$  # Katex Method
 
\\(x = y^2\\)  # MathJax method

This sentence uses `$` delimiters to show math inline:  $\sqrt{3x-1}+(1+x)^2$

**Here is some math!**

```math
\sqrt{3}
```


Some references:

https://mathwo.github.io/coverpages/2020-11-11-jekyll-doc-and-my-notes-index

Since the themes are stored in gem files, you can't edit them directly. 

First need locate theme minima files by following command in local repo folder:

```
bundle info minima
```

Then create a new scripts.html file in the _includes folder and added the code as suggested in this post. (Note: there was no scripts.html file so you can delete this if website crashed)

https://www.janmeppe.com/blog/How-to-add-mathjax-to-minimal-mistakes/ 

I had also added `mathjax: true` in the values section in _config.yml file.

Githubpages supports MathJax: 

https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions 