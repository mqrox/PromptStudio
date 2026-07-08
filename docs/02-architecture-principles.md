# Architecture Principles

## 全体像

PromptStudio は、最初から単一アプリにすべてを詰め込まない。

責務を以下に分ける。

```text
Chrome Extension
  -> Local Bridge
    -> Workspace / Skills / Knowledge / Artifacts
    -> Google Antigravity / Antigravity IDE or other execution engines
```

## Chrome拡張の責務

Chrome拡張は、ユーザーが毎日触る入口である。

担当するもの。

- チャットUI
- 設定画面
- ユーザー入力の整理
- 生成結果の表示
- 保存操作の起点
- GoogleログインUIの将来対応

担当しすぎないもの。

- 任意のローカルファイル操作
- IDE固有の処理
- skill更新の直接実行
- 重い生成処理
- セキュリティ上危険なローカル権限

## ローカルブリッジの責務

ローカルブリッジは、Chrome拡張とローカル環境をつなぐ境界である。

担当するもの。

- 設定されたworkspaceの読み取り
- skill / knowledge の読み取り
- 成果物フォルダーへの保存
- Google Antigravity / Antigravity IDE への実行依頼
- 将来のCLI / 別IDE / 別AI実行基盤への差し替え

Chrome拡張が直接ローカルファイルに自由アクセスする設計は避ける。

## Google Antigravity / Antigravity IDEの位置づけ

Antigravity / Antigravity IDE は、MVPにおける有力なローカル実行エンジンである。

正確には、Google Antigravity 2.0 は standalone app、Antigravity IDE、CLI、SDK を含むエコシステムとして扱う。PromptStudio では、そのうちローカルworkspace、agent、skill、artifactを扱える実行面として Antigravity / Antigravity IDE を利用する。

Antigravity を重視する理由。

- Google公式プロダクトであり、Googleアカウントを起点に導入しやすい
- 個人向け無料プランから試せるため、初期導入の心理的・金銭的ハードルが低い
- Google AI Pro / Ultra などで利用上限を増やす導線がある
- Gemini系モデルのagentic workflow、マルチモーダル理解、画像/動画入力との相性が良い
- Projects / Skills / Artifacts が、PromptStudio の workspace / skill / review artifact と近い考え方である
- editor、terminal、browser、MCPをまたいだagent実行により、保存、検証、レビュー、改善をつなげやすい
- Windows / macOS / Linux に対応しており、制作現場のPC環境へ広げやすい

注意点。

- Antigravity自体はクリエイティブ生成モデルではなく、agent実行基盤である
- 利用上限、対応モデル、料金、対応言語は変わる可能性がある
- Googleのヘルプでは、Antigravity のプロンプトと指示は英語のみ対応とされているため、日本語入力を扱うPromptStudio側で変換層を持つ

ただし、PromptStudio全体をAntigravity専用に固定しない。理由は以下。

- 将来、別のIDEやCLI実行環境を使う可能性がある
- Chrome拡張のUXをIDEの仕様変更に巻き込ませないため
- skill / knowledge / artifactの保存形式を長く使える資産にするため

設計上は、`ExecutionEngine` のような抽象境界を置き、その実装の1つとしてAntigravityを扱う。

## 複数モデル利用の前提

PromptStudio は、社員全員が同じAIチャットや同じ生成モデルだけを使う前提にしない。

実際の現場では、担当者や案件によって、使うAIチャット、画像生成モデル、動画生成モデル、外部サービスが変わる。そのため、PromptStudio は特定モデルへの入力欄ではなく、会社の前提、skill、knowledge、保存形式を揃える共通レイヤーとして設計する。

モデルごとの得意不得意、入力形式、必要な指定の粒度はskill側に持たせる。保存物には、どのモデルやサービスを想定したかを残す。

初期の対応候補には、GPT Image 2、Nano Banana Pro、Kling 3.0、Seedance 2.0、Runway Aleph / Runway系モデルなどを含める。ただし、これらを固定リストにせず、モデル追加時にskillを増やせる構造にする。

## データの流れ

1. ユーザーがChrome拡張で相談する
2. Chrome拡張が用途、意図、制約を整理する
3. ローカルブリッジがskill / knowledge / workspace文脈を読み取る
4. 実行エンジンがプロンプト案と副産物を生成する
5. Chrome拡張が結果を表示する
6. ユーザーが保存する
7. 入力画像 / 入力動画、参照素材、生成結果、成功 / 失敗を記録する
8. ローカルブリッジが成果物を保存する
9. 管理者が成果物をレビューする
10. レビュー結果をskill / knowledgeへ反映する

## 保存形式の原則

- 人間が読めるMarkdownを中心にする
- 機械処理しやすいJSONも併用する
- 1回の相談単位でフォルダーを分ける
- 参照したskillとknowledgeの記録を残す
- 後からレビュー、検索、改善に使える構造にする

## セキュリティの原則

- 実運用のAPIキーや認証情報はコミットしない
- Chrome拡張からローカル操作できる範囲を明示的に制限する
- workspace外への書き込みは設定で許可された場所だけにする
- Googleログインはユーザー識別と権限管理のために使い、MVPでは必須にしない
