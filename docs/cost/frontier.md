# Stochastic Frontier Analysis

## 概要

費用関数や生産関数から**効率性のフロンティア**を推定し、各企業の非効率性を測る。
IOよりも規制産業・公共経済学での使用が多い。

---

## モデル設定

費用フロンティア:

\[
\ln c_{it} = f(y_{it}, w_{it}; \beta) + v_{it} + u_{it}
\]

- \(v_{it} \sim N(0, \sigma_v^2)\): ランダムノイズ
- \(u_{it} \geq 0\): **非効率性**（半正規・指数・truncated 正規分布を仮定）

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| \(v_{it} \perp u_{it}\) | ノイズと非効率性が独立 |
| 非効率性の分布 | Half-normal, exponential, truncated normalのいずれか |
| 時間不変性 | \(u_{it} = u_i\) のバージョンも存在 |

---

## 推定

MLEで \((\beta, \sigma_v, \sigma_u)\) を同時推定。

---

## IO文脈での使用場面

- 規制産業（電力・水道・通信）の効率性評価
- 参入規制撤廃（deregulation）の効率性効果の測定

## 参照論文

- Aigner, Lovell, Schmidt (1977) *Journal of Econometrics* — 手法の提案
- Kumbhakar and Lovell (2000) — テキスト
