# BBL (Bajari, Benkard, Levin 2007) — Dynamic Games

## 概要

**複数エージェント間の戦略的相互作用**がある動的ゲームを推定する手法。
2段階推定: (1) 均衡戦略をデータから推定、(2) 均衡条件（偏差が損失をもたらす）で構造パラメータを推定。

---

## モデル設定

- 状態変数: \(s_t\)（産業の状態、各企業のTFP等）
- 各企業 \(i\) の行動: \(a_{it}\)
- 利得関数: \(\pi_i(a_t, s_t; \theta)\)（\(\theta\) を推定）
- **Markov Perfect Equilibrium (MPE)**: 均衡戦略 \(\sigma_i^*(s)\) は状態のみに依存

---

## 均衡条件（識別の鍵）

観察された戦略 \(\hat{\sigma}\) は最適戦略でなければならない:

\[
V_i(\hat{\sigma}; \theta) \geq V_i(\sigma_i^{dev}, \hat{\sigma}_{-i}; \theta) \quad \forall \text{ deviations } \sigma_i^{dev}
\]

→ **偏差からの損失が非負**という条件をモーメント不等式として使用

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **MPE** | 均衡は Markov Perfect Equilibrium |
| **均衡の一意性不要** | 観察された戦略が何らかの MPE であればよい |
| **First stage の一致性** | Step 1 の CCP 推定量が一致推定量 |
| **シミュレーションの精度** | 価値関数のシミュレーション誤差が小さい |

---

## 推定手順

### Step 1: 均衡戦略・価値関数の推定

1. データから \(\hat{\sigma}_i(s)\) をノンパラメトリックに推定
2. Forward simulation（\(\hat{\sigma}\) を使って状態を繰り返しシミュレート）で \(\hat{V}_i(\hat{\sigma}; \theta)\) を計算

### Step 2: 構造パラメータの推定

均衡条件から目的関数を構築:

\[
\hat{\theta} = \arg\min_\theta \sum_i \sum_{dev} \left[ \max\left(0,\; \hat{V}_i(\sigma_i^{dev}, \hat{\sigma}_{-i}; \theta) - \hat{V}_i(\hat{\sigma}; \theta)\right) \right]^2
\]

---

## Rust NFXP との比較

| | Rust NFXP | BBL |
|--|-----------|-----|
| エージェント数 | 単一 | 複数 |
| 均衡概念 | 動的最適化 | MPE |
| 均衡一意性 | — | 不要 |
| 識別 | 点識別 | 部分識別になりうる |
| 計算コスト | 中 | 高（シミュレーション） |

---

## 参照論文

- Bajari, Benkard, Levin (2007) *Econometrica*
