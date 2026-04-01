# OLS / Logit (Naive)

## 概要

価格・製品特性で市場シェアをOLS回帰、またはDiscrete ChoiceデータにLogitをあてるNaiveなアプローチ。
内生性への対処がないため**バイアスがある**。ベースラインとして使われる。

---

## モデル設定

効用関数:

\[
u_{ij} = \alpha p_j + x_j \beta + \xi_j + \epsilon_{ij}, \quad \epsilon_{ij} \sim \text{i.i.d. Type I EV}
\]

市場シェア（Logit）:

\[
s_j = \frac{\exp(\delta_j)}{1 + \sum_k \exp(\delta_k)}, \quad \delta_j = \alpha p_j + x_j\beta + \xi_j
\]

Berry (1994) の線形化:

\[
\ln s_j - \ln s_0 = \alpha p_j + x_j \beta + \xi_j
\]

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **IIA** | 任意の2製品間の選択確率の比は他製品に依存しない |
| **価格外生性** | \(\text{Cov}(p_j, \xi_j) = 0\)（Naiveの仮定。実際は違反） |
| **消費者同質性** | \(\alpha, \beta\) は全消費者で共通 |

---

## 内生性

- 企業は \(\xi_j\)（需要ショック）を観察して価格設定 → \(\text{Cov}(p_j, \xi_j) \neq 0\)
- OLS推定の価格係数は**上方バイアス**（価格弾力性の過小推定）

---

## 推定手順

1. \(\ln s_j - \ln s_0\) を計算（outside option \(s_0 = 1 - \sum_j s_j\)）
2. OLS: \(\ln s_j - \ln s_0 = \alpha p_j + x_j \beta + \xi_j\)

---

## 限界

- IIAにより代替パターンが非現実的（バス→地下鉄とバス→徒歩が同じ代替率）
- 価格の内生性により弾力性がバイアス
- → 上記2点を解決したのが [BLP](blp.md)・[Nested Logit](nested_logit.md)

## 参照論文

- Berry (1994) *RAND Journal*
