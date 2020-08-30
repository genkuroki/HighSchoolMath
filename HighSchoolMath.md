---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.1
  kernelspec:
    display_name: Julia 1.6.0-DEV depwarn
    language: julia
    name: julia-1.6-depwarn
---

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
# 高校数学の話題

黒木玄 (Gen Kuroki)

2018-08-15～2019-09-24, 2020-08-27～2020-08-30

このノートでは高校の数学の教科書にあるような話題を扱い, その数学的背景について解説する.

タイポや自明な誤りは自分で訂正して読むこと. 本質的な誤りがあれば著者に教えて欲しい.

* Copyright 2018, 2019, 2020 Gen Kuroki
* License: MIT https://opensource.org/licenses/MIT
* Repository: https://github.com/genkuroki/HighSchoolMath

このファイルは次の場所できれいに閲覧できる:

* <a href="http://nbviewer.jupyter.org/github/genkuroki/HighSchoolMath/blob/master/HighSchoolMath.ipynb">高校数学の話題 HTML版</a>

* <a href="https://genkuroki.github.io/documents/HighSchoolMath/HighSchoolMath.pdf">高校数学の話題 PDF版</a>

このノートの想定読者は大学である程度を数学を学んだで人で高校で習った数学について見直したい人達である. 

このファイルは<a href="https://julialang.org/">Julia言語</a>カーネルの <a href="http://jupyter.org/">Jupyter notebook</a> である. 自分のパソコンに<a href="https://julialang.org/">Julia言語</a>をインストールしたい場合には

* <a href="http://nbviewer.jupyter.org/gist/genkuroki/81de23edcae631a995e19a2ecf946a4f">WindowsへのJulia言語のインストール</a>

を参照せよ. このファイルは <a href="https://juliabox.com/">JuliaBox</a> でも使用できるかもしれない. このファイル中の<a href="https://julialang.org/">Julia言語</a>のコードを理解できれば, <a href="https://julialang.org/">Julia言語</a>から<a href="https://www.sympy.org">SymPy</a>を用いた数式処理や数値計算の結果のプロットの仕方を学ぶことができる.

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
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}, "toc": true} -->
<h1>目次<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#三角函数の加法定理" data-toc-modified-id="三角函数の加法定理-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>三角函数の加法定理</a></span><ul class="toc-item"><li><span><a href="#三角函数の加法定理の導出は易しい" data-toc-modified-id="三角函数の加法定理の導出は易しい-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>三角函数の加法定理の導出は易しい</a></span></li><li><span><a href="#三角函数の加法定理の導出は中学校レベル" data-toc-modified-id="三角函数の加法定理の導出は中学校レベル-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>三角函数の加法定理の導出は中学校レベル</a></span></li><li><span><a href="#三角函数の加法定理は複数の方法で得られる" data-toc-modified-id="三角函数の加法定理は複数の方法で得られる-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>三角函数の加法定理は複数の方法で得られる</a></span></li><li><span><a href="#三角函数の加法定理と内積の関係" data-toc-modified-id="三角函数の加法定理と内積の関係-1.4"><span class="toc-item-num">1.4&nbsp;&nbsp;</span>三角函数の加法定理と内積の関係</a></span></li></ul></li><li><span><a href="#3次方程式と4次方程式の解法" data-toc-modified-id="3次方程式と4次方程式の解法-2"><span class="toc-item-num">2&nbsp;&nbsp;</span>3次方程式と4次方程式の解法</a></span><ul class="toc-item"><li><span><a href="#ある3次式の因数分解から3次方程式の解法へ" data-toc-modified-id="ある3次式の因数分解から3次方程式の解法へ-2.1"><span class="toc-item-num">2.1&nbsp;&nbsp;</span>ある3次式の因数分解から3次方程式の解法へ</a></span><ul class="toc-item"><li><span><a href="#巡回行列式" data-toc-modified-id="巡回行列式-2.1.1"><span class="toc-item-num">2.1.1&nbsp;&nbsp;</span>巡回行列式</a></span></li></ul></li><li><span><a href="#ある4次式の展開公式から4次方程式の解法へ" data-toc-modified-id="ある4次式の展開公式から4次方程式の解法へ-2.2"><span class="toc-item-num">2.2&nbsp;&nbsp;</span>ある4次式の展開公式から4次方程式の解法へ</a></span></li></ul></li><li><span><a href="#べき乗和とベルヌイ多項式" data-toc-modified-id="べき乗和とベルヌイ多項式-3"><span class="toc-item-num">3&nbsp;&nbsp;</span>べき乗和とベルヌイ多項式</a></span><ul class="toc-item"><li><span><a href="#Bernoulli多項式" data-toc-modified-id="Bernoulli多項式-3.1"><span class="toc-item-num">3.1&nbsp;&nbsp;</span>Bernoulli多項式</a></span></li><li><span><a href="#Bernoulli多項式とべき乗和の関係" data-toc-modified-id="Bernoulli多項式とべき乗和の関係-3.2"><span class="toc-item-num">3.2&nbsp;&nbsp;</span>Bernoulli多項式とべき乗和の関係</a></span></li><li><span><a href="#べき乗和の直接的な取り扱い" data-toc-modified-id="べき乗和の直接的な取り扱い-3.3"><span class="toc-item-num">3.3&nbsp;&nbsp;</span>べき乗和の直接的な取り扱い</a></span></li><li><span><a href="#第2種Stirling数とべき乗和" data-toc-modified-id="第2種Stirling数とべき乗和-3.4"><span class="toc-item-num">3.4&nbsp;&nbsp;</span>第2種Stirling数とべき乗和</a></span></li><li><span><a href="#第2種Stirling数とBernoulli数の関係" data-toc-modified-id="第2種Stirling数とBernoulli数の関係-3.5"><span class="toc-item-num">3.5&nbsp;&nbsp;</span>第2種Stirling数とBernoulli数の関係</a></span></li><li><span><a href="#べき乗和とHurwitzのゼータ函数の関係" data-toc-modified-id="べき乗和とHurwitzのゼータ函数の関係-3.6"><span class="toc-item-num">3.6&nbsp;&nbsp;</span>べき乗和とHurwitzのゼータ函数の関係</a></span></li></ul></li><li><span><a href="#平面上の点と直線の距離" data-toc-modified-id="平面上の点と直線の距離-4"><span class="toc-item-num">4&nbsp;&nbsp;</span>平面上の点と直線の距離</a></span></li><li><span><a href="#Jensenの不等式と相加相乗調和平均" data-toc-modified-id="Jensenの不等式と相加相乗調和平均-5"><span class="toc-item-num">5&nbsp;&nbsp;</span>Jensenの不等式と相加相乗調和平均</a></span><ul class="toc-item"><li><span><a href="#Jensenの不等式" data-toc-modified-id="Jensenの不等式-5.1"><span class="toc-item-num">5.1&nbsp;&nbsp;</span>Jensenの不等式</a></span></li><li><span><a href="#相加相乗調和平均の不等式" data-toc-modified-id="相加相乗調和平均の不等式-5.2"><span class="toc-item-num">5.2&nbsp;&nbsp;</span>相加相乗調和平均の不等式</a></span></li><li><span><a href="#p乗平均" data-toc-modified-id="p乗平均-5.3"><span class="toc-item-num">5.3&nbsp;&nbsp;</span>p乗平均</a></span></li><li><span><a href="#p→0でのp乗平均の挙動" data-toc-modified-id="p→0でのp乗平均の挙動-5.4"><span class="toc-item-num">5.4&nbsp;&nbsp;</span>p→0でのp乗平均の挙動</a></span></li><li><span><a href="#p乗平均のpに関する依存性(1)" data-toc-modified-id="p乗平均のpに関する依存性(1)-5.5"><span class="toc-item-num">5.5&nbsp;&nbsp;</span>p乗平均のpに関する依存性(1)</a></span></li><li><span><a href="#p乗平均のpに関する依存性(2)" data-toc-modified-id="p乗平均のpに関する依存性(2)-5.6"><span class="toc-item-num">5.6&nbsp;&nbsp;</span>p乗平均のpに関する依存性(2)</a></span></li><li><span><a href="#単位円に内接する多角形の周長と面積の最大値" data-toc-modified-id="単位円に内接する多角形の周長と面積の最大値-5.7"><span class="toc-item-num">5.7&nbsp;&nbsp;</span>単位円に内接する多角形の周長と面積の最大値</a></span></li></ul></li><li><span><a href="#三角函数の微積分" data-toc-modified-id="三角函数の微積分-6"><span class="toc-item-num">6&nbsp;&nbsp;</span>三角函数の微積分</a></span><ul class="toc-item"><li><span><a href="#高校の数学の教科書の方針" data-toc-modified-id="高校の数学の教科書の方針-6.1"><span class="toc-item-num">6.1&nbsp;&nbsp;</span>高校の数学の教科書の方針</a></span></li><li><span><a href="#曲線の長さが速さの積分になることの応用" data-toc-modified-id="曲線の長さが速さの積分になることの応用-6.2"><span class="toc-item-num">6.2&nbsp;&nbsp;</span>曲線の長さが速さの積分になることの応用</a></span></li><li><span><a href="#楕円積分,-楕円函数,-楕円曲線暗号" data-toc-modified-id="楕円積分,-楕円函数,-楕円曲線暗号-6.3"><span class="toc-item-num">6.3&nbsp;&nbsp;</span>楕円積分, 楕円函数, 楕円曲線暗号</a></span></li></ul></li><li><span><a href="#Gauss積分の大学入試問題" data-toc-modified-id="Gauss積分の大学入試問題-7"><span class="toc-item-num">7&nbsp;&nbsp;</span>Gauss積分の大学入試問題</a></span></li><li><span><a href="#ガンマ函数の応用" data-toc-modified-id="ガンマ函数の応用-8"><span class="toc-item-num">8&nbsp;&nbsp;</span>ガンマ函数の応用</a></span><ul class="toc-item"><li><span><a href="#多項式×指数函数の積分" data-toc-modified-id="多項式×指数函数の積分-8.1"><span class="toc-item-num">8.1&nbsp;&nbsp;</span>多項式×指数函数の積分</a></span></li><li><span><a href="#Stirlingの公式" data-toc-modified-id="Stirlingの公式-8.2"><span class="toc-item-num">8.2&nbsp;&nbsp;</span>Stirlingの公式</a></span></li><li><span><a href="#Stirlingの公式を使うと簡単に解ける大学入試問題" data-toc-modified-id="Stirlingの公式を使うと簡単に解ける大学入試問題-8.3"><span class="toc-item-num">8.3&nbsp;&nbsp;</span>Stirlingの公式を使うと簡単に解ける大学入試問題</a></span></li></ul></li><li><span><a href="#ベータ函数の応用" data-toc-modified-id="ベータ函数の応用-9"><span class="toc-item-num">9&nbsp;&nbsp;</span>ベータ函数の応用</a></span><ul class="toc-item"><li><span><a href="#1/6公式" data-toc-modified-id="1/6公式-9.1"><span class="toc-item-num">9.1&nbsp;&nbsp;</span>1/6公式</a></span></li><li><span><a href="#sinのべきの定積分" data-toc-modified-id="sinのべきの定積分-9.2"><span class="toc-item-num">9.2&nbsp;&nbsp;</span>sinのべきの定積分</a></span></li><li><span><a href="#ガンマ函数とベータ函数の関係" data-toc-modified-id="ガンマ函数とベータ函数の関係-9.3"><span class="toc-item-num">9.3&nbsp;&nbsp;</span>ガンマ函数とベータ函数の関係</a></span></li><li><span><a href="#ベータ函数の極限によるガンマ函数の表示とWallisの公式" data-toc-modified-id="ベータ函数の極限によるガンマ函数の表示とWallisの公式-9.4"><span class="toc-item-num">9.4&nbsp;&nbsp;</span>ベータ函数の極限によるガンマ函数の表示とWallisの公式</a></span></li><li><span><a href="#Gaussの超幾何函数への一般化" data-toc-modified-id="Gaussの超幾何函数への一般化-9.5"><span class="toc-item-num">9.5&nbsp;&nbsp;</span>Gaussの超幾何函数への一般化</a></span></li><li><span><a href="#Kummerの超幾何函数" data-toc-modified-id="Kummerの超幾何函数-9.6"><span class="toc-item-num">9.6&nbsp;&nbsp;</span>Kummerの超幾何函数</a></span></li></ul></li><li><span><a href="#Taylor展開" data-toc-modified-id="Taylor展開-10"><span class="toc-item-num">10&nbsp;&nbsp;</span>Taylor展開</a></span><ul class="toc-item"><li><span><a href="#Taylorの公式の証明" data-toc-modified-id="Taylorの公式の証明-10.1"><span class="toc-item-num">10.1&nbsp;&nbsp;</span>Taylorの公式の証明</a></span></li><li><span><a href="#Taylorの公式の剰余項の評価" data-toc-modified-id="Taylorの公式の剰余項の評価-10.2"><span class="toc-item-num">10.2&nbsp;&nbsp;</span>Taylorの公式の剰余項の評価</a></span></li><li><span><a href="#有名な交代級数の例" data-toc-modified-id="有名な交代級数の例-10.3"><span class="toc-item-num">10.3&nbsp;&nbsp;</span>有名な交代級数の例</a></span></li></ul></li></ul></div>
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
using Printf
using Base64

using Plots
pyplot(fmt=:png)

showimg(mime, fn; scale="") = open(fn) do f
    base64 = base64encode(f)
    option = ifelse(scale == "", "", """ width="$scale" """)
    display("text/html", """<img src="data:$mime;base64,$base64" $option />""")
end

using SymPy
using LaTeXStrings
using SpecialFunctions
using QuadGK
using Elliptic.Jacobi: cd, sn
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 三角函数の加法定理

**三角函数の加法定理:**

$$
\begin{aligned}
&
\cos(x+y) = \cos x\;\cos y - \sin x\;\sin y, 
\\ &
\sin(x+y) = \cos x\;\sin y + \sin x\;\cos y.
\qquad \QED
\end{aligned}
$$

この公式を**認めて**使えば, 三角函数に関する他の多くの公式が導かれることは知っているだろう. だからよく

>三角函数の加法定理だけは覚えておいて, 他の公式はそれから導けばよい.

というような教え方がされている場合がある. しかし, この教え方は数学の理解という観点からはひどく中途半端である. なぜならば, 三角函数の加法定理自体がそう難しくない結果だからである. しかもその本質は中学校レベルの幾何の問題に過ぎない.

**三角函数の加法定理は簡単に導けるので, 三角函数の加法定理さえ覚える必要はない.**
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 三角函数の加法定理の導出は易しい

以下の図を見て欲しい.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/trigonometric1.jpg", scale="40%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
縦の青の点線が黒線と重なっていることを嫌うなら次のように図を描けばよい.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/trigonometric2.jpg", scale="40%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 三角函数の加法定理の導出は中学校レベル

三角函数 $\cos\theta$, $\sin\theta$ の正式な定義のためには, まず弧度法の意味での角度を定義し, 弧度法の意味ので角度の函数としてそれらを定義しなければいけなくなる. 角度の測り方を固定しない場合には $\cos(a\theta)$, $\sin(a\theta)$ のように角度の測り方の不定性によって角度に定数倍 ($a$ 倍)の違いが生じる. 

しかし, $\cos\theta$, $\sin\theta$ の代わりに, $c(\theta)=\cos(a\theta)$, $s(\theta)=\sin(a\theta)$ を使っても, 三角函数の加法定理の形は変わらない:

$$
c(x+y) = c(x)c(y)-s(x)s(y), \quad s(x+y)=c(x)s(y)+s(x)c(y).
$$

このことから, 三角函数の加法定理を理解するためには弧度法による角度の定義を知っている必要がないことがわかる.

以下の図の問題を見て欲しい. それは実質的に三角函数の加法定理を示せという内容の問題である. そのことから, $\cos$, $\sin$ という記号を使わずに, 三角函数の加法定理と同等のことを述べることができることがわかる. そして, その問題の解答は完全に中学校数学の範囲内の議論で可能である. 
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/trigonometric3.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 三角函数の加法定理は複数の方法で得られる

自力で何も知らない状態から三角函数の加法定理を証明しようとすれば, 図の描き方に複数の選択肢があることに気付く. 実際にやってみればわかるようにどのように図を描いても, 結果的に三角函数の加法定理が得られる. 要するに, 三角函数の加法定理の証明のためには, 知らなければできそうもないテクニカルな議論をする必要はなく, どのように図を描いても証明できる. ああやっても証明できるし, こうやっても証明できる. そのようなことに気付けば, 三角函数の加法定理は真に易しい結果であることを納得できるはずである.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/trigonometric4.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
$\sin$ の倍角の公式はこれの右上の図を使うと容易に証明可能である. 右上の図で $\alpha=\beta$ のとき $a=1$ となるので, 

$$\sin(2\alpha)=\cos\alpha\,(\sin\alpha + 1 \sin\alpha)=2\cos\alpha\sin\alpha.$$
<!-- #endregion -->

### 三角函数の加法定理と内積の関係

三角函数の加法定理:

$$
\begin{aligned}
&
\begin{cases}
\cos(\alpha+\beta) = \cos\alpha\,\cos\beta - \sin\alpha\,\sin\beta, \\
\cos(\alpha-\beta) = \cos\alpha\,\cos\beta + \sin\alpha\,\sin\beta, \\
\end{cases}
\\ &
\begin{cases}
\sin(\alpha+\beta) = \sin\alpha\,\cos\beta + \cos\alpha\,\sin\beta, \\
\sin(\alpha-\beta) = \sin\alpha\,\cos\beta - \cos\alpha\,\sin\beta. \\
\end{cases}
\end{aligned}
$$

これらを成分がを極座標された2つの2次元ベクトル

$$
\vec{a} = 
\begin{bmatrix}
a\\
c\\
\end{bmatrix} =
\begin{bmatrix}
\|\vec{a}\|\cos\alpha \\
\|\vec{a}\|\sin\alpha \\
\end{bmatrix},
\quad
\vec{b} =
\begin{bmatrix}
b\\
d\\
\end{bmatrix} =
\begin{bmatrix}
\|\vec{b}\|\cos\beta \\
\|\vec{b}\|\sin\beta \\
\end{bmatrix}
$$

に適用してみよう. これらの対応する成分の積の和を計算すると $\cos$ の加法定理より,

$$
ab+cd = 
\|\vec{a}\|\|\vec{b}\|(\cos\alpha\,\cos\beta+\sin\alpha\,\sin\beta) =
\|\vec{a}\|\|\vec{b}\|\cos(\beta-\alpha)
$$

となる. これで, 2つの2次元ベクトルの対応する成分の和は2つのベクトルのあいだの角度の $\cos$ の $\|\vec{a}\|\|\vec{b}\|$ 倍になることがわかった. 我々はこれを「内積」と呼ぶのであった.

次に $ad-bc$ を計算してみよう:

$$
ad-bc = 
\|\vec{a}\|\|\vec{b}\|(\cos\alpha\,\sin\beta-\sin\alpha\,\cos\beta) =
\|\vec{a}\|\|\vec{b}\|\sin(\beta-\alpha).
$$

これの絶対値は2つのベクトルを辺とする平行四辺形の面積である. 我々は $ad-bc$ を行列

$$
\begin{bmatrix}
a & b \\
c & d \\
\end{bmatrix}
$$

の行列式と呼んでいるのであった.  $2\times2$ の行列式は平行四辺形の面積の $\pm1$ 倍という幾何学的意味を持っている.  2つの2次元ベクトルの**外積**を $ad-bc$ で定義することもできる.

このように, 三角函数の加法定理は2次元ベクトルの内積や $2\times 2$ の行列式(もしくは2次元ベクトルの外積)の幾何学的意味を記述している公式ともみなされる.

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 3次方程式と4次方程式の解法

高校数学レベルでの3次方程式と4次方程式の解法を解説する.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
### ある3次式の因数分解から3次方程式の解法へ

高校で次の因数分解の公式を習う:

