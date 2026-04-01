# Counterfactual の限界と注意点

## 主な限界

| 限界 | 説明 | 対処法 |
|------|------|--------|
| **モデルの誤特定** | 行動仮定・関数形の誤りが Counterfactual に伝播 | 感度分析・代替モデルとの比較 |
| **均衡選択問題** | 複数均衡がある場合、反事実均衡を一意に特定できない | 複数均衡での結果を報告 / Partial ID |
| **一般均衡効果の無視** | 産業レベルの分析は他産業・マクロへの波及を無視 | 明示的な限界として記述 |
| **Lucas Critique への依存** | 「大きな政策変化」では \(\theta\) が変化しうる | 漸進的な政策変化への限定 |
| **推定誤差の伝播** | Step 1 の推定誤差が Counterfactual 予測の信頼区間を広げる | Delta method / Bootstrap で信頼区間を計算 |

---

## 信頼性を高めるための実践

### 1. モデルの外的妥当性確認（Out-of-sample Validation）

- 推定サンプル外のデータでモデルの予測精度を確認
- 例: ある年のデータで推定し、別の年の価格変化を予測

### 2. 感度分析

- 行動仮定の変更（Bertrand → Cournot → カルテル）
- 需要の関数形（BLP → Nested Logit）
- IVの選択

### 3. Bounds / Partial Identification

- 強い仮定なしで結果の**範囲**を示す
- 「どんな仮定を置いても言えること」を明確化

### 4. 推定誤差の信頼区間

- Delta method または Bootstrap で Counterfactual の信頼区間を計算
- 点推定だけでなく不確実性を報告

---

## よく使われる Robustness Check の例

| Check | 内容 |
|-------|------|
| 行動仮定の変更 | Bertrand vs Cournot でのマークアップ比較 |
| IV の変更 | BLP IV vs Hausman IV vs GH IV |
| 弾力性の sensibility | 推定弾力性が外部情報と整合するか |
| 費用の妥当性 | 推定 mc が負でないか、費用 shifter と相関するか |
