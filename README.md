# 📓 Notebound — Evidence-Backed Study Companion


> **Built for students who can't afford AI hallucinations during exam prep.**  
> Notebound verifies every answer against your syllabus notes, quotes exact evidence verbatim, and turns passive study into an interactive, gamified habit.

---

## 📸 Screenshots

<p align="center">
  <img src="images/dashboard.png" alt="Notebound Dashboard Overview" width="800"/>
</p>

| Grounded QA & Evidence | Interactive Diagnostic Quizzes |
| :---: | :---: |
| ![Grounded QA](images/qa-evidence.png) | ![Quiz Section](images/quiz.png) |

| Collaborative Study Lounge | Leaderboard & Streaks |
| :---: | :---: |
| ![Study Lounge](images/lounge.png) | ![Leaderboard](images/leaderboard.png) |

---

## 🌟 What is Notebound?

Standard AI chatbots hallucinate concepts that aren't on your exam or introduce out-of-syllabus jargon. **Notebound** solves this by operating strictly as an **evidence-backed study companion**:

1. **Grounded Syllabus QA**: Answers student queries strictly from their uploaded notes.
2. **Three-Tier Verification Badges**:
   - `✓ Supported`: Explicitly stated in your notes with a verbatim citation.
   - `⚠️ Nuance / Partly Supported`: Partially in notes, clearly flagging what is verified vs. supplementary context.
   - `🚫 Not in Notes`: Prevents memorizing hallucinations by warning when a concept is outside the uploaded syllabus.
3. **Verbatim Quote Spotlight**: Clicking any citation instantly scrolls and highlights the exact sentence in your notebook view.
4. **Tap-to-Understand**: Instant one-tap explanations into **Simpler language**, **Real-world analogy/example**, or **Hinglish** (informal conversational style popular among Indian college students).
5. **Misconception-Targeted Quizzes**: Generates diagnostic questions directly from your notes, citing exact paragraphs in feedback.

---

## 📱 Mobile-First Paper Aesthetic

Styled after tactile physical student notebooks:
- **Ruled Paper Textures**: Subtle notebook lines and warm paper tones (`#FAF8F5` / `#F6F4EE`).
- **Washi Tape & Sticky Notes**: Neo-brutalist tape strips, hard drop shadows (`shadow-[3px_3px_0px_#0f172a]`), and clean 2px ink borders.
- **Persistent Bottom Deck**: Fixed mobile navigation deck (`Study`, `Quiz`, `Lounge`, `Streaks`, `Cloud`) accessible across all devices.
- **Overflow-Free Header**: Compact top bar fitting course selector, daily streak (`🔥 5d`), instant sync (`🔄`), and notifications (`🔔`) without horizontal scrolling.

---

## 🚀 Key Features

### 1. 🎓 Multi-Course Recommendations
Choose your current class or course to automatically load recommended subjects and curated syllabus topics:
- **B.Tech Computer Science**: Operating Systems (Deadlocks, Bankers Algorithm, Semaphores), Computer Networks, DBMS.
- **Medical & Biology (NEET / MBBS)**: Botany (Calvin Cycle & C3 pathway), Human Physiology, Cell Biology.
- **11th-12th Science (PCM / JEE)**: Thermodynamics & Carnot Engines, Wave Optics, Organic Chemistry.
- **Commerce & Finance**: Double-Entry Bookkeeping, Financial Statements, Cost Accounting.

### 2. 📄 PDF Note Extraction
- Upload your lecture slide PDFs, syllabus sheets, or handwritten note exports.
- Extracted via server-side `pdf-parse`, with Gemini automatically inferring the title and subject metadata.
- Notes are instantly chunked and indexed for grounded verification.

### 3. 👥 Real-Time Collaborative Study Lounge
- See peers currently studying the same topics in real time.
- Live activity feed showing peer milestones (quiz scores, completed revisions, verified quotes).
- Status broadcaster (`Studying`, `Quizzing`, `Reviewing`) with automatic presence sync.

### 4. 🏆 Gamified Progress & Streaks
- **Daily Study Streaks**: Visual flame badge (`🔥 5d`) with freeze shields to build consistent study habits.
- **XP & Levels**: Earn XP for asking grounded questions, completing quiz modules, enabling push notifications, and finishing revision milestones.
- **Class Leaderboard**: Real-time ranking with level badges and friendly peer competition.

