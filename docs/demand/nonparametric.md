# Nonparametric / Semiparametric Demand

## 概要

分布の関数形（正規分布等）に強い仮定を置かず、選好の分布をより柔軟に推定する手法群。
BLPの正規分布仮定への依存を緩和し、頑健な識別を目指す。

---

## 代表的手法

| 手法 | 概要 | 参照 |
|------|------|------|
| **Fox-Kim-Yang (2012)** | Random Coefficientsの分布をnonparametricに推定。有限混合分布で近似 | Fox et al. (2012) *RAND* |
| **Berry-Haile (2014)** | 集計データからの需要の識別条件を整理。BLPの識別を理論的に基礎づけ | Berry & Haile (2014) *Econometrica* |
| **Lewbel (2000)** | Special regressorを使ったsemiparametric推定 | Lewbel (2000) *RESTUD* |

---

## Nonparametricでも残る仮定

| 仮定 | 内容 |
|------|------|
| 外側財の存在 | 市場シェアの合計 < 1 |
| Market-level separability | 効用が観察可能・不可能部分に分離可能 |
| \(\xi_{jt}\) の特定 | 観察不能な需要ショックの存在と直交条件 |
| スカラー不観測変数 | \(\xi_{jt}\) が1次元（多次元だと識別が困難） |

---

## BLPとの使い分け

- **BLP（標準）**: 実証研究の主流。計算可能で結果の解釈が明確
- **Nonparametric**: 関数形の誤特定への感度分析、または理論的な識別研究に使用

## 参照論文

- Fox, Kim, Ryan, Bajari (2012) *RAND Journal*
- Berry and Haile (2014) *Econometrica*
