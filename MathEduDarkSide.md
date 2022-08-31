---
jupyter:
  jupytext:
    cell_metadata_json: true
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.10.3
  kernelspec:
    display_name: Julia 1.8.0
    language: julia
    name: julia-1.8
---

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
# 算数数学教育の暗黒面

黒木玄 (Gen Kuroki)

2018-08-21～2018-09-11, 2020-08-28, 2021-09-01, 2022-08-31

* Copyright 2018, 2020, 2021, 2022 Gen Kuroki
* License: MIT https://opensource.org/licenses/MIT
* Repository: https://github.com/genkuroki/HighSchoolMath

このファイルは次の場所できれいに閲覧できる:

* <a href="http://nbviewer.jupyter.org/github/genkuroki/HighSchoolMath/blob/master/MathEduDarkSide.ipynb">算数数学教育の暗黒面 HTML版</a>

* <a href="https://genkuroki.github.io/documents/HighSchoolMath/MathEduDarkSide.pdf">算数数学教育の暗黒面 PDF版</a>

このファイルは<a href="https://julialang.org/">Julia言語</a>カーネルの <a href="http://jupyter.org/">Jupyter notebook</a> である. 自分のパソコンに<a href="https://julialang.org/">Julia言語</a>をインストールしたい場合には

* <a href="http://nbviewer.jupyter.org/gist/genkuroki/81de23edcae631a995e19a2ecf946a4f">WindowsへのJulia言語のインストール</a>

を参照せよ. このファイル中の<a href="https://julialang.org/">Julia言語</a>のコードを理解できれば, <a href="https://julialang.org/">Julia言語</a>から<a href="https://www.sympy.org">SymPy</a>を用いた数式処理や数値計算の結果のプロットの仕方を学ぶことができる.

