# ISMS Flashcard - Claude Code Context

## プロジェクト概要
ISO/IEC 27001 情報セキュリティ学習用のフラッシュカードWebアプリケーション

## 技術スタック
- **フロントエンド**: Vanilla JavaScript (ES6+), HTML5, CSS3
- **バックエンド**: Google Apps Script (GAS) + Google Sheets
- **可視化**: Chart.js 4.5.0
- **ホスティング**: GitHub Pages
- **データ永続化**: LocalStorage

## ファイル構成
```
isms-flashcard/
├── index.html          # メインアプリケーション（HTML/CSS/JS一体型）
├── README.md           # プロジェクト概要
├── DEVELOPMENT_LOG.md  # 開発履歴
└── .claude/            # Claude Code設定
```

## 開発フロー

### ローカル開発
```bash
# 簡易HTTPサーバーを起動
python3 -m http.server 8000
# または
npx serve
```

### デプロイ
GitHub Pagesに自動デプロイ（mainブランチへのpush時）

### テスト
ブラウザで手動テスト
- URL: http://localhost:8000
- 主要機能: クイズ機能、フィルタリング、ダッシュボード、CSV出力、X共有

## 重要な外部依存
- **GAS API URL**: `index.html:193` に記載
- **Chart.js CDN**: `index.html:7` で読み込み

## よくある作業

### GAS URLの更新
```javascript
// index.html の 193行目を編集
const GAS_API_URL = 'https://script.google.com/macros/s/.../exec';
```

### スタイル調整
`index.html` の `<style>` タグ内（8-98行目）を編集

### ロジック修正
`index.html` の `<script>` タグ内（190-619行目）を編集

## 注意点
- CORS設定はGAS側で対応済み
- データはGoogle Sheetsで管理（15問のISMS試験問題）
- LocalStorageの容量制限に注意（約5-10MB）
