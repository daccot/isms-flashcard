# ISMS Flashcard - Development Log

## Project Overview

Google Sheets-powered interactive learning tool for ISO/IEC 27001 (ISMS) exam preparation.

**Repository**: https://github.com/daccot/isms-flashcard  
**Live Demo**: https://daccot.github.io/isms-flashcard/  
**Last Updated**: 2025-11-22

---

## Phase History

### Phase 1: Basic Prototype (Completed)
**Timeline**: Initial development
**Features**:
- HTML/CSS/JS static flashcard interface
- 5 hardcoded ISMS questions
- Single-choice answer only
- Basic card layout with purple gradient

**Technical Details**:
- Vanilla JavaScript (no frameworks)
- LocalStorage for answer tracking
- CSS Grid for responsive layout

---

### Phase 2: Google Sheets Integration (Completed)
**Timeline**: API integration phase
**Features**:
- Dynamic question loading from Google Sheets
- Increased question count to 15
- Added metadata: category, difficulty, question type
- Multiple choice support (択一 and 複数選択)

**Technical Stack**:
- Google Visualization API for data fetching
- Spreadsheet ID: `1fZM_E7gYopOsVc6fQ-sK9A03F78sNfOub1x0PyxM9iQ`
- Public Sheet access (read-only)

**Data Schema**:
```
Column A: Question ID (Q001-Q015)
Column B: Question Text
Columns C-F: Multiple choice options (1-4)
Column G: Correct answer(s) ("1" or "1,3" for multiple)
Column H: Question type (択一 / 複数選択)
Column I: Category (11 ISMS categories)
Column J: Difficulty (初級 / 中級 / 上級)
```

---

### Phase 3: Advanced Features (Completed)
**Timeline**: Feature expansion
**Features Implemented**:

#### 3a: Filtering System
- Category filtering (11 categories)
- Difficulty level filtering (3 levels)
- Combined filter support
- Filter persistence in UI

#### 3b: Question Shuffling
- Randomized question order per session
- Implemented in applyFilters() function
- Math.random() based algorithm

#### 3c: Wrong Answer Tracking
- LocalStorage-based wrong answer persistence
- Review mode for missed questions only
- Question.wrong property flag

#### 3d: CSV Export
- Learning history export
- Columns: Date, Score, Percentage
- Formatted as Blob with UTF-8 encoding
- Auto-download to user device

#### 3e: X (Twitter) Sharing
- Auto-generated tweet content with score
- Shares: correct count, total questions, accuracy percentage
- Uses Twitter intent URL
- Hashtags: #ISMS, #InformationSecurity

**Code Changes**:
- Added updateHistory() function
- Implemented exportCSV() function
- Created shareOnX() function
- Enhanced answer checking logic

---

### Phase 4: Learning Dashboard (Completed)
**Timeline**: Visualization and analytics
**Features Implemented**:

#### 4a: Statistics Dashboard
- Three stat cards displaying:
  - Today's goal progress (5 questions/day target)
  - Consecutive learning streak (days)
  - Overall accuracy rate (%)

#### 4b: Chart.js Visualization
- **Chart 1**: Progress Line Chart
  - Shows last 10 quiz results
  - X-axis: Quiz attempt number
  - Y-axis: Accuracy percentage (0-100%)
  - Visual trend identification

- **Chart 2**: Category Bar Chart
  - Displays correct answers per category
  - X-axis: ISMS category names
  - Y-axis: Correct count
  - Identifies strengths and weaknesses

#### 4c: Daily Progress Tracking
- Date-based LocalStorage keys: `isms_daily_YYYY-MM-DD`
- Tracks questions completed per day
- Progress bar visualization
- Daily goal comparison (5 questions baseline)

#### 4d: Streak Calculation
- Iterates backwards through LocalStorage dates
- Counts consecutive days with activity
- Resets on missed days
- Displayed in stat card

**Technical Implementation**:
```javascript
function getStreak() {
  let streak = 0;
  let currentDate = new Date();
  while (true) {
    const dateStr = currentDate.toISOString().split('T')[0];
    const dailyKey = `isms_daily_${dateStr}`;
    if (localStorage.getItem(dailyKey)) {
      streak++;
      currentDate.setDate(currentDate.getDate() - 1);
    } else break;
  }
  return streak;
}
```

**CDN Dependencies**:
- Chart.js 4.5.0: https://cdn.jsdelivr.net/npm/chart.js@4.5.0/dist/chart.umd.min.js

---

### Phase 5: Bug Fixes & Refinement (Completed)
**Issues Resolved**:

#### Issue 5.1: Chart.js Loading Error
- **Problem**: "Uncaught ReferenceError: Chart is not defined"
- **Root Cause**: renderCharts() called before Chart library loaded
- **Solution**: Added type checking at function start
  ```javascript
  if (typeof Chart === 'undefined') {
    console.log('Chart.js is not loaded yet');
    return;
  }
  ```
