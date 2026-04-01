# Merger Simulation

## 概要

合併後の**均衡価格と厚生変化**を予測する標準的な IO ツール。
独占禁止政策（Antitrust）の政策評価で広く使われる。

---

## 必要なもの

1. **需要推定** → 弾力性行列 \(\Delta\)（BLP 等）
2. **費用推定** → 合併前の限界費用 \(mc\)（FOC-Based で回収）
3. **合併後の所有構造** → \(\Omega^{post}\)（合併後の製品帰属）

---

## 手順

### 合併前（Pre-merger）の均衡確認

Bertrand FOC から限界費用をリカバリー:

\[
\mathbf{mc} = \mathbf{p}^{pre} + (\Omega^{pre} \odot \Delta)^{-1} \mathbf{s}^{pre}
\]

### 合併後（Post-merger）均衡の計算

所有構造の変化: \(\Omega^{pre} \to \Omega^{post}\)

新しい均衡価格 \(\mathbf{p}^{post}\) を数値的に解く:

\[
\mathbf{p}^{post} = \mathbf{mc} - (\Omega^{post} \odot \Delta(\mathbf{p}^{post}))^{-1} \mathbf{s}(\mathbf{p}^{post})
\]

（\(\mathbf{p}^{post}\) は両辺に入るため、反復法または非線形ソルバーで求解）

### 厚生の計算

**消費者余剰変化**（Small-Rosen 1981）:

\[
\Delta CS = \frac{-1}{\hat{\alpha}} \left[ \ln \sum_j \exp(\delta_j^{post}) - \ln \sum_j \exp(\delta_j^{pre}) \right] \times M
\]

**生産者余剰変化**:

\[
\Delta PS = \sum_j (p_j^{post} - mc_j) s_j^{post} M - \sum_j (p_j^{pre} - mc_j) s_j^{pre} M
\]

---

## 主要仮定

| 仮定 | 内容 | 違反した場合の影響 |
|------|------|----------------|
| **限界費用不変** | 合併後も mc は変わらない（費用効率化なし） | Efficiency がある場合は価格上昇を過大推定 |
| **Bertrand Nash 均衡** | 合併後も価格競争 | 行動仮定変更で結果が大きく変わる |
| **製品ラインナップ不変** | 合併後も同じ製品を販売 | 実際には製品廃止・新製品が起こりうる |
| **弾力性の安定性** | 大きな価格変化後も弾力性が安定 | 価格変化が大きい場合に誤差 |

---

## 感度分析

合併シミュレーションでは以下の感度分析が重要:

1. **行動仮定**: Bertrand vs Cournot vs Nash-in-Prices での結果比較
2. **Efficiency**: 費用削減 \(\Delta mc < 0\) を仮定した場合の価格変化
3. **Divestiture**: 一部製品を売却した場合の価格効果

---

## 参照論文

- Nevo (2000) "Mergers with Differentiated Products: The Case of the Ready-to-Eat Cereal Industry." *RAND Journal*
- Werden and Froeb (1994)
- Farrell and Shapiro (1990) *AER* — Cournot 合併の厚生分析
