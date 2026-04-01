# Production Function Estimation (OP / LP / ACF)

## 概要

工場・企業レベルのパネルデータを使い、**生産関数**を推定してTFPや限界費用を回収する手法。
需要側ではなく**供給側の直接推定**。

---

## モデル設定

生産関数（対数線形）:

\[
y_{it} = \beta_l l_{it} + \beta_k k_{it} + \omega_{it} + \epsilon_{it}
\]

- \(y_{it}\): 産出量（対数）
- \(l_{it}\): 労働投入（対数）
- \(k_{it}\): 資本投入（対数）
- \(\omega_{it}\): **観察不能な生産性ショック**（内生性の原因）
- \(\epsilon_{it}\): 測定誤差

---

## 内生性の問題

企業は \(\omega_{it}\) を観察して投入量を決定:

\[
l_{it} = l(k_{it}, \omega_{it}), \quad \Rightarrow \quad \text{Cov}(l_{it}, \omega_{it}) \neq 0
\]

OLSでは \(\beta_l, \beta_k\) が**上方バイアス**（高生産性企業が多く投入するため）。

---

## 各手法の比較

| 手法 | Proxy変数 | 識別戦略 | 主な仮定 |
|------|----------|---------|---------|
| **Olley-Pakes (1996)** | 投資 \(i_{it}\) | \(\omega_{it} = h(k_{it}, i_{it})\) | 投資が \(\omega\) に単調増加（Scalar unobservable） |
| **Levinsohn-Petrin (2003)** | 中間投入 \(m_{it}\) | \(\omega_{it} = h(k_{it}, m_{it})\) | 中間投入が \(\omega\) に単調増加。投資ゼロ企業にも適用可 |
| **ACF (2015)** | 中間投入 \(m_{it}\) | LP の関数形問題を修正。\(\beta_l\) を Stage 2 で識別 | LP より弱い仮定 |

---

## 推定手順（Levinsohn-Petrin を例に）

### Stage 1

\[
y_{it} = \beta_l l_{it} + \phi(k_{it}, m_{it}) + \epsilon_{it}
\]

- \(\phi(k_{it}, m_{it}) = \beta_k k_{it} + h(k_{it}, m_{it})\) をノンパラメトリックに推定
- → \(\hat{\phi}_{it}\) と \(\hat{\beta}_l\) を取得（\(\beta_k\) はまだ未識別）

### Stage 2

1. \(\omega\) の法則の運動: \(\omega_{it} = g(\omega_{it-1}) + \xi_{it}\)（AR(1)等を仮定）
2. 候補値 \(\beta_k^*\) に対して:

\[
\hat{\omega}_{it}(\beta_k^*) = \hat{\phi}_{it} - \beta_k^* k_{it}
\]

3. \(\hat{\omega}_{it}\) を \(\hat{\omega}_{it-1}\) に回帰 → 残差 \(\hat{\xi}_{it}\)
4. モーメント条件:

\[
E[\xi_{it} \cdot k_{it}] = 0, \quad E[\xi_{it} \cdot l_{it-1}] = 0
\]

5. GMMで \(\beta_k\) を推定

---

## ACF が修正した点

LP では Stage 1 で \(\beta_l\) を推定できない可能性（collinearity 問題）。  
ACF は \(l_{it}\) も \(\phi(k_{it}, m_{it})\) の関数として吸収されることを指摘し、  
\(\beta_l\) の識別を Stage 2 に移す。

---

## TFPの計算

\[
\hat{\omega}_{it} = y_{it} - \hat{\beta}_l l_{it} - \hat{\beta}_k k_{it}
\]

このTFPを使って産業動態・参入退出研究に応用（Ericson-Pakes型モデルとの接続）。

---

## 参照論文

- Olley and Pakes (1996) *Econometrica* — 電話機器産業
- Levinsohn and Petrin (2003) *RESTUD*
- Ackerberg, Caves, and Frazer (2015) *Econometrica*
