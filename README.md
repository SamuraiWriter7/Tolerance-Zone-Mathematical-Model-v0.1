# Tolerance-Zone-Mathematical-Model-v0.1
Draft mathematical model for an immune-tolerance layer in Immune Royalty OS, balancing path independence, transformation, novelty protection, and boundary safety.

免疫寛容帯の初期数理仕様

Tolerance Zone Mathematical Model v0.1（TZM v0.1） は、
Immune Royalty OS v0.1 における免疫寛容の中核モデルです。

この仕様の目的は、
類似構造への過剰反応を抑えつつ、独立した新芽・同期的到達・十分な変容を持つ派生を保護すること にあります。

それは、単なる「似ている／似ていない」の判定ではありません。
このモデルが扱うのは、保護すべき類似 と 警戒すべき類似 を分けるための、最小限の数理骨格です。

1. なぜ Tolerance Zone が必要なのか

印税OSや免疫型の権利処理システムでは、
痕跡を守ろうとするほど、別の危険が生まれます。

たとえば、

類似しているだけで新芽が攻撃される
独立した到達まで盗用扱いされる
新規構造が既存構造の影に押しつぶされる
境界が曖昧なものを急いで裁いてしまう
システムが過敏化し、自己免疫的に文明を傷つける

という問題です。

Tolerance Zone は、この問題に対して、
「即時排除」ではなく 保留・観察・限定的保護 を差し込むことで応答します。

2. このモデルの目的

TZM v0.1 は、次の5つを主目的とします。

盗用や擬似構造は見逃さない
シンクロニシティや独立創造は攻撃しない
類似のみを理由とした即時排除を防ぐ
新芽保護を数理的に扱う
protect / tolerate / hold / reject-candidate を分離する

つまりこのモデルは、
排除のための数理 ではなく、
過敏反応を抑えるための数理 です。

3. 設計原理

TZM v0.1 は、以下の5原理に基づいて設計されます。

3.1 Tolerance before Rejection

排除の前に、保留・観察・寛容を差し込む。
いきなり敵とみなさない。

3.2 Path and Transformation First

類似度だけで判断しない。
経路独立性 と 変容の質 を主要軸に置く。

3.3 Novelty Bias for Young Structures

新規構造には限定的な初期保護を与える。
発芽したばかりの構造は、防御力が弱い。

3.4 Boundary Safety

自己／非自己の境界が曖昧な場合は、即裁定しない。
まず保留して見直す。

3.5 Reject Requires Separate Confirmation

Tolerance Score 単独では reject しない。
最終的な排除は、擬似構造判定 と必ず連動させる。

4. このモデルが使う変数

TZM v0.1 では、以下の変数を用います。

コア変数
S: Similarity Score

構造類似度。
0.0 から 1.0 の範囲を取ります。

P: Path Independence Score

生成経路の独立性。
どれだけ独立した道筋で到達したかを表します。

T: Transformation Score

変容の実質度。
親構造からどれだけ本質的な変化が起きたかを表します。

免疫補助変数
B: Boundary Confusion Score

自己／非自己境界の混乱度。
高いほど、作者性や親子関係の誤認リスクが高い状態です。

I: Inflammation Score

過敏反応リスク。
高いほど、システム全体が過剰反応しやすい状態です。

新芽保護変数
W: Novelty Window Factor

新規保護期間内にあるかを示す補助値です。
生成直後ほど高く、保護期間が終わるほど低くなります。

v0.1 では次のように定義します。

W = max(0, 1 - age_days / novelty_protection_window_days)
5. 審査帯
Similarity Activation

Tolerance Zone は、すべての候補に対して働くわけではありません。
まずは、類似しているために誤攻撃の危険があるものだけ を審査帯に入れます。

定義

θ_hold を審査開始閾値、δ を保護帯の幅とすると、

S >= (θ_hold - δ)

で活性化します。

v0.1 の初期値
θ_hold = 0.78
δ = 0.12

したがって、初期の活性化条件は次になります。

S >= 0.66

つまり、

S < 0.66 は主審査対象外
S >= 0.66 は Tolerance Zone の検討対象

です。

6. 寛容ポテンシャル
Tolerance Potential

次に、その候補が 保護されるだけの価値を持つか を測ります。
これを Tolerance Potential（TP） と呼びます。

定義式
TP = (0.45 * P) + (0.35 * T) + (0.20 * W)
意味
P が高いほど独立性が強い
T が高いほど単なる表層コピーではない
W が高いほど新芽保護の必要性が高い

