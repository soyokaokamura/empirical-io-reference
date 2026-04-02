# Demand Estimation — 概要

消費者の需要・選好を**構造的に推定**する手法群。  
推定されたパラメータから価格弾力性・代替パターンを計算し、Counterfactual分析に使う。

## 手法一覧と比較

| 手法 | 消費者異質性 | IIA問題 | 計算コスト | 主な用途 |
|------|------------|---------|-----------|---------|
| [OLS / Logit](ols_logit.md) | なし | あり | 低 | ベースライン |
| [Nested Logit](nested_logit.md) | グループ内相関 | グループ間はIIA | 低 | グループ構造が明確な場合 |
| [BLP](blp.md) | Random Coefficients | 解消 | 高 | **IOの標準手法** |
| [BLP + Micro Moments](blp_micro.md) | Random Coefficients | 解消 | 高 | 個票データとの組み合わせ |
| [Hausman IV](hausman_iv.md) | BLP/NLと組み合わせ | — | — | IV戦略として使用 |
| [Nonparametric](nonparametric.md) | 分布自由 | 解消 | 非常に高 | 頑健な識別 |

## 共通の内生性問題

需要推定における最大の課題は**価格の内生性**。

- **理由**: 企業は観察不能な需要ショック $\xi_{jt}$（例：ブランドイメージ）を観察して価格を設定する  
  → $\text{Cov}(p_{jt}, \xi_{jt}) \neq 0$
- **結果**: OLSで推定すると価格係数が**上方バイアス**（価格弾力性の過小推定）
- **解決**: 操作変数（IV）による2SLS / GMM

## IVの種類（需要推定共通）

| IV | 直感 | 有効性の条件 |
|----|------|------------|
| BLP IV（自社他製品の特性） | 製品間の競合度を通じて価格に影響 | $\xi_j$と独立 |
| Rival IV（他社製品の特性） | 競合構造が価格を変化させる | 他社の需要ショックと無相関 |
| Hausman IV（他市場の同一製品価格） | 共通コストショック | 市場間で需要ショックが独立 |
| Cost shifters（原材料・賃金） | 供給側に直接影響 | 需要側と独立 |
| GH IV（特性空間での距離） | BLP IVの改善版 | BLP IVより強い関連性 |

---

## Interpretation：推定後の弾力性（Implicit Elasticity）

### なぜ推定された係数を直接比較してはいけないか

需要推定で得られる**価格係数 \(\hat{\alpha}\) は弾力性ではない**。
係数をそのまま異なる製品・市場・モデル間で比較することは意味をなさない。

理由は2つ：

**1. 係数はスケールに依存する**

\(\hat{\alpha}\) は「価格が1単位上がったときの効用変化」であり、
価格の単位（円・ドル・千円）が変わると係数の大きさも変わる。
→ 係数の大きさ自体に経済的な意味はない。

**2. 弾力性はシェアと価格の水準に依存する**

同じ \(\hat{\alpha}\) でも、製品の価格水準 \(p_j\) やシェア \(s_j\) が異なれば弾力性は異なる。
Logitモデルでは弾力性はシェアと価格の**積**で決まるため、
係数だけを見ても代替パターンの強さはわからない。

---

### Implicit Elasticity とは

推定された係数から**計算される**価格弾力性のこと。
「モデルが暗示する（implicit）弾力性」という意味で使われる。

係数 \(\hat{\alpha}\) を推定した後、それを使って弾力性を**導出**する。
これが経済的に解釈可能な量であり、先行研究との比較や妥当性チェックに使う。

---

### 導出方法

#### Logit モデルの場合

自己価格弾力性：

\[
\varepsilon_{jj} = \frac{\partial s_j}{\partial p_j} \cdot \frac{p_j}{s_j} = \hat{\alpha} \cdot p_j \cdot (1 - s_j)
\]

交差価格弾力性（\(k \neq j\)）：

\[
\varepsilon_{jk} = \frac{\partial s_j}{\partial p_k} \cdot \frac{p_k}{s_j} = -\hat{\alpha} \cdot p_k \cdot s_k
\]

!!! warning "IIAの問題がここに現れる"
    Logitでは交差弾力性 \(\varepsilon_{jk}\) が **\(j\) に依存しない**。
    つまり「製品Aの価格が上がったとき、製品BとCへの代替が同じ」になる（IIA）。
    → これが非現実的であり、BLPが必要な理由。

#### BLP（Random Coefficients Logit）の場合

解析式がないため、**シミュレーションで数値的に計算**する：

\[
\varepsilon_{jk} = \frac{\partial s_j}{\partial p_k} \cdot \frac{p_k}{s_j}, \quad \frac{\partial s_j}{\partial p_k} \approx \frac{1}{ns} \sum_{i=1}^{ns} \frac{\partial P_{ij}}{\partial p_k}
\]

- \(ns\): シミュレーションの消費者数
- \(\frac{\partial P_{ij}}{\partial p_k}\): 消費者 \(i\) の製品 \(j\) の選択確率の価格微分

Random Coefficientsがあるため、消費者ごとに価格感応度 \(\alpha_i\) が異なる
→ 交差弾力性が製品ペアによって異なり、IIAが解消される。

#### Nested Logit の場合

同一グループ内（\(k \in g_j\)）の交差弾力性：

\[
\varepsilon_{jk} = -\hat{\alpha} p_k \left[ \frac{\sigma}{1-\sigma} s_{k|g} + s_k \right]
\]

異なるグループ（\(k \notin g_j\)）の交差弾力性：

\[
\varepsilon_{jk} = -\hat{\alpha} p_k s_k
\]

同一グループ内の代替が強くなる（\(\sigma > 0\) のとき）。

---

### 弾力性の妥当性チェック

推定後に以下を確認する：

| チェック項目 | 期待される値 | 違反した場合 |
|------------|------------|------------|
| 自己価格弾力性の符号 | 必ず負（\(\varepsilon_{jj} < 0\)） | モデルの誤特定・IVの問題 |
| 自己価格弾力性の大きさ | \(|\varepsilon_{jj}| > 1\)（独占企業はelastic regionで操業） | 行動仮定・価格設定の問題 |
| 交差価格弾力性の符号 | 代替財は正、補完財は負 | グループ設定やモデルの問題 |
| Implied marginal cost | 正（\(\widehat{mc}_j > 0\)） | 弾力性の過小推定・行動仮定の問題 |

!!! note "Lerner Index との整合性"
    Bertrand競争を仮定すると、均衡では：
    \[
    \frac{p_j - mc_j}{p_j} = \frac{-1}{\varepsilon_{jj}}
    \]
    推定された弾力性からimplied marginal costを計算し、
    それが産業の既知の収益性・費用構造と整合しているかを確認することで
    需要推定全体の妥当性をチェックできる。