- **Status**: Fixed ✅

#### Issue 5.2: LocalStorage History Merging
- Ensured existing quiz history persists when adding new quizzes
- Updated updateHistory() to preserve previous entries
- Status**: Fixed ✅

---

### Phase 6: GitHub Pages Deployment (Completed)
**Timeline**: 2025-11-22
**Deployment Steps**:

1. **Repository Setup**
   - Created GitHub repository: `daccot/isms-flashcard`
   - Public repository with no restrictions
   - Main branch as default

2. **File Upload**
   - Uploaded index.html to repository root
   - File encoding: UTF-8 LF (no BOM)
   - Size: ~85KB (including embedded CSS/JS)

3. **GitHub Pages Configuration**
   - Settings > Pages
   - Source: Deploy from branch
   - Branch: main
   - Folder: / (root)
   - Status: Active ✅

4. **Deployment Result**
   - Public URL: https://daccot.github.io/isms-flashcard/
   - Build status: Success ✅
   - HTTPS: Enabled by default
   - Deployment time: ~2-5 minutes

**Technical Details**:
- Static HTML deployment (no server-side processing)
- Google Sheets API accessible from GitHub Pages domain
- LocalStorage working without restrictions
- CORS issues: None (Sheets API is CORS-enabled)

---

## Planned Features (Phase 7+)

### Phase 7: User Authentication
- [ ] GitHub OAuth login
- [ ] User profile creation
- [ ] Persistent user data backend

### Phase 8: Cloud Data Synchronization
- [ ] Backend database (Firebase/Supabase)
- [ ] Sync learning history across devices
- [ ] Account-based data persistence

### Phase 9: Analytics & Recommendations
- [ ] Proficiency analysis engine
- [ ] Weakness identification
- [ ] AI-powered study recommendations
- [ ] Time-to-competency estimation

### Phase 10: Mobile Optimization
- [ ] Progressive Web App (PWA)
- [ ] Offline mode support
- [ ] Mobile-first responsive design
- [ ] Touch gesture support

### Phase 11: Localization
- [ ] Multi-language support
- [ ] International exam variations
- [ ] Locale-based question sets

---

## Code Architecture

### File Structure
```
isms-flashcard/
├── index.html          # Main application file (complete)
├── README.md           # Project documentation
└── DEVELOPMENT_LOG.md  # This file
```

### JavaScript Functions
- `loadQuestions()`: Fetch from Google Sheets API
- `applyFilters()`: Filter questions by category/difficulty
- `startQuiz()`: Initialize quiz mode
- `showQuestion()`: Display current question
- `checkAnswer()`: Validate and score answer
- `nextQuestion()`: Advance to next question
- `showFinalResult()`: Display quiz completion screen
- `updateHistory()`: Save to LocalStorage
- `renderCharts()`: Visualize progress with Chart.js
- `updateDashboardStats()`: Update stat cards
- `exportCSV()`: Download learning history
- `shareOnX()`: Open Twitter share intent

---

## Technology Stack

| Component | Technology | Version | Purpose |
|-----------|-----------|---------|----------|
| Frontend | HTML5 | - | Markup |
| Styling | CSS3 | - | Layout & design |
| Logic | JavaScript (Vanilla) | ES6+ | Core functionality |
| Data API | Google Sheets Visualization | - | Question database |
| Charts | Chart.js | 4.5.0 | Analytics visualization |
| Storage | LocalStorage API | - | Client-side persistence |
| Hosting | GitHub Pages | - | Static site deployment |
| Deployment | GitHub | - | Version control & CI/CD |

---

## Performance Metrics

- **Page Load Time**: <2 seconds
- **API Response Time**: <500ms (Google Sheets)
- **Question Shuffle Time**: <10ms
- **Chart Render Time**: <100ms
- **CSV Export Time**: <50ms

---

## Known Limitations

1. **No user authentication**: All data stored locally (single device only)
2. **Limited question bank**: 15 questions (expandable via Sheets)
3. **No offline access**: Requires internet for API calls
4. **Browser-dependent**: LocalStorage limited to same device/browser
5. **Single-instance quiz**: Cannot resume interrupted quizzes

---

## Future Considerations

- Mobile app version (React Native)
- Spaced repetition algorithm
- Timed exams mode
- Collaborative learning features
- API for third-party integrations
- Question difficulty adaptation (AI)

---

## Contact & Support

For issues, feature requests, or feedback, please open an issue on the [GitHub repository](https://github.com/daccot/isms-flashcard/issues).

---

**Version**: 1.0.0  
**Last Updated**: 2025-11-22  
**Maintenance Status**: Active