### 5. ☁️ Cloud Sync & Study Reminders
- Sync study progress, notes, and milestones seamlessly across devices.
- Built-in study deadline manager with milestone completion checkboxes.
- Web Push Notifications to alert students before upcoming exam deadlines.

### 6. 🔐 Google Authentication Simulation
- Replicates the multi-account Google sign-in modal inspired by WorkSquare for fast profile switching.

---

## 🛠️ Architecture & Tech Stack

```
├── server.ts                  # Express backend + Vite middleware mode
│   ├── /api/gemini/grounded-qa       # Notes QA with verbatim quotes & evidence categorization
│   ├── /api/gemini/tap-to-understand # Simpler, Example, or Hinglish explanations
│   ├── /api/gemini/generate-quiz     # Notes-grounded quizzes with paragraph citations
│   ├── /api/parse-pdf                # PDF text extraction & AI metadata tagging
│   └── /api/sync/*                   # Real-time peer lounge & cloud sync endpoints
├── src/
│   ├── components/
│   │   ├── Navbar.tsx                # Mobile header (Course, Streaks, Sync, Bell)
│   │   ├── GroundedQASection.tsx     # Notebook reader, QA input, Quote spotlight, Tap-to-understand
│   │   ├── QuizSection.tsx           # Interactive quiz with instant citation feedback
│   │   ├── CollaborativeDashboard.tsx# Live study lounge & peer activity feed
│   │   ├── LeaderboardAndStreaks.tsx # Gamified streak counter, level progress & board
│   │   ├── CloudSyncAndReminders.tsx # Push notifications & study deadline tracker
│   │   ├── CourseSelectorModal.tsx   # Course curriculum switcher modal
│   │   ├── PdfUploadModal.tsx        # PDF drag-and-drop file uploader
│   │   └── GoogleAuthModal.tsx       # WorkSquare Google account sign-in
│   ├── data/
│   │   ├── coursesData.ts            # Curated syllabus topics for CS, Bio, PCM, Commerce
│   │   └── mockStudentData.ts        # Peer avatars, sample leaderboard, reminders
│   ├── utils/
│   │   └── confetti.ts               # Canvas confetti celebrations for streaks & quiz mastery
│   ├── App.tsx                       # Main application shell with bottom deck
│   └── main.tsx                      # React root entry point
```

### Technologies Used
- **Frontend**: React 19, TypeScript, Tailwind CSS v4, Lucide React icons, Canvas Confetti.
- **Backend**: Express 4, Node.js, `tsx`, Vite 8 in middleware mode.
- **AI Engine**: Google Gen AI SDK (`@google/genai`) strictly powered by **Google Gemma 4** open-weight reasoning models (`gemma-4-26b-a4b-it` & `gemma-4-31b-it`) with JSON schema enforcement.
- **Document Processing**: `pdf-parse`.

---

## 🏃 Getting Started Locally

### Prerequisites
- Node.js (v18+)
- npm or bun

### 1. Install Dependencies
```bash
npm install
```

### 2. Configure Environment Variables
Copy `.env.example` to `.env` and supply your Gemini API key:
```bash
cp .env.example .env
```
Inside `.env`:
```env
GEMINI_API_KEY="your-gemini-api-key"
```

### 3. Run the Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 💡 How to Test the Demo Flow

1. **Test Pre-Loaded Notes**:
   - Switch courses using the pill at top left (e.g., *B.Tech CS*, *NEET Biology*, or *PCM Science*).
   - Click one of the quick test chips from the deck:
     - `"Can deadlock occur if mutual exclusion is eliminated?"` (`✓ Supported`)
     - `"Is aging a complete cure for starvation?"` (`⚠️ Nuance / Partly Supported`)
     - `"Does Python optimize deadlock with Banker's Algorithm?"` (`🚫 Not in Notes`)
2. **Inspect Evidence**:
   - Notice the green verbatim evidence quote card.
   - Click the quote to automatically highlight the exact sentence in the notebook viewer.
3. **Try Tap-to-Understand**:
   - Click **Simpler**, **Example**, or **Hinglish** to get an instant alternate explanation grounded in the notes.
4. **Take a Quiz**:
   - Switch to the **Quiz** tab in the bottom deck. Answer the diagnostic questions and inspect the misconception feedback with syllabus citations.
5. **Upload Your Own PDF**:
   - Click **Upload PDF Notes** or use the included demo PDF to parse and test custom notes.