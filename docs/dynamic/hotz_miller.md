# Hotz-Miller (1993) — CCP (Conditional Choice Probability) Approach

## 概要

Rust の NFXP（毎回ベルマン方程式を解く）を回避するために、
データから観察される **Conditional Choice Probabilities (CCP)** を使って
将来価値を近似する手法。計算コストを大幅に削減。

---

## 核心アイデア

将来価値 \(EV(x_{t+1})\) をベルマン方程式を解かずに CCP から計算できる。

Type I Extreme Value の場合:

\[
EV(x; \hat{P}) = \log \hat{P}(a^*|x) + \gamma_E
\]

（\(\gamma_E \approx 0.5772\)：オイラー定数）

→ **観察されたCCPを将来価値の近似として使う**

---

## 主要仮定

| 仮定 | 内容 |
|------|------|
| **Finite Dependence** | 特定の行動パスを経ると将来の状態分布が同一になる（識別に使用） |
| **定常性** | CCP が時間を通じて安定している |
| **i.i.d. Type I EV** | \(\epsilon_t\) の分布仮定（CCPをLogitで推定可能にする） |

---

## 推定手順（2段階）

### Step 1: CCP の推定

\[
\hat{P}(a|x) = \text{データから Logit/Probit でノンパラメトリック推定}
\]

### Step 2: 構造パラメータの推定

- \(\hat{P}\) を使って \(EV(x; \hat{P})\) を計算
- 近似した将来価値を所与として MLE または GMM

\[
\hat{\theta} = \arg\max_\theta \sum_t \log P(a_t | x_t; \theta, \hat{P})
\]

---

## Rust NFXP との比較

| | NFXP (Rust) | CCP (Hotz-Miller) |
|--|-------------|-------------------|
| 計算コスト | 高（毎回VFI） | 低（1回のCCP推定） |
| 精度 | 高 | Step 1 の推定誤差が伝播 |
| 状態空間の次元 | 困難 | 比較的対応可能 |
| 不観測異質性 | 困難 | Arcidiacono-Miller で対応 |

---

## 拡張

**Arcidiacono-Miller (2011)**:
- 観察不能な消費者/企業タイプとの組み合わせ
- EM アルゴリズムで不観測異質性を推定しながら CCP を更新

---

## 参照論文

- Hotz and Miller (1993) *RESTUD*
- Arcidiacono and Miller (2011) *Econometrica*
