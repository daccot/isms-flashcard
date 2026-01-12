# Claude Code - よく使うコマンド

## 開発サーバー起動

### Python（推奨）
```bash
python3 -m http.server 8000
```
アクセス: http://localhost:8000

### Node.js（serve）
```bash
npx serve -p 8000
```

## Git操作

### 現在のブランチで作業
```bash
git status
git add .
git commit -m "メッセージ"
git push -u origin claude/integrate-cli-workflow-Gs90W
```

### 新しいブランチを作成
```bash
git checkout -b claude/feature-name-xxxxx
```

## ブラウザでテスト
```bash
# Macの場合
open http://localhost:8000

# Linuxの場合
xdg-open http://localhost:8000
```

## コードフォーマット

### HTMLの整形
```bash
# prettierを使用する場合
npx prettier --write index.html
```

## デバッグ

### ブラウザコンソールでエラーチェック
1. ブラウザの開発者ツールを開く（F12）
2. Consoleタブでエラーを確認
3. Networkタブで GAS API のレスポンスを確認

### LocalStorageの確認
```javascript
// ブラウザコンソールで実行
localStorage.getItem('isms_quiz_history')
localStorage.getItem('isms_daily_2025-01-12')
```

### LocalStorageのクリア
```javascript
// テスト用にデータをクリア
localStorage.clear()
```
