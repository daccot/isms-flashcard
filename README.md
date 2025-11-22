# ISMS Flashcard Learning App

Google Sheets-powered interactive learning tool for ISO/IEC 27001 information security.

## Public URL

https://daccot.github.io/isms-flashcard/

## Implemented Features

### Core Functionality
- Google Sheets API integration for dynamic question loading
- 15 ISMS exam questions with metadata
- Single choice and multiple choice support
- Category and difficulty filtering
- Wrong answer review mode

### Advanced Features  
- X (Twitter) sharing with auto-generated content
- CSV export of learning history
- Question shuffling
- LocalStorage-based learning history persistence

### Dashboard & Visualization
- Chart.js visualization (line chart for progress, bar chart for category breakdown)
- Daily goal tracking (5 questions/day)
- Consecutive learning streak counter
- Overall accuracy rate display

## Technology Stack

- Frontend: HTML5, CSS3, Vanilla JavaScript
- Database: Google Sheets (API-based)
- Visualization: Chart.js 4.5.0
- Data: LocalStorage
- Hosting: GitHub Pages
- Encoding: UTF-8 LF

## Google Sheets Data Schema

| Column | Field | Format |
|--------|-------|--------|
| A | Question ID | Q001-Q015 |
| B | Question Text | String |
| C-F | Options 1-4 | String |
| G | Correct Answer | Single: "1" / Multiple: "1,3" |
| H | Question Type | "択一" or "複数選択" |
| I | Category | 11 ISMS categories |
| J | Difficulty | "初級", "中級", "上級" |

## Usage

1. Visit the public URL above
2. Set filters (category, difficulty)
3. Click "Start Quiz"
4. Answer questions and check results
5. View dashboard statistics
6. Share results or export CSV

## Development Status

- Phase 1-5: Core features ✅
- Phase 6: GitHub Pages deployment ✅
- Phase 7+: Future enhancements (see DEVELOPMENT_LOG.md)

## Next Steps

- User authentication (OAuth)
- Cloud-based learning history
- Proficiency analysis engine
- Mobile PWA support
- Offline functionality

For detailed development history, see [DEVELOPMENT_LOG.md](./DEVELOPMENT_LOG.md)

---

**Last Updated**: 2025-11-22  
**Version**: 1.0.0 (GitHub Pages deployed)
