# Ericson-Pakes (1995) — Dynamic Entry/Exit

## 概要

企業が**投資・参入・退出**を動的に決定する産業動態モデル。
Markov Perfect Equilibrium の枠組みで、産業の長期的な進化を分析。

---

## モデル設定

状態変数: 各企業の「競争力」\(\omega_{it}\)（例: TFP・品質）

毎期の決定:

| アクター | 決定変数 | 内容 |
|---------|---------|------|
| **継続企業** | 操業 or 退出 | スクラップ価値 \(\phi\) と継続価値を比較 |
| **継続企業** | 投資水準 \(x_{it}\) | 次期の競争力 \(\omega_{it+1}\) を確率的に改善 |
| **潜在参入者** | 参入 or 非参入 | 参入費用 \(\kappa\) と将来価値を比較 |

**状態遷移**:

\[
\omega_{it+1} = \omega_{it} + \xi_{it+1}(x_{it}), \quad \xi \sim F(x_{it})
\]

---

## 均衡（MPE）

各企業の戦略 \(\sigma_i(\omega_t)\) が MPE の条件を満たす:
- 退出閾値 \(\bar{\omega}_i\): \(\omega_{it} < \bar{\omega}_i\) なら退出
- 参入閾値: 将来価値 ≥ 参入費用

---

## 推定

- BBL / Hotz-Miller 的な CCP アプローチを使用
- **次元の呪い**: 企業数が増えると状態空間が指数的に拡大
  - → Pakes-McGuire (1994) の近似アルゴリズム
  - → Doraszelski-Judd (2012) の乱択化手法

---

## 応用

- 産業の参入・退出・集中度の動態分析
- R&D 競争・特許の動学分析
- [Production Function Estimation](../cost/production_function.md) で推定した TFP を状態変数に使用

---

## 参照論文

- Ericson and Pakes (1995) "Markov-Perfect Industry Dynamics: A Framework for Empirical Work." *RESTUD*
- Pakes and McGuire (1994) *RAND Journal* — 計算アルゴリズム
