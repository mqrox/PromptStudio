# Skills

会社共通のプロンプトskillを置く場所です。

skill は単なるテンプレートではなく、制作意図を生成AIが扱いやすい形に変換するための実務ノウハウです。

初期候補。

- 画像生成向けプロンプト設計
- 動画生成向けプロンプト設計
- ネガティブプロンプト設計
- VFX / CG 制作レビュー観点
- モデル別の癖と制約

モデル別skillの初期候補。

- GPT Image 2
- Nano Banana Pro
- Kling 3.0
- Seedance 2.0
- Runway Aleph / Runway系

各skillには、公式ガイドライン由来の注意点、社内検証で改善された指定方法、成功 / 失敗パターン、入力画像 / 入力動画の扱い方、レビュー観点を含めます。

公式ガイドラインやモデル仕様は更新されるため、skillには情報源、バージョン、最終確認日を残します。

## 管理者用skill

現場スタッフ用のprompt skillとは別に、管理者が蓄積artifactを分析して改善を進めるためのskillも置きます。

初期候補。

- `artifact-review`: 保存された成果物を読み、依頼、入力素材、モデル選択、prompt、結果、reviewを点検する
- `skill-gap-analysis`: 失敗例やレビューコメントから、不足しているskillや古いskillを見つける
- `model-skill-maintenance`: 公式ガイドライン、社内検証、失敗傾向をもとにモデル別skillの更新候補を出す
- `review-summary`: 週次 / 月次で成功例、失敗例、改善候補を管理者向けに要約する

管理者用skillは、改善案、根拠artifact、対象skill / knowledge、影響範囲、confidenceを出します。

共通skillの更新は、管理者の確認と承認を通して行います。
