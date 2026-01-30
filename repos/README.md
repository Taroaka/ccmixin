# repos/

このフォルダに統合したいClaude Code向けOSSリポジトリをクローンしてください。

## 使い方

```bash
cd repos/

# 例: 2つのOSSをクローン
git clone https://github.com/user1/awesome-claude-skills
git clone https://github.com/user2/claude-best-practices

# Claude Codeで /ccmixin を実行
cd ..
# Claude Code CLIで
/ccmixin
```

## 統合対象

Claude Codeは以下を自動的に検出・統合します:
- `.claude/commands/` - スラッシュコマンド/skills
- `.claude/settings.json` - hooks設定
- `CLAUDE.md` - プロジェクトガイド
- `README.md` - プロジェクト説明
- `scripts/` - スクリプトファイル
- その他すべてのファイル

## 注意事項

- `.git/`, `node_modules/`, `.env` などは自動的に除外されます
- 2つのリポジトリを配置することを推奨（3つ以上も可能）
- ファイルの衝突がある場合、Claude Codeが確認します
