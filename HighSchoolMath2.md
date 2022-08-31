---
jupyter:
  jupytext:
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

# 高校数学の話題2

* 黒木玄 (Gen Kuroki)
* 2022-08-30
* Copyright 2022 Gen Kuroki
* License: MIT https://opensource.org/licenses/MIT
* Repository: https://github.com/genkuroki/HighSchoolMath
$
\newcommand\ds{\displaystyle}
\newcommand\op{\operatorname}
\newcommand\BetaBinom{\op{BetaBinom}}
\newcommand\Polya{\op{Polya}}
\newcommand\Binomial{\op{Binomial}}
\newcommand\Hypergeom{\op{Hypergeom}}
\newcommand\R{\mathb{R}}
\newcommand\Z{\mathb{Z}}
$

このノートでは高校の数学の教科書にあるような話題を扱い, その数学的背景について解説する.

タイポや自明な誤りは自分で訂正して読むこと. 本質的な誤りがあれば著者に教えて欲しい.

このノートの想定読者は大学である程度を数学を学んだで人で高校で習った数学について見直したい人達である.

このノートは未完成であり, 後で新たな話題を追加する可能性がある.

<!-- #region toc=true -->
<h1>目次<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#ポリアの壺" data-toc-modified-id="ポリアの壺-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>ポリアの壺</a></span><ul class="toc-item"><li><span><a href="#問題：n回目に赤玉が出る確率" data-toc-modified-id="問題：n回目に赤玉が出る確率-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>問題：n回目に赤玉が出る確率</a></span></li><li><span><a href="#解答例：n回目に赤玉が出る確率の漸化式による導出" data-toc-modified-id="解答例：n回目に赤玉が出る確率の漸化式による導出-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>解答例：n回目に赤玉が出る確率の漸化式による導出</a></span></li><li><span><a href="#解答例：n回目に赤玉が出る確率の漸化式を使わない導出" data-toc-modified-id="解答例：n回目に赤玉が出る確率の漸化式を使わない導出-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>解答例：n回目に赤玉が出る確率の漸化式を使わない導出</a></span></li><li><span><a href="#ポリアの壺の大学入試問題の例：名古屋大学2007年文系前期3(b)" data-toc-modified-id="ポリアの壺の大学入試問題の例：名古屋大学2007年文系前期3(b)-1.4"><span class="toc-item-num">1.4&nbsp;&nbsp;</span>ポリアの壺の大学入試問題の例：名古屋大学2007年文系前期3(b)</a></span></li><li><span><a href="#問題：名古屋大学2007年文系前期3(b)の一般化" data-toc-modified-id="問題：名古屋大学2007年文系前期3(b)の一般化-1.5"><span class="toc-item-num">1.5&nbsp;&nbsp;</span>問題：名古屋大学2007年文系前期3(b)の一般化</a></span></li><li><span><a href="#解答例：P(k|n,a,b)の漸化式による導出" data-toc-modified-id="解答例：P(k|n,a,b)の漸化式による導出-1.6"><span class="toc-item-num">1.6&nbsp;&nbsp;</span>解答例：P(k|n,a,b)の漸化式による導出</a></span></li><li><span><a href="#解答例：P(k|n,a,b)の漸化式を使わない導出" data-toc-modified-id="解答例：P(k|n,a,b)の漸化式を使わない導出-1.7"><span class="toc-item-num">1.7&nbsp;&nbsp;</span>解答例：P(k|n,a,b)の漸化式を使わない導出</a></span></li></ul></li><li><span><a href="#ポリアの壺と二項分布や超幾何分布の関係" data-toc-modified-id="ポリアの壺と二項分布や超幾何分布の関係-2"><span class="toc-item-num">2&nbsp;&nbsp;</span>ポリアの壺と二項分布や超幾何分布の関係</a></span><ul class="toc-item"><li><span><a href="#ベータ二項分布,-二項分布,-超幾何分布" data-toc-modified-id="ベータ二項分布,-二項分布,-超幾何分布-2.1"><span class="toc-item-num">2.1&nbsp;&nbsp;</span>ベータ二項分布, 二項分布, 超幾何分布</a></span></li><li><span><a href="#ベータ二項分布,-二項分布,-超幾何分布の統一的理解-(ポリア分布)" data-toc-modified-id="ベータ二項分布,-二項分布,-超幾何分布の統一的理解-(ポリア分布)-2.2"><span class="toc-item-num">2.2&nbsp;&nbsp;</span>ベータ二項分布, 二項分布, 超幾何分布の統一的理解 (ポリア分布)</a></span></li><li><span><a href="#問題：二項分布がポリア分布の極限になっていること" data-toc-modified-id="問題：二項分布がポリア分布の極限になっていること-2.3"><span class="toc-item-num">2.3&nbsp;&nbsp;</span>問題：二項分布がポリア分布の極限になっていること</a></span></li><li><span><a href="#解答例：二項分布がポリア分布の極限になっていること" data-toc-modified-id="解答例：二項分布がポリア分布の極限になっていること-2.4"><span class="toc-item-num">2.4&nbsp;&nbsp;</span>解答例：二項分布がポリア分布の極限になっていること</a></span><ul class="toc-item"><li><span><a href="#二項分布,-ベータ二項分布,-超幾何分布の同時プロット(素朴な方法)" data-toc-modified-id="二項分布,-ベータ二項分布,-超幾何分布の同時プロット(素朴な方法)-2.4.1"><span class="toc-item-num">2.4.1&nbsp;&nbsp;</span>二項分布, ベータ二項分布, 超幾何分布の同時プロット(素朴な方法)</a></span></li><li><span><a href="#二項分布,-ベータ二項分布,-超幾何分布の同時プロット(1つの函数にまとめる方法)" data-toc-modified-id="二項分布,-ベータ二項分布,-超幾何分布の同時プロット(1つの函数にまとめる方法)-2.4.2"><span class="toc-item-num">2.4.2&nbsp;&nbsp;</span>二項分布, ベータ二項分布, 超幾何分布の同時プロット(1つの函数にまとめる方法)</a></span></li></ul></li><li><span><a href="#問題：ポリア分布の期待値と分散" data-toc-modified-id="問題：ポリア分布の期待値と分散-2.5"><span class="toc-item-num">2.5&nbsp;&nbsp;</span>問題：ポリア分布の期待値と分散</a></span></li><li><span><a href="#解答例：ポリア分布の期待値と分散" data-toc-modified-id="解答例：ポリア分布の期待値と分散-2.6"><span class="toc-item-num">2.6&nbsp;&nbsp;</span>解答例：ポリア分布の期待値と分散</a></span></li></ul></li><li><span><a href="#ポリアの壺試行の別の解釈" data-toc-modified-id="ポリアの壺試行の別の解釈-3"><span class="toc-item-num">3&nbsp;&nbsp;</span>ポリアの壺試行の別の解釈</a></span><ul class="toc-item"><li><span><a href="#ベータ分布,-ベータ函数,-ガンマ函数" data-toc-modified-id="ベータ分布,-ベータ函数,-ガンマ函数-3.1"><span class="toc-item-num">3.1&nbsp;&nbsp;</span>ベータ分布, ベータ函数, ガンマ函数</a></span></li><li><span><a href="#成功確率がベータ分布に従ってランダムに決まるようなベルヌーイ試行" data-toc-modified-id="成功確率がベータ分布に従ってランダムに決まるようなベルヌーイ試行-3.2"><span class="toc-item-num">3.2&nbsp;&nbsp;</span>成功確率がベータ分布に従ってランダムに決まるようなベルヌーイ試行</a></span></li><li><span><a href="#余談：生まれつきの才能か,-努力の結果か？" data-toc-modified-id="余談：生まれつきの才能か,-努力の結果か？-3.3"><span class="toc-item-num">3.3&nbsp;&nbsp;</span>余談：生まれつきの才能か, 努力の結果か？</a></span></li><li><span><a href="#問題：ポリアの壺試行で大数の法則が成立することの確認" data-toc-modified-id="問題：ポリアの壺試行で大数の法則が成立することの確認-3.4"><span class="toc-item-num">3.4&nbsp;&nbsp;</span>問題：ポリアの壺試行で大数の法則が成立することの確認</a></span></li><li><span><a href="#解答例：ポリアの壺試行の側で大数の法則が成立することの確認" data-toc-modified-id="解答例：ポリアの壺試行の側で大数の法則が成立することの確認-3.5"><span class="toc-item-num">3.5&nbsp;&nbsp;</span>解答例：ポリアの壺試行の側で大数の法則が成立することの確認</a></span><ul class="toc-item"><li><span><a href="#ポリアの壺試行の側で大数の法則が成立することの確認" data-toc-modified-id="ポリアの壺試行の側で大数の法則が成立することの確認-3.5.1"><span class="toc-item-num">3.5.1&nbsp;&nbsp;</span>ポリアの壺試行の側で大数の法則が成立することの確認</a></span></li><li><span><a href="#ポリアの壺試行での大数の法則の収束先の分布がベータ分布になることの確認" data-toc-modified-id="ポリアの壺試行での大数の法則の収束先の分布がベータ分布になることの確認-3.5.2"><span class="toc-item-num">3.5.2&nbsp;&nbsp;</span>ポリアの壺試行での大数の法則の収束先の分布がベータ分布になることの確認</a></span></li></ul></li></ul></li></ul></div>
<!-- #endregion -->

