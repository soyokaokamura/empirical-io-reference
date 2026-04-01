# Empirical IO Reference Guide

実証産業組織論（Empirical IO）の推定手法を辞書的に参照できるリファレンスガイドです。

## セットアップ

```bash
pip install mkdocs-material
mkdocs serve   # ローカルプレビュー
mkdocs build   # 静的サイトのビルド
```

## 公開

GitHub Pages への自動デプロイは `.github/workflows/deploy.yml` で設定済み。
`main` ブランチへの push で自動的にデプロイされます。

## サイト構成

- Demand Estimation（BLP, Nested Logit等）
- Cost Estimation（Markup/FOC, OP/LP/ACF等）
- Dynamic Parameter Estimation（Rust, BBL等）
- Entry/Exit Models（Bresnahan-Reiss, Ciliberto-Tamer等）
- Counterfactual Analysis
