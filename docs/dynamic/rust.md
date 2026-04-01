# Rust (1987) — NFXP (Nested Fixed Point Algorithm)

## 概要

**無限期間の動学的最適化問題**を解く単一エージェントモデルの推定手法。
エージェントが将来の状態を考慮して離散的な行動を選択する。
代表例: バスエンジンの交換タイミング（Zurcher問題）。

---

## モデル設定

- 状態変数: \(x_t\)（例: 走行距離）
- 行動: \(a_t \in \{0, 1\}\)（例: エンジン継続 vs 交換）
- 期間効用: \(u(a_t, x_t; \theta) + \epsilon_t(a_t)\)

**ベルマン方程式**:

\[
V(x_t, \epsilon_t) = \max_{a_t} \left[ u(a_t, x_t; \theta) + \epsilon_t(a_t) + \beta \int V(x_{t+1}, \epsilon_{t+1}) \, dP \right]
\]

\(\epsilon_t \sim\) i.i.d. Type I Extreme Value → **選択確率**:

\[
P(a_t = 1 | x_t) = \frac{\exp(v_1(x_t; \theta))}{exp(v_0(x_t; \theta)) + \exp(v_1(x_t; \theta))}
\]

ここで \(v_a(x_t; \theta) = u(a, x_t; \theta) + \beta EV(x_t, a; \theta)\) は **ex ante value function**。

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **Conditional Independence (CI)** | \(\epsilon_t \perp x_t\)（構造ショックは状態変数と独立） |
| **Additive Separability** | \(U = u(a_t, x_t; \theta) + \epsilon_t(a_t)\) |
| **Markov Property** | 状態遷移は \((x_t, a_t)\) のみに依存 |
| **Rational Expectations** | エージェントは遷移確率を正しく認識 |
| **i.i.d. Type I EV** | \(\epsilon_t\) の分布仮定 |

---

## 推定手順（NFXP）

```
外側ループ: θ を探索（最適化）
    ↓
内側ループ: V(x; θ) を Value Function Iteration で解く
    ↓
選択確率 P(a|x; θ) を計算
    ↓
尤度関数 L(θ) を評価
    ↓
MLE: max L(θ)
```

**内側ループ（Value Function Iteration）**:

\[
V^{(r+1)}(x) = \log \sum_a \exp\left( u(a, x; \theta) + \beta \sum_{x'} V^{(r)}(x') P(x'|x,a) \right)
\]

収束まで繰り返す（通常数十〜数百回）。

**尤度関数**:

\[
L(\theta) = \prod_{t} P(a_t | x_t; \theta) \cdot p(x_t | x_{t-1}, a_{t-1})
\]

---

## 計算上の課題

**次元の呪い（Curse of Dimensionality）**:
- 状態変数が多次元になると Value Function の計算が指数的に困難
- \(x_t \in \mathbb{R}^d\) で \(d > 2\) だと現実的に計算不可

**解決策**:
- [Hotz-Miller CCP アプローチ](hotz_miller.md): 内側ループを省略
- 状態空間の離散化・次元削減

---

## 参照論文

- Rust (1987) "Optimal Replacement of GMC Bus Engines: An Empirical Model of Harold Zurcher." *Econometrica*
