# 03_ZZ-MTA-5P Strategy BT Plan

## 目的

`v8.1α-ZZ-MTA-5P-B5.2 Strategy v1.1` の初期バックテストを行い、5P手法が既存ZZ-MTA-B5.2と比較可能な候補になるか確認する。

---

## Step 1：基準BT

まずは以下を固定して、基準結果を確認する。

```text
Pair：USDJPY
Chart TF：5m
HTF：60m
ZZ：ATR x 2.0
Time Filter：JST 09:00〜24:00
SL：5P Zone Opposite
RR：2.0
Expire：240m
Initial Break Mode：Strict After Zone Created
Pre H/L Mode：First Pivot After Break
Commission：0.04%
Slippage：2
Order Size：2% of equity
```

確認項目：

```text
Trades
Win Rate
PF
Max DD
Avg P/L
Entry位置
SL/TP位置
違和感のあるトレード
```

---

## Step 2：Mode比較

以下の4パターンを比較する。

| Pattern | Initial Break Mode | Pre H/L Mode | Memo |
|---|---|---|---|
| A | Strict After Zone Created | First Pivot After Break | 基準 |
| B | Strict After Zone Created | Latest Pivot Before Setup | Pre位置比較 |
| C | Allow Already Broken | First Pivot After Break | 初回戻り許可 |
| D | Allow Already Broken | Latest Pivot Before Setup | 拡張版 |

目的：

```text
どのSetup思想が最も自然で、BT結果も良いか確認する。
```

---

## Step 3：RR比較

Mode比較で良さそうなものに対して、RRを比較する。

```text
RR 1.5
RR 2.0
RR 2.5
RR 3.0
```

まずは既存B5.2で有力だった `RR 2.0 / 2.5` を中心に見る。

---

## Step 4：Expire比較

RR比較後、Expireを比較する。

```text
Expire 180m
Expire 240m
Expire 300m
```

初期基準は `240m`。  
既存B5.2との比較用に `300m` も確認する。

---

## Step 5：OOS確認

良さそうな候補が出たら、OOSで確認する。

```text
IS：2021/01/01〜2024/12/31
OOS：2025/01/01〜2025/12/31
```

OOSで大きく崩れる場合は、過剰最適化の可能性あり。

---

## 記録用テーブル

| Version | Pair | Chart TF | HTF | Initial Break | Pre H/L | ATR | RR | Expire | Time Filter | Trades | Win Rate | PF | Max DD | Avg P/L | Memo |
|---|---|---|---|---|---|---:|---:|---:|---|---:|---:|---:|---:|---:|---|
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 2.0 | 240m | 09-24 | 188 | 36.70% | 0.619 | 0.27% | -12.98 | 基準 |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 2.0 | 240m | 09-24 | 195 | 34.36% | 0.624 | 0.26% | -12.41 |  |
| v1.1 | USDJPY | 5m | 60m | Allow Already Broken | First Pivot | 2.0 | 2.0 | 240m | 09-24 | 242 | 33.47% | 0.572 | 0.41% | -16.49 |  |
| v1.1 | USDJPY | 5m | 60m | Allow Already Broken | Latest Pivot | 2.0 | 2.0 | 240m | 09-24 | 251 | 33.07% | 0.627 | 0.36% | -13.17 |  |

---

## Step 2 結果メモ

Initial Break / Pre H/L の4パターン比較では、全体的にPF 0.57〜0.63で厳しい結果。

- Strict系の方がAllow Already Brokenより安定
- Allow Already Brokenはトレード数は増えるがPF改善なし
- Pre H/L Modeの差は小さい
- 現時点ではStrict系を優先してRR比較へ進む

次は以下を比較する。

| Pattern | Initial Break | Pre H/L |
|---|---|---|
| A | Strict | First Pivot |
| B | Strict | Latest Pivot |

RR候補：1.0 / 1.3 / 1.5 / 2.0 / 2.5

##比較表

## Strict系 RR比較

| Version | Pair | Chart TF | HTF | Initial Break | Pre H/L | ATR | RR | Expire | Time Filter | Trades | Win Rate | PF | Max DD | Avg P/L | Memo |
|---|---|---|---|---|---|---:|---:|---:|---|---:|---:|---:|---:|---:|---|
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 1.0 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 1.3 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 1.5 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 2.0 | 240m | 09-24 | 188 | 36.70% | 0.619 | 0.27% | -12.98 | 基準 |
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 2.5 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 1.0 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 1.3 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 1.5 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 2.0 | 240m | 09-24 | 195 | 34.36% | 0.624 | 0.26% | -12.41 | 基準 |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 2.5 | 240m | 09-24 |  |  |  |  |  |  |

## 次フェーズ候補：Filter検証

| Priority | Filter | 内容 | 目的 |
|---:|---|---|---|
| 1 | Time Filter | 09-15 / 09-18 / 15-24 / 21-24 など | 悪い時間帯を削る |
| 2 | HTF EMA Filter | Bull時 close > HTF EMA、Bear時 close < HTF EMA | 大きい流れに逆らうSetupを削る |
| 3 | SL幅 Filter | SL幅が狭すぎる/広すぎるTradeを除外 | ノイズSLと過大リスクを削る |
| 4 | Zone幅 Filter | 5P Zone幅が極端なSetupを除外 | 汚いゾーンを削る |
| 5 | Distance Filter | Break後PivotがZoneから一定以上離れた場合のみ | 浅すぎるBreakを削る |

## 注意

最初から触るパラメーターを広げすぎない。

優先して見るもの：

```text
1. Initial Break Mode
2. Pre H/L Mode
3. RR
4. Expire
```

ATR倍率、Pivot本数、時間帯は、まず上記の方向性が見えてから検討する。
