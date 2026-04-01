# Aguirregabiria-Mira (2007) — NPL (Nested Pseudo-Likelihood)

## 概要

Hotz-Miller の CCP アプローチを**複数回反復（Nested Pseudo-Likelihood）**することで、
推定の効率性を向上させる手法。初期 CCP の選択に依存した漸近バイアスを低減。

---

## NPL アルゴリズム

\[
\hat{P}^{(0)} \xrightarrow{\text{初期推定}} \hat{\theta}^{(1)} \xrightarrow{\text{CCP更新}} \hat{P}^{(1)} \xrightarrow{} \hat{\theta}^{(2)} \xrightarrow{} \cdots
\]

1. **初期化**: \(\hat{P}^{(0)}\) をノンパラメトリック Logit で推定
2. **パラメータ推定**: \(\hat{\theta}^{(k)} = \arg\max_\theta L(\theta; \hat{P}^{(k-1)})\)（Pseudo MLE）
3. **CCP の更新**: \(\hat{P}^{(k+1)} = \Psi(\hat{P}^{(k)}, \hat{\theta}^{(k)})\)（モデルから CCP を再計算）
4. **収束判定**: \(\|\hat{P}^{(k+1)} - \hat{P}^{(k)}\| < \varepsilon\) になるまで繰り返す

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| Hotz-Miller と同様 | CCP の定常性・分布仮定等 |
| **不動点の存在** | 更新演算子 \(\Psi\) が不動点を持つ（収束の保証） |

---

## Hotz-Miller との比較

| | Hotz-Miller | AM NPL |
|--|-------------|--------|
| 反復回数 | 1回（2段階） | 複数回 |
| 効率性 | 低（初期CCP依存） | 高（反復で改善） |
| 計算コスト | 低 | 中 |
| 収束保証 | — | 不動点に依存 |

---

## 参照論文

- Aguirregabiria and Mira (2007) *Econometrica*
