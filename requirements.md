# Project Requirements — ByteBudget (Spending Bot)

## Problem
People spend money across UPI, cards, wallets, and cash, but *don’t understand* where it goes or why they overspend. Existing expense trackers often feel manual, confusing, or “numbers-only” and don’t teach users what to do next. Users need a **super easy UI** and an AI assistant that turns transactions into clear insights, explains patterns in plain language, and provides **predictive money analysis** (forecasting upcoming spend and risk of overspending).

## Users

### Primary Users
- **Target Audience**: Students and early professionals who want to control spending and learn budgeting without effort.
- **User Personas**
  - *Student Saver*: limited pocket money, wants daily limits and alerts.
  - *New Earner*: salary just started, wants to build habits and savings goals.
  - *Impulse Spender*: wants gentle nudges and “why this happens” explanations.
- **User Context**: Mobile-first, quick check-ins (1–3 min) after spending, weekly review on weekends, chat-style Q&A anytime.

### Secondary Users
- **Stakeholders**: Parents/guardians (optional shared summaries), finance coaches/mentors (optional view-only reports).
- **Decision Makers**: The user themselves; optionally families/communities recommending the app.

## Goals

### Primary Goal
Help users **understand spending clearly and improve budgeting behavior** using an **easy, low-friction UI** + AI explanations + predictive insights.

### Secondary Goals
- Reduce “end-of-month surprise” via **spend forecasting** and early warnings.
- Build financial literacy via micro-lessons and simple explanations.
- Expand later to goal-based saving, subscriptions, credit-score friendly behavior, and regional language support.

## User Stories

### Core User Stories
- **As a** student, **I want** my transactions auto-categorized **so that** I don’t have to manually track expenses.
- **As a** user, **I want** a clean, simple UI that shows my key numbers instantly **so that** I don’t feel overwhelmed.
- **As a** user, **I want** predictive analysis (month-end forecast, overspend probability) **so that** I can adjust early.
- **As a** new earner, **I want** a weekly summary + overspend reasons **so that** I learn what to fix.

### Additional User Stories
- **As a** user, **I want** to ask “Where did my money go?” in chat **so that** I get answers instantly.
- **As a** user, **I want** smart budget limits and alerts **so that** I don’t exceed my spending targets.

## Functional Requirements

### Core Features
1. **Easy UI (Must-have)**
   - Minimal steps: Upload/Add → See summary → Ask chat → Get nudges.
   - Home screen shows: spent this month, remaining budget, top category, forecast.
   - Simple language, minimal charts, one-tap actions.
2. **Transaction Input**
   - Upload CSV / bank statement export (hackathon MVP) and/or manual quick-add.
   - Normalize fields: date, amount, merchant, notes, payment mode.
3. **Auto-Categorization + Tagging**
   - Categorize spends using rules + AI.
   - Allow user correction; system learns from corrections.
4. **Insights + Explanations**
   - Weekly/monthly summary: top categories, trends, unusual spends.
   - “Explain my spending” in plain language (why overspent, what changed).
5. **Predictive Money Analysis (Must-have)**
   - Month-end spend forecast based on recent pace + past patterns.
   - “Overspend risk” indicator (low/medium/high) per category and overall.
   - Suggested safe daily/weekly spending to stay within budget.
6. **Chat Q&A**
   - Natural language queries: “Spent on cafes last week?”, “Biggest expenses this month?”
7. **Smart Nudges**
   - Budget alerts + 2–3 simple actions (“Cap dining at ₹X this week”).
   - Early warning when forecast crosses budget threshold.

### Secondary Features
1. **Goals**
   - Set a savings goal; show progress and recommended weekly target.
2. **Subscriptions & Recurring Detection**
   - Detect repeated merchants and remind before renewal.
3. **Learning Mode**
   - Micro-lessons: “50/30/20”, “needs vs wants”, “how to set category budgets”.

### Integration Requirements
- **APIs (optional)**: LLM API for summarization/explanations; optional notifications (email/push).
- **Third-party Tools**: Firebase/Auth (if making an app), database (Postgres/Firestore).
- **Data Sources**: User-uploaded transaction exports (CSV/PDF converted to CSV).

## Non-Functional Requirements

### Performance
- **Response Time**: Summaries + forecasts + chat responses within ~3–5 seconds for typical datasets (≤5,000 rows).
- **Throughput**: MVP supports single user; scalable to 100+ concurrent sessions with caching.
- **Scalability**: Modular pipeline (ingest → clean → categorize → insights → prediction → chat).

### Security
- **Authentication**: Email/OTP or simple login for MVP.
- **Authorization**: Users can access only their own data.
- **Data Protection**
  - Encrypt data at rest and in transit (HTTPS).
  - Minimize data shared with LLM (send only necessary fields; mask identifiers when possible).

### Usability
- **User Experience**
  - “3-click rule” for main flows (upload → summary → forecast).
  - Accessible fonts, clear labels, low cognitive load.
- **Learning Curve**: User should get first insights within 2 minutes of upload.
- **Mobile Compatibility**: Responsive UI; mobile-first screens.

### Reliability
- **Uptime**: 99% for demo environment.
- **Error Handling**: Clear messages for invalid files/columns; fallback to rule-based categories if AI fails.
- **Data Integrity**: Consistent totals; no double-counting; audit log of category edits.

## Assumptions

### Technical Assumptions
- Hackathon MVP uses CSV uploads (not live bank integrations).
- Predictive model can start simple (trend/rolling average) and evolve to ML later.
- LLM usage is rate-limited and cost-controlled; fallback logic exists.
- Single developer can deliver a usable demo with a small dataset.

### Business Assumptions
- Users value “easy UI + predictive insights + coaching” more than raw tracking.
- Privacy-first messaging increases adoption.
- Freemium possible later: advanced forecasts, multi-account, exports.

### User Assumptions
- Users can export transactions or provide a sample file.
- Users prefer simple categories and short explanations.
- Users will correct categories occasionally to improve accuracy.

## Success Metrics

### Primary Metrics
- **Time-to-Value**: User gets first summary + forecast within 2 minutes of uploading data.
- **Forecast Usefulness**: Users understand and act on forecast (measured by clicks on “suggested actions”).
- **Categorization Accuracy**: ≥80% correct on first pass (improves with corrections).

### Secondary Metrics
- **User Engagement**: Weekly active usage; number of chat questions asked; nudges acknowledged.
- **Performance Metrics**: Error rate <2% on valid CSV uploads; median response time <5s.
- **Business Impact**: Reduction in discretionary spend (self-reported) over 4 weeks.

### Measurement Timeline
- **Short-term (Hackathon/Demo)**: Upload → summary → forecast → chat Q&A → nudges.
- **Medium-term (1–3 months)**: Returning users, improved accuracy, consistent weekly reports.
- **Long-term (6+ months)**: Habit change indicators, savings goal completion, retention growth.
