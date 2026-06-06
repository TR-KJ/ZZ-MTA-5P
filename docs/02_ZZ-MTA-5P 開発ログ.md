# 02_ZZ-MTA-5P 開発ログ

## 現在位置

ZZ-MTA-5P は、従来のMTA本体ゾーン接触ではなく、MTA対応高値／対応安値ゾーンのリテストを狙う5点目手法。

現在は Indicator v1.0 の検証を終え、Strategy v1.0 へ移行。

## Indicator開発の流れ

- v0.1  
  5P Zone単純接触でSetup。早すぎるため破棄寄り。

- v0.2〜v0.3  
  Break → Pivot → Retest Guardを追加。ブレイク前Setupが残る。

- v0.4  
  Away条件を追加。早すぎるSetupを抑制。

- v0.5  
  Away判定をPivot価格基準へ変更。

- v0.6〜v0.8  
  Retest方向判定を調整。最終的に前足終値基準へ。

- v0.9  
  Setup発生時の5P Zone / SL / Pre H/Lを固定。Pre H/L Modeを追加。

- v1.0  
  Initial Break Modeを追加。
  - Strict After Zone Created
  - Allow Already Broken

## Strategy v1.0

Indicator v1.0 のSetup/TriggerロジックをそのままStrategy化。

基本条件：
- Pair: USDJPY
- Setup TF: 1H
- Trigger TF: 5m
- ZZ: ATR x 2.0
- Time Filter: JST 09:00〜24:00
- SL: 5P Zone Opposite
- TP: RR指定
- pyramiding = 0
- commission = 0.04%

## 次にやること

1. Strategy v1.0 のコンパイル確認
2. TradingView実チャートでRuntime Error確認
3. USDJPY 1H/5mでBT
4. 以下を比較
   - Initial Break Mode
   - Pre H/L Mode
   - RR 2.0 / 2.5
   - Expire 240m / 300m
5. 既存ZZ-MTA-B5.2と比較