$$
x^3+y^3+z^3 - 3xyz = (x+y+z)(x^2+y^2+z^2-xy-xz-yz).
$$

1の原始3乗根を $\omega$ と書く: $\omega^2+\omega+1=0$, 

$$
\omega = e^{\pm 2\pi i/3} = \frac{-1\pm\sqrt{3}\;i}{2}.
$$

以下では, $\omega^2+\omega+1=0$ とそれから導かれる $\omega^3=1$, $\omega\ne 1$ のみを使う.

1の原始3乗根 $\omega$ を使うと上の因数分解の公式は

$$
x^3+y^3+z^3-3xyz = (x+y+z)(x+\omega y+\omega^2 z)(x+\omega^2 y+\omega z)
$$

と書き直される. 最初の因数分解の公式の右辺の $-xy$, $-xz$, $-yz$ の係数 $-1$ は $\omega^2+\omega=-1$ によって再現される.

さらに, $p = yz$, $q=y^3+z^3$ とおくと, 上の因数分解の公式は

$$
x^3 -3px + q = (x+y+z)(x+\omega y+\omega^2 z)(x+\omega^2 y+\omega z)
$$

と書き直される. この公式を使うと3次方程式の解の公式を作れる.

任意に与えられた $p$, $q$ に対して, $p=yz$, $q=y^3+z^3$ を満たす $y,z$ は以下のようにして求めることができる. $y^3 z^3=p^3$ と $y^3+z^3=q$ より

$$
\lambda^2 - q\lambda + p^3 = (\lambda - y^3)(\lambda - z^3).
$$

ゆえに, 必要ならば $y,z$ の立場を交換すれば

$$
y^3 = \frac{q + \sqrt{q^2-4p^3}}{2}, \quad z^3 = \frac{q-\sqrt{q^2-4p^3}}{2}
$$

が成立している. 右辺の3乗根を取れば $y,z$ も求まる:

$$
y = \sqrt[3]{\frac{q + \sqrt{q^2-4p^3}}{2}}, \quad z = \sqrt[3]{\frac{q-\sqrt{q^2-4p^3}}{2}}.
$$

上の $x^3 -3px + q$ の因数分解の公式より, $x^3-3px+q=0$ の解はこの $y,z$ を使って,

$$
x = -y-z,\ -\omega y-\omega^2 z,\ -\omega^2 y-\omega z. 
$$

と表わされる. これは本質的に所謂**Cardanoの公式**(カルダノの公式)である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**問題:** 以上の計算を確認し, さらに解の公式を実際に作ってみよ. $\QED$

解答略.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# 1の原始3乗根

x, y, z = symbols("x y z")
ω₃ = factor((-1+√Sym(-3))/2)
latexstring(raw"\ds ω =", sympy.latex(ω₃))
```

```julia slideshow={"slide_type": "-"}
# 因数分解の公式の確認

ω = symbols("ω")
f3_factored = (x+y+z)*(x+ω*y+ω^2*z)*(x+ω^2*y+ω*z)
f3 = simplify(f3_factored(ω=>ω₃))
latexstring(sympy.latex(f3_factored), "=", sympy.latex(f3))
```

```julia slideshow={"slide_type": "-"}
pp = y*z
qq = y^3+z^3
latexstring("p=", sympy.latex(pp)) |> display
latexstring("q=", sympy.latex(qq)) |> display

p, q = symbols("p q")
latexstring(sympy.latex(x^3 - 3p*x + q), "=", sympy.latex((x^3 - 3pp*x + qq)))
```

```julia slideshow={"slide_type": "-"}
# (m-y^3)(m-z^3) の係数

m = symbols("m")
f2_org = (m-y^3)*(m-z^3)
f2 = expand((m-y^3)*(m-z^3))
latexstring(sympy.latex(f2_org), "=", sympy.latex(f2)) |> display
c2 = sympy.Poly(f2, m).all_coeffs()
latexstring(raw"\text{coefficients:}\ ", sympy.latex(c2))
```

```julia slideshow={"slide_type": "-"}
# 2次方程式の解

p, q = symbols("p q")
equ = m^2-q*m+p^3
sol = factor.(solve(equ, m))
latexstring(sympy.latex(equ), "=0") |> display
latexstring(raw"\ds m = ", sympy.latex(sol[1]), ",", sympy.latex(sol[2]))
```

```julia slideshow={"slide_type": "-"}
# 3次方程式の解が得られていることの確認

y = sol[2]^(Sym(1)/3)
z = p/y
X = -[
    y+z
    ω*y+ω^2*z
    ω^2*y+ω*z
]
equ = @. X^3 - 3p*X + q
res = @.(simplify((f->f(ω=>ω₃))(equ)))
for i in 1:3
    latexstring("x_{$i}^3-3px_{$i}+q=", sympy.latex(res[i])) |> display
end
latexstring(raw"\ds x_1 = ", sympy.latex(X[1])) |> display
latexstring(raw"\ds x_2 = ", sympy.latex(X[2])) |> display
latexstring(raw"\ds x_3 = ", sympy.latex(X[3])) |> display
```

```julia slideshow={"slide_type": "-"}
# 3次方程式の解 (SymPyのsolve函数による直接計算)

x, p, q = symbols("x p q")
equ = x^3-3p*x+q
sol = solve(equ, x)
latexstring("x^3-3px+q=0") |> display
display(L"x = x_1,x_2,x_3")
latexstring(raw"\ds x_1 = ", sympy.latex(sol[1])) |> display
latexstring(raw"\ds x_2 = ", sympy.latex(sol[2])) |> display
latexstring(raw"\ds x_3 = ", sympy.latex(sol[3])) |> display
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
#### 巡回行列式

1の原始3乗根 $\omega$ を用いた因数分解の公式

$$
x^3+y^3+z^3-3xyz = (x+y+z)(x+\omega y+\omega^2 z)(x+\omega^2 y+\omega z)
$$

は行列式を用いて次のように書き直される:

$$
\begin{vmatrix}
x & y & z \\
z & x & y \\
y & z & x \\
\end{vmatrix} =
\prod_{k=0}^2 (x + \omega^k y + \omega^{2k} z).
$$

この公式は $1$ の原始 $n$ 乗根 $\zeta$ を用いた公式

$$
\begin{vmatrix}
x_0     & x_1     & x_2    & \ddots  & x_{n-1} \\
x_{n-1} & x_0     & x_1    & \ddots  & \ddots \\
\ddots  & x_{n-1} & x_0    & \ddots  & x_2 \\
x_2     & \ddots  & \ddots & \ddots  & x_1 \\
x_1     & x_2     & \ddots & x_{n-1} & x_0 \\
\end{vmatrix} =
\prod_{k=0}^{n-1} (x_0 + \zeta^k x_1 + \zeta^{2k} x_2 + \cdots + \zeta^{(n-1)k} x_{n-1}).
$$

に一般化される.  この公式の証明は例えば

* 佐武一郎, 線型代数学, 数学選書1, 裳華房

の第II章の研究課題に書いてある.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
### ある4次式の展開公式から4次方程式の解法へ

$f$ を次のように定める:

$$
f = (w+x+y+z)(w+x-y-z)(w-x+y-z)(w-x-y+z).
$$

このとき,

$$
p = x^2+y^2+z^2, \quad
q = xyz, \quad
r = x^2y^2 + x^2z^2 + y^2z^2
\tag{$*$}
$$

とおくと,

$$
f = w^4 - 2pw^2 + 8qw + p^2-4r.
$$

ゆえに, もしも与えられた $p,q,r$ に対して, 条件($*$)を満たす $x,y,z$ を求めることができたならば, $w$ に関する4次方程式 $f=0$ は次のように解ける:

$$
w = -x-y-z, \ -x+y+z, \ x-y+z, \ x+y-z.
$$

与えられた $p,q,r$ に対して条件 ($*$) を満たす $x,y,z$ を求めるためには, 条件

$$
x^2+y^2+z^2 = p, \quad
x^2y^2+x^2z^2+y^2z^2 = r, \quad
x^2y^2z^2 = q^2
\tag{$**$}
$$

を満たす $x^2,y^2,z^2$ を求め, それらの平方根を取ればよい. ただし, 平方根の取り方には $\pm1$ 倍の不定性があることに注意せよ. 条件 $xyz=q$ より, $x,y,z$ のうち2つが決まれば残りは一意的に決まる.

条件 ($**$) を満たす $x^2,y^2,z^2$ は3次方程式の解と係数の関係より, 次の3次方程式の解である:

$$
\lambda^3 - p\lambda^2 + r\lambda - q^2 = 0.
$$

この3次方程式は $\lambda = \Lambda+p/3$ とおけば次の形になる:

$$
\Lambda^3 - P\Lambda + Q = 0, \quad
P = \frac{p^2}{3} - r, \quad
Q = -\frac{2p^3}{27} + \frac{pr}{3} - q^2.
$$

この形の3次方程式は前節の結果を用いれば解ける.

