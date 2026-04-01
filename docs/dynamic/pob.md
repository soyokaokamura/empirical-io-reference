# Pakes-Ostrovsky-Berry (2007) — Moment Inequalities

## 概要

BBLと同様の動的ゲームの推定だが、**モーメント不等式**を使って**識別集合**を推定する。
観察不能な異質性があっても頑健な推定が可能。

---

## モーメント不等式の論理

最適行動 \(a_t^*\) と代替行動 \(a_t^{dev}\) の比較:

\[
E\left[\pi(a_t^*, s_t) + \beta V(s_{t+1}) \,\middle|\, s_t\right] \geq E\left[\pi(a_t^{dev}, s_t) + \beta V(s_{t+1}) \,\middle|\, s_t\right]
\]

これを条件付きモーメント不等式に変換:

\[
E\left[\left(\pi(a_t^*, s_t) - \pi(a_t^{dev}, s_t)\right) \cdot h(s_t)\right] \geq 0
\]

（\(h(s_t)\): 状態の関数で定義される「instruments」）

---

## 識別集合

\[
\Theta_I = \left\{ \theta : \text{全モーメント不等式が満たされる} \right\}
\]

- 点推定量ではなく**集合推定量**
- Confidence regionの計算には Romano-Wolf や Andrews-Guggenberger 等を使用

---

## BBL との違い

| | BBL | POB |
|--|-----|-----|
| 推定の形式 | 点推定 | 識別集合 |
| 不等式の使い方 | 目的関数 | モーメント条件 |
| 観察不能異質性 | 困難 | 頑健 |
| 解釈 | \(\hat{\theta}\) | \(\Theta_I\) |

---

## 参照論文

- Pakes, Ostrovsky, Berry (2007) *RAND Journal of Economics*
- Tamer (2003) *RESTUD* — partial identification の基礎
