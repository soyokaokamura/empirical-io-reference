# Empirical IO Reference Guide

実証産業組織論（Empirical IO）の推定手法を**辞書的に参照できる**リファレンスガイドです。

## このサイトの使い方

論文を読む際に「この推定手法はどういうもの？」と思ったらここを参照してください。  
各手法について以下の構成で記述しています：

| 項目 | 内容 |
|------|------|
| **概要** | 何をするための手法か |
| **モデル設定** | 数式・定義 |
| **主要仮定** | どんな仮定を置いているか |
| **内生性** | どこに内生性があり、なぜか |
| **IV** | どんな操作変数が使われるか、なぜ有効か |
| **推定手順** | ステップバイステップ |
| **参照論文** | オリジナル論文 |

---

## トピック一覧

### [Demand Estimation](demand/index.md)
消費者の需要・選好を構造的に推定する手法群。

- [OLS / Logit (Naive)](demand/ols_logit.md)
- [BLP (Berry, Levinsohn, Pakes 1995)](demand/blp.md)
- [BLP with Micro Moments](demand/blp_micro.md)
- [Nested Logit](demand/nested_logit.md)
- [Hausman IV](demand/hausman_iv.md)
- [Nonparametric / Semiparametric](demand/nonparametric.md)

### [Cost Estimation](cost/index.md)
企業の限界費用・費用構造を推定する手法群。

- [Markup / FOC-Based Cost Recovery](cost/markup.md)
- [Production Function Estimation (OP / LP / ACF)](cost/production_function.md)
- [Stochastic Frontier Analysis](cost/frontier.md)

### [Dynamic Parameter Estimation](dynamic/index.md)
将来を考慮した動的最適化・動的ゲームの推定手法群。

- [Rust (1987) — NFXP](dynamic/rust.md)
- [Hotz-Miller (1993) — CCP](dynamic/hotz_miller.md)
- [BBL (2007) — Dynamic Games](dynamic/bbl.md)
- [Pakes-Ostrovsky-Berry — Moment Inequalities](dynamic/pob.md)
- [Aguirregabiria-Mira — NPL](dynamic/npl.md)

### [Entry / Exit Models](entry/index.md)
市場参入・退出の決定を推定する手法群。

- [Bresnahan-Reiss (1991)](entry/bresnahan_reiss.md)
- [Berry (1992)](entry/berry.md)
- [Ciliberto-Tamer (2009) — Partial Identification](entry/ciliberto_tamer.md)
- [Ericson-Pakes (1995) — Dynamic Entry](entry/ericson_pakes.md)

### [Counterfactual Analysis](counterfactual/why.md)
推定したパラメータを使って反事実分析を行う方法と注意点。

- [なぜ構造モデルが必要か（Lucas Critique）](counterfactual/why.md)
- [Merger Simulation](counterfactual/merger.md)
- [Entry / Exit Counterfactual](counterfactual/entry_exit.md)
- [Policy Counterfactual (Dynamic Models)](counterfactual/policy.md)
- [限界と注意点](counterfactual/limitations.md)

---

## 参考
- Kawaguchi Kohei — [Empirical IO Lecture Notes](https://kohei-kawaguchi.github.io/EmpiricalIO/)
- Berry, Levinsohn, Pakes (1995) *Econometrica*
- [参照文献一覧](references.md)
