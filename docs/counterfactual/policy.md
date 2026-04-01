# Policy Counterfactual (Dynamic Models)

## 概要

動的モデルを推定した後、**政策変化が長期的な行動・投資・産業構造**に与える影響を分析。

---

## 例 1: バス会社の補助金政策（Rust 1987型）

**Counterfactual**: 「エンジン交換補助金があったらどのくらい交換タイミングが変わるか」

### 手順

1. 推定した \(\hat{\theta}\) を保持
2. 補助金を利得関数に組み込む:

\[
u^{cf}(a=1, x; \hat{\theta}) = u(a=1, x; \hat{\theta}) + \text{subsidy}
\]

3. 新しいベルマン方程式を解く（NFXP または CCP）
4. 行動変化・費用変化を計算

---

## 例 2: R&D 補助金の産業効果（Ericson-Pakes型）

**Counterfactual**: 「R&D 補助金が産業の TFP 分布と価格にどう影響するか」

### 手順

1. 利得関数・状態遷移を推定
2. 政策変化（補助金）を利得関数に追加:

\[
\pi_i^{cf}(a_t, s_t) = \pi_i(a_t, s_t) + \mathbf{1}[a_t = R\&D] \cdot \text{subsidy}
\]

3. 新しい MPE を計算（BBL / NPL）
4. Forward simulation で産業動態を予測（企業数・TFP 分布・価格）

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **パラメータの invariance** | \(\theta\)（選好・費用）は政策に依存しない（Lucas Critique への対処） |
| **均衡概念の維持** | 政策後も同じ均衡概念（MPE等）が成立 |
| **期待形成の変化なし** | エージェントの期待形成ルールが政策後も同じ |

---

## 参照論文

- Rust (1987) *Econometrica* — single agent counterfactual の例
- Bajari, Benkard, Levin (2007) *Econometrica* — dynamic game counterfactual
