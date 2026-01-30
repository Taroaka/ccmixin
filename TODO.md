# Claude Code Mixin OSS - 実装TODO

## 📋 プロジェクト概要
複数のClaude Code向けOSSをClaude Code自身が分析・統合して、ベストプラクティスを集めた統合OSSを生成するツール

**重要**: マージロジックはスクリプトではなく、Claude Code自身が2つのリポジトリを理解して最適な統合を行う

---

## Phase 1: クリーンアップ ✅

### 削除するファイル（ドキュメントミラー機能）
- [x] `install.sh` - 旧インストーラー
- [x] `uninstall.sh` - 旧アンインストーラー
- [x] `UNINSTALL.md` - アンインストール手順
- [x] `scripts/fetch_claude_docs.py` - ドキュメント取得スクリプト
- [x] `scripts/claude-docs-helper.sh.template` - ヘルパースクリプト
- [x] `scripts/requirements.txt` - Python依存関係
- [x] `.github/workflows/update-docs.yml` - 自動更新ワークフロー

### 残すファイル
- [x] `docs/` フォルダ全体 - **Claude Code公式ドキュメント参照用**
- [x] `docs/docs_manifest.json` - ドキュメント一覧

---

## Phase 2: 基本ディレクトリ構造の作成 ✅

- [x] `repos/` フォルダ作成（ユーザーがOSSをクローンする場所）
- [x] `repos/README.md` 作成 - クローン手順を説明
- [x] `.gitignore` 更新
  - [x] `repos/*` を無視（ユーザーがクローンしたOSSを追跡しない）
  - [x] `ccmixin/` を無視（生成された出力を追跡しない）

---

## Phase 3: `/ccmixin` コマンド作成 ✅

### コマンドファイル
- [x] `.claude/commands/ccmixin.md` 作成
  - [x] Claude Codeへの指示プロンプトを記述
  - [x] タスク: `repos/` 配下の2つのOSSディレクトリを検出
  - [x] タスク: 両方のディレクトリ構造を理解
  - [x] タスク: ファイルを比較・分析
  - [x] タスク: 重複や衝突を検出してユーザーに確認
  - [x] タスク: 統合版を `ccmixin/` に生成

### マージ対象の明記
- [x] 統合するファイルタイプを列挙
  - [x] `CLAUDE.md` - 両方の内容を統合
  - [x] `README.md` - 両方の内容を統合
  - [x] `.claude/commands/*` - スラッシュコマンド/skills
  - [x] `.claude/settings.json` - hooksを配列として統合
  - [x] `scripts/` - スクリプトファイル
  - [x] その他すべてのファイル

### 除外ルール
- [x] `.git/` を除外
- [x] `node_modules/`, `venv/`, `.env` などを除外
- [x] ビルド成果物を除外

---

## Phase 4: ユーザー確認フロー（プロンプト内で指示） ✅

### 確認が必要なケース
- [x] 既存の `ccmixin/` フォルダがある場合
  - [x] 削除していいか確認
  - [x] バックアップ提案

- [x] 同名ファイルで内容が異なる場合
  - [x] どちらを優先するか選択
  - [x] 両方統合するか選択
  - [x] リネームして両方保持するか選択

- [x] 衝突するスラッシュコマンド
  - [x] どちらを採用するか
  - [x] 両方保持（リネーム）するか

---

## Phase 5: ドキュメント更新 ✅

### README.md 書き換え
- [x] プロジェクト名: Claude Code Mixin OSS
- [x] 概要: 複数のOSSを統合するツール
- [x] インストール不要（このリポジトリをクローンするだけ）
- [x] 使い方
  ```bash
  # 1. このリポジトリをクローン
  git clone <this-repo>

  # 2. repos/配下にClaude Code OSSをクローン
  cd repos/
  git clone <oss-repo-1>
  git clone <oss-repo-2>

  # 3. Claude Codeで /ccmixin を実行
  /ccmixin

  # 4. ccmixin/フォルダに統合版が生成される
  ```
- [x] 使用例セクション
- [x] トラブルシューティング

### CLAUDE.md 更新
- [x] プロジェクト目的を明記
- [x] `/ccmixin` コマンドの動作説明
- [x] `repos/` と `ccmixin/` の役割
- [x] `docs/` フォルダの役割（Claude Code公式ドキュメント参照用）

---

## Phase 6: テストと検証 ⏳

### 手動テスト
- [ ] 2つのテストリポジトリを `repos/` に配置
- [ ] `/ccmixin` を実行
- [ ] 衝突検出が動作するか確認
- [ ] 統合結果が適切か確認

### エッジケース
- [ ] `repos/` が空の場合
- [ ] 1つしかリポジトリがない場合
- [ ] 3つ以上ある場合の動作
- [ ] 既存の `ccmixin/` がある場合

---

## Phase 7: 公開準備 ⏳

- [ ] LICENSE ファイル追加（必要に応じて）
- [ ] CONTRIBUTING.md 追加（必要に応じて）
- [ ] GitHub リポジトリ説明を更新
- [ ] 使用例のスクリーンショット追加（オプション）

---

## 現在のステータス
**Phase 1-5**: 完了 ✅
**Phase 6**: テストが必要
**Phase 7**: 公開準備（ユーザーの判断で実施）

---

## 実装完了の確認

以下のファイルが正しく作成されていることを確認：

- [x] `.claude/commands/ccmixin.md` - コマンド定義
- [x] `repos/README.md` - ユーザー向けの使い方
- [x] `README.md` - プロジェクト説明
- [x] `CLAUDE.md` - Claude Code向けガイド
- [x] `.gitignore` - `repos/`と`ccmixin/`を除外

---

## 次のステップ

1. **テスト実行**: 実際に2つのOSSを`repos/`にクローンして`/ccmixin`を試す
2. **ドキュメント調整**: 必要に応じてREADMEやCLAUDE.mdを微調整
3. **GitHub公開**: リポジトリをGitHubに公開（準備完了）