つまり TP は、
「この候補をすぐに攻撃してはいけない理由の強さ」
を表します。

7. 免疫圧
Immune Pressure

候補が保護価値を持っていても、
境界混乱や過敏反応が強い場合は、即 protect にしてはいけません。

そのため v0.1 では Immune Pressure（IP） を導入します。

定義式
IP = (0.60 * B) + (0.40 * I)
意味
B が高いほど、自己／非自己の誤認リスクが高い
I が高いほど、システムが過敏化している

つまり IP は、
「この候補を安全に保護できるかにかかる抑制圧」
です。

8. 寛容スコア
Tolerance Score

最終的な寛容判定では、
保護価値から免疫圧を差し引いた Tolerance Score（Z_tol） を用います。

定義式
Z_tol = TP - IP

展開すると次の通りです。

Z_tol = (0.45 * P) + (0.35 * T) + (0.20 * W) - (0.60 * B) - (0.40 * I)
解釈
Z_tol が高いほど protect / tolerate に近づく
Z_tol が低いほど hold / reject-candidate に近づく
9. 判定ゾーン

v0.1 では、Z_tol を4つの領域に分けます。

9.1 Protect Zone
Z_tol >= 0.55
AND P >= 0.72
AND T >= 0.40
AND B < 0.50

この場合は、
Independent Novelty または Synchronistic Convergence として保護候補に入ります。

9.2 Tolerate Zone
0.40 <= Z_tol < 0.55
AND T >= 0.30
AND B < 0.50

この場合は、
Tolerated Derivation として許容し、還元計算へ回します。

9.3 Hold Zone
0.25 <= Z_tol < 0.40
OR B >= 0.50

この場合は、
追加のトレース確認 や 人間監査 に回します。

9.4 Reject-Candidate Zone
Z_tol < 0.25

この場合、Tolerance Zone 側からの保護はかかりません。
ただし、これだけで即 reject してはいけません。

最終的な reject は、後述する 擬似構造判定 R_pseudo と組み合わせて行います。

10. 判定の優先順位

TZM v0.1 では、次の順序で判定を進めます。

Step 1

S >= 0.66 かどうかを見る。
審査帯に入っていなければ、主審査対象外。

Step 2

B >= 0.50 なら、まず hold_for_boundary_review。
境界混乱は最優先で保留する。

Step 3

W を計算する。

Step 4

TP を計算する。

Step 5

IP を計算する。

Step 6

Z_tol を計算する。

Step 7

Protect / Tolerate / Hold / Reject-Candidate の帯を割り当てる。

Step 8

最後に 擬似構造判定 と照合し、reject の可否を確定する。

11. 擬似構造判定との接続

Tolerance Zone は、擬似構造検出を置き換えるものではありません。
むしろ、保護の誤動作を防ぎつつ、最終 reject を安全にする補助層 です。

安全原則
Z_tol < 0.25 だけでは reject しない
R_pseudo の閾値超過を要求する
B が高い場合は reject より hold を優先する

つまり、
Reject は Tolerance Score 単独ではなく、擬似構造判定との二重確認で行う
というのが v0.1 の原則です。

12. Novelty Window の役割

新規構造は、発芽直後ほど脆弱です。
そのため v0.1 では W を使って、限定的な初期保護バイアス を与えます。

主な役割
既存構造との近さだけで新芽を即排除しない
hold / protect 側へわずかに寄せる
老化した旧痕跡が新芽を塞ぐのを防ぐ
制約

W は補助項です。
P や T が極端に低い擬似構造を救済するためには使いません。

13. v0.1 の初期パラメータ
Similarity Activation
θ_hold = 0.78
δ = 0.12
Zone Thresholds
Protect threshold: 0.55
Tolerate threshold: 0.40
Hold threshold: 0.25
Protect Constraints
P_min = 0.72
T_min = 0.40
B_max = 0.50
Tolerate Constraints
T_min = 0.30
B_max = 0.50
Novelty Protection
novelty_window_days = 90

これらは固定真理ではなく、
偽陽性率・偽陰性率・新芽生存率 を見ながら将来的に調整される前提です。

14. 典型例
例1：独立到達
S = 0.82
P = 0.84
T = 0.48
B = 0.12
I = 0.10
W = 0.70
TP = 0.686
IP = 0.112
Z_tol = 0.574

この場合は Protect Zone。
構造は近くても、経路独立性と変容が十分あるため保護されます。

例2：派生だが慎重に扱うべきケース
S = 0.80
P = 0.58
T = 0.44
B = 0.18
I = 0.16
W = 0.40
TP = 0.495
IP = 0.172
Z_tol = 0.323

