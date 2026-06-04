# ZZ-MTA-5P 開発ログ

## 目的

既存のZZ-MTAは、MTA本体ゾーンへの接触をSetupにしていた。

次は、MTA対応高値/対応安値へのリテストを「5点目」として狙う。

```text
ZZ-MTA-5P
= MTA対応高値/安値ZoneへのリテストSetup
```

## 5Pの考え方

### Long

```text
Bull ZZ-MTA中
MTA対応高値Zoneへ価格が再接触
↓
Long 5P Setup
```

### Short

```text
Bear ZZ-MTA中
MTA対応安値Zoneへ価格が再接触
↓
Short 5P Setup
```

## Zone定義

### Bull 5P Zone

```text
対応高値のヒゲ高値
〜
対応高値の実体上限
```

### Bear 5P Zone

```text
対応安値の実体下限
〜
対応安値のヒゲ安値
```

## 初期仕様

| Item | Spec |
|---|---|
| Name | ZZ-MTA-5P |
| Setup TF | 1H想定 |
| Trigger TF | 5m想定 |
| Setup | 5P Zoneヒゲ接触 |
| Trigger | B5.2 Fixed Pre H/L |
| SL | 5P Zone Opposite |
| Expire | 240m想定 |

## 初期バージョン

```text
v8.1α-ZZ-MTA-5P-B5.2 Indicator v0.1
```

## 確認項目

```text
1. 5P Zoneが対応高値/安値に正しく表示されるか
2. 5P Zone接触でSetupが出るか
3. Setup中はPre H/Lが固定されるか
4. Trigger発動までPre H/Lが更新されないか
5. 5P Zone OppositeのSL候補が自然か
6. MTA終了・期限切れでSetupが失効するか
```

## 次の予定

```text
1. Indicator v0.1 挙動確認
2. 問題なければStrategy化
3. 既存ZZ-MTA-B5.2と比較
4. 初期BT条件は以下
```

| Setup TF | Trigger TF | ATR | SL Mode | Time Filter | RR | Expire |
|---|---|---:|---|---|---:|---:|
| 1H | 5m | 2.0 | 5P Zone Opposite | Trade 09-24 | 2.0 | 240m |
| 1H | 5m | 2.0 | 5P Zone Opposite | Trade 09-24 | 2.5 | 240m |
