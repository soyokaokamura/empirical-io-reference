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

## 2つの推定アプローチ：Berry inversion + OLS vs. Logit MLE

Logitモデルの推定には2通りのアプローチがある。**仮定が同じなら同じ推定量に収束する**が、使えるデータと拡張のしやすさが異なる。

### アプローチ1: Berry inversion + OLS（集計データ）

**Berry (1994)** の線形化を使い、市場シェアを変換してからOLS:

\[
\underbrace{\ln s_j - \ln s_0}_{\text{観察可能}} = \alpha p_j + x_j \beta + \xi_j
\]

- **データ**: 集計データ（市場レベルのシェア \(s_j\) が観察できればよい）
- **推定**: 線形OLS（またはIVを使えば2SLS）
- **IVの拡張**: 右辺を \(Z'\xi = 0\) のモーメント条件に変えるだけなので**IVを入れやすい**

### アプローチ2: Logit MLE（個票データ）

各消費者 \(i\) の選択確率を直接最大化:

\[
L(\alpha, \beta) = \prod_i \prod_j P(j|i)^{y_{ij}}, \quad P(j|i) = \frac{\exp(\alpha p_j + x_j\beta)}{1+\sum_k \exp(\alpha p_k + x_k\beta)}
\]

- **データ**: 個票データ（誰が何を選んだかがわかるデータ）
- **推定**: 非線形MLE
- **IVの拡張**: MLEにIVを組み込むには特別な処理が必要で複雑

### 比較まとめ

| | Berry inversion + OLS | Logit MLE |
|--|--|--|
| **必要なデータ** | 集計データ（市場シェア） | 個票データ |
| **推定方法** | 線形OLS | 非線形MLE |
| **漸近効率性** | MLEより劣る | 漸近有効推定量 |
| **IVの拡張** | 自然（2SLSへ） | 複雑 |
| **仮定が同じなら** | 同じ \(\alpha, \beta\) に収束 | 同じ \(\alpha, \beta\) に収束 |

!!! note "どちらを使うか"
    - **産業レベルのデータ**（製品ごとのシェア・価格）しかない → Berry inversion + OLS/2SLS
    - **個票データ**（消費者調査・購買履歴）がある → Logit MLE
    - **IVで内生性を処理したい** → Berry inversion + 2SLS が実装しやすい
    - BLPも内側ループでBerry inversionを使って \(\delta_j\) を回収し、そこからGMMをかける構造になっており、「Berry inversionしてから線形推定」はIOの基本パターン。

---

## 推定手順

### Berry inversion + OLS の場合

1. \(\ln s_j - \ln s_0\) を計算（outside option \(s_0 = 1 - \sum_j s_j\)）
2. OLS: \(\ln s_j - \ln s_0 = \alpha p_j + x_j \beta + \xi_j\)

### Logit MLE の場合

1. 個票データから各消費者の選択 \(y_{ij} \in \{0,1\}\) を用意
2. 対数尤度 \(\ell = \sum_i \sum_j y_{ij} \ln P(j|i;\alpha,\beta)\) を数値最適化で最大化

---

## 限界

- IIAにより代替パターンが非現実的（バス→地下鉄とバス→徒歩が同じ代替率）
- 価格の内生性により弾力性がバイアス
- → 上記2点を解決したのが [BLP](blp.md)・[Nested Logit](nested_logit.md)

## 参照論文

- Berry (1994) *RAND Journal*