この場合は Hold Zone。
派生としては有望ですが、v0.1 では自動 tolerate にせず、追加レビューへ回すのが安全です。

例3：擬似構造に近いケース
S = 0.93
P = 0.18
T = 0.12
B = 0.14
I = 0.20
W = 0.85

この場合、W は高くても P と T が低すぎるため、保護はかかりません。
Tolerance Zone は Reject-Candidate とし、最終的には R_pseudo 判定へ接続されます。

15. 出力すべきもの

TZM v0.1 は、少なくとも以下を出力できるべきです。

activation_result
W
TP
IP
Z_tol
zone_assignment
triggered_precedence_rules
final_recommended_action
human_readable_reason

つまり、
なぜ protect なのか
なぜ hold なのか
なぜ reject-candidate なのか
を説明できなければなりません。

16. ガバナンス
調整方針
human-supervised
監視すべき指標
false_positive_rate
false_negative_rate
novelty_survival_rate
hold_to_protect_conversion_rate
hold_to_reject_conversion_rate
調整対象
theta_hold
delta
protect_zone_min
tolerate_zone_min
hold_zone_min
P_min
T_min
B_trigger
禁止される挙動
類似度だけでの rejection
pseudo 判定との照合なしの automatic reject
boundary confusion の無視
低 P・低 T ケースを novelty window で救済すること
17. 現時点の位置づけ

Tolerance Zone 数理モデル v0.1 は、
完成済みの最終理論ではなく、最初の可動モデル です。

この段階で重要なのは、次の4点です。

類似構造への即時攻撃を止める
Path / Transformation を protect 側の主軸に置く
新芽保護を補助項として導入する
Reject を必ず pseudo 判定と接続する

つまり v0.1 は、
文明OSにおける寛容の最小骨格 です。

18. 今後の拡張候補
Auto Tuning

偽陽性率と新芽生存率に基づく閾値自動調整。

Domain Profiles

分野ごとに Tolerance Zone のプロファイルを切り替える。

Probabilistic Hold Model

固定閾値だけでなく、確率的な hold 判定へ拡張する。

Immune Map Binding

Immune Map 可視化レイヤーへ接続する。

19. 一文で言えば

Tolerance Zone 数理モデル v0.1 とは、
似ている構造を即座に敵とみなさず、
独立性・変容・新芽保護を数理的に評価して、
protect / tolerate / hold / reject-candidate を分けるための免疫寛容モデルです。

Schema Usage

This repository provides JSON Schemas and sample files for validating the current draft specifications.

Available schema files
immune-royalty-os-v0.1.schema.json
immune-royalty-os-v0.1.sample.json
tolerance-zone-v0.1.schema.json
tolerance-zone-v0.1.sample.json
What is validated

Each schema is used for two purposes:

Schema validation
Checks whether the schema itself is structurally valid.
Sample validation
Checks whether the provided sample JSON conforms to the schema.

This makes the repository usable both as a conceptual specification and as a machine-checkable draft.

Validate locally with AJV

You can validate the files locally with ajv-cli.

Immune Royalty OS
npx --yes ajv-cli@5.0.0 compile \
  -s immune-royalty-os-v0.1.schema.json \
  --spec=draft2020 \
  --strict=false

npx --yes ajv-cli@5.0.0 validate \
  -s immune-royalty-os-v0.1.schema.json \
  -d immune-royalty-os-v0.1.sample.json \
  --spec=draft2020 \
  --strict=false \
  --errors=text
Tolerance Zone
npx --yes ajv-cli@5.0.0 compile \
  -s tolerance-zone-v0.1.schema.json \
  --spec=draft2020 \
  --strict=false

npx --yes ajv-cli@5.0.0 validate \
  -s tolerance-zone-v0.1.schema.json \
  -d tolerance-zone-v0.1.sample.json \
  --spec=draft2020 \
  --strict=false \
  --errors=text
Validate in GitHub Actions

This repository also includes a GitHub Actions workflow that validates:

the schema files themselves
the sample JSON files against each schema

The workflow is intended as a minimum safety check for draft evolution.
If a schema is broken or a sample drifts from the spec, the workflow will fail.

Recommended workflow

When updating a draft spec:

edit the YAML / README / conceptual definition
update the JSON Schema
update the sample JSON
run local validation
push and confirm GitHub Actions passes
Design note

The schemas are intentionally strict around core structure, while allowing human-readable formulas and descriptive fields to remain flexible.
This keeps the specifications machine-checkable without forcing premature over-formalization of the conceptual layer.
