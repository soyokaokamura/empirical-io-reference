# Ciliberto-Tamer (2009) — Partial Identification

## 概要

参入ゲームで**複数均衡**が存在する場合、パラメータは点識別されない。
**モーメント不等式**を使い、データと整合するパラメータの**識別集合（Identified Set）**を推定。

---

## 複数均衡問題

2企業の参入ゲームの例:

| 均衡 | 条件 |
|------|------|
| 両社参入 | 両社とも相手の参入を前提としても利潤 ≥ 0 |
| A のみ参入 | A は利潤 ≥ 0、B は A の参入を前提に利潤 < 0 |
| B のみ参入 | B は利潤 ≥ 0、A は B の参入を前提に利潤 < 0 |
| 両社非参入 | 両社とも相手の非参入を前提としても利潤 < 0 |

→ パラメータによっては複数の均衡が存在し、データがどの均衡に対応するか不明

---

## モーメント不等式の設定

参入確率の**上限・下限**を計算:

\[
\underline{p}(\theta) \leq P(\text{outcome}|\text{data}) \leq \overline{p}(\theta)
\]

識別集合:

\[
\Theta_I = \left\{ \theta : \underline{p}(\theta) \leq P^{obs} \leq \overline{p}(\theta) \right\}
\]

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **均衡選択ルール不要** | どの均衡が実現するかを仮定しない |
| **Rationalizability** | 観察データは何らかの均衡に対応 |
| **観察不能変数の分布** | \(\xi_i \sim N(0, \Sigma)\) 等を仮定 |

---

## 推定と統計的推論

- 識別集合の推定: \(\hat{\Theta}_I\)（有限サンプル）
- Confidence set: \(CS_n\) ⊇ \(\Theta_I\) w.p. \(1-\alpha\)
- 検定: Romano-Wolf, Andrews-Guggenberger 等

---

## 参照論文

- Ciliberto and Tamer (2009) "Market Structure and Multiple Equilibria in Airline Markets." *Econometrica*
- Tamer (2003) "Incomplete Simultaneous Discrete Response Model with Multiple Equilibria." *RESTUD*
