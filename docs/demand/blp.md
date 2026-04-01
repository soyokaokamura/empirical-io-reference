# BLP (Berry, Levinsohn, Pakes 1995)

## 概要

消費者の**選好の異質性（Random Coefficients）**を導入し、IIA問題を解消した需要推定の標準手法。  
集計データ（市場シェア）のみから構造パラメータを推定できる。

---

## モデル設定

消費者 \(i\) の製品 \(j\) に対する効用（市場 \(t\)）:

\[
u_{ijt} = \underbrace{\bar{\alpha} p_{jt} + x_{jt}\bar{\beta} + \xi_{jt}}_{\delta_{jt} \text{（平均効用）}} + \underbrace{\mu_{ijt}}_{\text{個人偏差}} + \epsilon_{ijt}
\]

**Random Coefficients** の構造:

\[
\begin{pmatrix} \alpha_i \\ \beta_i \end{pmatrix} = \begin{pmatrix} \bar{\alpha} \\ \bar{\beta} \end{pmatrix} + \Pi D_i + \Sigma \nu_i, \quad \nu_i \sim N(0, I)
\]

- \(D_i\): 観察可能な消費者特性（収入・年齢等）
- \(\Pi\): 消費者特性と選好のinteraction
- \(\Sigma\): 観察不能な選好の分散

個人偏差: \(\mu_{ijt} = (\Pi D_i + \Sigma \nu_i)' (p_{jt}, x_{jt})'\)

**市場シェア**:

\[
s_{jt}(\delta_t, \theta_2) = \int \frac{\exp(\delta_{jt} + \mu_{ijt})}{1 + \sum_k \exp(\delta_{kt} + \mu_{ikt})} \, dF(\nu_i, D_i)
\]

（解析解なし → シミュレーションで近似）

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **市場均衡** | 観察シェア = 均衡シェア: \(s_{jt}^{obs} = s_{jt}(\delta_t, \theta_2)\) |
| **直交条件** | \(E[\xi_{jt} \cdot z_{jt}] = 0\)（IVの有効性） |
| **消費者分布** | \(\nu_i \sim N(0,I)\)（正規分布を仮定） |
| **外側財の存在** | 購入しない選択肢を含む（市場シェアの合計 < 1） |
| **Logitショック** | \(\epsilon_{ijt} \sim\) i.i.d. Type I Extreme Value |

---

## 内生性

**価格 \(p_{jt}\) の内生性**：

- 企業は観察不能な需要ショック \(\xi_{jt}\)（品質・ブランド価値）を知った上で価格を設定
- → \(\text{Cov}(p_{jt}, \xi_{jt}) \neq 0\)
- → OLSでは \(\bar{\alpha}\)（価格係数）が**上方バイアス**（弾力性の過小推定）

---

## IV（BLPで使われるもの）

| IV | 構成方法 | 関連性の根拠 | 除外条件 |
|----|---------|------------|---------|
| **BLP IV** | \(\sum_{k \neq j,\, k \in \mathcal{F}_j} x_{kt}\)（自社他製品の特性の和） | 製品間競合度 → 価格に影響 | \(\xi_j\) と独立 |
| **Rival IV** | \(\sum_{k \notin \mathcal{F}_j} x_{kt}\)（競合他社製品の特性） | 競合構造 → 価格に影響 | 他社需要ショックと無相関 |
| **Hausman IV** | 同一製品の他市場での価格 | 共通コストショック | 市場間需要ショック独立 |
| **GH IV** | 特性空間での距離加重 | BLP IVより強い関連性 | BLPと同様 |
| **Cost shifters** | 原材料価格・賃金等 | 限界費用 → 価格に影響 | 需要側と無関係 |

!!! note "Gandhi-Houde (GH) IVについて"
    BLP IVは製品数が少ないと弱いIVになる問題がある。  
    GH IVは特性空間での「競合製品との近さ」を直接測定することで、より強いIVを構成。

---

## 推定手順（BLP GMM）

```
外側ループ: θ₂ = (Π, Σ) を探索
    ↓
内側ループ: Contraction Mapping で δⱼₜ を解く
    ↓
ξⱼₜ = δⱼₜ - ᾱ pⱼₜ - xⱼₜ β̄ を計算
    ↓
GMM目的関数を最小化
    ↓
線形パラメータ (ᾱ, β̄) をリカバリー
```

**Step 1 — 外側ループ**

非線形パラメータ \(\theta_2 = (\Pi, \Sigma)\) の候補値を設定（最適化アルゴリズム）。

**Step 2 — 内側ループ（Contraction Mapping）**

Berry (1994) の contraction mapping で平均効用 \(\delta_{jt}\) を解く:

\[
\delta_{jt}^{(r+1)} = \delta_{jt}^{(r)} + \ln s_{jt}^{obs} - \ln s_{jt}(\delta_t^{(r)}, \theta_2)
\]

収束条件: \(\|\delta^{(r+1)} - \delta^{(r)}\|_\infty < \varepsilon\)（通常 \(\varepsilon = 10^{-12}\) 程度）

**Step 3 — \(\xi_{jt}\) の計算**

\[
\xi_{jt} = \delta_{jt} - \bar{\alpha} p_{jt} - x_{jt}\bar{\beta}
\]

線形パラメータ \((\bar{\alpha}, \bar{\beta})\) はこの段階でIVを使って線形推定（BLP inner linear step）。

**Step 4 — GMM目的関数**

\[
\hat{\theta} = \arg\min_\theta \; \xi(\theta)' Z \, (Z'WZ)^{-1} \, Z' \xi(\theta)
\]

- \(Z\): IV行列
- \(W\): 重み行列（2段階GMMで最適重み行列を推定）

---

## 価格弾力性の計算

推定後の弾力性（自己・交差）:

\[
\varepsilon_{jk} = \frac{\partial s_j}{\partial p_k} \cdot \frac{p_k}{s_j}
\]

\(\frac{\partial s_j}{\partial p_k}\) はシミュレーションで計算（解析式なし）。

---

## 参照論文

- Berry (1994) "Estimating Discrete-Choice Models of Product Differentiation." *RAND Journal of Economics*
- Berry, Levinsohn, and Pakes (1995) "Automobile Prices in Market Equilibrium." *Econometrica*
- Gandhi and Houde (2019) "Measuring Substitution Patterns in Differentiated Products Industries." Working Paper

## 関連ページ

- [BLP with Micro Moments](blp_micro.md) — 個票データとの組み合わせ
- [Nested Logit](nested_logit.md) — より簡単な代替手法
- [Markup / FOC-Based Cost Recovery](../cost/markup.md) — BLP後のコスト推定
- [Merger Simulation](../counterfactual/merger.md) — BLPを使ったCounterfactual