```julia
using Distributions
using StatsPlots
default(fmt=:png, size=(400, 250), titlefontsize=10,
    tickfontsize=6, guidefontsize=9, plot_titlefontsize=12)
using Random
Random.seed!(4649373)
```

```julia
# SymPy.jl はjuliaを起動した後に以下のようにすると良いだろう.
#
# julia> ENV["Python"] = ""
# julia> ]
# pkg> add SymPy
# pkg> バックスペースを押す.
# julia> using SymPy
# Python環境がJulia環境の中にインストールされる.

using SymPy

# Override the Base.show definition of SymPy.jl:
# https://github.com/JuliaPy/SymPy.jl/blob/29c5bfd1d10ac53014fa7fef468bc8deccadc2fc/src/types.jl#L87-L105

@eval SymPy function Base.show(io::IO, ::MIME"text/latex", x::SymbolicObject)
    print(io, as_markdown("\\displaystyle " * sympy.latex(x, mode="plain", fold_short_frac=false)))
end
@eval SymPy function Base.show(io::IO, ::MIME"text/latex", x::AbstractArray{Sym})
    function toeqnarray(x::Vector{Sym})
        a = join(["\\displaystyle " * sympy.latex(x[i]) for i in 1:length(x)], "\\\\")
        """\\left[ \\begin{array}{r}$a\\end{array} \\right]"""
    end
    function toeqnarray(x::AbstractArray{Sym,2})
        sz = size(x)
        a = join([join("\\displaystyle " .* map(sympy.latex, x[i,:]), "&") for i in 1:sz[1]], "\\\\")
        "\\left[ \\begin{array}{" * repeat("r",sz[2]) * "}" * a * "\\end{array}\\right]"
    end
    print(io, as_markdown(toeqnarray(x)))
end
```

## ポリアの壺

$a, b$ は正の整数であると仮定する.

注意: 実際には $a$, $b$ が $0$ 以上の実数であり, 少なくともどちらか片方が正であれば十分であるが, 壺から玉を取り出す設定で説明するためにこのように仮定しておく.

初期状態では壺の中に赤玉が $a$ 個, 白玉が $b$ 個入っていると仮定する. 

その初期状態から出発して, 以下の試行を繰り返す:

(1) 壺から玉を無作為に取り出して, 取り出された玉の色を記録する.

(2) 取り出した玉と同じ色の玉を壺に __2個__ 戻す.

この試行を1回行うごとに壺の中の玉の個数は1個ずつ増える.

これを以下では __ポリアの壺試行__ (Pólya' urn trial)もしくは __ポリアの壺過程__ (Pólya' urn process)と呼ぶことにする.


### 問題：n回目に赤玉が出る確率

ポリアの壺のついては次の問題が定番である.

>ポリアの壺試行において, $n$ 回目に取り出した玉の色が赤である確率を求めよ.

この問題について, 答えが分かるまでまたは1時間以上考えてから以下の節を読むと理解が深まるだろう.


### 解答例：n回目に赤玉が出る確率の漸化式による導出

__ポイント:__ 漸化式を作るときには, 「$n$ 回試行してから $1$ 回試行する」と考えるのではなく, 「$1$ 回試行してから, $n$ 回試行する」と考えるとよい. $1$ 回目の試行に関する確率計算は自明であるが, $n$ 回の試行後の壺の状態に関する確率の計算は非自明である.

初期状態で壺の中に赤玉が $a$ 個, 白玉が $b$ 個入っている場合のポリアの壺試行を考える.

$n$ 回目に取り出した玉の色が赤である確率を $p_n(a, b)$ と書こう.

$1$ 回目に取り出した玉の色が赤である確率は $a/(a+b)$ である:

$$
p_1(a, b) = \frac{a}{a+b}.
$$

$n+1$ 回目に取り出した玉の色が赤である確率は

* 1回目に赤玉が取り出される確率と<br>
壺の初期状態が赤玉 $a+1$ 個, 白玉 $b$ 個のポリアの壺試行の $n$ 回目で赤玉が取り出される確率の積
* 1回目に白玉が取り出される確率と<br>
壺の初期状態が赤玉 $a$ 個, 白玉 $b+1$ 個のポリアの壺試行の $n$ 回目で赤玉が取り出される確率の積

の和に等しいので,

$$
p_{n+1}(a, b) = \frac{a}{a+b}p_n(a+1,b) + \frac{b}{a+b}p_n(a, b+1).
$$

ゆえに,

$$
\begin{aligned}
p_2(a, b) &=
\frac{a}{a+b}p_1(a+1, b) + \frac{b}{a+b}p_1(a, b+1) \\ &=
\frac{a}{a+b}\frac{a+1}{a+b+1} + \frac{b}{a+b}\frac{a}{a+b+1} = \frac{a}{a+b}
\\
p_3(a, b) &=
\frac{a}{a+b}p_2(a+1, b) + \frac{b}{a+b}p_2(a, b+1) \\ &=
\frac{a}{a+b}\frac{a+1}{a+b+1} + \frac{b}{a+b}\frac{a}{a+b+1} = \frac{a}{a+b}
\\
\cdots & \cdots \cdots
\end{aligned}
$$

このように次々に $p_n(a, b) = a/(a+b)$ であることが帰納的に示される.

実際, $p_n(a, b)=a/(a+b)$ と仮定すると,

$$
\begin{aligned}
p_{n+1}(a, b) &=
\frac{a}{a+b}p_n(a+1, b) + \frac{b}{a+b}p_n(a, b+1) \\ &=
\frac{a}{a+b}\frac{a+1}{a+b+1} + \frac{b}{a+b}\frac{a}{a+b+1} = \frac{a}{a+b}.
\end{aligned}
$$

__答え:__ $\ds p_n(a, b) = \frac{a}{a+b}$.


### 解答例：n回目に赤玉が出る確率の漸化式を使わない導出

ポリアの壺試行の代わりに以下のような試行を考える.

$c$ は正の整数であると仮定する.

初期状態では $1$ から $c$ までの番号が付けられた $c$ 種類の玉が1個ずつ壺の中に入っていると仮定する.

初期状態では壺の中に $c$ 個の玉が入っていることになる.

その初期状態から出発して, 以下の試行を繰り返す:

(1) 壺から玉を無作為に取り出して, 取り出された玉の番号を記録する.