$
\newcommand\eps{\varepsilon}
\newcommand\ds{\displaystyle}
\newcommand\Z{{\mathbb Z}}
\newcommand\R{{\mathbb R}}
\newcommand\C{{\mathbb C}}
\newcommand\T{{\mathbb T}}
\newcommand\Q{{\mathbb Q}}
\newcommand\QED{\text{□}}
\newcommand\root{\sqrt}
\newcommand\bra{\langle}
\newcommand\ket{\rangle}
\newcommand\d{\partial}
\newcommand\sech{\operatorname{sech}}
\newcommand\cosec{\operatorname{cosec}}
\newcommand\sign{\operatorname{sign}}
\newcommand\sinc{\operatorname{sinc}}
\newcommand\arctanh{\operatorname{arctanh}}
\newcommand\sn{\operatorname{sn}}
\newcommand\cn{\operatorname{cn}}
\newcommand\cd{\operatorname{cd}}
\newcommand\dn{\operatorname{dn}}
\newcommand\real{\operatorname{Re}}
\newcommand\imag{\operatorname{Im}}
\newcommand\Ker{\operatorname{Ker}}
\newcommand\Im{\operatorname{Im}}
\newcommand\Li{\operatorname{Li}}
\newcommand\np[1]{:\!#1\!:}
\newcommand\PROD{\mathop{\coprod\kern-1.35em\prod}}
\newcommand{\stirlingsecond}[2]{\genfrac{\lbrace}{\rbrace}{0pt}{}{#1}{#2}}
$

**謝辞:** このノートの作成にはインターネット上で得た知人との膨大なやりとりの結果理解できたことが含まれている. 1人ひとり名前を挙げることはしないが, 私にたくさんのことを教えてくれた人達にとても感謝している. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}, "toc": true} -->
<h1>目次<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#微積分における記号法について" data-toc-modified-id="微積分における記号法について-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>微積分における記号法について</a></span><ul class="toc-item"><li><span><a href="#微分は分数商ではないのか？" data-toc-modified-id="微分は分数商ではないのか？-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>微分は分数商ではないのか？</a></span></li><li><span><a href="#積分の書き方について" data-toc-modified-id="積分の書き方について-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>積分の書き方について</a></span><ul class="toc-item"><li><span><a href="#積分記号-$\ds\int$-は和を意味する" data-toc-modified-id="積分記号-$\ds\int$-は和を意味する-1.2.1"><span class="toc-item-num">1.2.1&nbsp;&nbsp;</span>積分記号 $\ds\int$ は和を意味する</a></span></li><li><span><a href="#積分を-$\ds\int_a^b\!\!dx\;f(x)$-と書いてもよい" data-toc-modified-id="積分を-$\ds\int_a^b\!\!dx\;f(x)$-と書いてもよい-1.2.2"><span class="toc-item-num">1.2.2&nbsp;&nbsp;</span>積分を $\ds\int_a^b\!\!dx\;f(x)$ と書いてもよい</a></span></li><li><span><a href="#積分で-$dx$-を左側に書くスタイルのメリット" data-toc-modified-id="積分で-$dx$-を左側に書くスタイルのメリット-1.2.3"><span class="toc-item-num">1.2.3&nbsp;&nbsp;</span>積分で $dx$ を左側に書くスタイルのメリット</a></span></li></ul></li></ul></li><li><span><a href="#高校数学における三角函数の微積分は循環論法なのか？" data-toc-modified-id="高校数学における三角函数の微積分は循環論法なのか？-2"><span class="toc-item-num">2&nbsp;&nbsp;</span>高校数学における三角函数の微積分は循環論法なのか？</a></span></li><li><span><a href="#無理式とは根号内に文字を含む式のことなのか？" data-toc-modified-id="無理式とは根号内に文字を含む式のことなのか？-3"><span class="toc-item-num">3&nbsp;&nbsp;</span>無理式とは根号内に文字を含む式のことなのか？</a></span></li><li><span><a href="#単項式は多項式ではないのか？" data-toc-modified-id="単項式は多項式ではないのか？-4"><span class="toc-item-num">4&nbsp;&nbsp;</span>単項式は多項式ではないのか？</a></span></li><li><span><a href="#等式は方程式と恒等式に分類されるのか？" data-toc-modified-id="等式は方程式と恒等式に分類されるのか？-5"><span class="toc-item-num">5&nbsp;&nbsp;</span>等式は方程式と恒等式に分類されるのか？</a></span></li><li><span><a href="#「他方の辺に符号を変えて項を移す」という教え方は教育的に正しいか？" data-toc-modified-id="「他方の辺に符号を変えて項を移す」という教え方は教育的に正しいか？-6"><span class="toc-item-num">6&nbsp;&nbsp;</span>「他方の辺に符号を変えて項を移す」という教え方は教育的に正しいか？</a></span><ul class="toc-item"><li><span><a href="#誤解の例" data-toc-modified-id="誤解の例-6.1"><span class="toc-item-num">6.1&nbsp;&nbsp;</span>誤解の例</a></span></li><li><span><a href="#教科書通りの教え方の問題点" data-toc-modified-id="教科書通りの教え方の問題点-6.2"><span class="toc-item-num">6.2&nbsp;&nbsp;</span>教科書通りの教え方の問題点</a></span><ul class="toc-item"><li><span><a href="#枠で囲まれた「等式の性質」の記述はよろしくない" data-toc-modified-id="枠で囲まれた「等式の性質」の記述はよろしくない-6.2.1"><span class="toc-item-num">6.2.1&nbsp;&nbsp;</span>枠で囲まれた「等式の性質」の記述はよろしくない</a></span></li><li><span><a href="#「どんな等式の性質を使っているでしょうか」という問いもよろしくない" data-toc-modified-id="「どんな等式の性質を使っているでしょうか」という問いもよろしくない-6.2.2"><span class="toc-item-num">6.2.2&nbsp;&nbsp;</span>「どんな等式の性質を使っているでしょうか」という問いもよろしくない</a></span></li><li><span><a href="#「項を移すことができる」と教えることもよろしくない" data-toc-modified-id="「項を移すことができる」と教えることもよろしくない-6.2.3"><span class="toc-item-num">6.2.3&nbsp;&nbsp;</span>「項を移すことができる」と教えることもよろしくない</a></span></li></ul></li></ul></li><li><span><a href="#問題-6÷2(1+2)=?,-2a÷2a=?-の答えは唯一つに決まるか？" data-toc-modified-id="問題-6÷2(1+2)=?,-2a÷2a=?-の答えは唯一つに決まるか？-7"><span class="toc-item-num">7&nbsp;&nbsp;</span>問題 6÷2(1+2)=?, 2a÷2a=? の答えは唯一つに決まるか？</a></span></li><li><span><a href="#ゼロは倍数ではないのか？" data-toc-modified-id="ゼロは倍数ではないのか？-8"><span class="toc-item-num">8&nbsp;&nbsp;</span>ゼロは倍数ではないのか？</a></span></li><li><span><a href="#括弧やかけ算の式は1つの数量を表すか？" data-toc-modified-id="括弧やかけ算の式は1つの数量を表すか？-9"><span class="toc-item-num">9&nbsp;&nbsp;</span>括弧やかけ算の式は1つの数量を表すか？</a></span></li><li><span><a href="#かけ算の順序が逆の「式」は誤りなのか？" data-toc-modified-id="かけ算の順序が逆の「式」は誤りなのか？-10"><span class="toc-item-num">10&nbsp;&nbsp;</span>かけ算の順序が逆の「式」は誤りなのか？</a></span><ul class="toc-item"><li><span><a href="#掛け算順序問題の実態" data-toc-modified-id="掛け算順序問題の実態-10.1"><span class="toc-item-num">10.1&nbsp;&nbsp;</span>掛け算順序問題の実態</a></span></li><li><span><a href="#掛け算順序問題が生じる原因" data-toc-modified-id="掛け算順序問題が生じる原因-10.2"><span class="toc-item-num">10.2&nbsp;&nbsp;</span>掛け算順序問題が生じる原因</a></span></li><li><span><a href="#かけ算の式が数値や数量ではなく場面を表わすと教えている！" data-toc-modified-id="かけ算の式が数値や数量ではなく場面を表わすと教えている！-10.3"><span class="toc-item-num">10.3&nbsp;&nbsp;</span>かけ算の式が数値や数量ではなく場面を表わすと教えている！</a></span></li><li><span><a href="#掛け算順序固定強制指導には教育的効果がない" data-toc-modified-id="掛け算順序固定強制指導には教育的効果がない-10.4"><span class="toc-item-num">10.4&nbsp;&nbsp;</span>掛け算順序固定強制指導には教育的効果がない</a></span></li><li><span><a href="#1951年の文部省学習指導要領算数科編試案" data-toc-modified-id="1951年の文部省学習指導要領算数科編試案-10.5"><span class="toc-item-num">10.5&nbsp;&nbsp;</span>1951年の文部省学習指導要領算数科編試案</a></span></li><li><span><a href="#100年以上の歴史がある！" data-toc-modified-id="100年以上の歴史がある！-10.6"><span class="toc-item-num">10.6&nbsp;&nbsp;</span>100年以上の歴史がある！</a></span></li><li><span><a href="#パターンマッチ教育の恐怖" data-toc-modified-id="パターンマッチ教育の恐怖-10.7"><span class="toc-item-num">10.7&nbsp;&nbsp;</span>パターンマッチ教育の恐怖</a></span></li><li><span><a href="#パターンマッチ教育の極北" data-toc-modified-id="パターンマッチ教育の極北-10.8"><span class="toc-item-num">10.8&nbsp;&nbsp;</span>パターンマッチ教育の極北</a></span></li></ul></li></ul></div>
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
using Logging; disable_logging(Logging.Warn)
using Printf
using Base64

using Plots
pyplot(fmt=:png)

function showimg(mime, fns...; scale="")
    option = ifelse(scale == "", "", """ width="$scale" """)
    html = ""
    for fn in fns
        open(fn) do f
            base64 = base64encode(f)
            html *= """<img src="data:$mime;base64,$base64" $option />"""
        end
    end
    display("text/html", html)
end

using SymPy
using LaTeXStrings
using SpecialFunctions
using QuadGK
using Elliptic.Jacobi: cd, sn
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 微積分における記号法について

**まとめ:**

* 微分 $\ds\frac{dy}{dx}$ を分数だとみなしてもよい.

* 積分を $\ds\int_a^b\!\!dx\;f(x)$ と書いてもよい.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
### 微分は分数商ではないのか？

>$\ds\frac{dy}{dx}$ は $dy \div dx$ の意味ではないので, 「$dx$ 分の $dy$」と読んではいけない.

と教えている先生が一部にいるようだ. これは本当に正しいだろうか? 微分形式を含む現代数学における**微分**のスタイルを知っていれば, **そのような教え方は誤り**になるので注意しなければいけない.

実際, 高木貞治『<a href="https://www.google.co.jp/search?q=%E9%AB%98%E6%9C%A8%E8%B2%9E%E6%B2%BB+%E8%A7%A3%E6%9E%90%E6%A6%82%E8%AB%96">解析概論</a>』には以下のように書いてある.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/kaisekigairon-bibun1.jpg", scale="70%")
```

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/kaisekigairon-bibun2.jpg", scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
以上のように, 高木貞治『解析概論』には

> 記号 $\ds\frac{dy}{dx}$ において $dx$ および $dy$ が各々独立の意味を有するから, $\ds\frac{dy}{dx}$ は商として意味を有する.

とはっきり書いてある.  高木貞治氏による $dx$, $dy$ の定義は筆者が独立に描いた次の図と本質的に同じである.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/bibun.jpg", scale="30%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
$df$ の定義を $f(x+dx)-f(x)$ とするのではなく, 上の図のように接線上での変位に取ることが, $\ds\frac{df}{dx}$ を真の分数商とみなすときのポイントになる. 数学の定義はこのような「みもふたもない」ものが多い. この図の $df$ の定義を一般化することによって1次の**微分形式**(differential form)が定義される. 微分形式は現代数学における基本的な概念である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
### 積分の書き方について
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
#### 積分記号 $\ds\int$ は和を意味する

積分 $\ds\int_a^b f(x)\,dx$ における $\ds\int_a^b$ と $dx$ をまるで「括弧」と「括弧閉じる」のような記号だとみなすと, それらの記号の由来からかけ離れたニュアンスで記号を使うことになるので要注意である. 

$f(x)$ が閉区間 $[a,b]$ 上の連続函数であれば, 区間 $[a,b]$ を $a=x_0 < x_1 < x_2 < \cdots < x_n=b$ と分割し, $x_i^*\in[x_{i-1}, x_i]$ 達を任意に取って, $\Delta x_i = x_i - x_{i-1}$ とおくと, 

$$
\sum_{i=1}^n f(x_i)\,\Delta x_i
$$

は $\max\{\Delta x_1,\ldots,\Delta x_n\}\to 0$ で収束し, その収束先を(Riemannの意味での)積分と呼び,

$$
\int_a^b f(x)\,dx
$$

と書くのであった. 記号 $\int$, $dx$ はそれぞれ $\sum$, $dx$ に対応している.  $\int$ は縦に長い $S$ で「和」を意味している.  このことを理解していれば, $\int_a^n$ と $dx$ をまるで「括弧」と「括弧閉じる」のように使うのは「おかしい」と感じられると思う.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
#### 積分を $\ds\int_a^b\!\!dx\;f(x)$ と書いてもよい

微積分は多くの分野で使用される基本的なツールになっており, 各分野ごとに記号の使い方の慣習が異なることがある. だから, この手の書き方のスタイルについては寛容な態度を取ることが望ましい. 

ところが, 

>積分を $\ds\int_a^b\!\!dx\;f(x)$ と書いてはいけない.

と教わっている人達がいるらしい.  前節の記号のもとで, 

$$
\sum_{i=1}^n f(x_i)\,\Delta x_i =
\sum_{i=1}^n \Delta x_i\, f(x_i)
$$

であり, その極限が

$$
\int_a^b f(x)\,dx =
\int_a^b\!\!dx\; f(x)
$$

であると了解しておけば, $dx$ を左側に書くスタイルも受け入れ易いと思われる.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
#### 積分で $dx$ を左側に書くスタイルのメリット

例えば, 函数 $g(x)$ に複数回不定積分

$$
g \mapsto \left(x\mapsto \int_a^x g(x')dx'\right)
$$

を作用させた結果を, $dx$ を右側に書くスタイルで曖昧さなく書こうとすると,

$$
\int_a^x\left(
\int_a^{x_1}\left(
\int_a^{x_2}\left(
\int_a^{x_3}
g(x_4)\,dx_4
\right)dx_3
\right)dx_2
\right)dx_1
$$

のように括弧が大量に必要になり, 積分変数 $x_i$ の動く範囲を知るためには括弧の左側と右側の離れた部分を両方確認する必要が生じる.  しかし, $dx$ を左側に書くスタイルであれば

$$
\int_a^x\!\!dx_1
\int_a^{x_1}\!\!dx_2
\int_a^{x_2}\!\!dx_3
\int_a^{x_3}\!\!dx_4\;g(x_4)
$$

とシンプルに書ける. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
$dx$ を左側に書くスタイルで $f^{(4)}(x)$ を4回不定積分してみよう.

$$
\begin{aligned}
f'''(x_3) &= f'''(a) + \int_a^{x_3}\!\!dx_4\; f^{(4)}(x_4),
\\
f''(x_2) &= f''(a) + \int_a^{x_2}\!\!dx_3\; f'''(x_3)
\\ &=
f''(a) + f'''(a)(x_2-a) + 
\int_a^{x_2}\!\!dx_3\int_a^{x_3}\!\!dx_4\; f^{(4)}(x_4),
\\
f'(x_1) &= f'(a) + \int_a^{x_2}\!\!dx_2\; f''(x_2)
\\ &=
f'(a) + f''(a)(x_1-a) + f'''(a)\frac{(x_1-a)^2}{2} 
\\ &+
\int_a^{x_1}\!\!dx_2\int_a^{x_2}\!\!dx_3\int_a^{x_3}\!\!dx_4\; f^{(4)}(x_4),
\\
f(x) &= f'(a) + \int_a^{x}\!\!dx_1\; f'(x_1)
\\ &=
f(a) + f'(a)(x-a) + f''(a)\frac{(x-a)^2}{2} + f'''(a)\frac{(x-a)^3}{3!} 
\\ &+
\int_a^{x}\!\!dx_1\int_a^{x_1}\!\!dx_2\int_a^{x_2}\!\!dx_3\int_a^{x_3}\!\!dx_4\; f^{(4)}(x_4).
\end{aligned}
$$

これを一般化すれば, 積分剰余項付きのTaylorの公式を一般的に証明可能である.  Taylorの公式は「複数回微分して微分した回数だけ不定積分すればもとの函数に戻る」という当たり前の結果に過ぎないこともこれでわかる.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 高校数学における三角函数の微積分は循環論法なのか？

答えは**いいえ**である.

高校数学IIIの教科書には「曲線の長さを速さの積分で表す公式」が書いてある:

$$
L = \int_a^b \sqrt{x'(t)^2+y'(t)^2}\,dt.
$$

その公式を用いて弧度法の意味での角度 $\theta$ を $(x(t),y(t))=(\sqrt{1-t^2}, t)$ から得られる

$$
\theta = F(y) = \int_0^y \frac{dt}{\sqrt{1-t^2}}
$$

で定義したり, $\ds (X(u),Y(u))=\left(\frac{1}{\sqrt{1+u^2}},\frac{u}{\sqrt{1+u^2}}\right)$ から得られる

$$
\theta = G(a) = \int_0^a \frac{du}{1+u^2}
$$

で定義することによって,  高校数学のスタイルそのままの三角函数の定義に基いて三角函数の微積分の理論を展開できるようになる. $\theta = F(y)$, $\theta = G(a)$ の逆函数はそれぞれ $y=\sin\theta$, $a=\tan\theta$ の高校数学教科書における定義そのものになっている.

このようにして, 循環論法に陥らないだけではなく, 高校数学の三角函数の定義をそのまま採用することによって, べき級数による天下り的な定義の採用したり, その他様々な技巧をこらした三角函数の定義を採用する必要はなくなり, さらに楕円函数論にも容易に接続できるような議論の仕方が可能になる.

数学的にはそういう事情になっているので, 数学を本当に理解する気があるならば, どこかで聞き齧った情報に基いて安易に「高校数学における三角函数の微積分は循環論法である」などと言ってはいけない.

実際の理論の展開の仕方の素描を「<a href="https://github.com/genkuroki/HighSchoolMath">高校数学の話題</a>」の方に書いておいたので参照して欲しい.

**補足:** 前者と後者の $\theta$ の表示は

$$
\begin{aligned}
& t = \frac{u}{\sqrt{1+u^2}}, \quad & & y = \frac{a}{\sqrt{1+a^2}}, \\
& u = \frac{t}{\sqrt{1-t^2}}, \quad & & a = \frac{y}{\sqrt{1-y^2}}.
\end{aligned}
$$

という変換によって同値であることも確認できる. 前者の表示における $t$ と $y$ は単位円の右半分上の点の $y$ 座標であり, 後者の表示における $u$ と $a$ は原点と単位円の右半分上の点を通る直線の傾きである. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
plot(size=(400,400), legend=false)
plot!(xlims=(-1.2,1.3), ylims=(-1.2,1.2), aspect_ratio=1)
plot!([-2,2], [0,0], color=:grey, lw=0.5)
plot!([0,0], [-2,2], color=:grey, lw=0.5)
plot!([1,1], [-2,2], color=:grey, lw=0.5)
t = -1:0.001:1
X = @.(√(1-t^2))
Y = t
plot!(X, Y, color=:grey, ls=:dash)
y = 0.6
t = 0:0.001:y
X = @.(√(1-t^2))
Y = t
plot!(X, Y, color=:red)
plot!([0,2], [0,0], color=:black)
plot!([0,2], [0,2y/√(1-y^2)], color=:black)
plot!([0,√(1-y^2)], [y,y], color=:blue)
annotate!(-0.1, y, text("\$y\$", 13, :blue, :center))
annotate!(1.1, 0.95y/√(1-y^2), text("\$a\$", 13, :black, :center))
annotate!(0.8, 0.25, text("\$\\theta\$", 13, :red, :center))
annotate!(-0.1, -0.12, text("\$0\$", 13, :grey, :center))
```

```julia slideshow={"slide_type": "-"}
t, y = symbols("t y", real=true)
integrate(1/√(1-t^2), (t,0,y)) # asin(y) = arctin y になる.
```

```julia slideshow={"slide_type": "-"}
u, a = symbols("u a", real=true)
integrate(1/(1+u^2), (u,0,a)) # atan(a) = arctan a になる.
```

```julia slideshow={"slide_type": "-"}
# 積分変数の変換 t = u/√(1+u^2)

u = symbols("u", real=true)
t = u/√(1+u^2)
simplify(1/√(1-t^2) * diff(t, u)) 
```

```julia slideshow={"slide_type": "-"}
# 積分変数の変換 u = t/√(1-t^2)

t = symbols("t", real=true)
u = t/√(1-t^2)
simplify(1/(1+u^2) * diff(u, t))
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 無理式とは根号内に文字を含む式のことなのか？

高校の数学の教科書を見ると,

>$\sqrt{x+1}$, $\sqrt{2x^2-3}$ などのように根号内に文字を含む式をその文字についての**無理式**といい, $x$ についての無理式で表された関数を $x$ の**無理関数**という. (実教出版『数学III』2009年1月25発行)

のように書いてある. これは**高校の数学の教科書外では通用しない可能性が高い「定義」**である. 

数については, $\sqrt{2}$ などが無理数なだけではなく, $\sqrt[3]{4}$ も無理数だし, $\pi$ のような超越数も無理数である. 数と函数の類似に従えば, $\sin x$ のような超越函数も無理函数と呼びたくなるのだが, 上の定義に従うとそれは不可能になる.

それ以前の問題として, **上に引用した無理式の定義がおそろしくあいまい**である. $\sqrt{\sin x}$ は無理式なのだろうか?

無理式(irrational expression)や無理函数(irrational function)は19世紀の数学の教科書に見付かる用語である. 19世紀の時代遅れなスタイルが伝言ゲームによって21世紀の現代まで伝わっているいるのだろう.

上に引用したような定義になっていない「定義」は数学の本質と無関係である. 数学を教えるときには, 歴史的な経緯や数学とは無関係の「大人の事情」によって不適切な記述が教科書に残ってしまうことがある. 

**数学を教えるときには, 教科書に忠実に従おうとしてはいけない.** 

その理由は単に教科書が誤りを含む可能性があるからだけではなく, 非標準的な用語や非標準的な流儀を採用していることが普通にあって, そのような場合にはそれが非標準的であることがわかるように教えなければいけないからである. 教科書に書いてあることは標準的であることを意味しない. 

場合によっては教える必要がないことが教科書に書いてあることもある. 

数学を教えるときには, 教科書とは独立に何が標準的で何が正しくて何が良い議論の仕方なのかについて知っておく必要がある. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**参考情報:** <a href="https://en.wikipedia.org/wiki/Rational_function">Rational function - Wikipedia</a> には

>The adjective "irrational" is not generally used for functions.

と書いてある. 形容詞「無理」は「函数」には一般的には使用されないらしい. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/adjective-irrational.png", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
以下は

* Silvestre François Lacroix, An Elementary Treatise on the Differential and Integral Calculus, 1816, 720 pages. <a href="https://books.google.co.jp/books?id=px4AAAAAMAAJ&pg=PA206#v=onepage&q&f=false">Google Books</a>

のp.206からの引用. おそらく, irrational function は rational でない function の意味で使われており, 正式に定義して irrational function と書いているのではないと思われる.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/IrrationalFunctions1816.jpg", scale="40%")
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 単項式は多項式ではないのか？

現代における標準的なスタイルでは**単項式は多項式の特別な場合になる.**

しかし, 非常に残念なことに, 中学校と高校の数学の教科書における用語の体系は以下のようになっているように見える.

|中学高校の数学教科書  |現代的に標準的なスタイル|
|:--------------------:|:----------------------:|
|整式                  |多項式|
|単項式                |単項式|
|多項式                |複数の項を持つ多項式|

現代ではほとんどの通信や放送がデジタル化されている. デジタル通信では情報の符号化とプライバシーを守るための暗号の技術が必要になる. それらの技術を理解するためには多項式環の理論も理解しておかなければいけない. そのような実用的な数学を学ぶためには, 現代的には常識的なスタイルの用語法に従う必要がある.

このような事情になっているにもかかわらず, 中学と高校の数学の教科書は19世紀以来の時代遅れのスタイルを採用してしまっている.  

この点は改善されるべきなのだが, そのような改善が行われる目途は現時点ではまったくない.

下の方の画像はGoogle Booksからの引用である. 以下のリンク先で読める:

* James B. Dodd, High School Arithemtic, 1852, 362 pages. <a href="https://books.google.co.jp/books?id=-UIXAAAAYAAJ&pg=PA129&dq=monomial+polynomial#v=onepage&q=monomial%20polynomial&f=false">Google Books</a>

* Elias Loomis, The Elements of Algebra 1870, 281 pages. <a href="https://books.google.co.jp/books?id=FodTAAAAYAAJ&pg=PA45&dq=monomial+polynomial#v=onepage&q=monomial%20polynomial&f=false">Google Books</a>

* Kunihiko Kodaira, Mathematics 1: Japanese Grade 10, American Mathematical Soc., 1996, 247 pages. <a href="https://books.google.co.jp/books?id=nOkrDAAAQBAJ&pg=PA27&dq=integral-expression+monomial+polynomial#v=onepage&q=integral-expression%20monomial%20polynomial&f=false">Googl Books</a>

以下の引用を見れば19世紀には「単項式は多項式ではない」というスタイルで教科書が書かれていたことがわかる. 問題なのはそういう時代遅れなスタイルが21世紀の現代日本の数学の教科書でも採用されていることである. 日本の教科書の英訳を見ると, 19世紀のスタイルをそのまま踏襲しているように見える.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/polynomial1852.jpg", scale="50%")
```

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/polynomial1870.jpg", scale="40%")
```

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/polynomial1996.jpg", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 等式は方程式と恒等式に分類されるのか？

答えは**いいえ**である.  

あらゆる等式は単に「左辺と右辺が等しい」という意味を持つに過ぎない. 

等式を与えただけでその等式が, 方程式になったり, 恒等式になったりするわけではない. 

例えば, 等式 $x=x$ について,

* $x=x$ を満たすすべての実数 $x$ を求めよ.

という問題を考えれば方程式を考えていることになるし, 

* $x=x$ はすべての実数 $x$ について成立している.

と言えば $x=x$ が実数直線上の恒等式であることを主張している. 

等式に含まれる文字が増えた場合も同様である.

例えば, $ax+b=c$ を $x$ に関する方程式とみなすときには, 「$a$, $b$, $c$ が与えられているときに, 等式 $ax+b=c$ を満たす $x$ を求めること」を考えていることになる.

例えば, $ax+b=c$ を $x$ に関する恒等式とみなすときには, 「すべての数 $x$ について等式 $ax+b=c$ が成立するような $a,b,c$ 」について考えていることになる.

等式だけを見て, その等式が方程式であるか恒等式であるかを判定することは不可能である.

しかし, <a href="https://www.google.co.jp/search?q=%E7%AD%89%E5%8F%B7+%E6%96%B9%E7%A8%8B%E5%BC%8F+%E6%81%92%E7%AD%89%E5%BC%8F">「等式 方程式 恒等式」をGoogleで検索</a>すると, 等式の方程式と恒等式への分類にこだわっている解説が多数見つかる.

実はこれもまた「19世紀の時代遅れのスタイルが中学高校での数学教育に残ってしまっている」という問題の一例に過ぎない.

19世紀の教科書には, equations (等式という意味)を identities (恒等式)と conditional equations (条件によって成立したり成立しなかったりする等式, 単に equation と書かれることも多い)に分けて説明するスタイルを採用しているものがあって, そのスタイルが日本語圏の中学高校の数学教育における「等式を恒等式と方程式に分けて説明するスタイル」として生き残っているものだと推測される. 

|19世紀スタイル         | 意味 |
|:---------------------:|:----------------------------------:|
|equation               | 等式 |
|identity               | 恒等式 |
|conditional equation   | 条件によって成立不成立が変わる等式 |

あらゆる等式は単に両辺が等しいことを意味する式(記号列)に過ぎない. 文脈によってニュアンスを変えたい場合に恒等式と呼んだり, 方程式と呼んだりするだけである.

以下の引用は

* C. A. Van Velzer and Chas. S. Slichter, University Algebra, 1892, 732 pages. <a href="https://books.google.co.jp/books?id=rkQ1AQAAMAAJ&pg=PA135#v=onepage&q&f=false">Google Books</a>

のp.135より. 19世紀の教科書による説明.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/equation1892.jpg", scale="40%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
実際には様々な条件が複雑に入り組んだ問題を考えることが多い. 例えば, 

>**問題(<a href="https://www.kahoku.co.jp/special/exam2018_tohokudai/index_sp.html"></a>東北大学入試問題2018年前期日程</a>, 理系\[3\]):** 整数 $a,b$ は等式
>
>$$3^a - 2^b = 1 \qquad\qquad\cdots\cdots\text{①}$$
>
>を満たしているとする。
>
>(1) $a,b$ はともに正となることを示せ。
>
>(2) $b>1$ ならば, $a$ は偶数であることを示せ。
>
>(3) ①を満たす整数の組 $(a,b)$ をすべてあげよ。

これは広い意味での方程式の問題なのだが, **方程式という用語を使ってもこの問題を解くためには役に立たない**. このような問題を解くためには, 

**どのような仮定のもとで, どのような条件を満たす何を求めたいのか？もしくは考えるのか？**

というような普遍的に通用するスタイルを採用する必要がある. 

例えば, (1)では $a$ が0以下の場合に等式①が成立しないことと, $b$ が0以下のとき等式①が成立しないことを示さなければいけない. 

(2)では $b$ が2以上の整数のとき, 等式①を満たす整数 $a$ が偶数でなければいけないことを示さなけばいけない(ヒント: mod 4 で考えよ). 

(3)では(2)を使って $b>1$ の場合に等式①を満たす $a$ をすべて求めなければいけないだろう(ヒント: $a=2k$ のとき①は $3^{2k}-1=2^b$ すなわち $(3^k+1)(3^k-1)=2^b$ と同値になる. $3^k+1$ と $3^k-1$ の最大公約数を互除法で求めよ). $b=1$ の場合は $a=1$ となることがすぐにわかる.

上に述べたような普遍的なスタイルで常に考えるようにすれば19世紀由来の「等式を恒等式と方程式に分類するスタイル」は完全に忘れても大丈夫である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**まとめ:** 中学校と高校の数学の教科書には現代では標準的とは言えない古臭いスタイルが残っている. それらの大部分は19世紀の数学の教科書に由来していると推測される. 教える側は教科書のスタイルに忠実に従うのではなく, 現代において標準的なスタイルが何であるかを理解し, 教科書にある時代遅れのスタイルに注意を払いながら, 生徒に害を与えないように注意深く教える必要がある. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 「他方の辺に符号を変えて項を移す」という教え方は教育的に正しいか？

答えは**教育的には正しくない**である. その理由を以下で説明しよう. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 誤解の例

中学生は「項」や「移す」の意味を正確に理解できない場合がある. 下の方で引用したようなやりとりを見かける.

一般に生徒がどのように誤解しているかを知るにはインターネット上での生徒どうしが勉強を教え合っている場面を検索して見つけるとよい. 多くの場合に教え方に問題があるせいで, 当然のごとく誤解が生じている場合を多数見付けることができる. これを生徒の側の理解力の問題にするようでは教育者として失格になってしまうので注意して欲しい.

**やりとり1:** https://twitter.com/genkuroki/status/999661788890251265 から孫引き

Aさんが正解を解説して曰く
>$4x=-2$<br>
>$x=-2/4$<br>
>$x=-1/2$

質問していたBさん曰く
>4を右に持っていけいいんですね！<br>
>**反対側に数字を動かす時には符号変わるんじゃなかったっけ？**

Bさんは $4x=-2$ の $4$ を右辺に移すときに符号を変える必要があるんじゃないかと誤解していた. そうなってしまう理由は「項」や「移す」の意味を覚え難いからである. 「項を移す」という教え方を全廃すればこのような誤解が生じる恐れはなくなるだろう. $\QED$

**やりとり2:** https://twitter.com/genkuroki/status/999671200023429120

Cさんの答案
>$30x+12y=138$<br>
>$30y+12x=156$<br>
>　　　↓<br>
>$30x+12y=138$<br>
>$-12x+30y=156$<br>
>　　　↓<br>
>　　以下略

Bさんの指摘
>$12x$ の前の**マイナスが違うと思います！**

Cさん曰く
>**＝を跨がず、左辺、右辺内の移項は符号変わらないんですね。**

これも「項を符号を変えて移す」と教えているせいで生じた誤解の例になっている. $\QED$

以上のような誤解が広範に生じていることは

* <a href="https://www.nier.go.jp/tyousakekka/03chuu_chousakekka_houkokusho.htm">平成１９年度　全国学力・学習状況調査【中学校】報告書</a>, <a href="https://www.nier.go.jp/tyousakekka/gaiyou_chuu/19chuu_houkoku4_2.pdf">数学 PDF</a>

のpp.152-153を見ても確認できる.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/19chuu_houkoku4_2_152.png"; scale="50%")
showimg("image/jpeg", "images/19chuu_houkoku4_2_153.png"; scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
$7x=5x+6$ を $7x-5x=6$ に変形する「移項」について「両辺に $5x$ をたした」「両辺に $5$ をかけた」「両辺を $-5$ でわった」と答えた中学3年生が合計で $36.9\%$ (3人に1人超)いた. この調査結果を見れば, 「項を移す」という教え方がひどく失敗していることは明らかだと思われる. 

そもそも, 手際よく計算するためにも「項を移す」という考え方をする必要は一切ない. 「両辺に同じ項を足す(から同じ項を引く, 項の個数は複数でもよい」という基本に忠実な考え方さえあれば十分である. それだけで十分なのに, 「項が移動する」という見方に誘導して基本に忠実な考え方を上書きしようとするから教育に失敗してしまうのである.

**注意:** <a href="https://www.nier.go.jp/14chousakekkahoukoku/report/middle/math/"></a>平成26年度の調査</a>では「移項が行われているのは，どの式からどの式に変形するときですか」というスタイルの問題が出されていて, 正答率が $90.0\%$ と高くなっているが, この事実は「移項の教育が改善したこと」を意味**しない**。なぜならば, どこで移項をしたかを問う問題と, 移項がどのような理由で可能なったかを問う問題では難易度が大きく違うからである. 理由を問う方が問題の難易度は高く, 単に「項を移すこと」ができるだけでは理解したとは言えず, 理由を答えられるかどうかを問う問題の方が調査的には重要である. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 教科書通りの教え方の問題点

以下の教科書からの引用はすべて

* https://twitter.com/sekibunnteisuu/status/999430597222121472

からの孫引きである. 学校図書の数学教科書『中学校数学1』より.

#### 枠で囲まれた「等式の性質」の記述はよろしくない
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/gakkotosho-iko1.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
「等式の性質」というタイトルを付けて枠で囲んで目立つように説明してある部分が不適切である.

等式の性質は「両辺が完全に等しい」という意味から自然に導かれる. 枠の内側にある加減乗除に制限した結果のみが等式の性質ではないし, 枠外にある「A=BならばB=A」も当たり前に等式の性質である. わざわざ枠で囲んで等式の性質の中から極めて特殊なものを選んでそれに「等式の性質」という名前を付けることは生徒に間違った印象を与えてしまうことになるだろう. 

こういう教え方をするから, 実際には平易な事柄が難しく感じられるようになってしまうのである.

**等式の性質の復習:** 等式の最も基本的な性質は

(1) $A=A$.

(2) $A=B$ ならば $A$ と $B$ は完全に同じ性質を満たしている($A$ を $B$ で置き換えられる).

のである. (1)より $A+C=A+C$ となり, (2)より $A=B$ ならば右辺の $A$ を $B$ で置き換えることで $A+C=B+C$ が得られる.  $A=B$ ならば等式の両辺に同じ操作 $f$ を施した結果 $f(A)=f(B)$ も常に成立する. (2)より $A=B$ ならば $A=A$ の左辺の $A$ を $B$ で置き換えることができるので $B=A$ が得られる. これで $A=B$ ならば $B=A$ が証明された. これらの議論を見れば上の(1),(2)が等式の基本性質であることを納得できると思う. 形式化された記号論理学でも同様の考え方で等号の性質を公理化する. $\QED$

「$A=A$ である」ことと, 「$A=B$ ならば $A$ と $B$ は完全に同じ性質を満たす」という「等しい」ならば当然成立するべきことさえ知っていれば, 等式の性質はそこからすべて導きだされる.

等式の変形における基本は「両辺に同じ操作を施しても等式は保たれる」ということである. 四則演算だけに限定する必要はない.  例えば, $A=B$ ならば両辺を $2$ 乗して $A^2=B^2$ も成立するし, $A=B$ がともに0以上の実数ならば $\sqrt{A}=\sqrt{B}$ も成立する.

#### 「どんな等式の性質を使っているでしょうか」という問いもよろしくない
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/gakkotosho-iko2.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
わざわざ枠で囲んで①から④まで番号を付けた「等式の性質」を使わずに, 「両辺に同じ操作を施しても等式は保たれる」という「等しい」の意味から当たり前のことを使うだけなのに, 「どんな等式を使っているのでしょうか」と聞いてしまっているので, 生徒は「等式の性質の◯番を使いました」などと答えなければいけない気持ちにさせられる可能性がある.

しかも, この教え方は, 生徒が

* 等式 $x-9=3$ の両辺に $9$ を足して等式 $x=12$ を得た.

* 等式 $2x=6+x$ の両辺から $x$ を引いて等式 $x=6$ を得た.

のように言えることを目標にしているのではない!

生徒には

* 等式 $x-9=3$ の左辺の $-9$ が消えて右辺に $+9$ が現われる.

という見方をさせようとしている!

このような教え方をするから, 上の方で実例を引用したような誤解をする生徒が出て来るのである.

* $x-9=3$ の両辺に $9$ を足せば $x=12$ となる.

と理解した方が普遍的に正しい考え方をし易くなるし, 計算も十分に効率的である.

#### 「項を移すことができる」と教えることもよろしくない
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/gakkotosho-iko3.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
以上で引用したように, 教科書では

>等式では, 一方の辺にある項を, 符号を変えて他方の辺に移すことができる。<br>
>このような操作を, **移項**という。

という結論になっている. これと

* 両辺に同じ操作を施しても等式は等式のままになる.

* 例えば, 等式に両辺に同じものを足すと別の等式が得られ, 等式の両辺から同じものを引いても別の等式が得られる. 等式の両辺に同じ数をかけたり, 両辺を同じ数で割っても同様である. 両辺が分数なら両辺の分母分子をひっくりかえしても等式は保たれる.  他にも多数の例がある. 

と比較すると, 多くの点で「一方の辺にある項を, 符号を変えて他方の辺に移すことができる」は誤解を招き易い. 

まず「項」という言葉が難しい. 上の方では $4x=-2$ の左辺の $4$ を左辺の項だと誤解している例を紹介した. 

さらに「一方の辺にある項を他方の辺に移す」の部分を忘れて, $30y+12x$ の $12x$ の項を符号を変えて移して $-12x+30y$ としている例も紹介した.

* 等式の両辺に同じ操作を施せば別の等式が得られる.

という普遍的に通用する原理と比較すると「移項」の説明は圧倒的に複雑である. 

もしもその複雑な説明の内容をマスターすれば「計算が速くなる」というようなメリットがあるならば習得する価値があるかもしれないが, 

* $x-9=3$ の両辺に $9$ を足せば $x=12$ となる.

と比較して,

* $x-9=3$ の左辺の $-9$ を右辺に $+9$ の形で移して $x=3+9=12$ を得る.

が計算法として**「手際が良い」とは決して言えない**. 

**まとめ:** 「項を移す」という教え方のせいで, 文字式の等式の計算がまともにできなくなっている中学生が結構いる.  「$x-9=3$ の両辺に $9$ を足せば $x=12$ となる」のように常に考え, 手際よく計算できるように練習すれば, 「項を移す」という教え方によって生じる害は消え去り, 十分に効率的な計算も可能になる. $\QED$

**注意:** 「項を移す」もしくは「移項」という用語も**便利なので使ってよい**と思う. しかし, 生徒の側にとっては無用でかつ複雑でわかりにくい説明になっている可能性が高いので, 中学生に数学を教えるときにはこのようなことに細心の注意を払うことが必要である. 基本的に教科書に完全に忠実な教え方をすると有害な数学教育になる可能性が高まる. 何が数学的に本質的であるかについて教える側は十分に理解を払い, 無用で害のある考え方を生徒に教え込んでしまわないように注意を払わなければいけない. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 問題 6÷2(1+2)=?, 2a÷2a=? の答えは唯一つに決まるか？

答えは**決まらない**である.

* <a href="https://www.google.co.jp/search?q=%226%C3%B72(1%2B2)%22">6÷2(1+2)をGoogleで検索</a>

「6÷2(1+2)=?」はインターネット上で話題になった問題である.

数式は決められた規則によって解釈されなければいけない. しかし, その規則が決まっていない場合には解釈が唯一つに確定しないことになっていまう. 「6÷2(1+2)=?」はまさにそのような例になっている.

「6÷2(1+2)」には少なくとも「(6÷2)×(1+2)」と「6÷(2×(1+2))」の2通りの解釈があり得る. 前者ならば答えは9になり, 後者ならば1になる. インターネット上では「答えは9」派と「答えは1」派が争うことに成り易いのだが, そのどちらの派閥も間違っていることになる. 解釈が一意に確定しない問題について答えがどちらになるかを争っても無意味である.

「6÷2(1+2)」問題については英語の次のサイトが秀逸である:

* <a href="https://math.stackexchange.com/questions/33215/what-is-48%C3%B7293">What is 48÷2(9+3)?</a>

そこでは**「数学的記号法に最高裁判所は存在しない」**という回答の人気が高い.

世界中に存在する数学ユーザーのあいだで数学記号の使い方の詳細がすべて一致しているわけでもないし, 細かいところまですべてのルールが決められているわけでもない. だから, 数学記号を使って説明する場合には, 世界の数学ユーザーのあいだで標準的に使われている記号やルール以外の記号やルールを使う場合には但し書きを付けておく必要がある. 実際のコミュニケーションでは「その記号の意味は何ですか?」という質問とそれに対する回答が必要になるかもしれない. 実際には数学力が十分であれば文脈で未知の記号の意味を正しく推定できることが多い. 数学力が低い数学ユーザーのためにはできるだけ優しく(易しく)説明した方がよいだろう.

$2a\div 2a$ についても少なくとも $((2\times a)\div 2)\times a$ と $(2\times a)\div (2\times a)$ の2通りの解釈が存在するので, 答えは唯一に確定しない. しかし, 中学校の数学の教科書的には $2a\div 2a$ は $1$ のみが正解であるということになっており, しかも正解をそれに限定するためのルールが教科書では一切説明されていない. そして, 仮にルールが説明されていたとしても, そのルールは単なるローカルルールに過ぎず, 日本の中学校の外では通用しない. ところが, 非常に恐ろしいことに $6ab \div 2a$ のような曖昧な問題は全国の高校入試における定番の問題になっている! 表沙汰になっていない被害者は相当な数にのぼるものと推測される. 

将来, 中学校や高校の数学の先生になった人は, この重大な問題に注意を払い, 世界の数学ユーザーのあいだでは通用していないローカルルールであり, しかも教科書でも明瞭に説明されていないルールを使って, 高校の入学試験の採点を行わないように働きかけて欲しい.

日本語圏において, ただでさえ混乱し易いインターネット上の議論をさらに混乱させたのは, おかしな主張をしている「論文」の存在である. 具体的には次の2つの「論文」の内容には問題がある. 

* \[熊倉2006\] 熊倉啓之, 乗除混合演算式についての理解と指導に関する研究 : A÷B×CとA÷BCのタイプの式に焦点を当てて, 2006. <a href="https://shizuoka.repo.nii.ac.jp/?action=pages_view_main&active_action=repository_view_main_item_detail&item_id=113&item_no=1&page_id=13&block_id=21">リポジトリ</a>

* \[熊倉2016\] 熊倉啓之, 文字式の計算順序に関する指導 : 「かけ算記号省略優先」規則に焦点を当てて, 2016. <a href="https://shizuoka.repo.nii.ac.jp/?action=pages_view_main&active_action=repository_view_main_item_detail&item_id=8171&item_no=1&page_id=13&block_id=21">リポジトリ</a>

\[熊倉2006\]のp.51には次のように書いてある.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/kumakura2006.png"; scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
厳密に言えばこれだけの引用でニュアンスが確定しないが, 以上で引用した部分は「かけ算記号が省略された部分については, 優先して計算を行う」という確固たるルールがあるのにそれを教えないのは「けしからん」というニュアンスの主張であると解釈される.

インターネット上ではこの論文を引用して, 「6÷2(1+2)」における「かけ算記号がされた部分」である「2(1+2)」は「優先して計算を行う」ことになっているので, 答えは1になると主張している人達がいた.

もちろんこのような議論の仕方は誤りである. 「誰かの論文に書いてあること」は「正しいこと」の証拠にはならない. 「論文」に書いてあるか否かではなく, 「証拠」が提出されているかが本質的なのである.

実際には存在しないルールがあたかも当然のルールであるかのように語っている論文を引用して証拠として採用することは単なる権威主義であり, 正誤の問題を議論する態度ではない.

さらに, \[熊倉2016\] には以下に引用するように書いてある.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/kumakura2016-1.png", scale="40%")
showimg("image/png", "images/kumakura2016-2.png", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
「かけ算記号が省略されている場合は, その部分を先に計算する」(規則vi)を使用したときのメリットを4つ述べているので順番にコメントして行こう.

①は確かに正しい. 規則viを使用すれば確かに括弧の使用量を減らすことができる. しかし, 括弧の使用量を減らしたければ, 横線の分数表記 $\ds\frac{3a}{2a}$ を使えばよいだけなので規則viのメリットはほぼない.

②も $\div$ 記号の使用継続にこだわるという不合理な方針を採用しているので, 規則vi採用の合理的な理由として採用できない. 

熊倉氏は横線の分数表記(例: $\ds\frac{b}{c}$)と横に記号を並べる記号法(例: $bc$)を同様に扱いたいようだが, そもそも演算の優先順位の観点から横線の分数表記と横に記号を並べる記号法の仕組みが全く異なることを理解しているのだろうか?

横線の分数表記では横線の長さの分だけひとかたまりとみなされ優先的にその部分が先に計算される. 横に記号を並べる記号法では演算子の優先順位を決めることによって括弧の使用量を減らすことができるように工夫する. 横線の分数表記で括弧が必要がなくても, 横に記号を並べる記号法では括弧が必要になることがあっても何にも問題がない.

③は全くのナンセンス. 

この文脈で, プロセス(過程)は「計算が終わっていない式」というような意味で, プロダクト(結果)は「計算が終わった式」というような意味である.

算数では「36÷12」のような式における36も12も「計算が終わった式」とみなされており, 「36÷12」の全体は「計算が終わっていない式」とみなされる. 例えば「36÷(3×4)」における3×4は「計算が終わっていない式」とみなされる. 算数ではおおむね演算子 $+,-,\times,\div$ を含む式は「計算が終わっていない式」とみなされる.

それとの類似で「3a÷2a」についても教えようというのが③の主旨であると思われる. 

$2a$ の部分には $\times$ という演算子記号が存在しないので, 算数に慣れた生徒が「12」のような「計算が終わった式」とみなすことを期待しているのだろう.

しかし, 数学を正しく理解するためには式を「計算が終わっていない式」と「計算が終わった式」に分類することは有害である. 

式の取り扱いを理解するための基本は「式を目的ごとに適切な形式に等値変形すること」である. 例えば $2a$ は $2\times a$, $a\times 2$, $a+a$, $5a-3a$ のどれとも等しい. 目的によっては $2a$ をもっと複雑な形式に書き直した方がよい場合があるかもしれない. 例えば

$$3a,\quad 5a,\quad 9a,\quad 17a,\quad \ldots$$

は

$$(2+1)a,\quad (2^2+1)a,\quad (2^3+1)a,\quad (2^4+1)a,\quad\ldots$$

と書き直した方が規則性が見易いだろう. 目的ごとにどのような形式に式を整理した方がよいかは大幅に変化する.

他にも, $(x+2)^2 - 1$ は展開した結果を見たいならば $x^2+4x+3$ と変形することになるが, 因数分解された $(x+1)(x+3)$ の形の式が欲しいことは実に多い. 

こういう事情があるので, (式の取り扱いが全般的におかしい)算数教育に過剰に不適切な形で適応してしまったせいで, 演算子が残っているか否かに基いて「計算が終わっていない式」「計算が終わった式」というよろしくない分類をしがちな生徒に対して, そのよろしくない分類を維持させるような教え方をするのは止めた方がよい. 

「計算が終わっていない式」「計算が終わった式」のような分類をしなくてすむような考え方をしっかり教えるように工夫しなければいけない.

算数の教科書通りの教え方では, $6$, $2+4$, $8-2$, $2\times 3$, $12\div 2$ のどれもが完全に同一の数を表す記号列(式)であることを教えない.  そもそもそれらがどれも数を表す記号列(式)であることさえ教えない. この点については後で触れる. 

算数教育における式の取り扱いは全般的にひどいので, 中学校以上の数学教育では算数教育におけるひどいスタイルを積極的に否定して, 上書きして行く必要がある.

もちろん, 本当は算数教育の段階で式の取り扱いを標準的でまともなものに改善することが望ましい. 

例えば, 算数の段階で $9-1$ と $2\times 4$ が完全に同一の数を表す異なる記号列(式)であるとしっかり教えていれば, $(x+2)^2-1$ と $(x+1)(x+3)$ が完全に同一の多項式を表す記号列(式)であることも納得し易いだろう.

現実の数学教育における困難の多くが算数教育における問題のある教え方に起因している.

④ $\ds\frac{a}{2}$ と $\ds\frac{1}{2}a$ は確かに完全に同一の多項式を表す記号列(式)であるが, 前者は $a$ を $2$ で割った結果を意味し, 後者は $1/2$ と $a$ の積である. それらを式の解釈時に使用されるルール(構文解析のルール)で同じように扱う必然性はない. むしろ, 構文解析レベルで異なる扱いを受ける記号列(式)が結果的に同一の数学的対象を表すこともあるという理解をする方が望ましい.

もしも生徒が次のような考え方をしていたら, 教師はそれは誤りだとはっきり指摘しなければいけない. 

**誤った考え方:** $\ds\frac{1}{2}a$ は演算記号 $\times$ 記号を含まないので, $\ds\frac{1}{2}\times a$ と違って計算が終わった式とみなされる. ゆえに $\ds\frac{1}{2}a$ は算数における計算問題の答えと同じように扱ってよい. 算数の計算問題において $12$ が分離できない1つの数とみなされるのと同様に, $\ds\frac{1}{2}a$ も分離できないひとかたまりの式とみなされる. $\QED$

$3a\div\frac{1}{2}a$ の解釈は $\div$ とかけ算記号を省略した並置積表記のどちらの優先順位が高いかを決めないと決まらない. そしてどちらを優先するかに関する標準的なルールは存在しない.

以上のように, 熊倉氏による意見①～④にはまったく説得力がない. 説得力がないどころか, 教育的に有害な意見を述べているようにも見える.

**数学は学校内で使用できればよい知識ではない. 勝手にローカルルールを作ってしまうことのデメリットは大きい. 非標準的なローカルルールを導入して混乱が減ると考えるのは基本的に誤りである.**

岩倉氏の調査でも日本以外では横線の分数表記を主に扱っている教科書が結構多い. そして, 日本でも $\div$ 記号はより高級な数学を学ぶ過程でほとんど使用されなくなる. 中学校以降は $\div$ 記号の使用を止めて, 見易さで優る横線の分数表記に移行するようになっている.

$$
(x^2+1)\div(x^2+x+1) = \frac{x^2+1}{x^2+x+1}
$$

では右辺の書き方の方が一目でどういう意味の式であるかが見易いだろう. $\div$ 記号を使用した式は見易くなく, 人間にとって優しく(易しく)ない.  国際的には, 横線の分数表記を使いたくない場合には, $\div$ ではなく, $/$ を使うことの方が圧倒的に多い. 

中学生にも $\div$ の代わりに横線の分数表記や $/$ を主に使うことを教えた方が標準的な記号法に慣れるという意味で好ましいのではないか?
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## ゼロは倍数ではないのか？

常識的には**0はあらゆる数の倍数**である.

しかし, 実際に算数の教科書を確認すると以下のように書いてある. 以下では東京書籍の算数教科書を引用するが他社の算数教科書についてほぼ同様である. 驚くべきことに

* 0は偶数とします。

* 0は, 倍数には入れないことにします。

と書いてある! **極めて紛らわしい!** 常識的には**0は偶数でかつあらゆる数の倍数**である.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/kyokasho-gusu.jpg", scale="50%")
sleep(0.1); println("上の偶数に関する説明は非常にわかりやすい."); sleep(0.1)
showimg("image/jpeg", "images/kyokasho-baisu.jpg", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
最小公倍数を「0以外の公倍数を最小のもの」と定義しておけば問題ないのに, 「0は, 倍数には入れないことにします」と非常識なローカルルールを宣言しており, しかも**0を含む**数直線上の倍数を丸で囲ませる問題が掲載されている(問題文は引用しなかった次のページにある). そして, 0も丸で囲んだ児童は誤りを指摘され, 消しゴムで囲んだ丸を消すことを要求される. これが日本の算数教育の実態である.

このような事情になっているので, 中学校や高校で数学を教えるときには, 「算数の教科書には非常識なことが書いてあったこと」をはっきり述べて, 「0は倍数には入れない」という誤解を訂正しておかなければいけない. 

さて, それで文科省の立場はどうなのだろうか？ 文科省著作物の学習指導要領解説算数編(学習指導要領そのものと違って『解説』には拘束力はない)には次のように書いてある.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/kaisetsu-baisu.jpg", scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
2008年版(平成20年版)の学習指導要領解説算数編には

>8の倍数は {8, 16, 24, 32, ...} であり, 

と0を倍数から除いてはいるが, 0を倍数に含めていないことは強調していなかった. しかし, 平成29年告示版では括弧の中に0を倍数に含めていないことを強調する但し書きが追加されている. 

おそらく, これによって「0があらゆる数の倍数である」という事実を知らずに一生を終える人が増えてしまうことになるだろう. 

**補足:** 小学校の算数教科書の世界では「偶数であることと1の位が偶数であることは同値である」は正しいが, 「2の倍数であることと1の位が2の倍数であることは同値である」は正しくない主張であることになってしまう. なぜならば $10$ は1の位の0を2の倍数と呼ぶと誤りだとされてしまうからである. $\QED$

**警告:** 平成29年告示版の小学校学習指導要領解説算数編は平成20年版と比較して大幅にページ数が増えているが, 教育的に有害な教え方を示唆している疑いのある記述が大幅に増えており, 小学生に対しておかしな算数の教え方がされる場合が増えることが危惧される. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**参照文献**

* 東京書籍の算数教科書, 新しい算数5上, 平成26年2月28日検定済

* 文部科学省, <a href="http://www.mext.go.jp/a_menu/shotou/new-cs/youryou/syokaisetsu/index.htm">小学校学習指導要領解説</a> 算数編, 平成20年6月

* 文部科学省, <a href="http://www.mext.go.jp/a_menu/shotou/new-cs/1387014.htm">小学校学習指導要領(平成29年3月告示)解説</a> 算数編 

**注意** 学習指導要領と学習指導要領解説を厳密に区別せよ! 学習指導要領は**告示**になるが, 学習指導要領解説は文科省による**著作物**に過ぎず, 法的な拘束力がない. すなわち, 学習指導要領解説に何が書いてあったとしても, それに教育関係者が従う義務はないということである.

実際, 文科省のウェブサイトにある<a href="http://www.mext.go.jp/b_menu/shingi/chukyo/chukyo3/039/siryo/attach/1402682.htm">教育課程部会 教育課程企画特別部会（第8回）配付資料3 学習指導要領（解説）等の位置付けについて</a>には次のように書いてある:

>学習指導要領解説
>
>　（文部科学省著作物）：総則及び各教科、道徳、特別活動について、学校種ごとに、学習指導要領等の改善の趣旨及び内容について解説したもの。
　※　小・中学校について、平成元年までは「指導書」としていたが、**学習指導要領と同様の拘束力を有すると誤解されるとの指摘もあったため、その位置付けを一層明確にする観点から、高等学校と同様に「解説」に改めた**。
 
太字化は引用者による. 「解説」は「拘束力を有する」と誤解されないようにするために付けられた名前である.
 
教育関係者の中には, 「学習指導要領によれば」と言いながら, 「学習指導要領解説」を引用して来る人がいるので注意が必要である. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**資料追加:** 以下は高校の先生と大学の先生の報告の引用である. それぞれ

* https://twitter.com/tsatie/status/799138128619442177

* https://twitter.com/esumii/status/1021326851250065412

より。高校で $-20$ から $20$ までの整数で $5$ の倍数に丸で囲ませたら, $-20,-15,-10,-5$, $5,10,15,20$ と $0$ をとばして丸を付けた生徒が多数いたのだそうだ. 大学の試験の採点をしてみても同様に $0$ を倍数から除いている学生がいたらしい. このどちらも原因は小学校での算数教育だろう. 
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/baisu2.png", scale="50%")
showimg("image/png", "images/baisu1.png", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 括弧やかけ算の式は1つの数量を表すか？

<a href="http://www.edu-ctr.pref.okayama.jp/chousa/study/index.htm">岡山県総合教育センター</a>研究紀要平成18年275号には以下のように書いてある.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/okayama-kakezan.png", scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
「2×4」が8という一つの数を表していることは常識だろう. しかし, 「3+5」も「10-2」も「16÷2」もどれも8という一つの数を表している. だから, 上の引用文はそのような常識的解釈では意味不明の事柄について述べていることになる.

引用されている小学校学習指導要領解説算数編を見てみよう.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/kaisetsu-kakko1.jpg", scale="60%")
showimg("image/jpeg", "images/kaisetsu-kakko2.png", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
確かに「乗法を用いて表された式が一つの数量を表したりする」とはっきり書いてある. しかし, それと乗法を加法よりも先に計算するという規則との関係は曖昧である. 学習指導要領解説算数編の特徴はこのような曖昧な記述である. 学生のレポートならば「もっとクリアに書きなさい」と指導して全文書き直しを命じたくなるレベルで曖昧な書き方になっている.

岡山県総合教育センターではこれを「1つの数量なのだから, 先に計算するのは当然のことになる」と解釈しているようだ.

おそらく解釈は正しいが, その内容は滅茶苦茶である. 「3+2×4」という記号列(式)の構文解析のルールを決めない限り, 「どの部分がひとかたまりだとみなされるか」「どのような順序で計算するか」は決まらない. 乗法を加法より先に計算するという規則は天下り的に与えられる構文解析のルールに過ぎない. 括弧は単にその内側を「ひとかたまり」とみなして先に計算することを指定するための記号に過ぎない.

学習指導要領解説算数編におけるこのようなデタラメな「解説」には片桐重男氏の影響が疑われている. その理由は

* 片桐重男 『算数科の指導内容の体系』 東京、東洋館出版社、2001

に下の方で引用するような説明があるからである. 片桐氏のデタラメな主張がそのまま学習指導要領解説算数編で採用されてしまった経緯はまだよくわかっていない. 

以上のように学習指導要領解説算数編には, 括弧の使い方(単に先に計算したい部分を括弧で囲む)やどうして足し算よりも掛け算を先に計算するか(単なる天下り的なルール)についてデタラメな説明がある. 

中学校や高校で数学を教える人は以上のような事実に注意を払って, 教えている生徒が括弧で囲まれた部分やかけ算やわり算の式が1つの数量を表すと誤解している可能性にも注意を払う必要があるかもしれない. 

式の取り扱いに関して最も基本的な点においても算数教育はおかしなことになっているので注意が必要である.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/katagiri-taikei1.jpg", scale="60%")
showimg("image/jpeg", "images/katagiri-taikei2.jpg", scale="60%")
```

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/katagiri-taikei3.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
以上の片桐氏の本からの引用は

* https://twitter.com/temmusu_n/status/819901948140716032

からの孫引きである.

**以上に引用した片桐重男氏の説はすべてデタラメである.**

**計算の順序に関する規則は単なる約束事に過ぎない.**
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**構文解析に関する補足:** 「$25$ は1つの数なので $5\div 25$ は $(5\div 2)\times 5$ にはならず, $5\div(25)$ の意味になる」という説明の仕方は構文解析的には誤りである. $25$ が1つの数であっても, $(5\div256$ は $(4\div25)6$ の意味にはならないとするべきである.

記号列 $5\div 25$ にどのような計算が対応するかを確定させるためには, 記号列 $5\div 25$ を計算の手続きに変換するためのルールが必要である. そのようなルールを構文解析のルールと呼ぶ.

標準的な構文解析のルールでは, 数字 $0,1,2,3,4,5,6,7,8,9$ が並んでいる部分を1つの数とみなすことの優先順位は高い. 数字が並んでいる部分は最優先に十進法で表わされた数だとみなされる. $\div$ などの演算子と他の記号の結び付きは隣り合った数字どうしの結び付きよりも弱い.

$3+2\times 4$ においては $+$ と $\times$ では $\times$ の方が優先順位が高いので $3+(2\times 4)$ と解釈される. これが普通の説明の仕方である. 標準的ではない構文解析のルールも許すならば, $+$ の優先順位は $\times$ よりも高いとしても矛盾は生じない.

仮に片桐氏的に $2\times 4$ を1つの数とみなしたとしても, $3+2\times48$ を $3+(2\times 4)8$ と解釈されてしまうようでは困るだろう. 記号列(式)を標準的に解釈するためには, 数の並びを十進法での数とみなすことの優先順位が高いという構文解析のルールが必要である.

記号列(式)の解釈では最初に構文解析の手続きが必須であることを理解できずに, 「1つの数とみなされる」というような解釈(意味論)から構文解析のルールが導かれるかのように語っている片桐氏は構文解析に関する教養が決定的に欠けている. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## かけ算の順序が逆の「式」は誤りなのか？

もちろん正解は「誤りではない」である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 掛け算順序問題の実態

これがどのような問題であるかを誤解せずにすむためにはまず次の引用を見て欲しい.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/keirinkan6nen.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
これを見ればわかるように, ある算数教科書出版社は, 文字 $x,y$ を使う小学校6年生の段階になっても, 掛け算の順序が逆ならば誤りとする教え方を教師にすすめる方針になっている. しかも誤りになる理由を

>$x\times 8$ が $8\times x$ になっている場合は, 「8円のノートが $x$ 冊」という意味になってしまうので問題文とは合わない。常に式の意味をしっかり意識させることが大事である。

としている. もちろんこれは完全にデタラメである. $x\times 8$ も $8\times x$ も「$x$ 円のノートが8冊分の代金の**数値**」を正確に表しているので, どちらでも正しい. 算数教育の世界では $x\times 8$ のような式は数値ではなく, **場面**を表している教えていることが多い. 上に引用した事例では「$8\times x$ は8円のノートが $x$ 冊の**場面**を表しているので問題文と合わない」と教えようとしている. もちろん, これは標準的には完全にデタラメである.

**注意:** (教師用)指導書朱註は教科書のマニュアル本のような書籍で「教科書のすべてのページのコピー」と「その上に赤字で印刷された問題の答え」と「解説」で構成されている. 教科書の教師用指導書は教科書出版社による私的な著作物に過ぎない. しかも, 教科書そのものと違って万人の目に晒されていないので, おかしなことがたくさん書いてある. 上の引用部分はその氷山の一角に過ぎない. $\QED$

**注意:** このような話題では, 学習指導要領(文科省告示), 学習指導要領解説(文科省著作物), 教科書の教師用指導書(教科書出版社の私的著作物)を混同してはいけない. $\QED$ 

掛け算の交換法則は小2の段階で習う. 学習指導要領でもそのように決められている.

例えば東京書籍の教科書の小2下の算数教科書では, 5の段と2の段と3の段の九九をやった後の4の段の九九の段階で, 「4×3=3×4」を例に交換法則(可換性)が一般的に成立する仕組みについて学ぶように編集されている.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/tokyoshoseki2b1.png", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
4個を含む集まりが3つある状況はまとめ方を変えれば3個を含む集まりが4つある状況ともみなせることを児童に理解させようとしていると解釈される. 

しかし, その直後のp.21には次のような問題がある.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/tokyoshoseki2b2.png", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
教師用指導書の方では「ずつ」のようなキーワードに下線を引かせて, 「ずつ」がついている数が「1つ分をあらわす数」だと教えることが指示されている.  教科書出版社によれば, 小問2の「しき」の正解は①2×5=10, ②5×2=10であるらしい. 掛け算の式の順序を逆にすると誤りになる.

この授業を受ける小2の児童は掛け算の交換法則が一般的に成立する仕組みを直前に習っている. だから, 「5×2=2×5だから掛け算の順序はどちらでもよい」と正しくてかつ常識的な考え方を児童はできる段階になっている.

実は算数教育界における主流の考え方では, 交換法則を知ってしまった児童が「掛け算の順序はどうでもよい」と考えて**しまわない**ように上のような指導を行うのである.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 掛け算順序問題が生じる原因

そのような指導が行われてしまう根本原因は, 算数教育界における「式」の概念が我々が知っている通常の式の概念と大きく異なっていることである.

算数教育界において「式はどうなりますか？」という問題の正解は「場面を忠実に翻訳して得られる式」になる. しかし, 2×5や5×2のようなこれ以上情報をそぎ落とせないほど簡略化された記号列に「場面を忠実に翻訳」できるはずがない. しかし, それを常にやらせようとしているので, 様々な弊害が生じるのである.

例えば「えんぴつを2人に5本ずつくばる場面」の正しい「式」は「2×5」ではなく、「5×2」になるらしい. 

実は同様のことはすでに<a href="https://togetter.com/li/901635">小1でのたし算の段階から始まっている</a>. 小学校入学前の子の保護者は注意した方がよい.

「2×5」は通常「2個を含む集まりが5つある場面」を表す記号列ではなく, 「2個を含む集まりが5つあるときの全部の個数」を意味している. 「2×5」は場面ではなく, 数を表している.

そして, 等号=は両辺が完全に等しいことを意味し, 「2×5=5×2」は「2個を含む集まりが5つあるときの全部の個数と5個を含む集まりが2つあるときの全部の数が等しいこと」を意味している. そして, 等しくなる理由は「2個を含む集まりが5つあるとき, まとめ方を変えれば, 5個を含む集まりが2つあるともみなせる」からである. 「2×5=5×2」なので「5個を含む集まりが2つあるときの全部の個数」は「5×2」だけではなく, 「2×5」とも表せる.

1つ前の段落で正確に述べた事柄は小学2年生レベルの算数に属する.

しかし, 算数教科書とその教師用指導書に忠実な教え方をされてしまうと, 「2×5」は「2個を含む集まりが5つある場面」を表すかのように教えられることになり, 「2×5」が「10」という記号列で表わされる数の別の表現に過ぎないことが蔑ろにされてしまう.

しかも, その過程で「ずつ」のようなキーワードをひろって単純なパターンマッチングで文章を読むことを教わってしまうので, 児童は「ずつのついている数は掛け算の式で先に書くんだよね」と言うようになる.  そのような文章の読解の仕方は典型的な邪道であり, そのような癖がつくと悪影響は算数だけにとどまらないだろう.

中学校や高校で数学を教える人は, 算数教育での式の取り扱いが非常識な内容になっていることを知っておく必要があると思われる.  中学1年生は「7+5」「15-3」「3×4」「36÷3」のすべてが「12」と表わされる数と同じ数を表していることを全く理解していない可能性が高い. 

その結果として, 等号=が単に「両辺が等しい」という意味を持つことも理解していない可能性が高い. 仮に「2×3」や「3×2」が上で説明したような場面を表しているなら, 「2個を含む集まりが3つある場面」と「3個を含む集まりが2つある場面」は異なるので, 「=」ではなく「≠」でなければいけない. このようにして, 「2×3=3×2」における=を単に「両辺が等しい」の意味に解釈できなくなる.

算数における式の取り扱い方は全般的におかしい.

要するに掛け算順序問題は算数教育における「式の取り扱い方が全般的におかしい」という大きな問題の氷山の一角に過ぎない.

**補足:** 算数の教材における文章題の解答欄は常に「式　　　答え　」の形式になっている. 解答欄の式の項目に書いて正解になる式は「式は場面を表す」というデタラメな考え方に基いて決められている. そして, 教師は児童に「正しい式」を書かせるために, 「ずつ」のようなキーワードに下線を引かせるなどして, 有害なパターンマッチによる「読解」を教えるようになる. このようなことが小学校の6年間ずっと続くのである. この問題は公立私立は関係ない. 算数の教科書に忠実に算数を教えられてしまうとほぼ確実にそうなってしまう. この問題が解決される目途は現時点では全くない. もしかしたら, 「式　　　答え　」という解答欄の形式を廃止することも検討するべきかもしれない. 「考え方　　　答え　」の形式の方が好ましいのではないか? $\QED$
<!-- #endregion -->

### かけ算の式が数値や数量ではなく場面を表わすと教えている！

さらに調査してみると, かけ算を習う小学2年生向けの算数の教科書では「かけ算の式が数値や数量ではなく場面を表わす」と教えるように編集・執筆されていることが分かる. 下の方で証拠となる引用を示しておく.

「5人を含む集まりが3つあるとき, 全体の人数を5×3と表わす」であれば, 5×3が数値・数量を表すことになり, 常識的なかけ算の説明になる.

しかし, 実際には「5人を含む集まりが3つある場面を5×3と表し, 全体の人数が15人になることを, 5×3=15と書く」のように教えているように見える. この教え方では 5×3 は数値・数量ではなく, 場面を表すという非常識な考え方を子供の心に植え付ける教え方になってしまっている. 

この非常識なスタイルの延長線上にかけ算順序固定強制指導があるのである.

```julia
showimg("image/png", "images/sikihabamen01.jpg", scale="80%")
showimg("image/png", "images/sikihabamen02a.jpg", scale="80%")
showimg("image/png", "images/sikihabamen02b.jpg", scale="80%")
showimg("image/png", "images/sikihabamen02c.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 掛け算順序固定強制指導には教育的効果がない

* 若柳町立若柳小学校(当時)の伊藤宏先生による「日常生活の中で計算が活用できる子供の育成を目指した学習指導の一試み――「算数日記」を活用した３年「２位数×２位数」の授業実践を通して――」というタイトルの論文 (<a href="http://mnavidata.edu-c.pref.miyagi.jp/manage/wp-content/uploads/tmpFile/practice_research/01B0010.pdf">PDF</a>)

には次のように書いてある.  調査対象は小3のあるクラスである.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/itohiroshi-fig4.jpg", scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
さて,

>ここに4まいのふくろがあります。かずや君が, 1まいのふくろにりんごを3こずつ入れました。りんごは, ぜんぶでなんごありますか。
>
>①　こたえを出すためのしきを書いてください。

という問題の正解は何だろうか？ 「4×3」は「誤答」とされている. この場合には問題に出て来た数の順番を逆転させて「3×4」としなければいけないらしい. 日本語で書いた文の語順と「正しい」かけ算の順序は無関係である. 以下のルールに従うと確実に掛け算の順序で正解できることが知られている:

* 「ずつ」のついている数を掛け算の式では先に書く. 上の問題の例ならば「3こずつ」とあるので, 3を先に書いて掛け算の式を「3×4」とすれば正解になる.

* 「1あたり」のついている数を掛け算の式では先に書く. 仮に問題文が「1まいあたり3このりんごを入れました」になっていれば3を掛け算の式では先に描けばよい.

* 答えが◯◯個(人, 本, ...)の形式になるならば, 「個」(人, 本, ...)が付いている数を掛け算の式では先に書く. 例えば上の問題では「なんこありますか」と聞いているので「こ」のついている「３こ」の3を掛け算の式では先に書くと正解になる.

もちろん, こんなパターンマッチのルールを覚えても掛け算のことは何も理解できない. 理解せずに掛け算の式では丸をもらえるようになるだろう.

問題文に出て来た数値を逆順で書いた「3×4」(正解, 8名)と問題文に出て来た数値の順に書いた「4×3」(誤答, 21名)では後者の方が圧倒的に多数派である. しかし, 児童が書いた掛け算の順序の違いと, 絵を描く問題の正解率は同じである(おそらくどちらも $100\%$).

「3×4」または「4×3」と式を書いた児童の29名と「絵に正しく表すことができた児童」の合計29名は一致している可能性が高い. 仮に一致していなくても, 「4+2」「4-1」「1+3」と式を書いた4名の児童は「絵には正しく表すことができなかった児童」だったと推測されるので, 違いは1名以下だと推測される.

この調査結果は, 小3児童が掛け算の順序をどのように書いたかと, 問題文の内容を正しく絵に表すことができたかは全く関係が無さそうなことを強く示唆している. 現実の児童に関しては「文章題の読解では掛け算の順序は大事である」というような主張が誤りであるようだ.

誤答の様子を眺めると, 絵を正しく描けなかった児童は「4+2」「4-1」「1+3」と式を書いていると推測され, そもそも問題文の意味を何も理解できていない可能性が高い.  児童にとって重要なのは掛け算順序ではなく, 文章の読解力であるように見える.

このような調査結果を得たならば, 掛け算順序固定強制指導を行ってもメリットがなく, 単に有害なだけであり, 文章の読解力にもっと力を入れた方が良さそうだと気付きそうなものだが, 調査を行った伊藤宏先生は次のように書いている.

>このことは, 文章の意味は分かるのだが, 乗法の意味が明確に理解できていないということを示している. ～中略～ 問題の文章構成に惑わされることなく, 乗法を使った正しい立式ができるようにしていく必要がある.

このような先生の発言中の「乗法の意味」は実質的に「掛け算の順序」を意味している. 児童がどのような掛け算の順序で式を書いたかと文章題の読解は無関係であることが判明しても, 児童が「乗法の意味」＝「掛け算の順序」を理解していないことを問題にしなければいけないとしているのである. そのような無駄で有害な事柄に時間を割く余裕があるなら, 「4+2」「4-1」「1+3」と答えた児童のケアにコストを割くべきである. それが教育というものだろう.

このような事例は「算数教育に詳しい人達」に関しては普遍的である. 「掛け算の順序」を文章題の読解などのために便宜的に利用しようとしているのではなく, 「掛け算の順序」を児童に理解させなければいけないと信じているので, そのように教えようと頑張るのである.

これが現実であり, この現実を認めた上で, 現実の算数教育を社会的に厳しく批判して行く必要がある.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 1951年の文部省学習指導要領算数科編試案

「掛け算順序が逆ならば掛け算の意味を理解していない」(「掛け算の意味」＝「掛け算の順序」なのでほとんどとーろろじー)とする教え方の由来はまだ完全にはわかっていない. しかし, 1951年の「<a href="https://www.nier.go.jp/guideline/s26em/index.htm">小学校学習指導要領 算数科編 (試案) 昭和26年(1951)改訂版 文部省</a>」には下の方に引用するよう書いてあることはわかっている. そこに書いてある内容は現代における掛け算順序固定強制指導の内容とほぼ同じである. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
「<a href="https://www.nier.go.jp/guideline/s26em/chap4-1.htm">Ⅳ．算数についての学習指導法</a>」より(**太字**の強調は引用者による)
>(３)　計算などについて，理解をもたせる
>
>　「一冊５円のノートを，６冊買ったら，いくら支払えばよいでしょう。」という問題を解くときには，「５円×６」として，その結果を求めるのが普通である。ところが，この問題を，**「ノートを６冊買いました。どれも１冊５円でした。ぜんぶでいくら支払ったらよいでしょう。」とすると，「６×５＝30(円)」として結果を求めるこどもがでてくる**であろう。
>
>　**こどもが，このような誤った解決をするのは，かけ算の意味をひととおり理解しているにしても，その理解が形式的になっていることを示している**といえる。
>
>　問題が，どんな形式で出されようとも　また，いくつかの条件がどんな順序で書いてあろうとも，かけ算を式で示すとすれば，(グループの大きさ)×(グループの個数)＝(量全体の大きさ)であることが，こどもにじゅうぶん理解されておらなければならない。この一般化がふじゅうぶんなために，６×５＝30(円)というような式を書くのである。
>
>　とにかく，形式的な練習に移るにさきだって，技能などについての理解をじゅうぶんに伸ばすことを忘れたのでは，反復練習したものを有効に用いることができないであろう。

掛け算の交換法則によって, 5×6で正しい答えが出る場合には, 6×5でも必ず正しい答えが出る. それにも関わらず, 6×5を**誤った解決**とするのは掛け算の式の順序そのものを大事だ勘違いしているからである. 

おそらく, a×bが「グループの大きさがaでグループの個数がbの**場面**」を表していると誤解しているのだろう. a×bは「グループの大きさがaでグループの個数がbのときの**全体の数量**」を表す記号列(式)であることを理解していないのだ. 

「グループの大きさがaでグループの個数がbの**場面**」と「グループの大きさがbでグループの個数がaの**場面**」の違いを区別することと, **数量**を表すa×bとb×aを区別することが全く違う行為であることを理解していないように見える. 

a×bは「グループの大きさがaでグループの個数がbのときの**全体の数量**」であり, a×b=b×aが成立しているのだから, a×bはグループの大きさがbでグループの個数がaのときの**全体の数量**」でもある. だから, 5×6でも6×5でもどちらでも正解になることは論理的には当然なのだ.

このように1951年の時点で, 5×6のような単純な式が数量を表していることを理解していない人が学習指導要領試案なるものを作成して教育関係者に有害な悪影響を与えていたのである. これが現在まで「伝言ゲーム」によって伝わっているのだと推測される.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
掛け算順序固定強制指導についてはもう一ヶ所記述があるので引用しておこう.

「<a href="https://www.nier.go.jp/guideline/s26em/chap5.htm">Ⅴ．算数についての評価</a>」より(**太字**の強調は引用者による)
>>問題　**３人のこどもに，えんぴつを２本ずつあげようと思います。えんぴつがなん本いるでしょう。どんな九々をつかえばわかりますか。**
>
>　どんな九々をつかうかという問に対して，**３×２＝６と答えたものが予想以上に多いことがわかった。**これによってこどもは問題に出てくる数を，その数の意味を深く考えもしないで，出てくる順に書き並べ，その間に，かけ算記号を書き入れることがわかった。問題に出てくる数を頭の中にいったん収めて，演算の決定に導くように問題の場を組織だてる力が欠けているらしいことがわかった。そこで，その欠けていることについての再指導に入るわけである。
>
>　**３は人数を表わしている数である。それを２倍した答の６は何といったらよいか尋ねてみる。それで，６人となって問題の要求に合わないことを説明する。このようにして３×２＝６とするのが誤であることを明らかにしたとする。**
>
>　しかし，上のような指導だけでは，問題をすこし変えてテストしてみると，ほとんど進歩しないことがはっきりわかってきた。つまり，一方を否定するような消極的な指導だけでは，前に述べたような問題を組織だてる力を伸ばすのに，ほとんど役だたないことがわかった。これが再指導に対しての評価であって，指導の方法を修正する必要をつかんだわけである。そこで；問題解決を，同数累加の形にもどして，倍の概念をしっかり押えるように指導したのである。今度は成功した。この事実を教師が見届けたのもやはり評価である。

以上の引用は掛け算順序固定強制指導が具体的にどのように行われるかを詳しく説明している.

「３人のこどもに，えんぴつを２本ずつあげ」る場面では確かに「３は人数を表わしている数」である。しかし, 「3×2」は「3人のこどものあつまりが2つある場面」を表していないので, 「3人の2倍の人数」を意味すると解釈する必然性はない. 3×2=2×3なので「3×2」は「3人のこどもにえんぴつを2本ずつあげるときに必要な鉛筆の本数」を意味すると解釈しても論理的にはどこにも誤りはない. 

要するに「3×2」と答えた子どもの側が論理的には正しく, 教えている側がおかしな思い込みで誤りを一方的に犯しているのである. この場合に評価されるべきなのは教える側である. 子どもの側に「このように指導する教師は算数をもう一度学び直してほしい」と言われてしかるべきである.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
1951年の学習指導要領算数科編試案のような大昔の文書が現代の教育にも影響を与えていることを信用しない人もいるかもしれないので, 現代の算数教科書の教師用指導書を引用しておこう. この引用は

* <a href="http://d.hatena.ne.jp/filinion/20101118">教科書会社のトップ「東京書籍」に言わせると、「５×３≠３×５」らしい。</a>, 小学校笑いぐさ日記 2010-10-18

からの孫引きである. 2010年前頃の小2算数教科書の教師用指導書にはこのように書いてあった.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/png", "images/filinion2010.png", scale="66%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
1951年の文部省学習指導要領算数科編試案では, 「３人のこどもに，えんぴつを２本ずつあげ」る場面について

>３は人数を表わしている数である。それを２倍した答の６は何といったらよいか尋ねてみる。それで，６人となって問題の要求に合わないことを説明する。このようにして３×２＝６とするのが誤であることを明らかにしたとする。

と書いてあった. 現代の算数教科書の教師用指導書には, 「子どもが6人います。1人にあめを7こずつくばります」という場面について

>6×7では, 6人が7つ分になり, 答えは子どもの人数となってしまうことをおさえる。

と書いてあった. 完全に同じようなことが書いてある. これを見れば, 1951年の学習指導要領算数科編試案の悪影響が現代まで残っているという推測は十分に確からしいように思われる.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
実際には数十年間の「伝言ゲーム」によって様々な変種が発生している. 例えば「<a href="http://www.asahi.com/edu/student/teacher/TKY201101160133.html">2×8ならタコ2本足</a>」という教え方もされているようだ. その最後の部分は非常に怖い.

<a href="http://www.asahi.com/edu/student/teacher/TKY201101160133.html">花まる先生：２×８ならタコ２本足 (2011年1月17日)</a>より(**太字**の強調は引用者による)
>　最後に、代表してだれかが問題を作ることに。手を挙げた男の子が選んだのは、真っ赤なテントウムシ。パネルに７匹貼った。「テントウムシが７匹います。テントウムシには足が６本あります。全部で足は何本あるでしょう」
>
>　今度はみんなが「６×７」と答えられた。
>
>　「ちなみに７×６だとどうなるかな」と先生が言うと、**出題した男の子は棒状の黒いフェルトをテントウムシの足の部分に一本ずつ追加していった。**先生は「足が７本になっちゃった。テントウムシは昆虫の世界から出て行かなければいけなくなっちゃうよね」。

出題した男の子が**自主的に**棒状の黒いフェルトをテントウムシの足の部分に一本ずつ追加していったシーンに筆者は正直かなりの恐怖を感じた. 実際には昆虫の足の本数と掛け算の順序のあいだには何も関係がない. おそらく小3の男の子も関係がないことを知っているだろう. それにもかかわらず関係があるということを信じていることを示す行動を男の子に自主的にとらせることに成功してしまっているのだ.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 100年以上の歴史がある！

詳しい情報については

* https://twitter.com/genkuroki/status/1267851912566599681

を参照(OokuboTactさんから教えてもらった情報). 次のセルの画像は

* 鈴木筆太郎著, 『算術教授法に関する新研究』, 宝文館, 明44.1１ (1911年) 
* https://dl.ndl.go.jp/info:ndljp/pid/811527/35

からの引用である. 
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/HudetaroSuzuki1911.jpg", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
【5ヶ×42=210ヶとすべきを42×5ヶ=210ヶとする類】を誤り扱いしている. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### パターンマッチ教育の恐怖

児童の側が掛算順序固定強制指導に対処するためには, 

* 「ずつ」「1あたり」答えと同じ助数詞(個, 人, 本, ...)のついた数を掛算の式では先に書けばよい

という処方箋に従えばよいことについて上で説明した. そして, 掛算順序固定強制指導をすすめている教科書の教師用指導書で「ずつ」のついている数を掛算の式では先に書くと教えるように示唆している場合もある.

このようなキーワードのパターンマッチで対処する方法を教えることを**パターンマッチ教育**と呼ぶことにしよう.

算数におけるパターンマッチ教育は小学1年生から6年生までずっと続く可能性がある. パターンマッチ教育にさらされ続けた児童はどうなってしまうと予想されるだろうか? 数値的な情報を含むような文章や論理的に複雑な文章をまともに読解できなくなる可能性が高い. 

中学校や高校で数学を教える先生は以上の点に注意を払う必要がある.

算数教育によってパターンマッチ教育に心が支配されてしまった生徒は, 中学生・高校生になっても教師にパターンマッチ教育を要求するようになるだろう. そのとき, 中学校や高校の先生が, 「数学がよくできない子には単純なキーワードのパターンマッチで解く方法を教えざるをえない」という態度を取ったらどうなるだろうか? そのような算数・数学教育で小学校から高校までずっと塗り潰されてしまった生徒はどうなってしまうのだろうか?

私はそのような生徒のことを思うとかわいそうでならない. 救いがまったくない. 

中学校や高校の先生は, 生徒がパターンマッチ教育以外を強く拒否して来てもそれをきちんと否定して, 普通の常識的な考え方をするように粘り強く教える必要がある. 非常に大変な仕事になると思われるが, 教師を目指す人は基本的にそういう**本物の教育**をしたい人達であると信じたい. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### パターンマッチ教育の極北

最後に算数におけるパターンマッチ教育の極北の事例を紹介したい.

次に引用する画像は

* Googleでは2010年2月12日の日付を持つ「吹田市立北山田小学校の算数教室だより」
* https://twitter.com/temmusu_n/status/804680445967286274
* https://twitter.com/kuri_kurita/status/804840892355854336
* https://twitter.com/genkuroki/status/813962810807885824

より(リンクはすでに切れている). 

「わの前ののの前！」の意味をあなたはわかるだろうか?
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/wanomaenononomae1.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
「わの前ののの前！」の意味は以下の通り.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/wanomaenononomae2.jpg", scale="40%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
このようなひどい教育法(こっけいな教育法, 笑える教育法)が提案されてしまう背景には, 算数の教科書における割合教育の構成が

* 児童にとっては(実は大人にとっても)わかりにくい用語であることがよく知られている「比べ(られ)る量」「もとにする量」を使って教えようとする. それらの用語は割合の概念を理解するために全く必要ない. 不必要でかつ児童にとって分かり難い用語を使って教えようとしている.

* 教科書は次の3つの公式を使って割合の問題を解くように編集されている:
>(1) 比べ(られ)る量 ÷ もとにする量 = 割合<br>
>(2) もとにする量 × 割合 = 比べ(られ)る量<br>
>(3) 比べ(られ)る量 ÷ 割合 = もとにする量

* 児童はどの公式を使ってよいのかわからなくなり易いので, 「くもわ図」(テントウムシ型の図)を教える塾や教師が出て来る. (そもそも「どの公式を使うか」という発想をするようになった時点で割合に関するまともな理解は不可能になるだろう.)

* しかし, 児童は問題文中のどの数値が「比べ(られ)る量」「もとにする量」なのか判別できない. (そもそもそれらの用語自体が割合について理解するためには必要ない.)

かくして上に紹介したような「わの前ののの前！」のようなくだらない教え方が開発されることになるのである.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
「できない子のためにはこのように教えざるを得ない」と言っている人達は, 割合の概念の理解について根本的に誤解しているせいで, できない子をさらなる地獄に落とすような教え方をしているだけである. このようなタイプの教育者達こそ算数や数学が苦手な子の敵であることを認識しておかなければいけない.

割合概念のより真っ当な教え方(「比べ(られ)る量」「もとにする量」のような用語や3つの公式に頼らない教え方)については

* 吉田甫, 学力低下をどう克服するか―子どもの目線から考える, 新曜社, 2003/3/25, 251頁. <a href="https://www.amazon.co.jp/dp/4788508435">Amazon</a>

を参照されたい.  大人と同じように公式を使って計算する前に大雑把な概算が終わっていて, おかしな答えが出たら概算結果に基いて誤りを犯したことを自分で確認できるようになるような教え方が可能である. この本には教科書通りに割合について教わると, 「AはBの$130\%$でCはBの$80\%$のとき, ABCを大きな順に並べよ」のタイプの簡単な問題(3つの公式を使って答えを出せない問題)の正答率が$31\%$程度になってしまうそうだ. 工夫した実験的な教え方では正解率は$80\%$を軽く超える.

あと, 算数と数学の教え方については次の本が非常に参考になる:

* 見尾三保子, お母さんは勉強を教えないで―子どもの学習にいちばん大切なこと, 草思社, 2002/10/1, 222頁. <a href="https://www.amazon.co.jp/dp/4794211694">Amazon</a>, <a href="https://www.amazon.co.jp/dp/4101370311">文庫版</a>

この本のタイトルは非常によろしくない. タイトルがこれでなければもっと売れていたのではないかと思われる. タイトルと内容は無関係で特に算数と数学を例にどのように教えなければいけないかについて非常に分かり易く解説されている.
<!-- #endregion -->