以上の方法は**Eulerの方法**と呼ばれているらしい(https://en.wikipedia.org/wiki/Quartic_function).
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**問題:** 以上の計算を確認し, さらに解の公式を実際に作ってみよ. $\QED$

解答略.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# 展開結果の確認

w, x, y, z = symbols("w x y z")
f4_org = (w+x+y+z)*(w+x-y-z)*(w-x+y-z)*(w-x-y+z)
f4 = expand(f4_org)
latexstring(sympy.latex(f4_org)) |> display
latexstring("=", sympy.latex(f4)) |> display
```

```julia slideshow={"slide_type": "-"}
# 展開結果の 0,1,2,3,4 次の係数の確認.
# 3次の係数は0になっている.

display(L"\text{coefficients:}\ ")
c4 = sympy.Poly(f4, w).all_coeffs()
```

```julia slideshow={"slide_type": "-"}
p = c4[3]/(-2)
latexstring("p=", sympy.latex(p))
```

```julia slideshow={"slide_type": "-"}
q = c4[4]/8
latexstring("q=", sympy.latex(q))
```

```julia slideshow={"slide_type": "-"}
r = x^2*y^2 + x^2*z^2 + y^2*z^2
@show simplify(c4[5] - (p^2-4r))
latexstring("r=", sympy.latex(r))
```

```julia slideshow={"slide_type": "-"}
# p,q,rを使った公式の確認

ff4 = w^4 - 2p*w^2 + 8q*w + (p^2-4r)
simplify(f4 - ff4) |> display
latexstring("w^4-2pw^2+8qw+(p^2-4r)") |> display
latexstring("=", sympy.latex(f4)) |> display
```

```julia slideshow={"slide_type": "-"}
m = symbols("m")
equ = m^3 - p*m^2 + r*m - q^2
sol = simplify(factor(equ))
latexstring(sympy.latex(equ), "=", sympy.latex(sol))
```

```julia slideshow={"slide_type": "-"}
# 補助的な3次方程式の形の確認

p, q, r, m, M = symbols("p q r m M")
(f3 = m^3 - p*m^2 + r*m - q^2) |> display
(g3 = simplify(expand(f3(m => M+p/3)))) |> display
c3 = sympy.Poly(g3, M).all_coeffs()
```

```julia slideshow={"slide_type": "-"}
# w, p, q, r = symbols("w p q r")
# factor.(solve(w^4 - 2p*w^2 + 8q*w + (p^2-4r), w))
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## べき乗和とベルヌイ多項式

高校数学ではべき乗和

$$
\begin{aligned}
&
1+2+\cdots+n = \frac{n(n+1)}{2}, 
\\ &
1^2+2^2+\cdots+n^2 = \frac{n(n+1)(2n+1)}{6}, 
\\ &
1^3+2^3+\cdots+n^3 = \frac{n^2(n+1)^2}{4}
\end{aligned}
$$

について習う. これらの公式の背景にベルヌイ多項式が控えていることを解説したい.

ベルヌイ多項式については以下のツイッターにおける以下のスレッドも参照せよ:

* https://twitter.com/genkuroki/status/1111938896844095488
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Bernoulli多項式

**Bernoulli多項式**(ベルヌイ多項式) $B_k(x)$ が次のTaylor展開で定義される:

$$
\frac{ze^{zx}}{e^z - 1} = \sum_{k=0}^\infty \frac{B_k(x)}{k!}z^k.
$$

これの左辺をBernoulli多項式の**母函数**と呼ぶ.

**Bernoulli数:** Bernoulli多項式の定数項 $B_k=B_k(0)$ は**Bernoulli数**と呼ばれている.

$$
\begin{aligned}
\frac{ze^{zx}}{e^z - 1} &= 
\frac{z}{e^z - 1} e^{xz} =
\sum_{i=0}^\infty \frac{B_i z^i}{i!} \sum_{j=0}^\infty\frac{x^j z^j}{j!} 
\\ &=
\sum_{i,j=0}^\infty \frac{(i+j)!}{i!j!}B_i x^j \frac{z^{i+j}}{(i+j)!} =
\sum_{k=0}^\infty \sum_{j=0}^k \binom{k}{j} B_{k-j}x^j \frac{z^k}{k!}
\end{aligned}
$$

より, Bernoulli多項式はBernoulli数によって次のように表わされることがわかる:

$$
B_k(x) = 
\sum_{j=0}^k \binom{k}{j} B_{k-j}x^j.
$$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**Bernoulli多項式の微分:** Benoulli多項式の定義式の両辺を $x$ で偏微分すると

$$
\frac{z^2 e^{zx}}{e^z - 1} = 
\sum_{k=0}^\infty \frac{B_k'(x)}{k!}z^k
$$

となり, これの左辺は

$$
\frac{z^2 e^{zx}}{e^z - 1} = 
\sum_{m=0}^\infty \frac{B_m(x)}{m!}z^{m+1} =
\sum_{k=1}^\infty \frac{B_{k-1}(x)}{(k-1)!}z^k
$$

と書けるので, 上と比較して

$$
B_k'(x) = k B_{k-1}(x)
$$

が得られる. $B_0(x)=1$ なので $B_k(x)$ は最高次の係数が $1$ である $k$ 次の多項式になる.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**Bernoulli多項式の積分:** 上の結果より,

$$
\frac{d}{dx}\frac{B_{k+1}(x)}{k+1}=B_k(x)
$$

であるから, 

$$
\int_a^b B_k(x)\,dx = \frac{B_{k+1}(b)-B_{k+1}(a)}{k+1}.
$$

これの母函数表示は次の通り:

$$
\sum_{k=0}^\infty \int_a^b B_k(x)\,dx\;\frac{z^k}{k!} =
\int_a^b \frac{ze^{zx}}{e^z - 1}\,dx =
\left[\frac{e^{zx}}{e^z - 1}\right]_{x=a}^{x=b} = 
\frac{e^{zb}-e^{za}}{e^z - 1}.
$$

特に $a=0$, $b=1$ のとき, 右辺は $1$ になるので, 

$$
\int_0^1 B_k(x)\,dx = \delta_{k0}
$$

となることもわかる. $a=x$, $b=x+1$ の場合には

$$
\sum_{k=0}^\infty \int_x^{x+1} B_k(y)\,dy\;\frac{z^k}{k!} =
\frac{e^{z(x+1)}-e^{zx}}{e^z - 1} =
e^{zx} =
\sum_{k=0}^\infty x^k \frac{z^k}{k!}
$$

となるので, 

$$
\int_x^{x+1} B_k(y)\,dy = x^k.
$$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Bernoulli多項式とべき乗和の関係

べき乗和 $S_k(n)$ が次のように定義される:

$$
S_k(n) = \sum_{j=1}^n j^k = 1^k+2^k+\cdots+n^k.
$$

べき乗和の母函数は次のように計算される:

$$
\begin{aligned}
\sum_{k=0}^\infty \frac{S_k(n)}{k!}z^k &=
\sum_{k=0}^\infty \sum_{j=1}^n \frac{j^k}{k!}z^k =
\sum_{j=1}^n \sum_{k=0}^\infty \frac{j^k}{k!}z^k 
\\ &=
\sum_{j=1}^n e^{jz} =
\frac{e^{(n+1)z}-e^z}{e^z-1}.
\end{aligned}
$$

Bernoulli多項式の積分に関する結果より,

$$
\begin{aligned}
\frac{e^{(n+1)z}-e^z}{e^z-1} &=
\sum_{k=0}^\infty \int_1^{n+1}B_k(x)\,dx\;\frac{z^k}{k!} 
\\ &=
\sum_{k=0}^\infty \frac{B_{k+1}(n+1)-B_{k+1}(1)}{k+1} \frac{z^k}{k!}.
\end{aligned}
$$

したがって, 

$$
S_k(n) = \int_1^{n+1} B_k(x)\,dx = \frac{B_{k+1}(n+1) - B_{k+1}(1)}{k+1}.
$$

特に $S_k(n)$ は $n$ について $k+1$ 次の多項式になり, 最高次の係数は $1/(k+1)$ になることがわかる.

以上では母函数表示を経由して計算したが, 

$$
\int_x^{x+1} B_k(y)\,dy = x^k, \quad
\int B_k(x) dx = \frac{B_{k+1}(x)}{k+1}
$$

を使えば

$$
\begin{aligned}
S_k(n) &= \sum_{j=1}^n j^k =
\sum_{j=1}^n \int_j^{j+1} B_k(x)\,dx \\ &=
\int_1^{n+1} B_k(x)\,dx =
\frac{B_{k+1}(n+1) - B_{k+1}(1)}{k+1}
\end{aligned}
$$

と同じ公式がより平易に得られる.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# ベルヌイ多項式のリスト k = 0,1,2,…,12

B(k,x) = sympy.bernoulli(k,x)
SS(k,x) = (B(k+1,x+1) - B(k+1,Sym(1)))/(k+1)
x = symbols("x")
for k in 0:12
    latexstring("B_{$k}(x)=", sympy.latex(B(k,x))) |> display
end
```

```julia slideshow={"slide_type": "subslide"}
# べき乗和の公式のリスト k = 0,1,2,…,12

x = symbols("x")
for k in 0:12
    latexstring("S_{$k}(x)=", sympy.latex(factor(SS(k,x)))) |> display
end
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $k$ が3以上の整数のとき $B_k(0)=0$ となることを示せ. 

**証明:** $B_k(x)$ の母函数で $x=0$ とおくと,

$$
\begin{aligned}
\sum_{k=0}^\infty \frac{B_k(0)}{k!}z^k + \frac{z}{2} = 
\frac{z}{e^z - 1} + \frac{z}{2} = 
\frac{z}{2}\frac{e^z + 1}{e^z - 1} = 
\frac{z}{2}\frac{e^{z/2} + e^{-z/2}}{e^{z/2} - e^{-z/2}}.
\end{aligned}
$$

これは $z$ の偶函数なので, 左辺のべき級数の奇数次の係数はすべて消える. ゆえに $k$ が3以上の奇数ならば $B_k(0)=0$ となる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** 以下を示せ:

(1) $B_k(1-x)=(-1)^k B_k(x)$.

(2) $k$ が奇数のとき $B_k(1/2)=0$.

(3) $k$ が $3$ 以上の奇数のとき $B_k(1)=B_k(0)=0$.

(4) $k\geqq 2$ ならば $B_k(0)=B_k(1)$.

**証明:** (1) $B_k(x)$ の母函数で $x$ に $1-x$ を代入すると,

$$
\begin{aligned}
\sum_{k=0}^\infty \frac{B_k(1-x)}{k!}z^k &= 
\frac{ze^{z(1-x)}}{e^z - 1} = 
\frac{ze^{-zx}}{1 - e^{-z}} 
\\ &= 
\frac{(-z)e^{(-z)x}}{e^{-z}-1} = 
\sum_{k=0}^\infty \frac{B_k(x)}{k!}(-z)^k.
\end{aligned}
$$

なので両辺を比較すると, $B_k(1-x)=(-1)^k B_k(x)$ となることがわかる. 

(2) $x=1/2$ のとき $1-x = x$ であり, $k$ が奇数のとき $B_k(1-x)=-B_k(x)$ なので $B_k(1/2)=0$ となることがわかる. 

(3) 1つ前の問題より, $k$ が3以上の奇数のとき $B_k(0)=0$ なので $B_k(1)=B_k(1-0)=-B_k(0)=0$ となる.

(4) $k\geqq 2$ であるとする. $k$ が奇数ならば $B_k(0)=0=B_k(1)$ となり, $k$ が偶数ならば $B_k(0)=B_k(1-1)=B_k(1)$ となる. 
$\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** 以下を示せ:

(1) $S_k(x)$ は $x$ で割り切れる.

(2) $k\geqq 1$ のとき $S_k(x)$ は $x+1$ で割り切れる.

(3) $k$ が2以上の偶数ならば $S_k(x)$ は $x(x+1)(2x+1)$ で割り切れる.

(4) $k$ が3以上の奇数ならば $S_k(x)$ は $x^2(x+1)^2$ で割り切れる.

**証明:** (1) $S_k(0)=0$ を示せばよいが, 

$$
S_k(0) = \frac{B_{k+1}(1)-B_{k+1}(1)}{k+1} = 0.
$$

(2) $k\geqq 1$ のとき, 1つ前の問題の(4)より $B_{k+1}(0)=B_{k+1}(1)$ が成立するので, 

$$
S_k(-1) =  \frac{B_{k+1}(0)-B_{k+1}(1)}{m+1} = 0.
$$

ゆえに $S_k(x)$ は $k+1$ で割り切れる.

(3) $k$ が2以上の偶数のとき, 1つ前の問題の(2),(3)より $B_{k+1}(1/2)=0$, $B_{k+1}(1)=0$ が成立するので

$$
S_k(-1/2) =  \frac{B_{k+1}(1/2)-B_{k+1}(1)}{k+1} = 0.
$$

ゆえに $S_k(x)$ は $2x+1$ で割り切れる. 上の(1),(2)より, $S_k(x)$ は $x$ と $x+1$ でも割り切れるので, $x(x+1)(2x+1)$ で割り切れることがわかる.

(4) $\ds S_k(x) = \int_1^{x+1} B_k(t)\,dt = \int_0^x B_k(t+1)\,dt$ より,

$$
S_k'(x) = B_k(x+1)
$$

なので, 1つ前の問題の(3)より, $k$ が3以上の奇数ならば $S_k'(0)=B_k(1)=0$, $S_k'(-1)=B_k(0)=0$ となる. ゆえに $S_k'(x)$ は $x$ と $x+1$ で割り切れる. 上の(1),(2)より, $S_k(x)$ は $x$ と $x+1$ で割り切れる. これらより, $S_k(x)$ が $x^2(x+1)^2$ で割り切れることがわかる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $S_1(x)$ が $x(x+1)$ で割り切れることを用いて, $\ds S_1(x)=\frac{x(x+1)}{2}$ となることを示せ.

**証明:** $S_1(x)$ は最高次の係数が $1/2$ の2次の多項式になるので, それが $x(x+1)$ で割り切れることを使えば, $\ds S_1(x)=\frac{x(x+1)}{2}$ となることがただちに導かれる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $S_2(x)$ が $x(x+1)(2x+1)$ で割り切れることを用いて, $\ds S_2(x)=\frac{x(x+1)(2x+1)}{6}$ となることを示せ.

**証明:** $S_2(x)$ は最高次の係数が $1/3$ の3次の多項式になるので, それが $x(x+1)(2x+1)$ で割り切れることを使えば, $\ds S_2(x)=\frac{x(x+1)(2x+1)}{6}$ となることがただちに導かれる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $S_3(x)$ が $x^2(x+1)^2$ で割り切れることを用いて, $\ds S_3(x)=\frac{x^2(x+1)^2}{4}$ となることを示せ.

**証明:** $S_3(x)$ は最高次の係数が $1/4$ の4次の多項式になるので, それが $x^2(x+1)^2$ で割り切れることを使えば, $\ds S_3(x)=\frac{x^2(x+1)^2}{4}$ となることがただちに導かれる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $S_4(x)$ が $x(x+1)(2x+1)$ で割り切れることを用いて, $S_4(x)$ を求めよ.

**解答例:** $S_4(x)$ は最高次の係数が $1/5$ の5次の多項式になり, $x(x+1)(2x+1)$ で割り切れるので,

$$
S_4(x) = \frac{1}{10}x(x+1)(2x+1)(x^2+ax+b)
$$

と書ける. $S_4(1)=1$, $S_4(2)=17$ より,

$$
\frac{3}{5}(1+a+b)=1, \quad 3(4+2a+b)=17.
$$

左の等式の5倍を→の等式から引くと $3(3+a)=12$ となるので, $a=1$ が得られ, それを左の等式に代入すると $3(2+b)=5$ となり, $b=-1/3$ が得られる. したがって, 

$$
S_4(x) = 
\frac{1}{10}x(x+1)(2x+1)(x^2+x-1/3) =
\frac{1}{30}x(x+1)(2x+1)(3x^2+3x-1)
$$

であることがわかる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $S_5(x)$ が $x^2(x+1)^2$ で割り切れることを用いて, $S_5(x)$ を求めよ.

**解答例:** $S_5(x)$ は最高次の係数が $1/6$ の6次多項式になり, $x^2(x+1)^2$ で割り切れるので,

$$
S_5(x) = \frac{1}{6}x^2(x+1)^2(x^2+ax+b)
$$

と書ける. $S_5(1)=1$, $S_5(2)=33$ より,

$$
\frac{2}{3}(1+a+b)=1, \quad
6(4+2a+b)=33.
$$

前者の9倍を後者から引くと $6(3+a)=24$ となるので, $a=1$ が得られ, それを前者に代入すると, $2(2+b)=3$ となるので, $b=-1/2$ が得られる. ゆえに

$$
S_5(x)=
\frac{1}{6}x^2(x+1)^2(x^2+x-1/2)=
\frac{1}{12}x^2(x+1)^2(2x^2+2x-1).
\qquad\QED
$$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### べき乗和の直接的な取り扱い

ツイッターで<a href="https://twitter.com/piyopiyo1229">ぴよぴよさん</a>にBernoulli多項式に頼らない<a href="https://twitter.com/piyopiyo1229/status/1052534499169394688">直接的で平易なべき乗和の取り扱い</a>について教わったのでその内容を以下で説明する.

**定理:** べき乗和 $S_k(n)$ は $n$ に関する $k+1$ 次の多項式になる.

**証明:** 多項式 $f(x)$ で $f(0)=0$, $f(x)=f(x-1)+x^k$ を満たすものが唯一存在することを示せば十分である. (そのような $f(x)$ について $S_k(n) = f(n)$ となる.)

$f(x)$ の次数が $k+1$ 次より大きいならば $f(x)-f(x-1)$ の次数は $k+1$ 次以上になるので, $f(x)-f(x-1)=x^k$ が成立することはありえない.  $f(x)$ の次数は $k+1$ 次以下でなければいけない.

$\ds f(x)=\sum_{m=0}^{k+1} a_m x^m$ とおき, $f(0)=0$, $f(x)=f(x-1)+x^k$ を満たす $a_m$ 達が一意に定まることを示そう. $f(x-1)$ は

$$
f(x-1) = \sum_{m=0}^{k+1} a_i \sum_{i=0}^m\binom{m}{i}(-1)^{m-i}x^i =
\sum_{i=0}^{k+1}\left(\sum_{m=i}^{k+1}(-1)^{m-i}\binom{m}{i} a_m\right) x^i
$$

と書けることから, 条件 $f(0)=0$, $f(x)=f(x-1)+x^k$ は係数 $a_m$ 達に関する以下の連立一次方程式に書き直される:

$$
\begin{aligned}
&
-(k+1)a_{k+1} + 1 = 0,
\\ &
(i+1)a_{i+1} = \sum_{m=i+2}^{k+1} (-1)^{m-i} \binom{m}{i} a_m 
\quad (i=k-1,k-2,\ldots,0)
\\ &
a_0 = 0.
\end{aligned}
$$

これより, $\ds a_{k+1}=\frac{1}{k+1}$ から順番に $a_k,a_{k-1},\ldots,a_1, a_0$ が決まり, この連立一次方程式の解 $(a_0,a_1,\ldots,a_m)$ が唯一つ存在することがわかる. $\QED$

**注意:** 上の証明より, $S_k(n)$ の最高次の係数は $\ds a_{k+1}=\frac{1}{k+1}$ になることがわかる. さらに, $a_k$ を求めるための式は $i=k-1$ の場合から得られ, 

$$
k a_k = \frac{(k+1)k}{2}a_{k+1}
$$

になるので, $a_k=1/2$ となることもわかる. $\QED$

**注意:** $f(x)$ の次数が $k+1$ 次より大きいならば $f(x)-f(x-1)$ の次数は $k+1$ 次以上になるので, $f(x)-f(x-1)=x^k$ が成立することはありえない.  このことから $S_k(n)$ は $n$ について $k+2$ 次以上の多項式になることはありえないことがわかる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**注意:** 上の証明は直接的な計算にこだわりすぎて煩雑になってしまっている.  

上の証明の内容は, 有理数体上の1変数多項式環 $\Q[x]$ からそれ自身への線形写像 $D:\Q[x]\to\Q[x]$ を

$$
Df(x) = f(x) - f(x-1) \qquad(f(x)\in\Q[x])
$$

と定めると, $\Ker D = \Q$ かつ $\Im D = \Q[x]$ ($D$ は全射)になることに一般化される.  証明しておこう.

**証明:** $f(x)\in\Q[x]$ であるとする. $f(x)\in\Q$ ならば $f(x)=f(x-1)$ となるので $Df(x)=0$.  $f(x)\not\in\Q$ ならば $f(x)$ は $1$ 次以上になり, $f(x)$ の次数を $n\geqq 1$ と書き, 最高次の項を $ax^n$ と書くと, $Df(x)$ の最高次の項は $ax^n - a(x-1)^n$ の最高次の項 $anx^{n-1}\ne 0$ になるので, $Df(x)\ne 0$. ゆえに, $\Ker D = \Q$ である.

$D:\Q[x]\to\Q[x]$ の全射性を示そう.  $n$ 次以下の $Q[x]$ の元全体のなす $\Q[x]$ の部分空間を $V_n$ と書くことにする.  前段楽の議論によって, $DV_n\subset V_{n-1}$ となることがわかる.  $DV_n = V_{n-1}$ であることを示せば $D:\Q[x]\to\Q[x]$ が全射であることがわかるので, それを示したい.  線形代数における次元定理より, $\dim DV_n = \dim V_n - \Ker D = (n+1) - 1 = n = \dim V_{n-1}$ となる． ゆえに $DV_n = V_{n-1}$.  $\QED$

この証明より, $D$ の $xV_k$ (定数項のない $V_{k*1}$ の元全体のなす $V_{k+1}$ の部分空間) への制限が $V_k$ への全単射を定めることもわかる. 特に $k+1$ 次の多項式 $f(x)\in\Q[x]$ で $f(0)=0$ と $Df(x) = f(x) - f(x-1) = x^k$ を満たすものが唯一存在することがわかる.  この $f(x)$ が上の証明中の $f(x)$ である.

このように線形代数の抽象的な議論を使いこなすことができれば, 具体的な計算抜きに欲しい $f(x)$ の唯一存在をシンプルな議論で示せる.  もちろん, その具体形を求めたい場合には具体的な計算に関わる議論が必要になってしまうが, 欲しいものの存在と一意性が論理的に確定していれば, 具体形を求める議論では存在と一意性を自由に用いる相対的に楽な方法を採用し易くなる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**定理:** べき乗和を表す多項式 $S_k(x)$ は以下を満たしている.

(1) $S_k(x)$ は $S_k(0)=0$, $S_k(x)=S_k(x-1)+x^k$ という条件で一意的に特徴付けられ, その次数は $k+1$ であり, その最高次の係数は $1/(k+1)$ になる.

(2) $k\geqq 1$ ならば $S_k(-1)=0$ となり, $S_k(x)$ は $x(x+1)$ で割り切れる.

(3) $k\geqq 1$ ならば $S_k(x) = (-1)^{k+1}S_k(-1-x)$.

(4) $k$ が2以上の偶数ならば $S_k(-1/2)=0$ となり, $S_k(x)$ は $x(x+1)(2x+1)$ で割り切れる.

(5) $S_k'(x) = (-1)^k S_k'(-1-x)$.

(6) $k$ が3以上の奇数ならば $S_k'(0)=S_k'(-1)=0$ となり, $S_k(x)$ は $x^2(x+1)^2$ で割り切れる.

**証明:** (1)はすでに証明されている.

(2) $k\geqq 1$ のとき, $S_k(x)=S_k(x-1)+x^k$ で $x=0$ とおくと, $0=S_k(-1)$ が得られる. そのとき, $S_k(x)$ は $x+1$ で割り切れ, $S_k(0)=0$ より $x$ でも割り切れる.

(3) $S_k(x)=S_k(x-1)+x^k$ の $x$ に $-x$ を代入すると, $S_k(-x)=S_k(-x-1)+(-1)^k x^k$. これは $-S_k(-x-1)=-S_k(-1-(x-1))+(-1)^k x^k$, $(-1)^{k+1}S_k(-x-1)=(-1)^{k+1}S_k(-1-(x-1))+x^k$ と書き直される. $k\geqq 1$ のとき, $S_k(-1-x)$ で $x=0$ とおくと $S_k(-1-0)=S_k(-1)=0$ となる. ゆえに, $(-1)^{k+1}S_k(-1-x)$ は $S_k(x)$ を一意的に特徴付ける条件を満たしているので, $(-1)^{k+1}S_k(-1-x)=S_k(x)$ となることがわかる.

(4) $k$ は2以上の偶数であると仮定する. このとき, (3)より $S_k(x)=-S_k(-1-x)$ となる. ゆえに $x=-1/2$ とおくと $S_k(-1/2)=0$ が得られる. そのとき $S_k(x)$ は $2x+1$ で割り切れ, (2)より $x(x+1)$ でも割り切れる.

(5)は(3)からただちに得られる.

(6) $k$ は3以上の奇数であると仮定する. このとき, (5)より $S_k'(x)=-S_k'(-1-x)$ となり, 特に $S_k'(0)=-S_k'(-1)$ が得られる.  $S_k(x)=S_k(x-1)+x^k$ の両辺を微分すると $S_k'(x)=S_k'(x-1)+kx^{k-1}$ なので, 特に $S_k'(0)=S_k'(-1)$ が得らえる. それらより, $S_k'(0)=S_k'(-1)=0$ が得られる. $S_k(0)=S_k(-1)=0$ と合わせると, $S_k(x)$ は $x^2$ と $(x+1)^2$ で割り切れることがわかる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 第2種Stirling数とべき乗和

以下の内容については https://twitter.com/genkuroki/status/1052837557732433921 も参照せよ. 

集合 $\{1,2,\ldots,n\}$ を空でない $k$ 個の部分集合への分割($k$ 分割)の個数を**第2種Stirling数**と呼び, $\ds \stirlingsecond{n}{k}$ と書くことにする. 集合 $\{1,2,\ldots,n,n+1\}$ の $k$ 分割は, $\{1,2,\ldots,n\}$ の $k-1$ 分割と $\{n+1\}$ で構成された分割と $\{1,2,\ldots,n\}$ の $k$ 分割中の $k$ 個の部分集合のどれかに $n+1$ を付け加えてできる分割のどちらかになるので, 

$$
\stirlingsecond{n+1}{k} = \stirlingsecond{n}{k-1} + k\stirlingsecond{n}{k}
$$

を満たしている. この漸化式と $\ds \stirlingsecond{0}{k}=\delta_{k0}$ によって第2種Stirling数は一意的に特徴付けられる.

**定理:** $\partial=d/dx$ とおく. 微分作用素 $x\partial$ の $n$ 乗は以下のように表わされる:

$$
(x\partial)^n = \sum_{k=0}^n \stirlingsecond{n}{k} x^k\partial^k.
\tag{$*$}
$$

**証明:** $n$ に関する数学的帰納法. $n=1$ のとき $\ds \stirlingsecond{1}{k}=\delta_{k1}$ より($*$)は成立している. $n$ について($*$)が成立していると仮定する. このとき

$$
\begin{aligned}
(x\partial)^{n+1} &= 
\sum_{k=0}^n \stirlingsecond{n}{k} x\partial x^k\partial^k = 
\sum_{k=0}^n \stirlingsecond{n}{k} (x^{k+1}\partial^{k+1} + k x^k\partial^k) 
\\ &=
\sum_{l=1}^{n+1} \stirlingsecond{n}{l-1} x^l\partial^l +
\sum_{k=0}^n k\stirlingsecond{n}{k} x^k\partial^k
\\ &=
\sum_{k=0}^{n+1} \left(\stirlingsecond{n}{k-1} + k\stirlingsecond{n}{k}\right) x^k\partial^k =
\sum_{k=0}^{n+1} \stirlingsecond{n+1}{k} x^k\partial^k.
\end{aligned}
$$

これで $n$ が $n+1$ の場合にも($*$)が成立することがわかった. $\QED$

**注意:** 上の定理の公式は帰納法によらずに「項と $k$ 分割の一対一対応」を構成することによっても証明可能である.

* https://twitter.com/genkuroki/status/1052837562342027264

に簡単な説明がある. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**系:** 次が成立している:

$$
a^n = \sum_{k=0}^n \stirlingsecond{n}{k}a(a-1)\cdots(a-k+1).
$$

**証明:** $x^a$ に上の定理の公式の両辺を作用させ, さらに両辺を $x^a$ で割ればこの公式が得られる.

$a(a-1)\cdots(a-r)$ ($r+1$ 個の因子の積)と $a(a-1)\cdots(a-r+1)$ ($r$ 個の因子の積)ついて

$$
(a+1)a\cdots(a-r+1) - a(a-1)\cdots(a-r) = (r+1)a(a-1)\cdots(a-r+1).
$$

これの両辺を $a=n,n-1,\ldots,1,0$ について足し上げて, 全体を $r+1$ で割ると,

$$
\frac{(n+1)n(n-1)\cdots(n-r+1)}{r+1} = \sum_{a=0}^n a(a-1)\cdots(a-r+1).
$$

したがって, 上の系の公式を書き直した

$$
a^k = \sum_{r=0}^k \stirlingsecond{k}{r}a(a-1)\cdots(a-r+1)
$$

を $a=0,1,2,\ldots,n$ について足し上げると, 

$$
\sum_{a=0}^n a^k = \sum_{r=0}^k \stirlingsecond{k}{r} \frac{(n+1)n(n-1)\cdots(n-r+1)}{r+1}.
$$

左辺は $k=0$ のとき $1+S_0(n)=n+1$ に一致し, $k\geqq 1$ のとき $S_k(n)$ に一致する. $\ds\stirlingsecond{k}{0}=\delta_{k0}$ であることに注意せよ. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**注意:** 第2種Stirling数は次の母函数表示を持つ:

$$
\exp(x(e^t - 1)) = \sum_{n=0}^\infty\sum_{k=0}^n\stirlingsecond{n}{k} x^k \frac{t^n}{n!}.
$$

このことは $\exp(x)$ に $\exp(tx\partial)$ を作用させると,

$$
\exp(tx\partial)\exp(x) = \exp(x e^t)
$$

となり, 上の定理の公式より,

$$
\begin{aligned}
\exp(tx\partial)\exp(x) &= \sum_{n=0}^\infty (x\partial)^n\exp(x) \frac{t^n}{n!} 
\\&=
\sum_{n=0}^\infty \sum_{k=0}^n \stirlingsecond{n}{k}x^k\partial^k\exp(x) \frac{t^n}{n!} =
\exp(x)\sum_{n=0}^\infty \sum_{k=0}^n \stirlingsecond{n}{k}x^k\frac{t^n}{n!}
\end{aligned}
$$

となることからわかる. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# a(a-1)…(a-r+1) の和

a = symbols("a", integer=true)
n = symbols("n", integer=true, positive=true)
ff(a,r) = iszero(r) ? typeof(a)(1) : prod(a-i for i in 0:r-1)

for r in 0:4
    s = sympy.Sum(ff(a,r), (a,0,n))
    latexstring(sympy.latex(s), "=", sympy.latex(s.doit().factor())) |> display
end
```

```julia slideshow={"slide_type": "subslide"}
# Σ_{a=0}^n a^k を a(a-1)…(a-r+1) の和に帰着する方法で計算

stirlingsecond(n,k) = sympy.functions.combinatorial.numbers.stirling(n, k, kind=2)
n = symbols("n", integer=true, positive=true)
SSS(k,n) = expand(sum(stirlingsecond(k,r)*ff(n+1, r+1)/(r+1) for r in 0:k))

for k in 0:12
    latexstring(raw"\sum_{j=0}^n", "j^{$k} =", sympy.latex(factor(SSS(k,n)))) |> display
end
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 第2種Stirling数とBernoulli数の関係

Bernoulli数(正確にはBernoulli多項式 $B_n(x)$ の $x=1$ での値)を第2種Stirling数で表す公式が知られている:

$$
B_n(1) = \sum_{m=0}^\infty (-1)^m m! \stirlingsecond{n+1}{m+1}\frac{1}{m+1}.
$$

そしてさらに, 二項係数がPascalの三角形で計算できるのと同様に, Akiyama-Tanigawa法によって, Bernoulli数を計算できることを示せる.  そのことは, $a_{0m}$ ($m=0,1,2,\ldots$) から $a_{nm}$ ($n\geqq 1$) を帰納的に

$$
a_{n+1,m} = (m+1)(a_{nm} - a_{n,m+1})
$$

によって定めると,

$$
a_{n0} = \sum_{m=0}^\infty (-1)^m m! \stirlingsecond{n+1}{m+1}a_{0m}
$$

が成立することからわかる. $a_{0m}=1/(m+1)$ のとき $a_{n0}=B_n(1)$ となる.

以上の結果の証明については次の論文を参照せよ.

* Masanobu Kaneko. The Akiyama-Tanigawa algorithm for Bernoulli numbers. Journal of Integer Sequences, Vol. 3 (2000), Article 00.2.9. <a href="https://scholar.google.com/scholar?cluster=247561690595205390">Google Scholar</a>
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
struct AkiyamaTanigawa{T,S<:Integer}
    a::Array{T,2}
    N::S
end

Base.length(AT::AkiyamaTanigawa) = AT.N

function AkiyamaTanigawa(a0::AbstractArray{T,1}) where T
    N = size(a0,1)
    a = zeros(eltype(a0), N, N)
    a[0+1,:] = a0
    for n in 0:N-2
        for m in 0:N-n-2
            a[(n+1)+1,m+1] = (m+1) * (a[n+1, m+1] - a[n+1, (m+1)+1])
        end
    end
    AkiyamaTanigawa(a, N)
end

function displayAT(AT::AkiyamaTanigawa)
    N = length(AT)
    s = raw"\begin{matrix}" * "\n"
    for n in 0:N-1
        s *= prod(x * raw"&" for x in @.(sympy.latex(Sym(AT.a[n+1,1:N-n]))))
        s = replace(s, r"&$"=>"")
        s *= "& "^n * raw"\\\\" * "\n"
    end
    s *= raw"\end{matrix}" * "\n"
    l = latexstring(raw"\displaystyle", s)
    display(l)
end

L = 10
a0 = 1 .// collect(1:L+1)
AT = AkiyamaTanigawa(a0)
displayAT(AT)
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
以上の第 $n+1$ 行目が $a_{n0},a_{n1},\ldots,$ である. 隣り合った $a_{nm}$ と $a_{n,m+1}$ の差を取り, $m+1$ 倍したものが $a_{n+1,m}$ になっている. 例えば, 2行目の $a_{12}=1/4$ と $a_{13}=1/5$ の差 $1/20$ の3倍が3行目の $3/20$ になっている. そのように計算した結果の左端の $a_{n0}$ が $B_n(1)$ に一致していることを, 以下のセルの計算結果と比較するとわかる.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
[B(n,1) for n in 0:L]
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### べき乗和とHurwitzのゼータ函数の関係

$s>1$, $x\ne 0,-1,-2,\ldots$ に対して, Hurwitz(フルヴィッツ)のゼータ函数 $\zeta(s,x)$ が

$$
\zeta(s,x) = \sum_{k=0}^\infty\frac{1}{(x+k)^s} = 
\frac{1}{x^s} + \frac{1}{(x+1)^s} + \frac{1}{(x+2)^s} + \cdots
$$

によって定義される. これは形式的には $s=-m$ とおくと,

$$
\zeta(-m,x) = x^m + (x+1)^m + (x+2)^m + \cdots.
$$

と書け, さらに, $m=0,1,2,\ldots$ に対して, 形式的には

$$
\begin{aligned}
\zeta(-m,x) - \zeta(-m,x+n) &=
(x^m + \cdots + (x+n-1)^m + (x+n)^m + (x+n+1)^m + \cdots) 
\\ &\, - ((x+n)^m + (x+n+1)^m + \cdots)
\\ & = x^m + (x+1)^m + \cdots + (x+n-1)^m
\end{aligned}
$$

なので, 特に

$$
\zeta(-m,1) - \zeta(-m,n+1) = 1^m+2^m+\cdots+n^m = S_m(n).
$$

この公式はHurwitzのゼータ函数の解析接続によって論理的に正当化される.

一方, ガンマ函数 $\Gamma(s)=\int_0^\infty e^{-t}x^{s-1}\,dx$ の応用としてよく使われる公式

$$
\frac{1}{a^s} = \frac{1}{\Gamma(s)}\int_0^\infty e^{-at} t^{s-1}\,dt
$$

の $a=x,x+1,x+2,\ldots$ の場合をHurwitzのゼータ函数の定義式に代入して, 無限和と積分の順序を交換して, 等比級数の和の公式を使うと, 

$$
\begin{aligned}
\zeta(s,x) &= 
\frac{1}{\Gamma(s)} \sum_{k=0}^\infty \int_0^\infty e^{-(x+k)t} t^{s-1}\,dt
\\ &=
\frac{1}{\Gamma(s)} \int_0^\infty \frac{e^{-xt}}{1-e^{-t}} t^{s-1}\,dt
\\ &=
\frac{1}{\Gamma(s)} \int_0^\infty \frac{t e^{(1-x)t}}{e^t-1} t^{s-2}\,dt.
\end{aligned}
$$

このようにして, 自然にBernoulli多項式に $1-x$ を代入したものの母函数

$$
\frac{t e^{(1-x)t}}{e^t-1} = \sum_{k=0}^\infty B_k(1-x)\frac{t^k}{k!}
$$

が出て来る. この結果はべき乗和を無限和に拡張して得られるHurwitzのゼータ函数の中に自然にBernoulli多項式の母函数が現われることを意味している. さらに, $0$ から $\infty$ までの積分を $0$ から $1$ までの積分と $1$ から $\infty$ までの積分の和に分解し, $0$ から $1$ までの積分の中の $B_k(1-x)$ の母函数 $\ds \frac{t e^{(1-x)t}}{e^t-1}$ をそれから $\ds\sum_{k=0}^N B_k(1-x)\frac{t^k}{k!}$ を引いて足したもので置き換え, 足した分から得らえる項を $0$ から $1$ まで積分することによって, 次が得られる:

$$
\begin{aligned}
\zeta(s,x) = \frac{1}{\Gamma(s)}\biggl[&
\int_1^\infty \frac{t e^{(1-x)t}}{e^t-1} t^{s-2}\,dt 
\\ &\, +
\int_0^1 \left(\frac{t e^{(1-x)t}}{e^t-1} - \sum_{k=0}^N B_k(1-x)\frac{t^k}{k!}\right)t^{s-2}\,dt 
\\ &\, +
\sum_{k=0}^N \frac{B_k(1-x)}{k!}\frac{1}{s+k-1}
\biggr].
\end{aligned}
$$

この公式の右辺は $\imag s > -N$, $\imag x > 0$ で意味を持ち, そこへの $\zeta(s,x)$ の解析接続を与える.  $m\in\Z$,  $0\leqq m < N$ のとき $s\to -m$ とすることによって, 

$$
\zeta(-m,x) = \frac{(-1)^m B_{m+1}(1-x)}{m+1} = -\frac{B_{m+1}(x)}{m+1}.
$$

ここで $B_k(1-x)=(-1)^k B_k(x)$ および $\Gamma(s+1)=s\Gamma(s)$ より

$$
\frac{1}{\Gamma(s)} = \frac{s(s+1)\cdots(s+m)}{\Gamma(s+m+1)}
$$

となること(これは $s\to-1$ で $0$ になる)を使った($k=m+1$ の分母の $s+m$ と $1/\Gamma(s)$ の分子の $s+m$ がキャンセルすることに注意せよ). この結果を使っても, べき乗和をBernoulli多項式で表す公式

$$
S_m(n) = \zeta(-m,1) - \zeta(-m,n+1) = \frac{B_{m+1}(n+1)-B_{m+1}(1)}{m+1}
$$

が得られる. 

以上の経路でのこの公式の証明はHurwitzのゼータ函数という解析学の対象を用いた分だけ難しくなっているが, Bernoulli多項式の母函数がどのような形で自然に現われるかがよくわかる証明になっている.

べき乗和を真に理解するためにはHurwitzのゼータ函数のような解析学の対象にまで視界を広げる必要がある.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 平面上の点と直線の距離

$a,b,c$ は実数であり, $(a,b)\ne(0,0)$ であると仮定する.

高校の数学の教科書には, $xy$ 平面上の直線 $ax+by+c=0$ と $xy$ 平面上の点 $(X,Y)$ の距離 $d$ が

$$
d = \frac{|aX+bY+c|}{\sqrt{a^2+b^2}}
$$

と表わされることが書いてある. これは, そこに登場する様々な量の幾何学的な意味を理解していれば自明な公式に過ぎないことを以下で説明したい.

$xyz$ 空間内の傾いた平面 $z=ax+by+c$ を考えよう. この平面の傾きは $(a,b)$ で決まっている.

**定理:** $xyz$ 空間内における $z=ax+by+c$ のグラフはベクトル $(a,b)$ の方向が登り方向の傾いた平面になり, その方向の傾きの大きさは $\ds\sqrt{a^2+b^2}$ になる. すなわち, 単位ベクトル $\ds\frac{(a,b)}{\sqrt{a^2+b^2}}$ の分だけ $(x,y)$ をずらすと高さが $\sqrt{a^2+b^2}$ だけ増す.

**証明:** $z=ax+by+c$ は $(x,y)$ を $(\Delta x, \Delta y)$ だけずらすと, $a\Delta x+b\Delta y$ の分だけ変化する. Cauchy-Schwartzの不等式より,

$$
\begin{aligned}
&
-\sqrt{a^2+b^2}\sqrt{(\Delta x)^2+(\Delta y)^2} 
\\ & \qquad\qquad \leqq
a\Delta x+b\Delta y 
\\ & \qquad\qquad\qquad \leqq
\sqrt{a^2+b^2}\sqrt{(\Delta x)^2+(\Delta y)^2}
\end{aligned}
$$

が成立している. ゆえに $\sqrt{(\Delta x)^2+(\Delta y)^2}=1$ という条件のもとでの $a\Delta x+b\Delta y$ の最大値は $\ds(\Delta x,\Delta y)=\frac{(a,b)}{\sqrt{a^2+b^2}}$ のときの $\sqrt{a^2+b^2}$ である. $\QED$

このように $z = ax+by+c$ における $(a,b)$ は平面の傾きの方向と大きさを記述している.  

$xy$ 平面上の点 $(X,Y)$ から直線 $ax+by+c=0$ への距離を $d$ と書き, 点 $(X,Y)$ から直線 $ax+by+c=0$ におろした垂線の足を点 $(X_0, Y_0)$ と書くことにする. このとき, 点 $(X,Y)$ は $(X_0, Y_0)$ からベクトル $\pm (a,b)$ と同じ方向に距離 $d$ の位置にある. したがって, $z = ax+by+c$ の点 $(X,Y)$ における値は

$$
aX+bY+c = \pm\sqrt{a^2+b^2}\;d
$$

になる. $(X,Y)$ が $(X_0,Y_0)$ から見てベクトル $(a,b)$ と同じ方向にあれば符号は $+$ になり, その反対側にあれば符号は $-$ になる. これより, 

$$
d = \frac{|aX+bY+c|}{\sqrt{a^2+b^2}}.
$$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**補足:** 平面 $z=ax+by+c$ の傾き方を調べることは2つのベクトル $(a,b)$ と $(\Delta x, \Delta y)$ の内積

$$
a\Delta x + b\Delta y = \sqrt{a^2+b^2}\sqrt{(\Delta x)^2+(\Delta y)^2}\;\cos\theta
$$

を調べることに他ならない. ここで $\theta$ はそれら2つのベクトルのなす角度である. この公式から, $\sqrt{(\Delta x)^2+(\Delta y)^2}=1$ という条件のもとで $a\Delta x+b\Delta y$ が最大になるのは $\cos\theta=1$ のときであり, 最大値は $\sqrt{a^2+b^2}$ であることがわかる. さらに, $\cos\theta=1$ は 2つのベクトル $(a,b)$ と $(\Delta x, \Delta y)$ が同じ方向を向いていることを意味するので, そのことから, $\sqrt{(\Delta x)^2+(\Delta y)^2}=1$ という条件のもとで $a\Delta x+b\Delta y$ が最大になるのは, $\ds(\Delta x,\Delta y)=\frac{(a,b)}{\sqrt{a^2+b^2}}$ のときであることもわかる. 

高校での授業で「点と直線の距離の公式は内積を使えば容易に導ける」と習った人がいるかもしれないが, 内積の使用は実質的に「平面 $z=ax+by+c$ の傾き方」を調べていることに他ならない. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
a, b, c = 0.8, 0.5, 1.0
f(x,y) = a*x + b*y + c
x = -10:0.1:5
y = -10:0.1:15
surface(x, y, abs.(f.(x',y)), colorbar=false, size=(400,300))
plot!(title="\$z = |$a x + $b y + $c|\$")
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## Jensenの不等式と相加相乗調和平均

相加相乗平均の不等式はそれより圧倒的に一般的なJensenの不等式の特別な場合になっていることを解説する. さらに, 相加相乗調和平均の一般化になっている $p$ 乗平均についても解説する.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Jensenの不等式

$I$ は実数の区間であるとする. 例えば $I=\R$, $I=(0,\infty)$ のような場合を考える. 

$a_1,\ldots,a_n\in I$ であるとし, $p_1,\ldots,p_n\geqq 0$, $p_1+\cdots+p_n=1$ と仮定する.

区間 $I$ 上の実数値函数 $f(x)$ に対して, 実数 $E[f(x)]$ を対応させる函数(汎函数) $E[\ ]$ を

$$
E[f(x)] = p_1 f(a_1) + \cdots + p_n f(a_n)
$$

と定めると, $I$ 上の実数値函数 $f(x), g(x)$ と実数 $\alpha$, $\beta$ に対して以下が成立している.

(1) 線形性: $E[\alpha f(x)+\beta g(x)]=\alpha E[f(x)] + \beta E[g(x)]$.

(2) 単調性: $I$ 全体上で $f(x)\leqq g(x)$ ならば $E[f(x)]\leqq E[g(x)]$.

(3) 規格化条件: $I$ 上の定数値函数 $\alpha$ に対して, $E[\alpha]=\alpha$.

区間 $I$ 上の実数値函数 $f(x)$ が上に凸な函数であるとは, 

$$
a,b\in I,\ 0<t<1 \implies (1-t)f(a)+tf(b)\leqq f((1-t)a+tb)
$$

が成立することだと定める. 下に凸な函数は不等式の向きを逆転することによって定義される.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# log x は上に凸な函数

x = 0:0.01:2.0
a, b = 0.3, 1.5
f(x) = log(x)
t = 0:0.01:1.0
g(a,b,t) = (1-t)*f(a) + t*f(b)
h(a,b,t) = (1-t)*a + t*b
plot(size=(400,250), legend=:topleft, xlims=(0,2.0), ylims=(-2.0, 0.8))
plot!(x, f.(x), label=L"y = \log\,x")
plot!(h.(a,b,t), g.(a,b,t), label="")
plot!([a,a], [-10.0, f(a)], label=L"x = a", ls=:dash)
plot!([b,b], [-10.0, f(b)], label=L"x = b", ls=:dashdot)
```

```julia slideshow={"slide_type": "subslide"}
# exp(x) は下に凸な函数

x = -1:0.01:2
a, b = -0.3, 1.5
f(x) = exp(x)
t = 0:0.01:1.0
g(a,b,t) = (1-t)*f(a) + t*f(b)
h(a,b,t) = (1-t)*a + t*b
plot(size=(400,250), legend=:topleft, xlims=(-1,2), ylims=(0,8))
plot!(x, f.(x), label=L"y = e^x")
plot!(h.(a,b,t), g.(a,b,t), label="")
plot!([a,a], [-0.0, f(a)], label=L"x = a", ls=:dash)
plot!([b,b], [-0.0, f(b)], label=L"x = b", ls=:dashdot)
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**Jensenの不等式:** $f(x)$ が区間 $I$ 上の上に凸な函数ならば $E[f(x)]\leqq f(E[x])$. (下に凸ならば不等式の向きが逆になる.)

**証明:** $f(x)$ が $C^1$ 級の場合に限定して証明する. そのように仮定しない場合には接線の存在を微分に頼らずに直接示す必要が出て来る.

$f(x)$ は上に凸であると仮定し, $\mu=E[x]=p_1a_1+\cdots+p_na_n$ とおく. $E[f(x)]\leqq f(\mu)$ を示したい. $x=\mu$ における $y=f(x)$ の接線を $y=a(x-\mu)+f(\mu)$ と書く. $f(x)$ が上に凸であることより, $I$ 全体上で

$$
f(x) \leqq a(x-\mu)+f(\mu)
$$

が成立する. ゆえに $E[\ ]$ の性質より,

$$
E[f(x)]\leqq E[a(x-\mu)+f(\mu)]=a(E[x]-\mu)+f(\mu) = f(\mu).
$$

最初の等号で $E[\ ]$ の単調性を使い, 2つ目の等号で $E[\ ]$ の線形性と規格化条件を使い, 3つ目の等号で $E[x]=\mu$ を使った. $\QED$

**注意:** 以上の証明法ならば $n$ に関する数学的帰納法を使わずに, しかも $E[\ ]$ の定義に直接触れずに, その基本性質だけを使って証明をできた. $E[\ ]$ と同じ性質を持つものの例として, 確率密度函数 $p(x)$ に対する

$$
E[f(x)] = \int_I f(x)p(x)\,dx
$$

がある. これは確率密度函数 $p(x)$ を持つ確率分布における $f(x)$ の期待値である. $E[\ ]$ は**期待値汎函数**(expected value functional)と呼ばれる. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# 上に凸な函数 f(x) = log x の接線

x = 0:0.01:2.0
μ = 0.7
f(x) = log(x)
g(μ,x) = (1/μ)*(x-μ) + f(μ)
plot(size=(500,350), legend=:topleft, xlims=(0,1.7), ylims=(-2.2, 0.8))
plot!(x, f.(x), label=L"y = \log\,x")
plot!(x, g.(μ,x), label=L"y = a(x-\mu)+f(\mu)", ls=:dashdot)
plot!([μ, μ], [-3.0, f(μ)], label=L"x=\mu", ls=:dash)
plot!(size=(400,250))
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 相加相乗調和平均の不等式

一般の相加相乗平均の不等式は $p_1=p_2=\cdots=p_n=1/n$ と $f(x)=\log x$ の場合にJensenの不等式からただちに得られる. そのとき, $a_1,\ldots,a_n>0$ に対して,

$$
\begin{aligned}
&
E[\log x] = \frac{\log a_1+\cdots+\log a_n}{n} =
\log(a_1\cdots a_n)^{1/n}, 
\\ &
E[x] = \frac{a_1+\cdots+a_n}{n}
\end{aligned}
$$

なので, Jensenの不等式より, 

$$
\begin{aligned}
&
\log(a_1\cdots a_n)^{1/n} = E[\log x], 
\\ &
\log E[x] = \log \frac{a_1+\cdots+a_n}{n}
\end{aligned}
$$

なので, $\log x$ が単調増加函数であることより,

$$
(a_1\cdots a_n)^{1/n} \leqq \frac{a_1+\cdots+a_n}{n}.
$$

この不等式の $a_i$ 達をそれらの逆数で置き換えて, 全体の分子分母を交換することによって,

$$
\frac{n}{\dfrac{1}{a_1}+\cdots+\dfrac{1}{a_n}} \leqq
(a_1,\ldots,a_n)^{1/n}
$$

も得られる.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### p乗平均

$x_1,\ldots,x_n>0$ の $p$ 乗平均 $M_p(x_1,\ldots,x_n)$ を, $p\ne 0$ に対して

$$
M_p(x_1,\ldots,x_n) = \left(\frac{1}{n}\sum_{i=1}^n x_i^p\right)^{1/p}
$$

と定め, $p=0$ に対して

$$
M_0(x_1,\ldots,x_n) = (x_1,\ldots,x_n)^{1/n}
$$

と定める. $M_0$ は相乗平均である. そして, 

$$
\begin{aligned}
&
M_1(x_1,\ldots,x_n) = \frac{x_1+\cdots+x_n}{n}, 
\\ &
M_{-1}(x_1,\ldots,x_n) = \frac{n}{\dfrac{1}{x_1}+\cdots+\dfrac{1}{x_n}}.
\end{aligned}
$$

なので, $M_1$ は加法平均で, $M_{-1}$ は調和平均である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### p→0でのp乗平均の挙動

$p\to 0$ における $p$ 乗平均の挙動を調べよう.

$$
\begin{aligned}
\frac{1}{n}\sum_{i=1}^n x_i^p &= 
\frac{1}{n}\sum_{i=1}^n e^{p\log x_i} 
\\ &=
\frac{1}{n}\sum_{i=1}^n (1 + p\log x_i + O(p^2)) 
\\ &=
1 + p\log(x_1\cdots x_n)^{1/n} + O(p^2)
\end{aligned}
$$

なので, $\log(1+X)=X+O(X^2)$ を使うと, 

$$
\begin{aligned}
\log M_p(x_1,\ldots,x_n) &=
\frac{1}{p}\log \frac{1}{n}\sum_{i=1}^n x_i^p 
\\ &=
\frac{1}{p}\log\left(1 + p\log(x_1\cdots x_n)^{1/n} + O(p^2)\right) 
\\ &=
\log(x_1\cdots x_n)^{1/n} + O(p) 
\\ &=
\log M_0(x_1,\ldots,x_n) + O(p)
\end{aligned}
$$

これより, $M_p(x_1,\ldots,x_n)$ は $p=0$ でも解析的であることがわかる. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $p\to\infty$ のとき $M_p(x_1,\ldots,x_n)\to \max\{x_1,\ldots,x_n\}$ となることを示せ.

**解答例:** $x_1=\cdots=x_k>x_{k+1}\geqq\cdots\geqq x_n$ と仮定してよい. 

$$
\sum_{i=1}^n x_i^p = k x_1^p\left(1 + \sum_{i>k} \left(\frac{x_i}{x_1}\right)^p\right)
$$

なので,

$$
\begin{aligned}
\log M_p(x_1,\ldots,x_n) &=
\frac{1}{p}\log \frac{1}{n}\sum_{i=1}^n x_i^p 
\\ &= -
\frac{1}{p}\log n + \frac{1}{p}\log k + \log x_i 
\\ &\,+
\frac{1}{p}\log\left(1 + \sum_{i>k} \left(\frac{x_i}{x_1}\right)^p\right).
\end{aligned}
$$

であり, $i>k$ のとき $0<x_i/x_1<1$ なので, これは $p\to \infty$ のとき $\log x_1$ に収束し, $M_p(x_1,\ldots,x_n)\to x_1=\max\{x_1,\ldots,x_n\}$ となることがわかる. $\QED$

**注意:** 全く同様にして, $p\to-\infty$ のとき $M_p(x_1,\ldots,x_n)\to \min\{x_1,\ldots,x_n\}$ となることを示せる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### p乗平均のpに関する依存性(1)

$M_p = M_p(x_1,\ldots,x_n)$ とおき, $M_p$ の $p$ に関する依存性について調べたい.

$$
\begin{aligned}
\frac{d}{dp}\log M_p &= 
\frac{d}{dp}\frac{1}{p}\log \frac{1}{n}\sum_{i=1}^n x_i^p 
\\ &=
-\frac{1}{p^2}\log \frac{1}{n}\sum_{i=1}^n x_i^p
+\frac{1}{p}\frac{(1/n)\sum_{i=1}^n x_i^p\log x_i}{(1/n)\sum_{i=1}^n x_i^p}
\\ &=
\frac{1}{p^2(1/n)\sum_{i=1}^n x_i^p}
\\ &\times
\left(
\frac{1}{n}\sum_{i=1}^n x_i^p\log x_i^p - 
\frac{1}{n}\sum_{i=1}^n x_i^p\log \frac{1}{n}\sum_{i=1}^n x_i^p
\right).
\end{aligned}
$$

$f(x)=x\log x$ とおくと, $f'(x)=\log x + 1$, $f''(x)=1/x>0$ なので $f(x)$ は下に凸な函数である. Jensenの不等式を $E[f(x)] = \frac{1}{n}\sum_{i=1}^n f(x_i^p)$ と下に凸な函数 $f(x)=x \log x$ に適用すると, 

$$
\begin{aligned}
\frac{1}{n}\sum_{i=1}^n x_i^p \log x_i^p &=
E[x\log x] \geqq 
E[x]\log E[x] 
\\ &=
\frac{1}{n}\sum_{i=1}^n x_i^p \log\frac{1}{n}\sum_{i=1}^n x_i^p.
\end{aligned}
$$

これで $\ds \frac{d}{dp}\log M_p \geqq 0$ であることがわかった. $M_p$ は $p$ について単調増加函数になる:

$$
p\leqq q \implies M_p(x_1,\ldots,x_n) \leqq M_q(x_1,\ldots,x_n).
$$

この不等式は相加相乗平均の不等式の大幅な一般化になっている. 例えば $M_{-1}\leqq M_0\leqq M_1$ より相加相乗調和平均の不等式

$$
\frac{n}{\dfrac{1}{x_1}+\cdots+\dfrac{1}{x_n}} \leqq
(x_1,\ldots,x_n)^{1/n} \leqq
\frac{x_1+\cdots+x_n}{n}
$$

が得られる.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### p乗平均のpに関する依存性(2)

前節の結果の別証明を与えよう.

$x>0$ の函数 $f(x)=x^p$ は $p<0$, $p\geqq 1$ のとき下に凸で, $0<p<1$ のとき上に凸になる. ゆえにJensenの不等式より, 

$$
\begin{aligned}
&
p<0 \ \text{or}\ p\geqq 1 \implies \left(\frac{1}{n}\sum_{i=1}^n x_i\right)^p \leqq \frac{1}{n}\sum_{i=1}^n x_i^p,
\\ &
0<p<1 \implies \left(\frac{1}{n}\sum_{i=1}^n x_i\right)^p \geqq \frac{1}{n}\sum_{i=1}^n x_i^p.
\end{aligned}
$$

$p<0$ のとき $x\mapsto x^p$ が単調減少函数であることに注意すれば,

$$
\begin{aligned}
&
p\geqq 1 \implies \frac{1}{n}\sum_{i=1}^n x_i \leqq \left(\frac{1}{n}\sum_{i=1}^n x_i^p\right)^{1/p},
\\ &
p<0 \ \text{or}\ 0<p<1 \implies \frac{1}{n}\sum_{i=1}^n x_i \geqq\left(\frac{1}{n}\sum_{i=1}^n x_i^p\right)^{1/p}.
\end{aligned}
$$

$M_p$ は $p=0$ でも連続(実際には解析的)なので, これで

$$
p\leqq 1 \leqq q \implies 
\left(\sum_{i=1}^n x_i^p\right)^{1/p} \leqq
\frac{1}{n}\sum_{i=1}^n x_i \leqq
\left(\sum_{i=1}^n x_i^q\right)^{1/q}
\iff M_p \leqq M_1 \leqq M_q.
$$

が示された. $p\leqq q$ のあいだに $1$ が挟まっていることを取り除ければ, $M_p$ が $p$ について単調増加であることが示される. そのためには, 以上で得た結果の $x_i$ をそれぞれ $x_i^r$ で置き換えて, 全体を $1/r$ 乗すると, $r<0$ の場合には不等号の向きの反転が起こり, 結果的に次の不等式が得られる: $p\leqq 1 \leqq q$ のとき,

$$
\begin{aligned}
&
r>0 \implies
\left(\sum_{i=1}^n x_i^{pr}\right)^{1/(pr)} \leqq
\left(\frac{1}{n}\sum_{i=1}^n x_i^r\right)^{1/r} \leqq
\left(\sum_{i=1}^n x_i^{qr}\right)^{1/(qr)}
\quad \text{and}\quad pr\leqq r\leqq qr,
\\ &
r<0 \implies
\left(\sum_{i=1}^n x_i^{pr}\right)^{1/(pr)} \geqq
\left(\frac{1}{n}\sum_{i=1}^n x_i^r\right)^{1/r} \geqq
\left(\sum_{i=1}^n x_i^{qr}\right)^{1/(qr)}
\quad \text{and}\quad pr\geqq r\geqq qr.
\end{aligned}
$$

これと $M_p$ が $p=0$ でも連続であることを合わせれば, $M_p$ が $p$ について単調増加することが示される.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**プロット:** $p\ne 0$ のとき, $\ds M_p(x,y) = \left(\frac{x^p+y^p}{2}\right)^{1/p}$ なので $M_p(x,y)=1$ と $y=(2-x^p)^{1/p}$ と同値であり, $M_0(x,y)=\sqrt{xy}$ なので $M_0(x,y)=1$ と $y=1/x$ は同値である. $M_p(x,y)=1$ のグラフをプロットしよう.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
# M_p(x,y) = 1 のプロット

f(p,x) = iszero(p) ? 1/x : (2 - x^p)^(1/p)
P = plot(size=(500,500))
ps = [-10, -2, -1, 0, 1, 2, 10]
for p in ps
    a = 2^(1/p)
    if p > 0
        Δx = 2^(1/p)/1000
        x = Δx:Δx:a
    else
        Δx = 3/1000
        x = a+eps():Δx:3
    end
    plot!(x, f.(p,x), label="p = $p", ls=:auto)
end
plot(P, xlim=(0,3), ylim=(0,3), size=(300,300))
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 単位円に内接する多角形の周長と面積の最大値

正弦函数 $\sin\alpha$ が $0\leqq\alpha\leqq\pi$ において上に凸な函数であることにJensenの不等式を適用することによって, 単位円に内接する $n$ 角形の周長と面積が最大になるのは正 $n$ 角形の場合であることを示そう. 一般に上に凸な函数 $f(x)$ についてJensenの不等式より,

$$
\frac{1}{n}\sum_{i=1}^n f(x_i) \leqq f\left(\frac{1}{n}\sum_{i=1}^n x_i\right).
$$

が成立している. さらに, $f(x)$ が強い意味で上に凸ならば($f(x)$ のグラフに局所的に直線になっている部分が存在しなければ), 等号が成立するための必要十分条件は $x_1=\cdots=x_n$ となることである.

$\theta_1<\cdots<\theta_n<\theta_{n+1}=\theta_1+2\pi$ と仮定し, $A_i = (\cos\theta_i, \sin\theta_i)$ ($i=1,\ldots,n$) とおき, 単位円に内接する $n$ 角形 $A_1\cdots A_n$ を考える. 

$\alpha_i = \theta_{i+1}-\theta_i$ とおく. もしも $\alpha_i > \pi$ となる $i$ が存在するならば, 直線 $A_i A_{i+1}$ をそれに平行な原点を通る直線で線対称変換して得られる直線と単位円の交点を $A'_i$, $A'_{i+1}$ とし, $A_i,A_{i+1}$ のぞれぞれを $A'_i,A'_{i+1}$ で置き換えて得られる単位円に内接する $n$ 角形を考えることによって, 単位円に内接する $n$ 角形の周長と面積を真に大きくすることができる. ゆえに, 単位円に内接する $n$ 角形で周長の面積の最大化に興味があるならば, すべての $i=1,\ldots,n$ について $\alpha_i \leqq\pi$ であると仮定してよい. 以下ではそのように仮定する. 

**補足:** $\alpha_i = \theta_{i+1} - \theta_i > \pi$ のとき, $\theta'_i = \theta_i + (\alpha_i-\pi) = \theta_{i+1}-\pi$, $\theta'_{i+1}=\theta_{i+1}-(\alpha_i-\pi) = \theta_i+\pi$,  $A'_i = (\cos\theta'_i, \sin\theta'_i)$,  $A'_{i+1} = (\cos\theta'_{i+1}, \sin\theta'_{i+1})$ とおくと, 線分 $\overline{A_i A_{i+1}}$ と線分 $\overline{A'_i A'_{i+1}}$ は平行で同じ長さになり, $n$ 角形 $A_1\cdots A'_i A'_{i+1}\cdots A_n$ の周長と面積は $n$ 角形 $A_1\cdots A_n$ のそれらよりも真に大きくなる. 図を描いてみよ! $\QED$

以上の設定のもとで, $n$ 角形 $A_1\cdots A_n$ の周長 $L$ と面積 $S$ について以下が成立している.

線分 $\overline{A_i A_{i+1}}$ の長さは $2\sin(\alpha_i/2)$ に等しいので, 

$$
\begin{aligned}
L = 2\sum_{i=1}^n \sin\frac{\alpha_i}{2} = 2n\,\frac{1}{n}\sum_{i=1}^n \sin\frac{\alpha_i}{2} \leqq
2n \sin\left(\frac{1}{n}\sum_{i=1}^n\frac{\alpha_i}{2}\right) = 2n\sin\frac{\pi}{n}.
\end{aligned}
$$

この計算中の不等号は $\sin\alpha$ が $0\leqq\alpha\leqq\pi/2$ で上に凸であることとJensenの不等式から従う. この不等式の最右辺は単位円に内接する正 $n$ 角形の周長に等しい. $\sin\alpha$ が $0\leqq\alpha\leqq\pi/2$ で強い意味で凸であることを使えば, 逆に周長 $L$ が最大になるのは単位円に内接する $n$ 角形 $A_1\ldots A_n$ が正 $n$ 角形になるときであることもわかる.

三角形 $\triangle A_iOA_{i+1}$ の面積は $(1/2)\sin\alpha_i$ に等しいので, 

$$
\begin{aligned}
S = \frac{1}{2}\sum_{i=1}^n \sin\alpha_i = \frac{n}{2}\,\frac{1}{n}\sum_{i=1}^n \sin\alpha_i \leqq
\frac{n}{2} \sin\left(\frac{1}{n}\sum_{i=1}^n\alpha_i\right) = \frac{n}{2}\sin\frac{2\pi}{n}.
\end{aligned}
$$

この計算中の不等号は $\sin\alpha$ が $0\leqq\alpha\leqq\pi$ で上に凸であることとJensenの不等式から従う. この不等式の最右辺は単位円に内接する正 $n$ 角形の面積に等しい. $\sin\alpha$ が $0\leqq\alpha\leqq\pi$ で強い意味で凸であることを使えば, 逆に面積 $S$ が最大になるのは単位円に内接する $n$ 角形 $A_1\ldots A_n$ が正 $n$ 角形になるときであることもわかる.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# α_i > π ならば周長と面積をより大きくできること

t = range(0, 2π, length=400)
theta = 2π * [0, 3/20, 14/20, 16/20, 18/20, 1]
phi = copy(theta)
phi[2] = theta[3] - π
phi[3] = theta[2] + π
plot(size=(300,300), aspect_ratio=1, legend=false)
plot!(cos.(t), sin.(t), lw=0.5, color=:black)
plot!(cos.(theta), sin.(theta), color=:blue)
plot!(cos.(phi), sin.(phi), ls=:dash, color=:red)
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## 三角函数の微積分

高校数学の範囲内で三角函数の微分積分学を再構成してみせる. その結果は直接楕円函数論に一般化可能である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "-"}} -->
### 高校の数学の教科書の方針

高校の数学の教科書では以下のような筋道で $\sin x$ の導函数を求めている. 

$0< x <\pi/2$ のとき, 「面積の大小関係」によって

$$
\frac{1}{2}\sin x < \frac{1}{2}x < \frac{1}{2}\frac{\sin x}{\cos x}
$$

が得られ, 全体に $2$ をかけて, 逆数を取って, $\sin x$ をかけると, 

$$
1 > \frac{\sin x}{x} > \cos x
$$

となることから, 挟み撃ちによって

$$
\lim_{x\to 0} \frac{\sin x}{x}=1
$$

を示す. そのとき $\ds\frac{\sin(-x)}{-x}=\frac{\sin x}{x}$ であることに注意せよ. これより

$$
\frac{\cos x - 1}{x^2} = 
\frac{\cos^2 x - 1}{x^2(\cos x+1)} = 
\frac{\sin^2 x}{x^2(\cos x+1)} \to
\frac{1}{2} \quad (x\to 0)
$$

も得られる. 

そして, 三角函数の加法公式

$$
\begin{aligned}
&
\cos(x+y) = \cos x\;\cos y - \sin x\;\sin y, 
\\ &
\sin(x+y) = \cos x\;\sin y + \sin x\;\cos y.
\end{aligned}
$$

を使って, $h\to 0$ のとき

$$
\begin{aligned}
&
\frac{\cos(x+h)-\cos x}{h} =
\frac{\cos x\;\cos h - \sin x\;\sin h - \cos x}{h} 
\\ &\quad =
h\frac{\cos x\,(\cos h - 1)}{h^2} -
\frac{\sin x\;\sin h}{h} 
\to -\sin x,
\\ &
\frac{\sin(x+h) - \sin x}{h} =
\frac{\cos x\;\sin h + \sin x\;\cos h - \sin x}{h}
\\ &\quad =
h\frac{\sin x\,(\cos h - 1)}{h^2} +
\frac{\cos x\;\sin h}{h}
\to \cos x
\end{aligned}
$$

となることを示す. これで

$$
(\cos x)' = -\sin x, \quad (\sin x)' = \cos x
$$

であることが示された.

しかし, 以上の方針は次の節の方針と比較すると, 非常に遠回りになっており, 弧度法の意味での角度の定義(単位円弧の長さで角度を定義すること)が不明瞭になっているという問題がある.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Jikkyo20140125limitsinc.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 曲線の長さが速さの積分になることの応用

高校数学IIIの教科書には $(x(t),y(t))$, $a\leqq t\leqq b$ の軌跡の長さ(曲線の長さ) $L$ が

$$
L = \int_a^b \sqrt{x'(t)^2 + y'(t)^2}\,dt
$$

と表せることが説明されている.  $t$ を時間変数とみなすとき, 点 $(x(t),y(t))$ の運動の時刻 $t$ における速度ベクトルは $(x'(t), y'(t))$ になり, 速さは $\sqrt{x'(t)^2 + y'(t)^2}$ と書ける. 上の公式は曲線の長さを速さの積分で表せることを意味している.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/Jikkyo20140125ArcLength1.jpg", scale="60%")
```

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Jikkyo20140125ArcLength2.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
これを使えば(曲線の長さを上の公式で定義すれば), 三角函数の微分の導出を非常に簡潔な議論で行うことができる. そのことを以下で説明しよう.

$(x(t),y(t)) = (\sqrt{1-t^2}, t)$, $-1<t<1$ は単位円 $x^2+y^2=1$ の右半分の上を動き, $t$ は単位円上の点の $y$ 座標になる. このとき,  

$$
x'(t) = -\frac{t}{\sqrt{1-t^2}}, \quad
y'(t) = 1, \quad
x'(t)^2+y'(t)^2 = \frac{1}{1-t^2}
$$

なので, 単位円 $x^2+y^2=1$ の右半分上の点 $(x,y)$ に対応する弧度法の意味での角度(単位円弧の長さで定義された角度, 左回りに正, 右回りに負とみなす) $\theta=F(y)$ は

$$
\theta = F(y) = \int_0^y \frac{dt}{\sqrt{1-t^2}}
$$

と表わされる. この公式を使えば, 高校の数学の教科書の範囲内では不明瞭だった弧度法の意味での角度が積分論を使って明瞭に定義される.

一般に $\ds\frac{d}{dy}\int_0^y f(t)\,dt = f(y)$ が成立するので,

$$
\frac{d\theta}{dy} = F'(y) = \frac{1}{\sqrt{1-y^2}}.
$$

$\theta = F(y)$ は単位円上の点の $y$ 座標に弧度法の意味での角度を対応させる函数であり, $y = \sin\theta$ の定義は弧度法の意味ので角度 $\theta$ に単位円上の点の $y$ 座標を対応させる函数だったので, $y = \sin\theta$ の定義は $\theta = F(y)$ の逆函数である.

ゆえに, 逆函数の微分によって,

$$
\frac{d}{d\theta}\sin\theta = \frac{dy}{d\theta} = 
\sqrt{1-y^2} = \sqrt{1-\sin^2\theta} = \cos\theta
$$

が得られる.

要するに, 弧度法の意味での角度を単位円上の点の $y$ 座標を用いた積分で表わせば, 単に逆函数の微分として $\sin\theta$ の導函数が $\cos\theta$ になることがわかる. この議論は非常にシンプルである. 

単位円の右側に制限した議論を単位円全体に拡張する作業は読者にまかせる. 現代数学的には円を多様体とみなして議論するのがよい. 三角函数論を完璧に理解するためには「円を多様体とみなす」というような数学的教養が必要になる.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
t = symbols("t")
x = √(1-t^2)
y = t
equ = diff(x, t)^2 + diff(y, t)^2
sol = simplify(equ)
latexstring("x=", sympy.latex(x), raw",\quad y=", sympy.latex(y)) |> display
latexstring(raw"\ds\left(\frac{dx}{dt}\right)^2+\left(\frac{dy}{dt}\right)^2=", sympy.latex(sol))
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** 直線 $y=tx$ と単位円 $x^2+y^2=1$ の右半分の交点は

$$
(x(t),y(t)) = \left(\frac{1}{\sqrt{1+t^2}}, \frac{t}{\sqrt{1+t^2}}\right).
$$

原点を通る直線の傾き $a$ をそれに対応する弧度法の意味での角度 $\theta$ に対応させる函数 $\theta=G(a)$ が

$$
\theta = G(a) = \int_0^a \frac{dt}{1+t^2}
$$

と書けることを確認せよ. これと逆に角度 $\theta$ を直線の傾き $a$ に対応させる函数が $\tan$ の定義なので, $a=\tan\theta$ の定義は $\theta=G(a)$ の逆函数である. $\QED$

解答略.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
t, x, y = symbols("t x y")
equ = [y-t*x, x^2+y^2-1]
s = solve(equ, [x,y])
latexstring(raw"\text{euqation:}\; ", sympy.latex(equ[1]), raw"=0,\ ", sympy.latex(equ[2]), "=0") |> display
latexstring(raw"\text{solution:}\; x = ", sympy.latex(s[2][1]), ", y = ", sympy.latex(s[2][2])) |> display
```

```julia slideshow={"slide_type": "-"}
X, Y= s[2][1], s[2][2]
sol = simplify(diff(X,t)^2 + diff(Y,t)^2)
latexstring(raw"\ds X=", sympy.latex(X), raw",\quad Y=", sympy.latex(Y)) |> display
latexstring(raw"\ds\left(\frac{dX}{dt}\right)^2+\left(\frac{dY}{dt}\right)^2=", sympy.latex(sol))
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** 以下のセルの画像を解読して, 双曲線函数の微積分の理論について整理せよ. $\QED$

解答略.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/sin-sinh.jpg", scale="80%")
```

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/hyperbolicsine.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 楕円積分, 楕円函数, 楕円曲線暗号

$y = \sin\theta$ の逆函数 $\theta = F(y)$ は

$$
\theta = F(y) = \int_0^y \frac{dt}{\sqrt{1-t^2}}
$$

と書けるのであった. これの次の拡張は非常に有名である:

$$
u = F(y,k) = \int_0^y \frac{dt}{\sqrt{(1-t^2)(1-k^2 t^2)}}.
$$

これは**第一種楕円積分**と呼ばれており, その逆函数は $y = \sn(u,k)$ と書かれ, **Jacobiのsn函数**と呼ばれる**楕円函数**の有名な例になっている. $\sin\theta=\sn(\theta,0)$ なので, sn函数はsinの一般化になっている.

竹内端三著『楕圓函数論』は著作権が切れており, 現在では無料で入手可能である:

* <a href="http://kenboushoten.web.fc2.com/">原著の画像ファイル</a>

* <a href="http://yx4.life.coocan.jp/books/oldbooks.html">LaTeX化</a> (<a href="http://yx4.life.coocan.jp/books/takenouchi_daen20080317.pdf">PDF</a>)

* <a href="https://linesegment.web.fc2.com/books/mathematics/daenkansuron/">現代語訳</a>

以下, $k$ を略して, $y = \sn u=\sn(u,k)$ と書く. cn, dn, cd 函数を

$$
(\cn u)^2 = 1 - y^2, \quad
(\dn u)^2 = 1 - k^2 y^2, \quad
\cd u = \frac{\cn u}{\dn u}
$$

を満たすように定義すれば, $(x,y)=(\cd u, \sn u)$ は

$$
x^2 + y^2 = 1 + k^2 x^2 y^2
$$

を満たしている. この等式は**楕円曲線のEdwards形式**と呼ばれており, この方程式で定義される平面曲線は**Edwards曲線**と呼ばれている. Edwards曲線は $k=0$ の場合に単位円になるので, Edwards形式のもとで楕円曲線は単位円の一般化になっていることがわかる. 

$(x,y)=(\cos\alpha,\sin\alpha)$, $(X,Y)=(\cos\beta,\sin\beta)$ のとき, 三角函数の加法公式より,

$$
(\cos(\alpha+\beta),\sin(\alpha+\beta)) = (xX - yY, xY + yX).
$$

この公式は次のように拡張される: $(x,y)=(\cd u, \sn u)$, $(X,Y)=(\cd v, \sn v)$ のとき,

$$
(\cd(u+v), \sn(u+v)) = 
\left(\frac{xX-yY}{1-k^2xXyY}, \frac{xY+yX}{1+k^2xXyY}\right)
$$

を満たしている. これは $k=0$ の場合の三角函数の加法公式の拡張になっている. この公式は本質的にJacobiの楕円函数の加法公式である. この公式の代数幾何的な証明については次の論文を見よ:

* Thomas Hales, The Group Law for Edwards Curves, <a href="https://arxiv.org/abs/1610.05278">arXiv:1610.05278</a>

楕円曲線のEdwards形式の理論は単位円と三角函数の理論の楕円曲線と楕円函数の理論への拡張になっている. 

楕円曲線のEdwards形式における加法公式は楕円曲線暗号に応用されることによって我々の社会の中で役に立っている. 楕円曲線暗号の規格 <a href="https://www.google.co.jp/search?q=Ed25519+Edwards">Ed25519</a> について検索してみよ. このように, 高校のときに習う三角函数論は楕円函数論に自然に拡張されており, 三角函数の加法公式の楕円函数の加法公式への拡張は楕円曲線暗号の形で我々の社会の中で役に立っている.

19世紀のJacobiによる楕円函数に関する研究が約200年後のコンピューター社会でプライバシーを守るための暗号技術に使われることをJacobiは予想できていなかったはずである. 
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
# Edwards曲線の公式の確認

k, y = symbols("k y")
x² = (1-y^2)/(1-k^2*y^2)
y² = y^2
simplify(x² + y² - 1 - k^2*x²*y²)
```

```julia slideshow={"slide_type": "subslide"}
# Edwards曲線の二通りのプロット

k² = -20

y = -1:0.01:1
x = @. √((1-y^2)/(1-k²*y^2))
P1 = plot(title="\$x^2+y^2=1+k^2x^2y^2\$ for \$k^2=$k²\$", titlefontsize=10)
plot!(aspectratio=1, legend=false)
plot!(x, y, color=:red)
plot!(-x, y, color=:red)

u = 0:0.01:3
P2 = plot(title="(cd u, sn u) for \$k^2=$k²\$", titlefontsize=10)
plot!(aspectratio=1, legend=false)
plot!(cd.(u,k²), sn.(u,k²))

plot(P1, P2, size=(500, 260))
```

```julia slideshow={"slide_type": "subslide"}
# (cn u, sn u)のプロット

k² = -20
u = -5:0.01:5
plot(title="Jacobi's elliptic functions for \$k^2=$k²\$", titlefontsize=10)
plot!(u, cd.(u,k²), label="cd u", ls=:dash)
plot!(u, sn.(u,k²), label="sn u")
plot!(size=(500, 200), legend=:bottomleft)
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## Gauss積分の大学入試問題

Gauss積分の公式 $\ds\int_{-\infty}^\infty e^{-x^2}\,dx=\sqrt{\pi}$ は筆者の個人的な意見では新入生が習う定積分の公式の中で最も重要なものである. Gauss積分の公式の問題が大学入試問題として出題されたことがあるので紹介しておく.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
<a href="https://www.google.co.jp/search?q=%E6%9D%B1%E5%B7%A5%E5%A4%A7+2015+%E6%95%B0%E5%AD%A6">2015年の東京工業大学前期日程の入試問題</a>として次の問題が出題された.

>\[3\] $a>0$ とする. 曲線 $y=e^{-y^2}$ と $x$ 軸, $y$ 軸, および直線 $x=a$ で囲まれた図形を, $y$ 軸のまわりに1回転してできる回転体を $A$ とする.
>
>(1) $A$ の体積 $V$ を求めよ.
>
>(2) 点 $(t,0)$ ($-a\leqq t\leqq a$) を通り, $x$ 軸と垂直な平面による $A$ の切り口の面積を $S(t)$ とするとき, 不等式 $\ds S(t)\leqq\int_{-a}^a e^{-(s^2+t^2)}\,ds$ を示せ.
>
>(3) 不等式 $\ds \sqrt{\pi(1-e^{-a^2})}\leqq\int_{-a}^a e^{-x^2}\,dx$ を示せ.

この問題の内容は, 本質的に**Gauss積分の公式**

$$
\int_{-\infty}^\infty e^{-x^2}\,dx =
\lim_{a\to\infty}\int_{-a}^a e^{-x^2}\,dx = \sqrt{\pi}
$$

の高校数学の範囲内での証明である. 高校数学IIIの教科書にも以下のような問題が載っている. (前者の問題はGauss∫と関係しており, 後者の問題はゼータ函数と関係している.)
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Jikkyo20140125GaussZeta.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
問題文では曲線 $y=e^{-x^2}$ を $y$ 軸のまわりに回転しているが, 以下では $xyz$ 空間内の $xz$ 平面上の曲線 $z=e^{-x^2}$ を $z$ 軸のまわりに回転して得られる曲面を扱う. さらに $a$ の代わりに $r$ と書く. 

$xyz$ 空間内の $xz$ 平面 $y=0$ 上の曲線 $z=e^{-x^2}$ を $z$ 軸のまわりに回転して得られる曲面と高さ $0<t\leqq 1$ の平面 $z=t$ の交わりは, 平面 $z=t$ 内の半径の2乗が $-\log t$ の円になり, その曲面は

$$
z = e^{-(x^2+y^2)}
$$

と表わされることがわかる. 

以下 $r>0$ であるとする.

平面 $y=0$ 上の曲線 $z=e^{-x^2}$ と $x$ 軸と直線 $x=r$ で囲まれた領域を $z$ 軸のまわりに1回転してできる回転体を $A(r)$ と書く. 上で述べたことより, $A(r)$ の体積 $V(r)$ は次のように計算される:

$$
\begin{aligned}
V(r) &= 
\pi r^2 e^{-r^2} + \int_{e^{-r^2}}^1 \pi(-\log t)\,dt 
\\ &=
\pi r^2 e^{-r^2} - \pi[t\log t - t]_{e^{-r^2}}^1 
\\ &=
\pi r^2 e^{-r^2} -\pi(-1 + r^2 e^{-r^2} + e^{-r^2}) 
\\ &=
\pi(1-e^{-r^2}).
\end{aligned}
$$

曲面 $z=e^{-(x^2+y^2)}$ と $xy$ 平面 $z=0$ と4つの平面 $x=\pm r$, $y=\pm r$ で囲まれた領域を $B(r)$ と書く. そして, $-r\leqq t\leqq r$ のとき, $A(r)$ の平面 $y=t$ による断面の面積は

$$
\int_{-r}^r e^{-(x^2+t^2)}\,dx
$$

になるので, これを $-r\leqq t\leqq r$ で積分すれば $B(r)$ の体積 $W(r)$ が求まる. $t$ を $y$ と書くと,

$$
\begin{aligned}
W(r) &= 
\int_{-r}^r \left(\int_{-r}^r e^{-(x^2+y^2)}\,dx\right)\,dy 
\\ &=
\int_{-r}^r e^{-x^2}\,dx \int_{-r}^r e^{-y^2}\,dy 
\\ &=
\left(\int_{-r}^r e^{-x^2}\,dx\right)^2.
\end{aligned}
$$

$B(r)$ は $A(r)$ を含み, $A(\sqrt{2}\;r)$ に含まれる. それらは次の包含関係から導かれる:

$$
\begin{aligned}
&
\{(x,y)\in\R^2\mid x^2+y^2\leqq r^2\}
\\ & \qquad \subset
\{(x,y)\in\R^2\mid |x|,|y|\leqq r\}
\\ & \qquad\qquad \subset
\{(x,y)\in\R^2\mid x^2+y^2\leqq 2r^2\}.
\end{aligned}
$$

ゆえに, $V(r)\leqq W(r)\leqq V(\sqrt{2}\,r)$ となる. すなわち,

$$
\sqrt{\pi(1-e^{-r^2})} \leqq 
\int_{-r}^r e^{-x^2}\,dx \leqq 
\sqrt{\pi(1-e^{-2r^2})}.
$$

これより,

$$
\lim_{r\to\infty}\int_{-r}^r e^{-x^2}\,dx = \sqrt{\pi}
$$

となることがわかる.

以上の計算は次のようにまとめられる:

$$
\begin{aligned}
\left(\int_{-\infty}^\infty e^{-x^2}\,dx\right)^2 &=
\int_{-\infty}^\infty \int_{-\infty}^\infty e^{-(x^2+y^2)}\,dx\,dy 
\\ &=
\int_0^1 \pi(-\log z)\,dz = \pi[z\log z - z]_0^1 = \pi.
\end{aligned}
$$

Gauss積分は正規分布の確率密度函数の理解に必須であり, その他にも多くの場面に現われ, 非常に重要な定積分である.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
f(x,y) = exp(-(x^2+y^2))
g(x,y,r) = x^2+y^2 ≤ r^2 ? exp(-(x^2+y^2)) : zero(x)
h(x,y,r) = (abs(x) ≤ r && abs(y) ≤ r) ? exp(-(x^2+y^2)) : zero(x)

x = range(-2, 2, length=201)
y = range(-2, 2, length=201)
r = 1/√2
```

```julia slideshow={"slide_type": "-"}
# z = e^{-(x^2+y2)} のグラフ
surface(x, y, f.(x', y), size=(400,250), colorbar=false)
```

```julia slideshow={"slide_type": "-"}
# A(r) のグラフ (r=1/√2)
surface(x, y, g.(x', y, r), size=(400,250), colorbar=false)
```

```julia slideshow={"slide_type": "-"}
# B(r) のグラフ (r=1/√2)
surface(x, y, h.(x', y, r), size=(400,250), colorbar=false)
```

```julia slideshow={"slide_type": "-"}
# A(√2 r) のグラフ (r=1/√2)
surface(x, y, g.(x', y, √2*r), size=(400,250), colorbar=false)
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## ガンマ函数の応用

高校数学では $\cos x$, $\sin x$, $e^x$, $\log x$ などの初等函数について習うが, 大学新入生が新たに習う特殊函数として, ゼータ函数 $\ds\zeta(s)$, ガンマ函数 $\Gamma(s)$, ベータ函数 $B(p,q)$ は特に重要である. この節では高校数学にも密かにガンマ函数にあたるものが現われていたことについて解説する. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 多項式×指数函数の積分

$n$ は0以上の整数であるとする. 高校数学IIIの教科書にはよく次の形の不定積分を求める問題が書いてある:

$$
\int x^n e^x\,dx.
$$

以下ではこれと本質的に同じ($x$ を $-x$ で置き換えて得られる)

$$
\int x^n e^{-x}\,dx
$$

を扱う. 部分積分を次々に使うと,

$$
\begin{aligned}
&
\int x^n e^{-x}\,dx 
\\ &= -x^n e^{-x} + n\int x^{n-1}e^{-x}\,dx
\\ &= -x^n e^{-x} - nx^{n-1}e^{-x} 
\\ &+ n(n-1)\int x^{n-2}e^{-x}\,dx
\\ &= -x^n e^{-x} - nx^{n-1}e^{-x} - n(n-1)x^{n-2}e^{-x} 
\\ &\qquad + n(n-1)(n-2)\int x^{n-3}e^{-x}\,dx
\\ &=
\cdots\cdots\cdots\cdots
\\ &= -x^n e^{-x} - nx^{n-1}e^{-x} - n(n-1)x^{n-2}e^{-x} - \cdots 
\\ &\qquad + n(n-1)\cdots 2 x e^{-x} - n!e^{-x}
\\ &= -(x^n + nx^{n-1}e^{-x} + n(n-1)x^{n-2}+ \cdots 
\\ &\qquad+ n(n-1)\cdots 2 x + n!)e^{-x}.
\end{aligned}
$$

積分定数は省略した. これは $x\to\infty$ で $0$ に収束し, $x=0$ のとき $-n!$ になる. ゆえに

$$
\lim_{a\to\infty}\int_0^a x^n e^{-n}\,dx = 0 - (-n!) = n!.
$$

大学1年のときの解析学の授業でガンマ函数

$$
\Gamma(s) = \int_0^\infty e^{-x} x^{s-1}\,dx \quad (s > 0)
$$

について習う. 上の高校数学の範囲内の結果は $\Gamma(n+1)=n!$ が成立することを意味している.

以上のように高校数学IIIの教科書にある $\ds\int x^n e^x\,dx$ 型の不定積分を求める問題は本質的にガンマ函数に関する問題だとみなされる.

以下のセルに実際の教科書の様子を引用しておく. 例題はガンマ函数に研究課題は三角函数の**Laplace変換**(ラプラス変換)を実質的に扱っているとみなされる. 
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**注意:** $a>0$, $s>0$ に関する次の公式はよく使われる:

$$
\int_0^\infty e^{-at} t^{s-1}\,dt = \frac{\Gamma(s)}{a^s}.
$$

この公式は $t=x/a$ という置換積分によって容易に示される. この公式は

$$
\frac{1}{a^s} = \frac{1}{\Gamma(s)} \int_0^\infty e^{-at} t^{s-1}\,dt
$$

の形で使われることも多い. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Jikkyo20140125GammaLaplace.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Stirlingの公式

**準備:** $n\to\infty$ のとき, Taylor展開 $\log(1+X)=X-X^2/2+O(X^3)$ を使うと,

$$
\begin{aligned}
&
\log\left(e^{-\sqrt{n}\,y}\;\left(1+\frac{y}{\sqrt{n}}\right)^n\right) =
-\sqrt{n}\;y + n\log\left(1+\frac{y}{\sqrt{n}}\right) 
\\ &\qquad=
-\sqrt{n}\;y + n\left(\frac{y}{\sqrt{n}}-\frac{y^2}{2n} + O(n^{-3/2})\right) 
\\ &\qquad= -
\frac{y^2}{2} + O(n^{-1/2}) \to -\frac{y^2}{2}.
\end{aligned}
$$

なので, 

$$
\int_{-\sqrt{n}}^\infty e^{-\sqrt{n}\,y}\;\left(1+\frac{y}{\sqrt{n}}\right)^n\,dy \to
\int_{-\infty}^\infty e^{-y^2/2}\,dy = \sqrt{2\pi}.
$$

最後の等号で $a>0$ のとき

$$
\int_{-\infty}^\infty e^{-y^2/a}\,dy = \sqrt{a\pi}
$$

となることを使った. この公式はGauss積分の公式

$$
\int_{-\infty}^\infty e^{-x^2}\,dx = \sqrt{\pi}
$$

で $x=y/\sqrt{a}$ とおけば得られる. $\QED$

正の整数 $n$ の階乗 $n!$ をガンマ函数で表すと,

$$
n! = \Gamma(n+1) = \int_0^\infty e^{-x}x^n\,dx
$$

なので, $\ds x = n + \sqrt{n}\;y = n(1+y/\sqrt{n})$ と積分変数を変換すると,

$$
n! = 
n^n e^{-n}\sqrt{n}
\int_{-\sqrt{n}}^\infty e^{-\sqrt{n}\,y}\;\left(1+\frac{y}{\sqrt{n}}\right)^n\,dy.
$$

したがって, 上で準備した結果を使うと, $n\to\infty$ のとき

$$
n! \sim n^n e^{-n}\sqrt{n}\sqrt{2\pi} = n^n e^{-n} \sqrt{2\pi n}.
$$

これを**Stirlingの公式**(スターリングの公式)と呼ぶ. ここで $a_n\sim b_n$ は $a_n/b_n\to 1$ となることを意味する.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** Stirlingの公式の誤差が $n=1,2,\ldots,10$ でどの程度であるかを確認せよ. $\QED$

次のセルを参照せよ.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
stirling_approx(n) = n^n * exp(-n) * √(2π*n)
error(x, x₀) = x - x₀            # 誤差
relative_error(x, x₀) = x/x₀ - 1 # 相対誤差

@printf("%2s %10s %13s %13s %13s\n", "n", "n!", "Stirling", "Error", "Rel.Err.")
println("-"^60)
for n in 1:10
    ft = factorial(n)
    s = stirling_approx(n)
    err = error(s, ft)
    relerr = relative_error(s, ft)
    @printf("%2d %10d %13.4f %13.4f %13.4f\n", n, ft, s, err, relerr)
end
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
$n$ が大きくなるほどStirlingの公式の相対誤差は小さくなる. $n=5$ の段階ですでに相対誤差は $2\%$ を切っており, $n=9$ で相対誤差は $1\%$ を切っている.

Stirlingの公式よりも精密に

$$
n! = n^n e^{-n} \sqrt{2\pi n}\left(1 + \frac{1}{12n} + O(n^{-2})\right)
$$

が成立することが知られている. $1/(12n)$ で補正されたStirlingの公式は $n=1$ の段階ですでに相対誤差が $0.1\%$ 程度になっている:

$$
\frac{\sqrt{2\pi}}{e} = 0.92213\cdots, \quad
\frac{\sqrt{2\pi}}{e}\frac{13}{12} = 0.99898\cdots.
$$

$\sqrt{2\pi} = 2.50662\cdots$ の $13/12$ 倍の $2.71551\cdots$ が $e=2.71828\cdots$ に近いのは偶然ではなく, 補正されたStirlingの公式の $n=1$ の場合だということである.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
stirling_approx1(n) = n^n * exp(-n) * √(2π*n) * (1 + 1/(12n))

@printf("%2s %10s %20s %13s %13s\n", "n", "n!", "Improved Stirling", "Error", "Rel.Err.")
println("-"^65)
for n in 1:10
    ft = factorial(n)
    s₁ = stirling_approx1(n)
    err = error(s₁, ft)
    relerr = relative_error(s₁, ft)
    @printf("%2d %10d %20.5f %13.5f %13.5f\n", n, ft, s₁, err, relerr)
end
```

```julia slideshow={"slide_type": "subslide"}
@show stirling_approx(1)
@show stirling_approx1(1);
```

```julia slideshow={"slide_type": "-"}
@show √(2π)
@show √(2π) * 13/12
@show float(ℯ);
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Stirlingの公式を使うと簡単に解ける大学入試問題

<a href="https://www.google.co.jp/search?q=%E6%9D%B1%E5%B7%A5%E5%A4%A7%E5%85%A5%E8%A9%A6%E5%95%8F%E9%A1%8C+1988+%E6%95%B0%E5%AD%A6">1988年の東京工業大学の入試問題</a>に次の問題があった.

>\[5\] $\ds\lim_{n\to\infty}\left(\frac{_{3n}C_n}{_{2n}C_n}\right)^{1/n}$ を求めよ.

その他にも<a href="https://www.google.co.jp/search?q=%E6%9D%B1%E5%B7%A5%E5%A4%A7%E5%85%A5%E8%A9%A6%E5%95%8F%E9%A1%8C+1968+%E6%95%B0%E5%AD%A6">1968年の東京工業大学の入試問題</a>に次の問題があった.

>\[5\] 次の極限値を求めよ. 
>$$\ds\lim_{n\to\infty}\frac{1}{n}\sqrt[n]{_{2n}P_n}$$

これらの問題はStirlingの公式を使うとほぼただちに答えを得ることができる. 


**前者の問題の解答例:** Stirlingの公式を使うと, $n\to\infty$ のとき

$$
\begin{aligned}
\left(\frac{_{3n}C_n}{_{2n}C_n}\right)^{1/n} &=
\left(\frac{(3n)!/(2n)!}{(2n)!/n!}\right)^{1/n} =
\left(\frac{(3n)!n!}{((2n)!)^2}\right)^{1/n} 
\\ &\sim
\left(\frac
{(3n)^{3n}e^{-3n}\sqrt{2\pi n}\cdot n^n e^{-n}\sqrt{2\pi n}}
{(2n)^{4n}e^{-4n}2\pi n}
\right)^{1/n} =
\frac{3^3}{2^4}.
\end{aligned}
$$

ゆえに $\ds\lim_{n\to\infty}\left(\frac{_{3n}C_n}{_{2n}C_n}\right)^{1/n} = \frac{3^3}{2^4} = \frac{27}{16}$. $\QED$

**後者の問題の解答例:** Stirlingの公式を使うと, $n\to\infty$ のとき

$$
\begin{aligned}
\frac{1}{n}\sqrt[n]{_{2n}P_n} &=
\frac{1}{n}\left(\frac{(2n)!}{n!}\right)^{1/n} \sim
\frac{1}{n}\left(\frac{(2n)^{2n} e^{-2n} \sqrt{2\pi n}}{n^n e^{-n} \sqrt{2\pi n}}\right)^{1/n} =
2^2 e^{-1}.
\end{aligned}
$$

ゆえに $\ds \ds\lim_{n\to\infty}\frac{1}{n}\sqrt[n]{_{2n}P_n} = 2^2 e^{-1} = \frac{4}{e}$. $\QED$

高校の教科書にもこの後者の問題が掲載されている.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Jikkyo20140125Stirling.jpg", scale="80%")
```

```julia slideshow={"slide_type": "subslide"}
# 前者の問題の SymPy による解

n = symbols("n", positive=true)
binom(n,k) = gamma(n+1)/(gamma(k+1)*gamma(n-k+1))
sol = limit((binom(3n,n)/binom(2n,n))^(1/n), n=>oo)
latexstring(raw"\ds\lim_{n\to\infty}\left(\frac{\binom{3n}{n}}{\binom{2n}{n}}\right)^{1/n}=", sympy.latex(sol))
```

```julia slideshow={"slide_type": "-"}
# 後者の問題の SymPy による解

n = symbols("n", positive=true)
sol = limit((1/n)*(gamma(2n+1)/gamma(n+1))^(1/n), n=>oo)
latexstring(raw"\ds\lim_{n\to\infty}\frac{1}{n}\left(\frac{(2n)!}{n!}\right)^{1/n}=", sympy.latex(sol))
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** 上で扱った問題をStirlingの公式を使わずに解け. $\QED$

**ヒント:** 大学入試問題レベルなのでヒントは必要ないと思われるが, 念のためにヒントを与えておく. 対数を取ってから極限を取ると, 区分求積法によって定積分の計算に極限の計算が帰着する. $\QED$

**注意:** 対数を取ってから積分で近似するというアイデアでStirlingの公式を証明することもできる. $\QED$

**注意:** 以上の話題に関する詳しい解説については

* 黒木玄, <a href="https://genkuroki.github.io/documents/20160501StirlingFormula.pdf">ガンマ分布の中心極限定理とStirlingの公式</a>

の第4節を参照せよ. $\QED$

**注意:** Stirlingの公式は場合の数の漸近挙動の分析で基本的な役目を果たす. 二項係数 $\ds\binom{n}{k}$ の $n,k$ が大きなときの漸近挙動**はエントロピー**やその $-1$ 倍の**情報量**と関係がある. この点に関しては

* 黒木玄, <a href="https://genkuroki.github.io/documents/20160616KullbackLeibler.pdf">Kullback-Leibler情報量とSanovの定理</a>

の解説が詳しい. 統計学の授業で「尤度」(ゆうど)の概念について習うが, 尤度がどうして「尤もらしさ」(もっともらしさ)だと解釈できるかはSanovの定理について学ばないと理解不可能である. この意味でSanovの定理は大数の法則や中心極限定理に匹敵するほど統計学の基礎付けにおいて基本的な結果である.  以上の点は赤池弘次氏の論説

* 赤池弘次, <a href="https://www.jstage.jst.go.jp/article/butsuri1946/35/7/35_7_608/_article/-char/ja/">エントロピーとモデルの尤度(〈講座〉物理学周辺の確率統計)</a>, 日本物理学会誌, 1980年35巻7号, pp. 608-614

* 赤池弘次, <a href="https://ismrepo.ism.ac.jp/?action=pages_view_main&active_action=repository_view_main_item_detail&item_id=32568&item_no=1&page_id=13&block_id=21">統計的推論のパラダイムの変遷について</a>, 統計数理研究所彙報, 27巻1号, pp. 5-12, 1980-03

を参照せよ. 将来統計学を理解することが必要になったら, これらの文献を最初に眺めるとよい. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## ベータ函数の応用

この節では高校数学とベータ函数の関係について解説する.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 1/6公式

大学受験のために次の公式を「1/6公式」などと呼んで「暗記せよ」と教えている場合もあるようだ:

$$
\int_a^b (x-a)(b-x)\,dx = \frac{(b-a)^3}{6}.
$$

もちろんそのような数学の教え方はよくない. 実はこの公式は大学1年のときに習うベータ函数に関する公式の特殊な場合だとみなされる. ベータ函数は

$$
B(p,q) = \int_0^1 x^{p-1}(1-x)^{q-1}\,dx \quad(p,q>0)
$$

と定義される. 

ベータ函数はガンマ函数によって次のように表わされるのであった(後で証明する):

$$
B(p,q) = \frac{\Gamma(p)\Gamma(q)}{\Gamma(p+q)}.
$$

例えば $B(2,2)=\Gamma(2)^2/\Gamma(4)=(1!)^2/3!=1/6$ となることがわかる. 以下が成立している: $x=y+a$, $y=(b-a)z$ とおくと, 

$$
\begin{aligned}
&
\int_a^b (x-a)^{p-1}(b-x)^{q-1}\,dx =
\int_0^{b-a} y^{p-1}(b-a-y)^{q-1}\,dy 
\\ &\qquad=
\int_0^1 (b-a)^{p-1}z^{p-1}(b-a)^{q-1}(1-z)^{q-1}(b-a)\,dz
\\ &\qquad=
(b-a)^{p+q-1}B(p,q).
\end{aligned}
$$

これは「1/6公式」の大幅な一般化になっている.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** $B(p,q)=B(q,p)$ を示せ.

**略解1:** $B(p,q)=\Gamma(p)\Gamma(q)/\Gamma(p+q)$ より $B(p,q)=B(q,p)$ であることがわかる. $\QED$

**略解2:** $\ds B(p,q)=\int_0^1 x^{p-1}(1-x)^{q-1}\,dx$ において $x=1-y$ とおくと, $B(p,q)=B(q,p)$ であることがわかる. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**問題:** 高校の教科書にある次の問題をベータ函数を用いて解け.
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
showimg("image/jpeg", "images/Jikkyo20140125Beta.jpg", scale="80%")
```

<!-- #region {"slideshow": {"slide_type": "-"}} -->
**解答例:** 求めるべき面積を $S$ と書くと, 

$$
\begin{aligned}
S &= 2\int_0^1 \sqrt{x(1-x)^2}\;dx 
\\ &=
2\int_0^1 x^{3/2-1}(1-x)^{2-1}\,dx =
2B(3/2,2).
\end{aligned}
$$

そして, 

$$
\begin{aligned}
&
\Gamma(3/2)=\frac{1}{2}\Gamma(1/2)=\frac{\sqrt{\pi}}{2}, 
\\ &
\Gamma(2)=1!=1, 
\\ &
\Gamma(3/2+2)=\Gamma(7/2)=
\frac{5}{2}
\frac{3}{2}
\frac{1}{2}
\sqrt{\pi},
\\ &
S=2B(3/2,2) = \frac{2\Gamma(3/2)\Gamma(2)}{\Gamma(3/2+2)} 
\\ & \;\, =
2\times\frac{\sqrt{\pi}}{2}\times 1 \times \frac{2^3}{1\cdot3\cdot5\sqrt{\pi}} =
\frac{8}{15}.
\qquad\QED
\end{aligned}
$$
<!-- #endregion -->

```julia slideshow={"slide_type": "-"}
x = symbols("x", real=true)
sol = 2integrate(√(x*(1-x)^2), (x,0,1))
latexstring(raw"\ds 2\int_0^1\sqrt{x(1-x^2)}\,dx=", sympy.latex(sol))
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### sinのべきの定積分

$n$ は0以上の整数であるとする. 高校数学では

$$
S_n = \int_0^{\pi/2} \sin^n\theta\,d\theta
$$

の形の定積分を扱うことがある. これは本質的にベータ函数の特別な場合 $B(1/2, q)$ に一致する. 実際, $x=\cos^2\theta$ とおくと,

$$
\begin{aligned}
B(1/2, q) &= \int_0^1 x^{-1/2}(1-x)^{q-1}\,dx 
\\ &=
\int_0^{\pi/2} (\cos\theta)^{-1} \;(\sin\theta)^{2q-2}\;2\cos\theta\;\sin\theta\;d\theta
\\ &=
2\int_0^{\pi/2} (\sin\theta)^{2q-1}\,d\theta.
\end{aligned}
$$

特に

$$
\frac{1}{2}B\left(\frac{1}{2}, \frac{n+1}{2}\right) = \int_0^{\pi/2}\sin^n\theta\,d\theta. 
$$

より一般に

$$
\frac{1}{2}B\left(\frac{m+1}{2}, \frac{n+1}{2}\right) = 
\int_0^{\pi/2}\cos^m\theta\;\sin^n\theta\,d\theta. 
$$

ベータ函数の応用範囲は結構広い.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### ガンマ函数とベータ函数の関係

$p,q>0$ であると仮定する. 

ベータ函数は $x=1/(1+t)$, $dx=-dt/(1+t)^2$ という積分変数の変換によって

$$
\begin{aligned}
B(p,q)& = \int_0^1 x^{p-1}(1-x)^{q-1}\,dx 
\\&=
\int_0^\infty \frac{1}{(1+t)^{p-1}}\frac{t^{q-1}}{(1+t)^{q-1}}\frac{dt}{(1+t)^2} 
\\&=
\int_0^\infty \frac{t^{q-1}}{(1+t)^{p+q}}\,dt.
\end{aligned}
$$

この計算における最後の行によるベータ函数の表示は統計学における第2種ベータ分布で使用され, $\ds B(p,q)=\int_0^1 x^{p-1}(1-x)^{q-1}\,dx$ という表示は第1種ベータ分布で使用される. どちらの表示も重要である.

$a,b>0$ のとき, 積分変数の変換 $x=y/a$ によって,

$$
\begin{aligned}
\int_0^\infty e^{-ax}x^{b-1}\,dx &= 
\int_0^\infty e^{-y}\frac{x^{b-1}}{a^{b-1}}\frac{dy}{a} 
\\ &= 
\frac{1}{a^b}\int_0^\infty e^{-y}x^{b-1}\,dy = 
\frac{\Gamma(b)}{a^b}.
\end{aligned}
$$

ガンマ函数はこの形式で自然に現われることが非常に多い.

以上の準備のもとで, 

$$
\Gamma(p)=\int_0^\infty e^{-x}x^{p-1}\,dx, \quad
\Gamma(q)=\int_0^\infty e^{-y}y^{p-1}\,dy
$$

の積は以下のように計算される. $y=tx$ という積分変数の変換(これは平面上の $(x,y)$ を傾き $t$ の原点を通る直線と $x$ の値で表示する変数変換であり, それなりの自然さを持っている)と積分順序の交換によって,

$$
\begin{aligned}
\Gamma(p)\Gamma(q) &=
\int_0^\infty \left(\int_0^\infty e^{-x-y}x^{p-1}y^{q-1}\,dy\right)\,dx 
\\ &=
\int_0^\infty \left(\int_0^\infty e^{-x-y}x^{p-1}(tx)^{q-1}x\,dt\right)\,dx 
\\ &=
\int_0^\infty \left(\int_0^\infty e^{-x-tx}x^{p-1}(tx)^{q-1}x\,dt\right)\,dx 
\\ &=
\int_0^\infty \left(\int_0^\infty t^{q-1} e^{-(1+t)x}x^{p+q-1}\,dt\right)\,dx 
\\ &=
\int_0^\infty \left(\int_0^\infty t^{q-1} e^{-(1+t)x}x^{p+q-1}\,dx\right)\,dt 
\\ &=
\int_0^\infty t^{q-1}\frac{\Gamma(p+q)}{(1+t)^{p+q}}\,dt 
\\ &=
\Gamma(p+q) \int_0^\infty \frac{t^{q-1}}{(1+t)^{p+q}}\,dt 
\\ &=
\Gamma(p+q)B(p,q).
\end{aligned}
$$

これで

$$
\Gamma(p)\Gamma(q) = \Gamma(p+q)B(p,q)
$$

が示された. これと $x=\cos^2 \theta$ とおくことによって得られる

$$
\begin{aligned}
B(p,q) &= \int_0^1 x^{p-1}(1-x)^{q-1}\,dx 
\\ &=
2\int_0^{\pi/2} (\cos\theta)^{2p-1} (\sin\theta)^{2q-1}\,d\theta
\end{aligned}
$$

より, $p,q=1/2$ のとき $B(1/2,1/2)=\pi$ であるから,  $\ds\Gamma(1)=\int_0^\infty e^{-x}\,dx=[-e^{-x}]_0^\infty =1$ を使うと, 

$$
\Gamma(1/2)^2 = \Gamma(1)B(1/2,1/2) = \pi, \quad
\therefore\quad
\Gamma(1/2)=\sqrt{\pi}.
$$

さらに, $x=\sqrt{y}$ とおくと, 

$$
\begin{aligned}
\int_{-\infty}^\infty e^{-x^2}\,dx &= 
2\int_0^\infty e^{-x^2}\,dx 
\\ &=
\int_0^\infty e^{-y} y^{-1/2}\,dx =
\Gamma(1/2)=\sqrt{\pi}.
\end{aligned}
$$

要するにガンマ函数とベータ函数の関係はGauss積分の公式 $\ds\int_{-\infty}^\infty e^{-x^2}\,dx=\sqrt{\pi}$ を含んでいる. 

正規分布の確率密度函数を理解するためには, Gauss積分の公式を理解しておかないといけない. Stirlingの公式の導出でもGauss積分の公式を利用した. Gauss積分は多くの数学的場面に普遍的に現われる重要な積分である.
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Gamma-Beta-01.jpg", scale="60%")
```

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Gamma-Beta-02.jpg", scale="60%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### ベータ函数の極限によるガンマ函数の表示とWallisの公式

$\ds B(p,q)=\int_0^1 x^{p-1}(1-x)^{q-1}$ において, $p=s$, $q=n+1$, $x = t/n$ とおいて, $n\to\infty$ とすると,

$$
\begin{aligned}
n^s B(s,n+1) &= 
n^s \int_0^1 x^{s-1}(1-x)^n\,dx 
\\ &=
\int_0^n t^{s-1}\left(1-\frac{1}{n}\right)^n\,dx 
\\ &\to
\int_0^\infty x^{s-1} e^{-x}\,dx = \Gamma(s).
\end{aligned}
$$

特に $s=1/2$ のとき

$$
\sqrt{n}\;B(1/2,n+1)\to \Gamma(1/2) = \sqrt{\pi}.
$$

ベータ函数の三角函数を用いた表示を使うと, 

$$
2 n^s \int_0^{\pi/2} (\cos\theta)^{2s-1}(\sin\theta)^{2n+1}\,d\theta \to \Gamma(s), \quad
2 \sqrt{n} \int_0^{\pi/2} (\sin\theta)^{2n+1}\,d\theta \to \Gamma(1/2).
$$

$\sin$ のべきの $0$ から $\pi/2$ での定積分はGauss積分 $\ds \Gamma(1/2)=\int_{-\infty}^\infty e^{-x^2}\,dx$ の計算にこのような形で関係している.

$n$ が正の整数のとき, 

$$
\begin{aligned}
&
\Gamma(n+1)=n!, \quad \Gamma(1/2)=\sqrt{\pi},
\\ &
\Gamma(n+1/2)=\frac{2n-1}{2}\cdots\frac{3}{2}\frac{1}{2}\sqrt{\pi} 
\\&\qquad=
\frac{1\cdot3\cdots(2n-1)}{2^n}\frac{2\cdot4\cdots(2n)}{2^n n!}\sqrt{\pi} =
\frac{(2n)!}{2^{2n} n!}\sqrt{\pi},
\\ &
\Gamma(n+1+1/2) = 
(n+1/2)\Gamma(n+1/2) = 
\frac{2n+1}{2}\frac{(2n)!}{2^{2n} n!}\sqrt{\pi},
\\ &
\frac{1}{\sqrt{\pi}B(1/2,n+1)} = 
\frac{\Gamma(n+1+1/2)}{\sqrt{\pi}\;\Gamma(1/2)\Gamma(n+1)} 
\\ &\qquad=
\frac{2n+1}{2n}\sqrt{n}\;\frac{1}{2^{2n}}\binom{2n}{n} \to 
\frac{1}{\Gamma(1/2)}=\frac{1}{\sqrt{\pi}}
\quad (n\to\infty).
\end{aligned}
$$

ここで, $\ds\frac{2n+1}{2\sqrt{n}} = \frac{2n+1}{2n}\sqrt{n}$, $\ds\frac{(2n)!}{n!n!}=\binom{2n}{n}$ を使った. $\ds\frac{2n+1}{2n}\to 1$ より, 

$$
\sqrt{n}\;\frac{1}{2^{2n}}\binom{2n}{n} \to \frac{1}{\sqrt{\pi}}.
$$

すなわち

$$
\frac{1}{2^{2n}}\binom{2n}{n} \sim \frac{1}{\sqrt{\pi n}}
$$

が示された. これを**Wallisの公式**(ウォリスの公式)と呼ぶ. これとは見掛け上異なる同値な結果

$$
\prod_{n=1}^\infty \frac{(2n)(2n)}{(2n-1)(2n+1)} = \frac{\pi}{2}
$$

もWallisの公式と呼ぶこともある. 

**問題:** すぐ上の後者のWallisの公式を証明せよ. $\QED$

**ヒント:** すでに証明した前者のWallisの公式を使えば後者を示せる. $B(1/2,n+1)/B(1/2,n+1/2)\to 1$ を書き直しても後者のWallisの公式が得られる. もしくは高校の教科書の掲載されている $\sin$ のべきの $0$ から $\pi/2$ までの定積分の計算結果と上で述べたことを合わせて使ってみよ. 偶数べきと奇数べきの比を考えよ. $\QED$
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
showimg("image/jpeg", "images/Jikkyo20140125Wallis.jpg", scale="50%")
```

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
**参考:** 以上で扱った大学レベルの微分積分学については

* 黒木玄, <a href="https://github.com/genkuroki/Calculus/blob/master/README.md">微分積分学のノート</a>

を参照せよ. 例えば, Wallisの公式については「10 Gauss積分, ガンマ函数, ベータ函数」「12 Fourier解析」に非常に詳しい解説がある. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Gaussの超幾何函数への一般化

$\ds \int_a^b (x-a)^A (b-x)^B \,dx$ 型の積分は本質的にベータ函数とみなせるのであった. これを

$$
I = \int_a^b (x-a)^A (b-x)^B (c-x)^C \,dx
$$

に一般化するとどうなるか. このような一般化は高校生でも自然に思い付きそうである. 

$$
x = (1-t)a + t b = a + (b-a)t = b - (b-a)(1-t), \quad z = \frac{b-a}{c-a}
$$

とおくと, 

$$
I = (b-a)^{A+B+1}(c-a)^C \int_0^1 t^A (1-t)^B (1-zt)^C \,dt. 
$$

Gaussの超幾何函数 ${}_2F_1(a,b,c;z)$ が

$$
{}_2F_1(a,b,c;z) = \frac{1}{B(a,c-a)} \int_0^1 t^{a-1}(1-t)^{c-a-1}(1-zt)^{-b}\,dt
$$

と定義される. 上の積分 $I$ は本質的にGaussの超幾何函数である.

このように高校生が取り扱いに挑戦しそうなちょっとした積分であっても, 本質的にGaussの超幾何函数になってしまうことがある. 高校生に微積分を教える予定がある人はGaussの超幾何函数についても知っておいた方がよいだろう.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Kummerの超幾何函数

$\ds \int_a^b (x-a)^A (b-x)^B \,dx$ 型の積分は

$$
J = \int_a^b (x-a)^A (b-x)^B e^{rx} dx
$$

という型の積分にも一般化される. $r=0$ の場合が本質的にベータ函数の場合である. この積分は

$$
x = (1-t)a + t b = a + (b-a)t = b - (b-a)(1-t), \quad z = (b-a)r
$$

とおくと, 次のように書き直される:

$$
J = (b-a)^{A+B+1} e^{ra} \int_0^1 t^A (1-t)^B e^{zt}\,dt.
$$

Kummerの超幾何函数 ${}_1F_1(a,c;z)$ が

$$
{}_1F_1(a,c;z) = \frac{1}{B(a,c-a)}\int_0^1 t^{a-1}(1-t)^{c-a-1}e^{zt}\,dt
$$

と定義される. 上の積分 $J$ は本質的にKummerの超幾何函数である.

Kummerの超幾何函数はGaussの超幾何函数で

$$
z = \frac{z}{b}
$$

とおいて $b\to\infty$ とすれば得られる: $b\to\infty$ のとき

$$
\begin{aligned}
{}_2F_1\left(a,b,c;\frac{z}{b}\right) &=
\frac{1}{B(a,c-a)}\int_0^1 t^{a-1}(1-t)^{c-a-1}\left(1-\frac{zt}{b}\right)^{-b}\,dt \\
& \to
\frac{1}{B(a,c-a)}\int_0^1 t^{a-1}(1-t)^{c-a-1}e^{zt}\,dt =
{}_1F_1(a,c;z).
\end{aligned}
$$

この手続きは $z = b/t$ における特異点を $z=\infty$ における特異点に合流させる手続きになっており, Kummerの超幾何函数は合流型超幾何函数と呼ばれる超幾何函数の一族のうちの1つになっている.

Gauss積分($\Gamma(1/2)$ に等しい), ガンマ函数 $\Gamma(s)$, ベータ函数 $B(a,b)$, Gaussの超幾何函数 ${}_2F_1(a,b,c;z)$, Kummerの超幾何函数 ${}_1F_1(a,c;z)$ などは特殊函数の広い一族の一部分になっており, 高校数学でも自然に出て来てしまうものだと言える.

この点に関してはツイッターにおける以下のスレッドも参照せよ:

* https://twitter.com/genkuroki/status/1093510712125583360
<!-- #endregion -->

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>ベータ函数の現れ方(1)</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-01.jpg", scale="50%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>ベータ函数の現れ方(2)</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-02.jpg", scale="50%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>ガンマ函数の基礎</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-03.jpg", scale="80%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>Gaussの超幾何函数の現れ方(1)</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-04.jpg", scale="60%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>Gaussの超幾何函数の現れ方(2)</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-05.jpg", scale="70%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>Kummerの超幾何函数の現れ方</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-06.jpg", scale="70%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>ガンマ函数と正弦函数の関係</h4>")
showimg("image/jpeg", "images/Beta-Gamma-Gauss-Kummer-07.jpg", scale="70%")
```

```julia slideshow={"slide_type": "subslide"}
display("text/html", "<h4>Hurwitzのゼータ函数とガンマ函数の関係</h4>")
showimg("image/jpeg", "images/Hurwitz-Gamma.jpg", scale="70%")
```

<!-- #region {"slideshow": {"slide_type": "slide"}} -->
## Taylor展開

例えば, 実教出版の高校数学の教科書『数学III』2014年1月25日発行の終わりの方にはCauchyの平均値の定理の応用としてTaylotの公式を示す議論が載っている. その証明法は高木貞治『解析概論』におけるTaylorの公式の証明法と同じである. 以下ではより「初等的」な証明を解説する.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Taylorの公式の証明

以下では微分積分学の基本定理(微分して積分するとものとの函数に戻るという意味の公式)

$$
f(x) = f(a) + \int_a^x f'(x_1)\,dx_1
$$

のみを用いたTaylorの公式のシンプルな証明法を紹介する. 以下の方針であれば高木貞治『解析概論』におけるTaylorの公式の証明法と違って誰でも容易に理解できるものと思われる.

以下では繰り返し函数を積分する. そのとき括弧の使用量を減らすために積分を

$$
\int_a^x g(x_1)\,dx_1 = \int_a^x dx_1\, g(x_1)
$$

の右辺のように書く場合もある. 例えば,

$$
\begin{aligned}
&
\int_a^x \left(\int_a^{x_1}\left(\int_a^{x_2}g(x_3)\,dx_3\right)\,dx_2\right)\,dx_1 
\\ & \qquad=
\int_a^x dx_1 \int_a^{x_1}dx_2 \int_a^{x_2}dx_3\,g(x_3).
\end{aligned}
$$

右辺の書き方であれば括弧の使用量を大幅に減らすことができる.

以下, $n=4$ であると仮定し, $f(x)$ は $C^n$ 級($n$ 回微分可能で $f^{(n)}$ は連続)であると仮定する.  一般の $n$ についても以下の議論は同様に適用できる. $f^{(4)}(x_4)$ を $x_4=a$ から $x_4=x_3$ まで積分すると

$$
f'''(x_3) = f'''(a) + \int_a^{x_3}dx_4\,f^{(4)}(x_4).
$$

両辺を $x_3=a$ から $x_3=x_2$ まで積分すると

$$
\begin{aligned}
f''(x_2) &= f''(a) + \int_a^{x_2}dx_3\,f'''(x_3)
\\ &=
f''(a) + f'''(a)(x_2-a) + \int_a^{x_2}dx_3\int_a^{x_3}dx_4\,f^{(4)}(x_4).
\end{aligned}
$$

両辺を $x_2=a$ から $x_2=x_1$ まで積分すると

$$
\begin{aligned}
f'(x_1) &= f'(a) + \int_a^{x_1}dx_2\,f''(x_2)
\\ &=
f'(a) + f''(a)(x_1-a) + f'''(a)\frac{(x_1-a)^2}{2} + Q,
\\ 
Q &=\int_a^{x_1}dx_2\int_a^{x_2}dx_3\int_a^{x_3}dx_4\,f^{(4)}(x_4).
\end{aligned}
$$

両辺を $x_1=a$ から $x_1=x$ まで積分すると

$$
\begin{aligned}
f(x) &= f(a) + \int_a^{x}dx_1\,f'(x_1)
\\ &=
f(a) + f'(a)x + f''(a)\frac{(x-a)}{2} + f'''(a)\frac{(x-a)^3}{3!} + R_4,
\\ 
R_4 &=
\int_a^x dx_1\int_a^{x_1}dx_2\int_a^{x_2}dx_3\int_a^{x_3}dx_4\,f^{(4)}(x_4).
\end{aligned}
$$

一般の $n$ では以下が成立する:

$$
\begin{aligned}
&
f(x) = \sum_{k=0}^{n-1}f^{(k)}(a)\frac{(x-a)^k}{k!} + R_n, 
\\ &
R_n = \int_a^x dx_1\int_a^{x_1}dx_2\cdots\int_a^{x_{n-1}}dx_n\,f^{(n)}(x_n).
\end{aligned}
$$

これを**Taylorの公式**と呼び, $R_n$ を**剰余項**と呼ぶ.

Taylorの公式において $\ds\frac{(x-a)^k}{k!}$ の項が出て来る理由も以上の議論では明瞭である. 定数函数 $1$ を $a$ から $x$ まで積分することを $k$ 回繰り返すと, $\ds\frac{(x-a)^k}{k!}$ が出て来る. $n$ 階の導函数を $n$ 回積分するだけなので簡単である.
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### Taylorの公式の剰余項の評価

$R_n$ の大きさの評価不等式を作ろう. ある定数 $M_n$ が存在して, $a$ と $x$ のあいだの実数 $x_n$ について  $|f^{(n)}(x_n)|\leqq M_n$ が成立しているとする. このとき,

$$
|R_n| \leqq \left|\int_a^x dx_1\int_a^{x_1}dx_2\cdots\int_a^{x_{n-1}}dx_n\,M_n\right| =
\frac{M_n|x-a|^n}{n!}.
$$

したがって, もしも $n\to\infty$ のとき $\ds\frac{M_n|x-a|^n}{n!}\to 0$ が成立しているならば, **Taylor展開**

$$
f(x) = \sum_{k=0}^\infty f^{(k)}(a)\frac{(x-a)^k}{k!}
$$

が成立する. 

**例:** $f(x)=e^x$, $a=0$ の場合を考えよう. このとき, $f'(x)=f(x)$ と $f(0)=1$ より, $f^{(k)}(0)=1$ となる.  $r>0$ であるとし, $|x|\leqq r$ であると仮定する.  $0$ と $x$ のあいだの実数 $x_n$ について, $x<a$ ならば $0< f^{(n)}(x_n) = f(x_n) \leqq f(r)=e^r$ となる. したがって,

$$
e^x = 
f(x) =
\sum_{k=0}^{n-1} f^{(k)}(0)\frac{x^k}{k!} + R_n
\sum_{k=0}^{n-1} \frac{x^k}{k!} + R_n
$$

でかつ

$$
|R_n| \leqq 
\frac{e^r |x|^n}{n!} \leqq 
\frac{e^r r^n}{n!} \to 0 \quad (n\to\infty).
$$

$r$ は幾らでも大きくできるので, $|x|$ がどんなに大きくても, 

$$
e^x = \sum_{k=0}^\infty \frac{x^k}{k!}
$$

が成立している. $\QED$
<!-- #endregion -->

<!-- #region {"slideshow": {"slide_type": "subslide"}} -->
### 有名な交代級数の例

**例:** 以下の例のように剰余項の別の積分表示を使ってTaylor展開の収束を示せる場合もある. 等比数列の和の公式より, $x\ne 1$ のとき, 

$$
1+x+x^2+\cdots+x^{n-2} = \frac{1-x^{n-1}}{1-x}
$$

なので

$$
\frac{1}{1-x} = 1+x+x^2+\cdots+x^{n-2} + \frac{x^{n-1}}{1-x}.
$$

両辺を $0$ から $x$ まで積分すると

$$
-\log(1-x) = x+\frac{x^2}{2}+\frac{x^3}{3}+\cdots+\frac{x^{n-1}}{n-1} + 
\int_0^x \frac{t^{n-1}}{1-t}\,dt.
$$

そして, $|x|<1$ のとき, $n\to\infty$ ならば

$$
\left|\int_0^x \frac{t^{n-1}}{1-t}\,dt\right| \leqq
\frac{1}{1-|x|}\left|\int_0^x t^{n-1}\,dt\right| =
\frac{1}{1-|x|}\frac{|x|^n}{n} \to 0.
$$

したがって, $|x|<1$ のとき

$$
-\log(1-x)=\sum_{k=1}^\infty \frac{x^k}{k}=
x+\frac{x^2}{2}+\frac{x^3}{3}+\cdots.
$$

この公式はよく使われる. 

以上の $x$ を $-x$ で置き換えると, $x\ne -1$ のとき,

$$
\begin{aligned}
\log(1+x) &= x-\frac{x^2}{2}+\frac{x^3}{3}-\cdots+(-1)^{n-2}\frac{x^{n-1}}{n-1}
\\ & + 
(-1)^{n-1}\int_0^x \frac{t^{n-1}}{1+t}\,dt.
\end{aligned}
$$

$x\geqq 0$ のとき $0\leqq t\leqq x$ ならば $1/(1+t)\leqq 1$ となるので,

$$
0\leqq \int_0^x \frac{t^{n-1}}{1+t} \leqq
\int_0^x t^{n-1}\,dt = \frac{x^n}{n}.
$$

これは $0\leqq x\leqq 1$ ならば $n\to\infty$ で $0$ に収束する. ゆえに, $0\leqq x\leqq 1$ のとき

$$
\log(1+x) = x-\frac{x^2}{2}+\frac{x^3}{3}-\frac{x^4}{4}+\cdots.
$$

特に $x=1$ のとき

$$
\log 2 = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \cdots.
$$

これは有名な交代級数である. $\QED$

**例:** 次の公式から出発して1つ上の例と同様の議論を行ってみよう:

$$
1+(-x^2)+(-x^2)^2+(-x^2)^3+\cdots+(-x^2)^{n-1} = \frac{1-(-x^2)^n}{1+x^2}.
$$

これより,

$$
\frac{1}{1+x^2} =
1-x^2+x^4-x^6+\cdots+(-1)^{n-1}x^{2n-2} + (-1)^n\frac{x^{2n}}{1+x^2}.
$$

$x\geqq 0$ であるとし, 両辺を $0$ から $x$ まで積分すると,

$$
\begin{aligned}
\arctan x &= \int_0^x\frac{dt}{1+t^2} 
\\ &=
x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \cdots + (-1)^{n-1}\frac{x^{2n-1}}{2n-1} 
\\ &+
(-1)^n\int_0^x \frac{t^{2n}}{1+t^2}\,dt.
\end{aligned}
$$

そして,

$$
0\leqq\int_0^x \frac{t^{2n}}{1+t^2}\,dt \leqq
\int_0^x t^{2n}\,dt = \frac{x^{2n+1}}{2n+1}.
$$

これは $0\leqq x\leqq 1$ ならば $n\to\infty$ で $0$ に収束するので,

$$
\arctan x = \sum_{k=1}^\infty (-1)^{k-1}\frac{x^{2k-1}}{2k-1} =
x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \cdots
$$

が成立している. 特に $x=1$ のとき,

$$
\frac{\pi}{4} = \sum_{k=1}^\infty (-1)^{k-1}\frac{1}{2k-1} =
1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots.
$$

これも有名な交代級数である. **Leibniz級数**(ライプニッツ級数)と呼ばれているらしい. $\QED$
<!-- #endregion -->
