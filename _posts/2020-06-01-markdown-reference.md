---
title: MarkDown Reference
author: Luis Quintero
date: 2020-06-01 15:00:00 +0100
categories: [notes, writing]
tags: [others]
---

This Jekyll template totally compatible with Markdown syntax. Now, let's take a look for the text and typography in this theme.

## Emojis 😁

🚧🚧  For example **Work in Progress!** 🚧🚧

---

## Comments in MD

The most platform-independent syntax is

```
(empty line)
[//]: # (This may be the most platform independent comment)

<!-- or like this -->
```

Both conditions are important:

1. Using # (and not <>)
1. With an empty line before the comment. Empty line after the comment has no impact on the result.

## $$\LaTeX$$

LaTeX tests inline $$x = 2 * \sqrt(v)$$

Block:

$$\begin{align*}
    {\alpha}_{j,1}^{temp} &= P[\textbf{X}_1=x_1,S_1=j|\lambda]=q_j b_j(x_1), \quad j=1...N \\
    c_1 &= \sum_{k=1}^{N}  {\alpha}_{k,1}^{temp} \\
     \hat{\alpha}_{j,1} &=  {\alpha}_{j,1}^{temp}/c_1, \quad j=1...N
\end{align*}$$


## Titles

***
# H1

<h2 data-toc-skip>H2</h2>

<h3 data-toc-skip>H3</h3>

#### H4

***

## Paragraph

I wandered lonely as a cloud

That floats on high o'er vales and hills,

When all at once I saw a crowd,

A host, of golden daffodils;

Beside the lake, beneath the trees,

Fluttering and dancing in the breeze.

## Block Quote

> This line to shows the Block Quote.

## Tables

|Company|Contact|Country|
|:---|:--|---:|
|Alfreds Futterkiste | Maria Anders | Germany
|Island Trading | Helen Bennett | UK
|Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy

## Link

[http://127.0.0.1:4000](http://127.0.0.1:4000)

or

<http://127.0.0.1:4000>


## Footnote

Click the hook will locate the footnote[^footnote].


## Image

![Desktop View]({{ "/assets/img/sample/mockup.png" | relative_url }}){:width="50%"}


## Inline code

This is an example of `Inline Code`.


## Code Snippet

### Common

```
This is a common code snippet, without syntax highlight and line number.
```

### Specific Languages

#### Console

```console
$ date
Sun Nov  3 15:11:12 CST 2019
```


#### Terminal

```terminal
$ env |grep SHELL
SHELL=/usr/local/bin/bash
PYENV_SHELL=bash
```

#### Ruby

```ruby
def sum_eq_n?(arr, n)
  return true if arr.empty? && n == 0
  arr.product(arr).reject { |a,b| a == b }.any? { |a,b| a + b == n }
end
```

#### Shell

```shell
if [ $? -ne 0 ]; then
    echo "The command was not successful.";
    #do the needful / exit
fi;
```

#### Liquid

{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}

#### HTML

```html
<div class="sidenav">
  <a href="#contact">Contact</a>
  <button class="dropdown-btn">Dropdown
    <i class="fa fa-caret-down"></i>
  </button>
  <div class="dropdown-container">
    <a href="#">Link 1</a>
    <a href="#">Link 2</a>
    <a href="#">Link 3</a>
  </div>
  <a href="#contact">Search</a>
</div>
```

**Horizontal Scrolling**

```html
<div class="panel-group">
  <div class="panel panel-default">
    <div class="panel-heading" id="{{ category_name }}">
      <i class="far fa-folder"></i>
      <p>This is a very long long long long long long long long long long long long long long long long long long long long long line.</p>
      </a>
    </div>
  </div>
</div>
```


## Reverse Footnote

[^footnote]: The footnote source.