(2) 取り出した玉と同じ番号が付けられた玉を壺に __2個__ 戻す.

この試行を1回行うごとに壺の中の玉の個数は1個ずつ増える.

この試行は玉に付けられた $c$ 種類の番号について対称である.

ゆえに, $i$ が $1$ から $c$ までの番号のどれかだとすると, $n$ 回目に番号 $i$ の玉が取り出される確率は $1/c$ になる.

ポリアの壺試行は, $1$ 番から $a$ 番の玉が赤色で, $a+1$ 番から $a+b=c$ 番の玉が白色の場合における以上の試行と同等だと考えられる.

ゆえに, $n$ 回目の試行で $1$ から $a$ の番号が付けられた赤玉が取り出される確率は $a/c=a/(a+b)$ になる.


### ポリアの壺の大学入試問題の例：名古屋大学2007年文系前期3(b)

>袋の中に赤と白の玉が1個ずつ入っている. 「この袋から1個取り出して戻し, 出た玉と同じ色の玉を袋の中に1個追加する」という操作を $N$ 回繰り返した後, 赤の玉が袋の中に $m$ 個ある確率を $p_N(m)$ とする.
>
>(1) $p_3(m)$ を求めよ.
>
>(2) 一般の $N$ に対し, $p_N(m)$ を求めよ.

この問題の解答例を見たい人はインターネットで検索せよ:

