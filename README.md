# Claude Code Mixin OSS

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![Platform](https://img.shields.io/badge/platform-Claude%20Code-blue)]()

複数のClaude Code向けOSSを統合して、ベストプラクティスを集めた最強の設定を作成するツール。

## 🎯 これは何？

GitHub上には素晴らしいClaude Code向けのOSS（スラッシュコマンド、CLAUDE.md、設定など）がたくさんあります。しかし、1つだけでは満足できない...複数の良いところを組み合わせたい！

**Claude Code Mixin OSS**は、Claude Code自身が複数のOSSを分析・理解し、最適な形で統合します。

### 特徴

- 🤖 **AIによるインテリジェントなマージ** - Claude Codeが内容を理解して統合
- 📚 **完全自動** - スクリプト不要、`/ccmixin`コマンド1つで完了
- 🔄 **衝突解決** - 重複や矛盾を検出し、ユーザーに確認
- ✨ **品質重視** - 単純な連結ではなく、意味のある統合

## 📋 使い方

### 1. このリポジトリをクローン

```bash
git clone https://github.com/your-username/claude-code-docs.git
cd claude-code-docs
```

### 2. 統合したいOSSを`repos/`配下にクローン

```bash
cd repos/

# 例: 2つのClaude Code OSSをクローン
git clone https://github.com/user1/awesome-claude-skills
git clone https://github.com/user2/claude-best-practices

cd ..
```

### 3. Claude Codeで`/ccmixin`を実行

```bash
# Claude Code CLIで
/ccmixin
```

### 4. 統合版を確認

```bash
cd ccmixin/
ls -la

# 統合されたCLAUDE.md、README.md、スラッシュコマンドなどが生成されています
```

## 🔧 何がマージされる？

Claude Codeは以下を自動的に統合します：

| ファイル | マージ方法 |
|---------|-----------|
| `CLAUDE.md` | 両方の内容を理解し、統合版を生成 |
| `README.md` | プロジェクト説明やセクションを統合 |
| `.claude/settings.json` | hooksを配列として統合 |
| `.claude/commands/*.md` | 衝突時にユーザーに確認 |
| `scripts/` | 両方のスクリプトを保持または選択 |
| その他すべてのファイル | 独自ファイルはコピー、衝突時は確認 |

### 除外されるファイル

- `.git/` - Gitメタデータ
- `node_modules/`, `venv/` - 依存関係
- `.env` - 環境変数
- `.DS_Store`, `*.log` - システムファイル

## 💡 使用例

### 例1: スラッシュコマンドを統合

```bash
# Repo1: /commit, /review, /test
# Repo2: /commit, /deploy, /docs

# /ccmixin を実行
# → /commit が衝突 → ユーザーに確認
# → その他はすべて統合
# 結果: /commit (選択版), /review, /test, /deploy, /docs
```

### 例2: CLAUDE.mdを統合

```bash
# Repo1: プロジェクト構造の詳細説明
# Repo2: ベストプラクティスとコーディング規約

# /ccmixin を実行
# → Claude Codeが両方を理解
# 結果: 構造説明 + ベストプラクティスが統合された CLAUDE.md
```

## 📖 詳細ドキュメント

- [`CLAUDE.md`](./CLAUDE.md) - このプロジェクトの詳細ガイド
- [`repos/README.md`](./repos/README.md) - リポジトリのクローン方法
- [`docs/`](./docs/) - Claude Code公式ドキュメント（参照用）

## 🛠️ トラブルシューティング

### `repos/`にリポジトリが1つしかない

```
❌ エラー: 最低2つのリポジトリが必要です
```

**解決策**: もう1つOSSをクローンしてください。

### `ccmixin/`フォルダが既に存在する

Claude Codeが削除していいか確認します。削除を許可するか、手動で別の場所に移動してください。

### ファイルの衝突が多すぎる

ユーザー確認が必要なファイルが多い場合、Claude Codeが1つずつ確認します。時間がかかる場合は、事前に片方のリポジトリを調整することを検討してください。

## 🤝 コントリビューション

Issue、Pull Requestを歓迎します！

## 📝 ライセンス

このツール自体はMITライセンスです。統合されるOSSは各プロジェクトのライセンスに従います。

## 🙏 謝辞

- [Claude Code](https://claude.ai/code) - Anthropicの素晴らしいツール
- すべてのClaude Code OSSコミュニティ

---

**注意**: このツールは統合元のOSSの品質に依存します。信頼できる、メンテナンスされているOSSを選択してください。
