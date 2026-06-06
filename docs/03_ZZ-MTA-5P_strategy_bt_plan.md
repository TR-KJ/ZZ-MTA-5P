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
| v1.1 | USDJPY | 5m | 60m | Strict | First Pivot | 2.0 | 2.0 | 240m | 09-24 |  |  |  |  |  | 基準 |
| v1.1 | USDJPY | 5m | 60m | Strict | Latest Pivot | 2.0 | 2.0 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Allow Already Broken | First Pivot | 2.0 | 2.0 | 240m | 09-24 |  |  |  |  |  |  |
| v1.1 | USDJPY | 5m | 60m | Allow Already Broken | Latest Pivot | 2.0 | 2.0 | 240m | 09-24 |  |  |  |  |  |  |

---

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
