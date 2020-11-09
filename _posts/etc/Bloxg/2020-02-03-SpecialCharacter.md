---
date: 2020-02-03 20:23
title: 수식 및 특수문자 입력하기
category: Blog
# permalink: /blog/mathjax
tags: markdown mathjax
# published: false
---
# MathJax

## 설정 방법

### Tistory
- 스킨 수정 > HTML 편집 > HTML 파일에 입력
  : `<header>...</header>` 사이에 아래의 `<script>...</script>` 구문을 붙여넣기 후 '적용'

```html
<head>
    <!-- MATHML -->
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
        tex2jax: {inlineMath: [['$','$'], ['\(','\)']]}
        });
    </script>
    <script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML' async></script>
</head>
```

### Jekyll-TeXt-Theme  
- _includes/markdown-enhancements/mathjax.html
  - inlineMath : 1줄 코드 입력을 위한 설정
  - displayAlign : 수식 정렬 설정
  - displayIndent : 들여쓰기 설정

```html
{%- raw -%}
{%- include snippets/get-sources.html -%}
{%- assign _sources = __return -%}

{%- include snippets/assign.html target=site.data.variables.default.mathjax_autoNumber source0=site.mathjax_autoNumber source1=page.mathjax_autoNumber -%}
{%- assign _mathjax_autoNumber = __return -%}

<script type="text/x-mathjax-config">
	var _config = { 
		tex2jax: {
			inlineMath: [['$','$'], ['\\(','\\)']]
		},
		displayAlign: "left",
		displayIndent: ".5em"
	};
	{%- if _mathjax_autoNumber == true -%}
		_config.TeX = { equationNumbers: { autoNumber: "all" } };
	{%- endif -%}
	MathJax.Hub.Config(_config);
</script>
<script type="text/javascript" src="{{ _sources.mathjax }}" async></script>
{% endraw %}
```

## 사용법

> REF
> 
> - [Help:LaTeX Symbol Tables - Mathematics](https://wikieducator.org/Help:LaTeX_Symbol_Tables_-_Mathematics)
> - [수식 입력기](https://www.codecogs.com/latex/eqneditor.php)

- inline  
  $\chi^2$분포 확률변수 $\sum\_{i=1}^{n}\chi\_i^2$의 분포
    
- 기본  
  $$\sum\_{i=1}^{n}\chi\_i^2$$  
  $$  
  \because s\_d = \sqrt{\frac{\sum (d - \bar{d})^2}{n -1}} = \sqrt{\frac{\sum (y - \bar{y})^2}{n -1}} = s\_y  
  $$
    
- 줄바꿈 : `\\` \< 2개 입력해야 작동함  
  $$  
  s\_d = s\_y \\
  \because s\_d = \sqrt{\frac{\sum (d - \bar{d})^2}{n -1}} = \sqrt{\frac{\sum (y - \bar{y})^2}{n -1}} = s\_y  
  $$
    
  ```
  $$
  s_d = s_y \\
  \because s_d = \sqrt{\frac{\sum (d - \bar{d})^2}{n -1}} = \sqrt{\frac{\sum (y - \bar{y})^2}{n -1}} = s_y
  $$
  ```
    

# 그리스 문자 입력

|대문자|소문자|발음|대문자 코드|소문자 코드|소문자 수식|
|:-:|:-:|:-:|:-:|:-:|
|Α|α|Alpha : 알파|`&Alpha;`|`&alpha;`|`\alpha`
|Β|β|Bet(a) : 벳/베트/비타|`&Beta;`|`&beta;`|`\beta`
|Γ|γ|Gamma : 감마|`&Gamma;`|`&gamma;`|`\gamma`
|Δ|δ|Delta : 델타|`&Delta;`|`&delta;`|`\delta`
|Ε|ε|Epsilon : 엡실론 / (미국 가끔)엡사일론|`&Epsilon;`|`&epsilon;`|`\epsilon`
|Ζ|ζ|Zet(a) : 젯/제트/지타|`&Zeta;`|`&zeta;`|`\zeta`
|Η|η|Eta : 이타|`&Eta;`|`&eta;`|`\eta`
|Θ|θ|Theta : 씨타|`&Theta;`|`&theta;`|`\theta`
|Ι|ι|Iota : 요타 / (미국 가끔)아요타|`&Iota;`|`&iota;`|`\iota`
|Κ|κ|Kappa : 카파|`&Kappa;`|`&kappa;`|`\kappa`
|Λ|λ|Lambda : 람다|`&Lambda;`|`&lambda;`|`\lambda`
|Μ|μ|Mu : 뮤|`&Mu;`|`&mu;`|`\mu`
|Ν|ν|Nu : 뉴|`&Nu;`|`&nu;`|`\nu`
|Ξ|ξ|Xi(s/z/ks/gz)aɪ☜자이|`&Xi;`|`&xi;`|`\xi`
|Ο|ο|Omicron : 오미크론 / (미국 가끔)오마이크론|`&Omicron;`|`&omicron;`|`\omicron`
|Π|π|Pi : 파이|`&Pi;`|`&pi;`|`\pi`
|Ρ|ρ|Rho : 로|`&Rho;`|`&rho;`|`\rho`
|Σ|σ|Sigma : 사이마/시그마|`&Sigma;`|`&sigma;`|`\sigma`
|Τ|τ|Tau : 타우 (불어)또|`&Tau;`|`&tau;`|`\tau`
|Υ|υ|Upsilon : 윕실론 (미국 가끔)업사일론|`&Upsilon;`|`&upsilon;`|`\upsilon`
|Φ|φ|Phi : 파이|`&Phi;`|`&phi;`|`\phi`
|Χ|χ|Chi : 카이|`&Chi;`|`&chi;`|`\chi`
|Ψ|ψ|Psi : 싸이(영어라서 Psy 같은 발음)|`&Psi;`|`&psi;`|`\psi`
|Ω|ω|Omega : 오메가 / 오미가|`&Omega;`|`&omega;`|`\omega`

> **REF**  
> [LaTex 기호 모음](https://jjycjnmath.tistory.com/117)  
> [티스토리에-MathJax로-포스팅하기](https://kshoon92.tistory.com/entry/%ED%8B%B0%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%97%90-MathJax%EB%A1%9C-%ED%8F%AC%EC%8A%A4%ED%8C%85%ED%95%98%EA%B8%B0)  
> [마크다운과 수학 표현식이 만나다](%5Bhttp://pad.haroopress.com/page.html?f=mathematics-expression%5D(http://pad.haroopress.com/page.html?f=mathematics-expression))