* [名古屋大学2007年文系前期3(b)について検索](https://www.google.com/search?q=%E5%90%8D%E5%8F%A4%E5%B1%8B%E5%A4%A7%E5%AD%A62007%E5%B9%B4%E6%96%87%E7%B3%BB%E5%89%8D%E6%9C%9F3(b))

検索で得た情報を以下を読むときに参考にしてよい.

答えは次の通り:

$$
p_N(m) = \begin{cases}
1/(N+1) & (m=1,2,\ldots,N+1) \\
0       & (\text{otherwise}) \\
\end{cases}
$$

この問題はポリアの壺試行の初期状態が $a=b=1$ の特別な場合に対応しており, 答えが特別に簡単になる場合になっている.

一般の場合はどうなっているのだろうか?


### 問題：名古屋大学2007年文系前期3(b)の一般化

以下の問題を解け.

$a,b$ は正の整数であると仮定する.

初期状態で壺の中に赤玉が $a$ 個, 白玉が $b$ 個入っていると仮定する.

「この壺から玉を無作為に1個取り出して戻し, 出た玉と同じ色の玉を壺の中に1個追加する」

という操作を $n$ 回繰り返したときに, 赤玉が $k$ 回出る確率を $P(k|n,a,b)$ と書くことにする.

確率 $P(k|n,a,b)$ を求めよ. (確率 $P(k|n,a,b)$ を $k,n,a,b$ で表せ.)

__1時間かけても解けない場合は以下の節を見てもよい.__

__注意:__ この問題の $a=b=1$ の特別に簡単な場合が名古屋大学2007年文系前期3(b)の問題になっている.

答えの具体的な対応は $P(k|N,1,1) = p_N(1+k)$ で与えられる.


### 解答例：P(k|n,a,b)の漸化式による導出

$1$ 回目に赤玉が出る確率は $a/(a+b)$ であり, 白玉が出る確率は $b/(a+b)$ である. ゆえに,

$$
P(1|1,a,b) = \frac{a}{a+b}, \quad
P(0|1,a,b) = \frac{b}{a+b}.
$$

これ以外の場合には $P(k|1,a,b)=0$ となる.

$n+1$ 回の試行で赤玉が $k$ 回出る確率は

* 1回目に赤玉が取り出される確率と<br>
壺の初期状態が赤玉 $a+1$ 個, 白玉 $b$ 個のとき $n$ 回中赤玉が $k-1$ 回出る確率の積
* 1回目に白玉が取り出される確率と<br>
壺の初期状態が赤玉 $a$ 個, 白玉 $b+1$ 個のとき $n$ 回中赤玉が $k$ 回出る確率の積

の和に等しいので, 次の漸化式が得られる:

$$
P(k|n+1,a,b) = \frac{a}{a+b}P(k-1|n,a+1,b) + \frac{b}{a+b}P(k|n,a,b+1).
$$

この漸化式を使ってがんばって計算すると以下のようになることがわかる:

$$
\begin{aligned}
P(2|2,a,b) &= \frac{a(a+1)}{(a+b)(a+b+1)}, \\
P(1|2,a,b) &= 2\frac{ab}{(a+b)(a+b+1)}, \\
P(0|2,a,b) &= \frac{b(b+1)}{(a+b)(a+b+1)}, \\
\\
P(3|3,a,b) &= \frac{a(a+1)(a+2)}{(a+b)(a+b+1)(a+b+2)}, \\
P(2|3,a,b) &= 3\frac{a(a+1)b}{(a+b)(a+b+1)(a+b+2)}, \\
P(1|3,a,b) &= 3\frac{ab(b+1)}{(a+b)(a+b+1)(a+b+2)(a+b+2)}, \\
P(0|3,a,b) &= \frac{b(b+1)(b+2)}{(a+b)(a+b+1)(a+b+2)}, \\
\\ &
\\
P(4|4,a,b) &= \frac{a(a+1)(a+2)(a+3)}{(a+b)(a+b+1)(a+b+2)(a+b+3)}, \\
P(3|4,a,b) &= 4\frac{a(a+1)(a+2)b}{(a+b)(a+b+1)(a+b+2)(a+b+3)}, \\
P(2|4,a,b) &= 6\frac{a(a+1)b(b+1)}{(a+b)(a+b+1)(a+b+2)(a+b+3)}, \\
P(1|4,a,b) &= 4\frac{ab(b+1)(b+2)}{(a+b)(a+b+1)(a+b+2)(a+b+2)(a+b+3)}, \\
P(0|4,a,b) &= \frac{b(b+1)(b+2)(b+3)}{(a+b)(a+b+1)(a+b+2)(a+b+3)}. \\
\end{aligned}
$$

__実際に自分でも以上の結果を確認すると, 以下の証明の方針が自明に見えて来るはずである.__

これから, 次が成立することが予想される:

$$
P(k|n,a,b) =
\binom{n}{k}
\frac{a(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k-1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}.
$$

ここで $\binom{n}{k}$ は二項係数である:

$$
\binom{n}{k} = \frac{n(n-1)\cdots(n-k+1)}{k!} = \frac{n!}{k!(n-k)!}.
$$

二項係数は次の漸化式(Pascalの三角形)を満たしている:

$$
\binom{n}{k-1} + \binom{n}{k} = \binom{n+1}{k}.
$$

上の予想を帰納法で証明しよう.  これが $n$ について成立している仮定する. 上で示した漸化式を使うと,

$$
\begin{aligned}
P(k|n+1,a,b) &= \frac{a}{a+b}P(k-1|n,a+1,b) + \frac{b}{a+b}P(k|n,a,b+1)
\\ &=
\frac{a}{a+b}\binom{n}{k-1}
\frac{(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k)}
{(a+b+1)\cdots(a+b+n)}
\\ &+
\frac{b}{a+b}\binom{n}{k}
\frac{a(a+1)\cdots(a+k-1)\cdot (b+1)\cdots(b+n-k)}
{(a+b+1)\cdots(a+b+n)}
\\ &=
\left(\binom{n}{k-1} + \binom{n}{k}\right)
\frac{a(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k)}
{(a+b)(a+b+1)\cdots(a+b+n)}
\\ &=
\binom{n+1}{k}
\frac{a(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k)}
{(a+b)(a+b+1)\cdots(a+b+n)}.
\end{aligned}
$$

ゆえに $n$ を $n+1$ に置き換えた場合の上の予想も成立することがわかる.

数学的帰納法より, すべての正の整数 $n=1,2,3,\ldots$ について上の予想が成立することが示された.

結論: $P(k|n,a,b)$ は次のようになる:

$$
P(k|n,a,b) =
\binom{n}{k}
\frac{a(a+1)\cdots(a+k-1)\,b(b+1)\cdots(b+n-k-1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}.
$$

__注意:__ 例えば, $n=N$, $a=b=1$, $k=0,1,\cdots,N$ のとき,

$$
P(k|N,1,1) =
\frac{N!}{k!(N-k)!}
\frac{1\cdot2\cdots k\cdot 1\cdot2\cdots(N-k)}
{2\cdot3\cdots(N+1)} =
\frac{1}{N+1}.
$$

これはちょうど名古屋大学2007年文系前期3(b)の解答を与える.


### 解答例：P(k|n,a,b)の漸化式を使わない導出

ポリアの壺試行において, $i$ 回目に赤玉が出たら $X_i=1$ とおき, 白玉が出たら $X_i=0$ とおく.

$1$ と $0$ の列 $x_1, x_2, \ldots, x_n$ について, $X_1=x_1$, $X_2=x_2$, $\ldots$, $X_n=x_n$ となる確率を次のように書くことにする:

$$
P(x_1,x_2,\ldots,x_n|a, b).
$$

例えば, $n=7$, $x_1x_2\cdots x_n=0110010$ のとき, $P(x_1,\ldots,x_n|a,b)$ は試行回数 $n=7$ のポリアの壺試行によって, 玉が「白赤赤白白赤白」の順で出る確率になる.

この $P(x_1,x_2,\ldots,x_n|a, b)$ はポリアの壺試行における確率を最も詳細に記述している.

特に $n$ 回中赤玉が $k$ 回出る確率 $P(k|n,a,b)$ は $X_1,\ldots,X_n$ の中に $1$ が $k$ 個含まれる確率になるので,

$$
P(k|n,a,b) = \sum_{x_1+\cdots+x_n=k} P(x_1,\ldots,x_n|a, b).
$$

つまり, $P(x_1,x_2,\ldots,x_n|a, b)$ を求める問題は, 以上で扱っている問題のさらなる一般化になっている.

$P(x_1,x_2,\ldots,x_n|a, b)$ を求めよう.

例えば, $n=7$, $x_1x_2\cdots x_7 = 0110010$ (赤玉が $3$ 回, 白玉が $4$ 回)のとき,

$$
\begin{aligned}
P(x_1,x_2,\ldots,x_7|a,b) &=
\frac{b}{a+b}
\frac{a}{a+b+1}
\frac{a+1}{a+b+2}
\frac{b+1}{a+b+3}
\frac{b+2}{a+b+4}
\frac{a+2}{a+b+5}
\frac{b+3}{a+b+6}
\\ &=
\frac{a(a+1)(a+2)\cdot b(b+1)(b+2)(b+3)}{(a+b)(a+b+1)\cdots(a+b+6)}.
\end{aligned}
$$
 
最初の $i$ 回の試行で赤玉が出た回数を $r_i = x_1+\cdots+x_i$ と書き, 白玉が出た回数を $w_i = i - r_i$ と書く.

壺の中に赤玉が $a+r_{i-1}$ 個, 白玉が $b+w_{i-1}$ 個入っているときに無作為に取り出した玉が赤玉になる確率は $(a+r_{i-1})/(a+b+i-1)$ になり, 白玉になる確率は $(b+w_{i-1})/(a+b+i-1)$ になる.

それらの確率の積が $P(x_1,x_2,\ldots,x_n|a, b)$ になるので,

$$
P(x_1,x_2,\ldots,x_n|a, b) =
\frac{a^{x_1}b^{1-x_1}}{a+b}
\frac{(a+r_1)^{x_2}(b+w_1)^{1-x_2}}{a+b+1}
\cdots
\frac{(a+r_{n-1})^{x_n}(b+w_{n-1})^{1-x_n}}{a+b+n-1}
$$

$A^{x_i}B^{1-x_i}$ が $x_i=1$ のときに $A$, $x_i=0$ のときに $B$ になることを使った.

例えば, $n=7$, $x_1x_2\cdots x_7 = 0110010$ (赤玉が $3$ 回, 白玉が $4$ 回)のとき,

$$
\begin{aligned}
&
a^{x_1}(a+r_1)^{x_2}\cdots(a+r_{n-1})^{x_n}
\\ &=
a^0 a^1 (a+1)^1 (a+2)^0 (a+2)^0 (a+2)^1 (a+3)^0
\\ &= a(a+1)(a+2),
\\ &
b^{1-x_1}(b+2_1)^{1-x_2}\cdots(b+w_{n-1})^{1-x_n}
\\ &=
b^1 (b+1)^0 (b+1)^0 (b+1)^1 (b+2)^1 (b+3)^0 (b+3)^1
\\ &= b(b+1)(b+2)(b+3).
\end{aligned}
$$

$a^{x_1}(a+r_1)^{x_2}\cdots(a+r_{n-1})^{x_n}$ の中の $x_i=0$ に対応する因子は $1$ になり, $x_i=1$ が現れるたびに $r_i$ が $1$ 増え, $b^{1-x_1}(b+2_1)^{1-x_2}\cdots(b+w_{n-1})^{1-x_n}$ についても同様のことが言える.

これより, $k = r_n$ とおくと($n$ 回中赤玉が $k$ 回出た場合を考えると), 次のようになることがわかる:

$$
\begin{aligned}
&
a^{x_1}(a+r_1)^{x_2}\cdots(a+r_{n-1})^{x_n} = a(a+1)\cdots(a+k-1),
\\ &
b^{1-x_1}(b+w_1)^{1-x_2}\cdots(b+w_{n-1})^{1-x_n} = b(b+1)\cdots(b+n-k-1).
\end{aligned}
$$

したがって, $x_1,\ldots,x_n\in\{1,0\}$, $x_1+\cdots+x_n = k$ のとき, 

$$
P(x_1,x_2,\ldots,x_n|a, b) =
\frac{a(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k-1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}.
$$

特に $P(x_1,x_2,\ldots,x_n|a, b)$ は $n$ 回中に赤玉が出た回数 $x_1+\cdots+x_n = k$ だけで決まり, 赤玉が出る順序にはよらない.

$P(k|n,a,b)$ は $r_n=k$ の場合の $P(x_1,x_2,\ldots,x_n|a, b)$ の $x_1,\ldots,x_n$ の中から $1$ になる $k$ 個を選ぶ組み合わせの数倍になっている. 

ゆえに,

$$
P(k|n,a,b) =
\binom{n}{k}
\frac{a(a+1)\cdots(a+k-1)\,b(b+1)\cdots(b+n-k-1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}.
$$

__ポイント:__ $n$ 回中 $k$ 回赤玉が出る確率を求める問題を単に解くだけではなく, __より野心的に__, 

* ポリアの壺試行における確率を完全に記述している $P(x_1,x_2,\ldots,x_n|a, b)$ を求めてしまおう

と考え, さらに, __より謙虚に__, 

* $x_1x_2\cdots x_7 = 0110010$ の特別な場合について考える

と, $P(x_1,x_2,\ldots,x_n|a, b)$ が $x_1,x_2,\ldots,x_n$ を並べる順序によらないこともすぐにわかる.

そこまでたどりつけば以上の議論の全体を作り上げることは易しい.

__数学の問題を楽に解く極意は, より一般的な場合を考えることと, 特殊な場合を計算してみることの2つにある.__


## ポリアの壺と二項分布や超幾何分布の関係

<!-- #region -->
### ベータ二項分布, 二項分布, 超幾何分布

初期状態では壺の中に赤玉が $a$ 個, 白玉が $b$ 個入っていると仮定する.

(1) 前節の結果によって,

* 壺から取り出した玉と同じ色の玉を2個壺に戻す. (毎回壺の中の玉の個数は1個ずつ増える.)

というルール __ポリアの壺__ における $n$ 回の試行で赤玉が $k$ 回出る確率は

$$
P_{\BetaBinom}(k|n,a,b) =
\binom{n}{k}
\frac{a(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k-1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}.
$$

になることがわかっている.

これによって定まる $k$ の確率分布は __ベータ二項分布__ (Beta-binomial distribution)と呼ばれている.

なぜならば, この確率の式は次のように表されるからである:

$$
\begin{aligned}
\int_0^1 \binom{n}{k} p^k (1-p)^{n-k} \frac{p^{a-1}(1-p)^{b-1}}{B(a, b)}\,dp &=
\binom{n}{k} \frac{1}{B(a,b)} \int_0^1 p^{a+k-1}(1-p)^{b+n-k-1}\,dp
\\ &=
\binom{n}{k}
\frac{1}{B(a, b)} B(a+k, b+n-k)
\\ &=
\binom{n}{k}
\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \frac{\Gamma(a+k)\Gamma(b+n-k)}{\Gamma(a+b+n)}
\\ &=
\binom{n}{k}
\frac{a(a+1)\cdots(a+k-1)\cdot b(b+1)\cdots(b+n-k-1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}
\\ &=
P_{\BetaBinom}(k|n,a,b).
\end{aligned}
$$

下の方にある「ポリアの壺試行の別の解釈」の節により詳しい説明がある.

ベータ二項分布についてはWikipediaでの説明を参照せよ:

* https://en.wikipedia.org/wiki/Beta-binomial_distribution

ベータ二項分布というとらえ方をすると, $a,b$ が整数でなくても, $a,b$ が正の実数ならば, 上の式が $0$ 以上の整数に関する離散確率分布を定めることがわかる.

__注意:__ $k>n$ のとき, $\ds\binom{n}{k}=\frac{n(n-1)\cdots(n-k+1)}{k!}$ の右辺の分子が $0$ になるので, $\ds\binom{n}{k}=0$ となることに注意せよ.


(2) 試行のルールを

* 壺から取り出した玉をそのまま壺に戻す. (毎回壺の中の玉の個数は変わらない.)

にすると, $n$ 回の試行で赤玉が $k$ 回出る確率は次の __二項分布__ (binomial distribution)の確率になる:

$$
P_{\Binomial}(k|n, p) =
\binom{n}{k} p^k (1-p)^{n-k}, 
\quad p = \frac{a}{a+b}.
$$

これは次のようにも書ける:

$$
P_{\Binomial}\left(k\left|\,n, \frac{a}{a+b}\,\right.\right) =
\binom{n}{k} \frac{a^k b^{n-k}}{(a+b)^n}.
$$

(3) 試行のルールを

* 壺から取り出した玉を壺に戻さない. (毎回壺の中の玉の個数は1個ずつ減る.)

にすると, $n$ 回の試行で赤玉が $k$ 回出る確率は次の __超幾何分布__ (hypergeometric distribution)の確率になる:

$$
\begin{aligned}
P_{\Hypergeom}(k|n, a, b) &=
\binom{n}{k}
\frac
{a(a-1)\cdots(a-(k-1))
\cdot
b(b-1)\cdots(b-(n-k-1))}
{(a+b)(a+b-1)\cdots(a+b-(n-1))}
\\ &=
\left.
\binom{a}{k}
\binom{b}{n-k}
\!\right/\!\!
\binom{a+b}{n}.
\end{aligned}
$$

$n > a+b$ となることは不可能なことに注意せよ.

この確率の公式の1段目の右辺はポリアの壺の場合と同様の方法で得られる.

2段目の右辺は以下のようにして得られる.

壺に取り出した玉を戻さないという設定で $n$ 回中に赤玉が $k$ 回出る確率は次に等しい:

* 壺から $n$ 個の玉を無作為にまとめて取り出したとき, その中に赤玉が $k$ 個含まれる確率.

$a+b$ 個の玉が入っている壺から $n$ 個取り出す組み合わせ全体の個数が確率の分母になる.

その $n$ 個の中に赤玉が $k$ 個含まれている場合の組み合わせ全体の個数は $a$ 個の赤玉から $k$ 個選ぶ組み合わせの個数と $b$ 個の白玉から $n-k$ 個選ぶ組み合わせの個数の積に等しい.

このことから上の公式の2段目の右辺の式で求めたい確率が得られることがわかる.

さらに, 1段目の右辺と2段目の右辺が等しいことは以下のようにして確認される:

$$
\begin{aligned}
(\text{1段目})　&=
\frac{n!}{k!(n-k)!} \frac{a!}{(a-k)!} \frac{b!}{(b-(n-k))!} \frac{(a+b-n)!}{(a+b)!}
\\ &=
\frac{a!}{k!(a-k)!} \frac{b!}{(n-k)!(b-(n-k))!} \frac{n!(a+b-n)!}{(a+b)!} =
(\text{2段目}).
\end{aligned}
$$
<!-- #endregion -->

### ベータ二項分布, 二項分布, 超幾何分布の統一的理解 (ポリア分布)

$n$ は正の整数であるとし, $0$ 以上の整数 $k$ について, $P(k|n,a,b,d)$ を次のように定める:

$$
P(k|n,a,b,d) =
\binom{n}{k} \frac{a(a+d)\cdots(a+(k-1)d)\cdot b(b+d)\cdots(b+(n-k-1)d)}
{(a+b)(a+b+d)\cdots (a+b+(n-1)d)}.
$$

この式は $n,a,b$ が正の整数で, $d$ が $-1$ 以上の整数のとき, $0$ 以上の整数 $k$ に関する離散確率分布を定める. 

さらに, この式は $a,b,d$ が整数ではなく, 正の実数であっても, $0$ 以上の整数 $k$ に関する確率分布を定める.

この離散分布は __ポリア分布__ (Pólya distribution)と呼ばれている.

* https://encyclopediaofmath.org/wiki/P%C3%B3lya_distribution

このとき,

$$
\begin{aligned}
P_{\BetaBinom}(k|n,a,b) &= P(k|n,a,b,1),
\\
P_{\Binomial}(k|n,a/(a+b)) &= P(k|n,a,b,0),
\\
P_{\Hypergeom}(k|n,a/(a+b)) &= P(k|n,a,b,-1).
\end{aligned}
$$

すなわち, $d=1,0,-1$ の場合のポリア分布がそれぞれベータ二項分布, 二項分布, 超幾何分布になっている.


__コメント:__ 二項分布は高校でも習う.

袋の中に赤玉が $a$ 個, 白玉が $b$ 個入っているときに, 一度に $n$ 個を無作為に取り出したときに, その中に $k$ 個赤玉が含まれる確率の問題も高校まで扱う.

標本の抽出の仕方で言えば, 復元抽出の場合の分布が二項分布になっている.

標本の抽出の仕方で言えば, 非復元抽出の場合の分布が二項分布になっている.

この意味で二項分布と超幾何分布は母集団からの標本抽出について考えるときにも基本的である.

さらに, ポリアの壺に関係した問題は大学入試の定番の問題になっている.

これらについて教える側は, これらの確率分布が互いに無関係ではないことを認識しておくことが必要だと思われる.


### 問題：二項分布がポリア分布の極限になっていること

$0<p<1$ について, 次が成立することを示せ:

$$
\lim_{L\to\infty} P(k|n, Lp, L(1-p), d) = P_{\Binomial}(k|n,p).
$$

もしも可能ならば, さらに, $a,b$ が大きなとき, ベータ二項分布 $P_{\BetaBinom}(k|n, a, b)$ と超幾何分布 $P_{\Hypergeom}(k|n, a, b)$ が二項分布 $P_{\Binomial}(k|n, a/(a+b))$ で近似されることをコンピュータで視覚化せよ. (コンピュータに不慣れなら, 以下の視覚化の結果を見るだけでもよい.)


### 解答例：二項分布がポリア分布の極限になっていること

$a=Lp$, $b=L(1-p)$ のとき $a+b=L$ なので, $L\to\infty$ とすると,

$$
\begin{aligned}
&
P(k|n, Lp, L(1-p), d)
\\ &=
\binom{n}{k}
\frac{Lp(Lp+d)\cdots(Lp+(k-1)d)\cdot L(1-p)(L(1-p)+d)\cdots(L(1-p)+(n-k+1)d)}
{L(L+1)\cdots(L+n-1)}
\\ &=
\binom{n}{k}
\frac{p(p+d/L)\cdots(p+(k-1)d/L)\cdot (1-p)((1-p)+d/L)\cdots((1-p)+(n-k+1)d/L)}
{1(1+d/L)\cdots(1+(n-1)d/L)}
\\ &\to
\binom{n}{k} p^k (1-p)^{n-k} =
P_{\Binomial}(k|n,p)
\end{aligned}
$$


コンピュータによる視覚化は以下の通り.


#### 二項分布, ベータ二項分布, 超幾何分布の同時プロット(素朴な方法)

以下を [Download Julia](https://julialang.org/downloads/) からダウンロードしてインストールしたJulia言語を実行した状態で `julia> ` プロンプトの画面に貼り付ければ, そのまま実行できるはずである.

[Distributions.jl](https://github.com/JuliaStats/Distributions.jl), [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl) (ほぼ [Plots.jl](https://github.com/JuliaPlots/Plots.jl))の使い方はそれらのドキュメントを見ればわかる:

* https://juliastats.org/Distributions.jl/stable/
* https://docs.juliaplots.org/stable/

さらに次の検索結果も利用せよ:

* https://www.google.com/search?q=Plots.jl

```julia
# 使用パッケージの読み込み (少し時間がかかｋる)
using Distributions, StatsPlots
```

```julia
# プロットの仕方のデフォルトの設定を変更
default(fmt=:png, size=(400, 250), titlefontsize=10,
    tickfontsize=6, guidefontsize=9, plot_titlefontsize=12)
```

```julia
# 離散分布の確率質量函数を連続的に拡張
pmf(dist, x) = pdf(dist, round(Int, x))
```

```julia
# 分布のパラメータの設定
n, a, b = 20, 60, 140
p = a/(a+b)
```

```julia
# 分布の設定
# 上から順に二項分布, ベータ二項分布, 超幾何分布
bin = Binomial(n, p)
bb  = BetaBinomial(n, a, b)
hg  = Hypergeometric(a, b, n)
```

```julia
# プロットする範囲
μ, σ = mean(bb), std(bb)
xmin, xmax = max(-0.51, μ-4σ), min(n+0.51, μ+4σ)
```

```julia
# グラフのプロット
plot(x -> pmf(bin, x), xmin, xmax; label="Binomial")
plot!(x -> pmf(bb, x), xmin, xmax; label="BetaBinom", ls=:dash)
plot!(x -> pmf(hg, x), xmin, xmax; label="Hypergeom", ls=:dashdot)
title!("n=$n, a=$a, b=$b")
```

#### 二項分布, ベータ二項分布, 超幾何分布の同時プロット(1つの函数にまとめる方法)

```julia
function plot_polya(n, a, b; F=Bool[1,1,1], xtick=0:n, kwargs...)
    n ≤ a + b || (F[3] = false)
    p = a/(a+b)
    bin = Binomial(n, p)
    bb  = BetaBinomial(n, a, b)
    F[3] && (hg  = Hypergeometric(a, b, n))
    μ, σ = mean(bb), std(bb)
    xmin, xmax = max(-0.51, μ-4σ), min(n+0.51, μ+4σ)
    plot()
    F[1] && plot!(x -> pmf(bin, x), xmin, xmax; label="Binomial",  ls=:solid, c=1)
    F[2] && plot!(x -> pmf(bb,  x), xmin, xmax; label="BetaBinom", ls=:dash, c=2)
    F[3] && plot!(x -> pmf(hg,  x), xmin, xmax; label="Hypergeom", ls=:dashdot, c=3)
    title!("n=$n, a=$a, b=$b")
    plot!(; xtick, kwargs...)
end
```

超幾何分布は $n\le a+b$ の場合にのみ表示される.

```julia
plot((plot_polya(10, 3m, 7m) for m in (1, 3, 10, 30))...;
    size=(800, 500), layout=(2, 2))
```

```julia
plot((plot_polya(30, 3m, 7m) for m in (5, 10, 30, 100))...;
    size=(800, 500), layout=(2, 2))
```

```julia
plot((plot_polya(100, 3m, 7m) for m in (15, 30, 100, 300))...;
    size=(800, 500), layout=(2, 2), xtick=0:2:100)
```

### 問題：ポリア分布の期待値と分散

ポリア分布の期待値

$$
\mu = \sum_k k P(k|n,a,b,d)
$$

と分散

$$
\sigma^2 =
\sum_k (k - \mu)^2 P(k|n,a,b,d) =
\sum_k k^2 P(k|n,a,b,d) - \mu^2
$$

がそれぞれ

$$
\mu = \frac{na}{a+b}, \quad
\sigma^2 = \frac{nab(a+b+nd)}{(a+b)^2(a+b+d)}
$$

になることを示せ.

__注意:__ この結果の $d=1,0,-1$ の場合より, それぞれベータ二項分布(ポリアの壺の場合), 二項分布, 超幾何分布の分散も求まったことになる.  すなわち,

* $d=1$ の場合: $\ds\sigma^2 = \frac{nab(a+b+n)}{(a+b)^2(a+b+1)}$ (ベータ二項分布(ポリアの壺の場合)の分散),
* $d=0$ の場合: $\ds\sigma^2 = \frac{nab}{(a+b)^2}$ (二項分布の分散),
* $d=-1$ の場合: $\ds\sigma^2 = \frac{nab(a+b-n)}{(a+b)^2(a+b-1)}$ (超幾何分布の分散).


### 解答例：ポリア分布の期待値と分散

$m=0,1,\ldots,n$ であると仮定する.

ポリア分布における確率の総和が $1$ であるという公式

$$
\sum_k P(k|n,a,b,d) =
\sum_k \binom{n}{k} \frac{a(a+d)\cdots(a+(k-1)d)\cdot b(b+d)\cdots(b+(n-k-1)d)}
{(a+b)(a+b+d)\cdots (a+b+(n-1)d)} = 1
$$

の $n$, $a$ をそれぞれ $n-m$, $a+md$ で置き換え, 二項係数中の $k$ を $k-m$ で置き換えた場合を以下で使用する.

さらに,

$$
k\binom{n}{k} = k\frac{n(n-1)\cdots(n-k+1)}{k!} =
n\frac{(n-1)\cdots(n-k+1)}{(k-1)!} = n\binom{n-1}{k-1}
$$

から

$$
k(k-1)\cdots(k-(m-1))\binom{n}{k} = n(n-1)\cdots(n-(m-1))\binom{n-m}{k-m}
$$

であることも使用する. ただし, $k-m<0$ のとき, $\ds\binom{n-m}{k-m}=0$ であると約束しておく.

以上の準備を使うと,

$$
\begin{aligned}
&
\sum_k k(k-1)\cdots(k-(m-1))P(k|n,a,b,d)
\\ &=
\sum_k k(k-1)\cdots(k-(m-1))\binom{n}{k}
\frac{a(a+d)\cdots(a+(k-1)d)\cdot b(b+d)\cdots(b+(n-k-1)d)}
{(a+b)(a+b+d)\cdots (a+b+(n-1)d)}
\\ &=
\sum_k n(n-1)\cdots(n-(m-1))\binom{n-m}{k-m}
\frac{a(a+d)\cdots(a+(k-1)d)\cdot b(b+d)\cdots(b+(n-k-1)d)}
{(a+b)(a+b+d)\cdots (a+b+(n-1)d)}
\\ &=
n(n-1)\cdots(n-(m-1)) \frac{a(a+d)\cdots(a+(m-1)d}{(a+b)(a+b+d)\cdots(a+b+(m-1)d)}
\\ &\,\times
\sum_k \binom{n-m}{k-m}
\frac{(a+md)(a+(m+1)d)\cdots(a+(k-1)d)\cdot b(b+d)\cdots(b+(n-k-1)d)}
{(a+b+md)(a+b+(m+1)d)\cdots (a+b+(n-1)d)}
\\ &=
n(n-1)\cdots(n-(m-1)) \frac{a(a+d)\cdots(a+(m-1)d}{(a+b)(a+b+d)\cdots(a+b+(m-1)d)}.
\end{aligned}
$$

特に $m=1,2$ の場合より,

$$
\begin{aligned}
&
\mu = \sum_k k P(k|n,a,b,d) = n\frac{a}{a+b} = \frac{na}{a+b},
\\ &
\sum_k k(k-1)P(k|n,a,b,d) = n(n-1)\frac{a(a+d)}{(a+b)(a+b+d)}.
\end{aligned}
$$

ゆえに,

$$
\begin{aligned}
\sigma^2 &=
\sum_k k^2 P(k|n,a,b,d) - \mu^2
\\ &=
\sum_k (k(k-1) + k) P(k|n,a,b,d) - \mu^2
\\ &=
n(n-1)\frac{a(a+d)}{(a+b)(a+b+d)} + \mu - \mu^2
\\ &=
\frac{nab(a+b+nd)}{(a+b)^2(a+b+d)}.
\end{aligned}
$$

この計算の最後のステップについては以下の数式処理による計算を見よ.

```julia
using SymPy
@vars n a b d
expr = n*(n-1)*a*(a+d)/((a+b)*(a+b+d)) + n*a/(a+b) - (n*a/(a+b))^2
Eq(expr, expr.factor())
```

多項式や有理函数(＝有理式)の因数分解は数式処理ソフトを使うとよい.

人間には不可能そうに見える因数分解もやってくれる場合がある.


## ポリアの壺試行の別の解釈

以下の話は大学レベルの数学を含む. 

高校生にそのような話を教える必要はないが, 教える側は教養として知っておくべきことについて説明する.

__一般に, 高校生に数学を教える人は, 高校数学の範囲内について詳しいだけでは教養が足りず, 高校数学の範囲を超えた数学的教養を持っている必要がある.__


### ベータ分布, ベータ函数, ガンマ函数

$a,b$ がともに正の実数のとき, 次の確率密度函数によって $0<p<1$ に関する連続的な確率分布が定められる:

$$
f(p|a,b) = \frac{p^{a-1}(1-p)^{b-1}}{B(a, b)}
\quad (0 < p < 1).
$$

このようにして定まる確率分布をパラメータ $(a,b)$ の __ベータ分布__ と呼ぶ.

ただし, $B(a,b)$ は次のように定義される __ベータ函数__ である:

$$
B(a, b) = \int_0^1 p^{a-1}(1-p)^{b-1}\,dp
\quad (a>0,\ b>0).
$$

ベータ函数はガンマ函数で表すことができることがよく知られている(大学1年で習ったはず):

$$
B(a, b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}.
$$

__ガンマ函数__ $\Gamma(s)$ は

$$
\Gamma(s) = \int_0^\infty e^{-x} x^{s-1}\,dx \quad(s > 0)
$$

と定義され, 

$$
\Gamma(s+1) = s\Gamma(s), \quad \Gamma(1) = 1, \quad  \Gamma(1/2) = \sqrt{\pi}
$$

などの公式を満たすこともよく知られている(大学1年で習ったはず).

以下では, ガンマ函数について次が成立することが使われる: $k=0,1,2,\ldots$ について

$$
\begin{aligned}
\Gamma(s+k) &= (s+k-1)\Gamma(s+k-1) = (s+k-1)(a+k-2)\Gamma(s+k-2)
\\ &= \cdots =
(s+k-1)(a+k-2)\cdots(s+1)s\Gamma(s)
\end{aligned}
$$

となるので,

$$
\frac{\Gamma(s+k)}{\Gamma(s)} = s(s+1)\cdots(s+k-1).
$$


### 成功確率がベータ分布に従ってランダムに決まるようなベルヌーイ試行

次のようにして, $1$ と $0$ の長さ $n$ の列をランダムに生成することを考える.

(1) パラメータ $(a, b)$ のベータ分布に従って, $0<p<1$ をランダムに生成する.

(2) 確率 $p$ で $1$ を確率 $1-p$ で $0$ をランダムかつ独立に $n$ 回生成する(Bernoulli試行).

このとき, $1$ と $0$ の列 $x_1,\ldots,x_n$ に対して, このように生成された $1$ と $0$ の列が $x_1,\ldots,x_n$ に等しくなる確率 $Q(x_1,\ldots.x_n|a, b)$ は次のように計算される: $x_1+\cdots+x_n = k$ とおくと,

$$
\begin{aligned}
Q(x_1,\ldots,x_n|a, b) &=
\int_0^1 \prod_{i=1}^n\left(p^{x_i}(1-p)^{1-x_i}\right) \frac{p^{a-1}(1-p)^{b-1}}{B(a,b)}\,dp
\\ &=
\frac{1}{B(a,b)}\int_0^1 p^{a+k-1}(1-p)^{b+n-k-1}\,dp
\\ &=
\frac{1}{B(a,b)} B(a+k, b+n-k)
\\ &=
\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \frac{\Gamma(a+k)\Gamma(b+n-k)}{\Gamma(a+b+n)}
\\ &=
\frac{a(a+1)\cdots(a+k-1)\,b(b+1)\cdots(b+n-k+1)}
{(a+b)(a+b+1)\cdots(a+b+n-1)}
\\ &=
P(x_1,x_2,\ldots,x_n|a, b).
\end{aligned}
$$

要するに, __成功確率パラメータ $p$ がベータ分布に従ってランダムに決まるようなベルヌーイ試行は, ポリアの壺試行と同等である.__


### 余談：生まれつきの才能か, 努力の結果か？

以上によって, $1$ と $0$ のランダムな列を生成する2つの方法は確率的に同等であることがわかった.

以下, $a,b$ は正の実数であると仮定する.

__ポリアの壺試行__

(1) 初期状態は $(a_0, b_0) = (a, b)$ であるとする.

(2) すでに $1$ または $0$ がランダムに $i$ 回生成されているときに以下を実行する:

* 確率 $\dfrac{a_i}{a_i+b_i}$ で $1$ を生成し, $(a_{i+1}, b_{i+1}) = (a_i+1, b_i)$ とおく.
* 確率 $\dfrac{b_i}{a_i+b_i}$ で $0$ を生成し, $(a_{i+1}, b_{i+1}) = (a, b_i+1)$ とおく.

__成功確率がベータ分布に従ってランダムに決められたベルヌーイ試行__

(1) パラメータ $(a,b)$ のベータ分布に従ってランダムに $0<p<1$ を生成する.

(2) 確率 $p$ で $1$ を確率 $1-p$ で $0$ をランダムかつ独立に $n$ 回生成する.

これら2つの方法で生成せれた $1$ と $0$ のランダムな列は確率的に区別できない.

これは以下のように考えると少し奇妙に感じられることでもある.

以下では $1$ が出ることを「成功」と考え, $0$ が出ることを「失敗」と考える.

ポリアの壺試行では

* 成功するたびに次に成功する確率が高まり, 失敗するたびに次に失敗する確率が高まる. 

つまり, ポリアの壺試行では, 成功失敗の相乗効果が働いていると考えられる.  

成功確率がベータ分布に従ってランダムに決められたベルヌーイ試行では

* 最初に成功確率 $p$ がベータ分布に従ってランダムに決められている.
* それ以後は最初にランダムに決めた成功確率 $p$ に従って, 成功と失敗を繰り返す.

そして, 試行を沢山繰り返すと, 大数の法則より, 成功の割合は最初にランダムに決めた値 $p$ に近付くことになる.

その $p$ は __生まれつきの才能__ のように解釈される.

この2つが確率的に同等であることから, ポリアの壺試行でも, 試行回数を大きくする極限で, 成功の割合はある一定の値 $p$ に近付くことになる.

そして, 成功の割合が近付く先の値 $p$ が従う分布はパラメータ $(a, b)$ のベータ分布になることもわかる.

ポリアの壺試行におけるその $p$ は, 成功と失敗の試行錯誤によってたどりついた __努力の結果__ だと解釈される.

要するに, ポリアの壺試行と成功確率がベータ分布に従ってランダムに決まっているベルヌーイ試行が確率的に同等であるということは, 生まれつきの才能としての $p$ と努力の結果としての $p$ が成功失敗の列を眺めただけでは区別できないことを意味している.


### 問題：ポリアの壺試行で大数の法則が成立することの確認

コンピュータによる計算で以下を行え.

(1) ポリアの壺試行において, 試行回数 $n$ を大きくすると, 赤玉が出る回数 $k$ の割合 $k/n$ が一定の値 $p$ に近付くことを確認せよ.

(2) その近付く先の値 $p$ の分布がパラメータ $(a,b)$ のベータ分布に従うことを確認せよ.

コンピュータの操作にまだ不慣れならば, 以下の解答例をすぐに見てもよい.

これから数年かけて同じようなことをできるようになれば十分である.


### 解答例：ポリアの壺試行の側で大数の法則が成立することの確認


#### ポリアの壺試行の側で大数の法則が成立することの確認

```julia
# 使用パッケージの読み込み (少し時間がかかｋる)
using Distributions, StatsPlots
```

```julia
# プロットの仕方のデフォルトの設定を変更
default(fmt=:png, size=(400, 250), titlefontsize=10,
    tickfontsize=6, guidefontsize=9, plot_titlefontsize=12)
```

```julia
# 離散分布の確率質量函数を連続的に拡張
pmf(dist, x) = pdf(dist, round(Int, x))
```

```julia
# ポリアの壺試行の結果(1と0の長さnの列)を返す. 
function rand_polya_urn(n, a, b; X = Vector{Int}(undef, n))
    X[1] = 0
    for i in eachindex(X)
        if rand() ≤ a/(a+b)
            X[i] = 1 # 赤玉が出た (成功した)
            a, b = a+1, b
        else
            X[i] = 0 # 白玉が出た (失敗した)
            a, b = a, b+1
        end
    end
    X
end
```

```julia
using Random
Random.seed!(4648373)
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
@show rand_polya_urn(10, 3, 7);
```

```julia
# ポリアの壺試行の結果をプロット
# 横軸は試行回数で縦軸は1の割合
function plot_polya_urn(a, b; n = 10^4, e=0.1, kwargs...)
    X = rand_polya_urn(n, a, b)
    prob = cumsum!(X, X) ./ (1:n)
    ylim = prob[end] - e, prob[end] + e
    plot(prob; label="")
    plot!(; ylim, kwargs...)
end
```

Julia言語の環境で `?cumsum!` のように入力すればその解説を読むことができる.

```julia
?cumsum!
```

__問題:__ `?cumsum` の結果も表示させてみよ.


例えば, $a = [1, 2, 3, 4, 5]$ のとき $\op{cumsum!(a, a)}$ によって $a$ とその戻り値は $[1, 3, 6, 10, 15]$ になる.

```julia
a = [1, 2, 3, 4, 5]
@show a
cs = cumsum!(a, a)
@show a
@show cs;
```

```julia
# ポリアの壺試行の結果を5×4=20個プロット
function plot_polya_urns(a, b; n = 10^4, kwargs...)
    PP = [plot_polya_urn(30, 70; n) for _ in 1:20]
    plot(PP...; layout=(5, 4), size=(800, 600))
    plot!(plot_title="Polya’s urn trials: n=$n, a=$a, b=$b")
    plot!(; kwargs...)
end
```

```julia
plot_polya_urns(30, 70)
```

確かに $n$ を大きくすると, 成功割合は一定の値に近付いているように見える.

```julia
# 動画の作成
function anim_polya_urn(a, b; n = 10^4, e=0.15, fps=20, kwargs...)
    X = rand_polya_urn(n, a, b)
    prob = cumsum!(X, X) ./ (1:n)
    ylim = prob[end] - e, prob[end] + e
    s = n ÷ 200
    anim = @animate for t in [fill(s, fps); s:s:n; fill(n, fps)]
        plot(view(prob, 1:t); label="")
        title!("Polya’s urn trials: n=$n, a=$a, b=$b")
        plot!(; ylim)
    end
    gif(anim, "anim_polya_urn.gif"; fps)
end
```

```julia
using Random
Random.seed!(5963)
anim_polya_urn(30, 70)
```

上の動画はpdf版では動かない.  pdf版の閲覧者は動画を見るためには以下のリンク先を参照せよ:

* https://github.com/genkuroki/HighSchoolMath/blob/master/anim_polya_urn.gif


#### ポリアの壺試行での大数の法則の収束先の分布がベータ分布になることの確認

```julia
# スレッド並列化が有効になっていることの確認
# 値が2以上ならば有効になっている
# スレッド並列化を有効にする方法については
# https://docs.julialang.org/en/v1/manual/multi-threading/#man-multithreading
# を参照せよ.
Threads.nthreads()
```

```julia
# 私のパソコンでは次のように環境変数が設定されている.
ENV["JULIA_NUM_THREADS"]
```

```julia
# Monte Carlo シミュレーション
# ポリアの壺試行を L 回行って, 最終的な成功割合を記録する.
# lln は law of large numbers の略
function mc_polya_urn_lln(a, b; n = 10^4, L = 10^5)
    prob = Vector{Float64}(undef, L)
    tmp = [Vector{Int}(undef, n) for _ in 1:Threads.nthreads()]
    # Threads.@threads for ... end でスレッド並列化.
    # ループの内側は互いに独立に実行できなければいけない.
    Threads.@threads for i in 1:L
        X = rand_polya_urn(n, a, b; X = tmp[Threads.threadid()])
        prob[i] = sum(X)/n
    end
    prob
end
```

```julia
# ポリアの壺試行での大数の法則の収束先の分布をプロットする
function plot_polya_urn_lln(a, b; n = 10^4, L = 10^5, bin = 100, kwargs...)
    prob = @time mc_polya_urn_lln(a, b; n, L)
    xlim = extrema(prob)
    histogram(prob; norm=true, alpha=0.3, label="final k/n", bin)
    plot!(Beta(a, b), xlim...; label="Beta(a,b)", lw=1.5)
    title!("n=$n, a=$a, b=$b  (L=$L)")
    plot!(; kwargs...)
end
```

```julia
plot_polya_urn_lln(3, 7)
```

```julia
plot_polya_urn_lln(30, 70)
```

```julia
plot_polya_urn_lln(300, 700; n=50000)
```

以上のように, ポリアの壺試行での成功割合の収束先の分布が確かにベータ分布に従っていることが数値的に確認された.

そうなることはすでに証明されていることなので, こうなるのは当たり前のことではある.

しかし, $n\to\infty$ における数学的結果が, コンピュータで計算できる有限の $n$ においてどれだけの近似精度で成立しているかは実際に計算させてみないと分からないことが多い.

だから, 当然そうなるはずの結果であっても, コンピュータで確認しておくことにも数学的に価値がある.

そして, 以上のようにうまく行っていることがわかるきれいなグラフをプロットできると, 納得感が深まるという(自分に対する)教育的なメリットもある.

__我々は人間なので, 純粋に論理的に納得するだけではなく, 気持ちの上でも納得できるように工夫することは大事なことである.__

```julia

```
