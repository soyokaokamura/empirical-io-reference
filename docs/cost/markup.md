# Markup / FOC-Based Cost Recovery

## 概要

企業の**利潤最大化の一階条件（FOC）**から、価格と限界費用の差（マークアップ）を導出し、
限界費用を逆算する手法。**コストを直接推定するのではなく、均衡条件から回収する**。

---

## モデル設定（Bertrand価格競争）

企業 \(f\) は製品セット \(\mathcal{F}_f\) を保有し利潤最大化:

\[
\max_{p_j,\, j \in \mathcal{F}_f} \sum_{j \in \mathcal{F}_f} (p_j - mc_j) \cdot s_j(\mathbf{p}) \cdot M
\]

FOC（各製品 \(j\)）:

\[
s_j + \sum_{k \in \mathcal{F}_f} (p_k - mc_k) \frac{\partial s_k}{\partial p_j} = 0
\]

行列形式で解くと限界費用をリカバリー:

\[
\mathbf{mc} = \mathbf{p} + (\Omega \odot \Delta)^{-1} \mathbf{s}
\]

- \(\Delta_{jk} = \frac{\partial s_k}{\partial p_j}\): 価格微分行列（需要推定から取得）
- \(\Omega_{jk} = 1\) if \(j,k\) same firm, else \(0\)（所有構造行列）
- \(\mathbf{s}\): 観察されたシェアベクトル

---

## Cournot の場合

数量競争を仮定すると Lerner Index の形:

\[
\frac{p_j - mc_j}{p_j} = -\frac{s_j}{\varepsilon_{jj}}
\]

---

## Conduct Parameter アプローチ

競争度を連続パラメータ \(\theta \in [0,1]\) で表す:

\[
p_j - mc_j = -\frac{\theta \cdot s_j}{\partial s_j / \partial p_j}
\]

| \(\theta\) | 解釈 |
|-----------|------|
| 0 | 完全競争 |
| 1 | 独占 / 完全カルテル |
| \((0,1)\) | 中間的な競争 |

\(\theta\) をデータから推定可能だが、**識別が困難**なことが多い。

---

## 主要仮定

| 仮定 | 内容 | 感度 |
|------|------|------|
| **行動仮定** | Bertrand Nash を仮定 | 仮定が変わると mc が大きく変化 |
| **利潤最大化** | 企業はFOCを満たして行動 | — |
| **需要推定の正確性** | \(\Delta\) は第1段階から取得 | 需要推定誤差が伝播 |

---

## 推定手順

1. **第1段階**: 需要推定（BLP等）→ 弾力性行列 \(\hat{\Delta}\) を計算
2. **マークアップ計算**: \(\hat{\mu} = -(\Omega \odot \hat{\Delta})^{-1} \mathbf{s}\)
3. **限界費用のリカバリー**: \(\widehat{mc}_j = p_j - \hat{\mu}_j\)
4. **（任意）費用関数の回帰**:

\[
\ln \widehat{mc}_j = w_j \gamma + \eta_j
\]

- \(w_j\): 費用shifter（賃金・原材料価格等）
- 推定された \(\gamma\) の符号・大きさで妥当性を確認

---

## 妥当性チェック

- \(\widehat{mc}_j > 0\) が成立しているか
- 費用shifter（賃金・エネルギー価格）と正の相関があるか
- マークアップの水準が産業の既知の収益性と整合しているか

---

## 参照論文

- Berry, Levinsohn, Pakes (1995) *Econometrica* — 自動車産業
- Nevo (2001) *RAND Journal* — シリアル産業
- Werden and Froeb (1994) — Merger Simulation での使用
