# BLP with Micro Moments

## 概要

BLPに**ミクロモーメント**（個票データや消費者調査から計算）を追加し、
消費者異質性パラメータ（\(\Pi, \Sigma\)）の識別力を高める手法。

---

## モデル設定

BLPと同一。追加で「ミクロモーメント」を定義:

\[
\bar{m}(\theta) = E_{\text{model}}[\text{ミクロ統計量}], \quad \bar{m}^{data} = \text{データからの対応統計量}
\]

**ミクロモーメントの例**:

| モーメント | 計算方法 |
|-----------|---------|
| 高収入消費者が高価格製品を選ぶ確率 | \(E[\alpha_i \cdot \mathbf{1}(D_i > \bar{D})] \cdot \text{share}\) |
| 特定2製品を同時購入する確率 | 調査データから直接計算 |
| 平均支払価格 × 収入グループ | CPS等のマイクロデータ |

---

## GMM目的関数（拡張版）

\[
\hat{\theta} = \arg\min_\theta \begin{bmatrix} \xi(\theta) \\ \bar{m}(\theta) - \bar{m}^{data} \end{bmatrix}' W \begin{bmatrix} \xi(\theta) \\ \bar{m}(\theta) - \bar{m}^{data} \end{bmatrix}
\]

---

## 主要仮定

BLPの仮定に加えて:

| 仮定 | 内容 |
|------|------|
| **代表性** | ミクロデータが集計市場データと同一母集団を代表 |
| **測定誤差** | ミクロモーメントの計算誤差が小さい |

---

## BLP（通常版）との比較

| | BLP | BLP + Micro Moments |
|--|-----|-------------------|
| データ | 集計シェアデータのみ | 集計 + 個票/調査データ |
| \(\Pi\) の識別 | 弱い場合がある | 強い |
| Cross-price elasticity | 精度低 | 精度高 |
| データ要件 | 低 | 高 |

---

## 参照論文

- Berry, Levinsohn, Pakes (2004) *RAND Journal of Economics*
- Petrin (2002) *JPE* — minivan demand（Consumer Expenditure Surveyをミクロモーメントに使用）
