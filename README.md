


# SkillShield: Product Requirements Document (PRD) & MVP Spec

**Version:** 1.0  
**Date:** February 2, 2026  
**Author:** Product Strategy Team  
**Status:** MVP Planning

---

## Executive Summary

**SkillShield** is an AI-powered skill-decay detection and prevention platform that helps knowledge workers maintain professional competency in an age of AI over-reliance. While every other AI tool encourages maximum delegation, SkillShield tracks how AI usage affects your real skills and provides targeted "skill workouts" to prevent atrophy.

**Core Value Proposition:** "Stay competent, not just productive. SkillShield detects when AI is quietly eroding your skills and helps you rebuild them before it's too late."

**Target Market:** Individual knowledge workers (developers, writers, analysts, marketers) and teams concerned about long-term skill erosion from AI tool dependency[1][2].

**Business Model:** Freemium SaaS with subscription tiers (₹999/mo or $12/mo individual, ₹8,999/mo or $99/mo team plan).

---

## Problem Statement

### The Skill Decay Crisis

Research shows a documented phenomenon called "automation-induced deskilling"[3][4]:

- **Illusion of competence:** People feel productive using AI tools but their underlying skills quietly atrophy
- **Career risk:** As core skills decay, professionals become less hireable and more replaceable
- **No feedback loop:** Unlike physical fitness, skill decay is invisible until it's too late
- **Existing gap:** Every AI tool promotes *more* usage; zero tools help you stay sharp *despite* usage

### Market Evidence

- Growing awareness of "skill erosion" in developer communities[5]
- HR departments concerned about workforce deskilling[2][6]
- Individual anxiety about being "replaced by AI" driving demand for skill validation[1]

**Key insight:** The solution is not "stop using AI" (unrealistic) but "use AI strategically while exercising core skills regularly."

---

## Solution Overview

### Product Vision

SkillShield is a lightweight monitoring + intervention system that:

1. **Tracks** your work patterns (AI-assisted vs. self-work)
2. **Analyzes** which professional skills are active, fading, or decayed
3. **Intervenes** with micro-challenges to rebuild fading skills
4. **Measures** your skill health over time with clear metrics

Think: **Fitness tracker for professional competency**[7].

### Core User Experience

**For individual users:**

1. Install browser extension + optional desktop app
2. Grant permission to monitor work tools (IDE, docs, email, browser)
3. View personalized "Skill Health Dashboard" showing:
   - Active skills (exercised regularly)
   - Fading skills (declining activity)
   - Dormant skills (rarely used)
   - Recovery progress over time
4. Receive daily/weekly "Skill Workout" notifications:
   - 5-15 minute challenges targeting fading skills
   - E.g., "Write this email without AI," "Debug this code manually," "Summarize article yourself"
5. Complete workouts, see skill scores improve

**For team admins:**

- Aggregate view of team skill health (anonymized or role-based)
- Custom skill taxonomy for company-specific competencies
- Export reports for L&D and workforce planning

---

## Target Users & Personas

### Primary Persona: "Alex the AI-Dependent Developer"

- **Age:** 28-35
- **Role:** Full-stack developer, 3-7 years experience
- **Context:** Uses GitHub Copilot heavily, feels productive but worries about losing fundamental coding skills
- **Pain:** "I used to know algorithms cold. Now I can't solve a medium LeetCode without Copilot."
- **Goal:** Stay hireable and maintain technical depth despite AI assistance
- **Willingness to pay:** ₹999-1,499/mo ($12-18/mo) to protect career value

### Secondary Persona: "Priya the Content Strategist"

- **Age:** 26-32
- **Role:** Content writer/marketer
- **Context:** Uses ChatGPT for drafts, email, social posts
- **Pain:** "My writing voice is disappearing. Everything sounds AI-generated now."
- **Goal:** Maintain authentic creative voice and strategic thinking
- **Willingness to pay:** ₹799-999/mo ($10-12/mo)

### Tertiary Persona: "Rajesh the Engineering Manager"

- **Age:** 35-45
- **Role:** Team lead, 15-30 person team
- **Context:** Team heavily uses AI tools; concerned about junior developers never learning fundamentals
- **Pain:** "My juniors can ship features fast, but they can't debug without AI or explain how things work."
- **Goal:** Ensure team maintains core competencies for long-term success
- **Willingness to pay:** ₹8,999-14,999/mo ($99-199/mo) for team license

---

## MVP Feature Set (4-6 Week Build)

### Phase 1: Core Monitoring (Weeks 1-2)

**Feature 1.1: Browser Extension (Chrome/Edge)**

**What it does:**
- Tracks time spent on web-based work tools (VS Code Web, Google Docs, Gmail, Notion, ChatGPT, Claude, etc.)
- Detects AI tool usage patterns:
  - Copy/paste from AI chat interfaces
  - AI writing assistant usage (Grammarly, Jasper, etc.)
  - Time on AI tools vs. native work
- Logs activity data locally, syncs to backend

**Technical requirements:**
- Chrome Extension Manifest V3
- Content scripts for activity detection
- Local storage + periodic sync to backend API
- Privacy-first: no keystroke logging, only aggregate activity patterns

**Feature 1.2: Activity Classification Engine**

**What it does:**
- Maps detected activities to skill categories:
  - **Coding:** Time in IDE, commits, self-written vs. AI-generated code
  - **Writing:** Documents created, editing time, AI-assist usage
  - **Analysis:** Spreadsheets, dashboards, research tools
  - **Communication:** Email, Slack, meetings (tracked by integration)
- Assigns "self-work ratio" per skill per week

**Technical requirements:**
- Simple rule-based classifier (v1) with regex patterns
- Later: ML model for more accurate activity → skill mapping
- Skill taxonomy: 8-10 categories for MVP

**Feature 1.3: Skill Health Scoring**

**What it does:**
- Calculates skill health score (0-100) based on:
  - Self-work ratio trend (compared to baseline)
  - Frequency of skill usage
  - Recency of last self-work session
- Flags skills as: Active (80-100), Fading (50-79), Dormant (20-49), Decayed (0-19)

**Algorithm (simple MVP version):**
skill_score = (self_work_ratio * 0.5) + (usage_frequency * 0.3) + (recency_bonus * 0.2)

**Technical requirements:**
- Backend scoring service (Python/Node.js)
- Time-series data storage (PostgreSQL + TimescaleDB or similar)
- Daily batch scoring job

---

### Phase 2: Dashboard & Insights (Weeks 2-3)

**Feature 2.1: Skill Health Dashboard (Web App)**

**What it shows:**
- **Overview:** Overall skill health score + trend line
- **Skill breakdown:** List of tracked skills with individual scores and status badges
- **Weekly report:** "Skills exercised this week," "Skills at risk," "Recovery progress"
- **Activity timeline:** Visual representation of AI-usage vs. self-work over time

**Key visualizations:**
- Line chart: Skill health trends over 4-12 weeks
- Heat map: Skill activity by day/week
- Progress bars: Individual skill scores with targets

**Technical requirements:**
- React/Next.js web dashboard
- Chart library (Recharts or Chart.js)
- REST API for data fetching
- Responsive design (mobile-friendly)

**Feature 2.2: Insights & Recommendations**

**What it does:**
- Generates weekly insight messages:
  - "Your coding skills dropped 15% this week due to heavy Copilot usage"
  - "Great job! You completed 3 writing workouts and your writing score improved 8%"
- Suggests which skills need attention
- Celebrates progress and recovery

**Technical requirements:**
- Simple templated insight generation (v1)
- Later: LLM-generated personalized insights

---

### Phase 3: Skill Workouts (Weeks 3-5)

**Feature 3.1: Workout Generator**

**What it does:**
- Creates short (5-15 min) skill exercises tailored to fading skills:
  - **Coding:** "Implement this function without AI: [problem description]"
  - **Writing:** "Rewrite this AI-generated paragraph in your own voice"
  - **Analysis:** "Manually calculate this metric from raw data"
  - **Communication:** "Draft this email from scratch without AI assistance"
- Difficulty adapts based on user's baseline skill level

**Technical requirements:**
- Workout template library (20-30 templates for MVP)
- LLM API integration (OpenAI/Claude) for dynamic workout generation
- User profile: stores skill baselines and preferences

**Feature 3.2: Workout Delivery & Tracking**

**What it does:**
- Daily/weekly notifications: "Your writing skill needs attention. Try this 7-minute workout."
- In-app workout interface:
  - Challenge description
  - Input area (text editor, code sandbox, etc.)
  - Submit button
  - Simple validation (self-reported completion for MVP; automated checking v2)
- Logs completed workouts and updates skill scores

**Technical requirements:**
- Email + browser notification system
- Workout UI (modal or dedicated page)
- Completion tracking in database
- Score adjustment based on workout completion

**Feature 3.3: Workout Library**

**What it does:**
- Browse all available workouts by skill category
- Filter by difficulty, time commitment
- Save favorites
- Track completion history

**Technical requirements:**
- Simple catalog interface
- Search and filter functionality
- User workout history view

---

### Phase 4: Polish & Launch Prep (Weeks 5-6)

**Feature 4.1: Onboarding Flow**

**What it does:**
- Welcome screens explaining SkillShield's value
- Permission requests (browser monitoring, optional desktop access)
- Initial skill assessment: quick questionnaire to establish baseline
- First workout assignment

**Technical requirements:**
- Multi-step onboarding UI
- Baseline assessment logic
- User preferences storage

**Feature 4.2: Settings & Privacy Controls**

**What it does:**
- Toggle monitoring on/off
- Select which apps/sites to track
- Data retention settings
- Export personal data (GDPR compliance)
- Delete account

**Technical requirements:**
- Privacy-focused settings panel
- Data export API
- Account deletion workflow

**Feature 4.3: Basic Analytics & Gamification**

**What it does:**
- Streak tracking: "7-day workout streak!"
- Badges: "Skill Guardian" (30 workouts completed), "Coder's Edge" (maintained 80+ coding score for 4 weeks)
- Leaderboard (opt-in, anonymous): Compare your skill health percentile

**Technical requirements:**
- Achievement system (badge definitions + tracking)
- Leaderboard backend
- Social sharing (optional)

---

## Technical Architecture (MVP)

### Stack Recommendation

**Frontend:**
- **Extension:** Chrome Extension (Manifest V3), vanilla JavaScript + Webpack
- **Web Dashboard:** Next.js (React) + TypeScript + Tailwind CSS
- **Charts:** Recharts or Chart.js

**Backend:**
- **API:** Node.js (Express) or Python (FastAPI)
- **Database:** PostgreSQL (user data, skill scores) + TimescaleDB extension (time-series activity data)
- **Authentication:** Clerk or Auth0 for user management
- **Job Queue:** BullMQ or Celery for background scoring jobs

**AI/ML:**
- **Workout generation:** OpenAI GPT-4 or Anthropic Claude API
- **Activity classification:** Rule-based (v1) → simple ML classifier (scikit-learn or TensorFlow Lite) (v2)

**Infrastructure:**
- **Hosting:** Vercel (frontend) + Railway/Render (backend) for MVP
- **Monitoring:** Sentry (error tracking) + PostHog (product analytics)

**Storage:**
- User activity data: encrypted at rest
- Minimal PII collection (email only for MVP)

### Data Flow

1. Extension monitors activity → local storage
2. Periodic sync (every 1-6 hours) → Backend API
3. Backend stores activity logs → PostgreSQL/TimescaleDB
4. Daily batch job calculates skill scores
5. Web dashboard fetches scores via API
6. User completes workout → score updated immediately
7. Weekly insight email generated + sent

### Privacy & Security

- **Privacy-first design:** No keystroke logging, no document content capture
- **User control:** Granular permissions, pause monitoring anytime
- **Data minimization:** Store only aggregate activity patterns, not raw content
- **Encryption:** All data encrypted in transit (HTTPS) and at rest
- **Compliance:** GDPR-ready (data export, right to deletion)

---

## User Acquisition Strategy (MVP Phase)

### Target Launch Channels

1. **Developer communities:**
   - Reddit: r/programming, r/cscareerquestions, r/learnprogramming
   - Hacker News: "Show HN: I built a tool to prevent AI from eroding your coding skills"
   - Dev.to, Hashnode: Blog post about skill decay problem + solution

2. **Product Hunt launch:**
   - "SkillShield – Fitness tracker for your professional skills in the AI age"
   - Target: Product of the Day

3. **Twitter/X & LinkedIn:**
   - Thought leadership content about skill decay
   - Case studies: "I used SkillShield for 30 days and here's what happened"
   - Target audience: tech workers, managers, HR/L&D professionals

4. **Direct outreach:**
   - Tech bootcamps and upskilling platforms (integration partnerships)
   - HR/L&D leads at tech companies (team plan beta)

### Pricing (MVP)

**Individual Plan:**
- **Free:** Basic skill tracking, 1 workout/week, 30-day history
- **Pro (₹999/mo or $12/mo):** Unlimited workouts, full history, advanced insights, priority support
- **Annual (₹9,999/yr or $99/yr):** 2 months free

**Team Plan:**
- **₹8,999/mo or $99/mo for up to 10 users**
- Team dashboard, admin controls, custom skill taxonomy, usage reports
- Volume discounts for larger teams

### Success Metrics (3-Month Horizon)

- **Acquisition:** 500 signups, 100 paying users
- **Activation:** 60% complete onboarding, 40% complete first workout
- **Engagement:** 3+ workouts/user/week (active users)
- **Retention:** 50% D7 retention, 30% M1 retention
- **Revenue:** ₹1L or $1.2K MRR by month 3

---

## Development Roadmap

### Week 1-2: Foundation
- [ ] Set up project structure (frontend, backend, extension)
- [ ] Implement browser extension activity tracking
- [ ] Build basic backend API (user auth, activity logging)
- [ ] Design database schema
- [ ] Create activity classification rules (v1)

### Week 3-4: Core Features
- [ ] Implement skill health scoring algorithm
- [ ] Build web dashboard (overview + skill breakdown)
- [ ] Create workout template library (20 templates)
- [ ] Integrate LLM API for workout generation
- [ ] Implement workout delivery system

### Week 5: Polish
- [ ] Design onboarding flow
- [ ] Add privacy settings
- [ ] Implement email notifications
- [ ] Create insights generation logic
- [ ] Basic gamification (streaks, badges)

### Week 6: Testing & Launch Prep
- [ ] Internal testing (5-10 beta users)
- [ ] Fix critical bugs
- [ ] Write launch blog post + social content
- [ ] Prepare Product Hunt launch
- [ ] Set up analytics and monitoring
- [ ] Soft launch to developer communities

---

## Risk Assessment & Mitigation

### Technical Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Inaccurate skill classification | High | Medium | Start with rule-based + user feedback loop; iterate |
| Browser extension breaks with updates | Medium | High | Automated testing, fast update cycle |
| Data privacy concerns | Medium | High | Privacy-first design, clear communication, compliance |
| LLM API costs exceed budget | Medium | Medium | Cache common workouts, rate limits, tiered access |

### Market Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Users don't perceive skill decay as urgent | Medium | High | Content marketing: educate on long-term career risk |
| Hard to prove ROI | High | Medium | Track skill score improvements, user testimonials |
| Competing products emerge | Low | Medium | First-mover advantage, community building |
| AI tool makers integrate similar features | Low | High | Focus on cross-tool tracking, deeper insights |

### Competitive Landscape

**Direct competitors:** None identified (as of Feb 2026)

**Adjacent products:**
- Learning platforms (Coursera, Udemy): Focus on acquiring *new* skills, not maintaining existing ones
- AI coding assistants (GitHub Copilot): No skill-decay detection
- Productivity trackers (RescueTime): Track time, not skill health
- Corporate L&D platforms: Focus on training delivery, not individual skill monitoring

**Competitive advantage:**
- First mover in skill-decay detection category
- Privacy-first individual focus (vs. corporate surveillance)
- Lightweight, non-intrusive monitoring
- Actionable interventions (workouts), not just dashboards

---

## Go-to-Market Narrative

### Positioning Statement

"SkillShield helps knowledge workers stay competent, not just productive, in the age of AI. We detect when AI tools are quietly eroding your professional skills and provide targeted workouts to rebuild them—so you stay hireable, confident, and in control of your career."

### Key Messages

1. **Problem:** "AI tools make you feel productive, but your real skills are fading. You just don't notice until it's too late."
2. **Solution:** "SkillShield tracks your work patterns, detects skill decay early, and gives you micro-challenges to rebuild fading skills."
3. **Benefit:** "Maintain your professional edge. Use AI strategically without becoming dependent."
4. **Proof:** "Like a fitness tracker for your career—see your skill health improve week by week."

### Launch Story Hooks

- **Developer angle:** "I used Copilot for 6 months and almost forgot how to code. So I built SkillShield."
- **Research angle:** "Science says AI is quietly making us less competent. Here's how to fight back."
- **Career angle:** "Want to stay hireable in the AI age? You need to exercise your skills, not just outsource them."

---

## Post-MVP Roadmap (Months 2-6)

### v2 Features (Month 2-3)
- Desktop app for deeper IDE/app monitoring (VS Code, JetBrains, etc.)
- Advanced ML classification (activity → skill mapping)
- Automated workout validation (e.g., code execution, writing quality scoring)
- Mobile companion app (iOS/Android)

### v3 Features (Month 4-6)
- Team features: Manager dashboard, skill gap analysis, team challenges
- Integrations: Slack, Microsoft Teams, Linear, Jira
- Custom skill taxonomies (user-defined skills)
- Skill certification: Export verified skill profiles (e.g., for resumes, LinkedIn)
- Community features: Share workouts, leaderboards, skill challenges

### Long-term Vision (Year 2+)
- Enterprise plan: Custom deployments, SSO, compliance reporting
- B2B partnerships: Integrate with HR systems (Workday, BambooHR)
- Educational partnerships: Integrate with bootcamps and universities
- Skill marketplace: Connect users with projects that exercise specific skills
- AI skill coach: Personalized learning paths based on career goals and skill gaps

---

## Success Criteria (MVP)

**Validation that this is a viable business:**

1. **User interest:** 500+ signups in first month
2. **Willingness to pay:** 10%+ conversion to paid plans
3. **Engagement:** 40%+ weekly active users complete at least 1 workout
4. **Retention:** 30%+ users still active after 30 days
5. **Qualitative feedback:** 5+ strong testimonials about career impact

**If achieved → proceed to v2 and seed fundraising**  
**If not achieved → pivot messaging or target audience, or consider shutdown**

---

## Team & Resources (MVP Build)

### Recommended Team (Lean Startup)

**Solo founder path:**
- You (full-stack developer) + contract designer (UI/UX) + occasional LLM/ML consultant

**2-person founding team:**
- Technical co-founder (backend, ML, extension)
- Product/growth co-founder (frontend, design, marketing)

### Budget Estimate (6-week MVP)

| Item | Cost (INR) | Cost (USD) |
|------|------------|------------|
| Development time (opportunity cost) | ₹0-3L | $0-3.6K |
| Design (freelance, 2 weeks) | ₹40K-60K | $500-750 |
| OpenAI API credits (testing) | ₹5K | $60 |
| Infrastructure (dev + 3mo production) | ₹15K | $180 |
| Domain, logo, misc | ₹5K | $60 |
| **Total** | **₹65K-3.65L** | **$800-4.6K** |

*(Lower end assumes solo founder doing all dev work; higher end assumes some contractor help)*

### Tools & Services

- **Code:** VS Code, GitHub
- **Design:** Figma (free tier)
- **Project mgmt:** Linear or Notion
- **Communication:** Slack or Discord
- **Analytics:** PostHog (free tier), Google Analytics
- **Monitoring:** Sentry (free tier)
- **Email:** Resend or SendGrid (free tier)

---

## Appendix: Sample Workouts

### Coding Workout Examples

**Beginner:** "Implement a function that reverses a string without using built-in methods. Do not use AI. Time: 7 minutes."

**Intermediate:** "Given an array of integers, find two numbers that add up to a target sum. Implement in O(n) time. No AI assistance."

**Advanced:** "Design and implement a basic LRU cache with get() and put() operations in O(1) time. No AI tools."

### Writing Workout Examples

**Beginner:** "Rewrite this AI-generated paragraph in your own voice: [AI text]. Aim for authenticity and personality."

**Intermediate:** "Write a 200-word product description for [random product] without AI assistance. Focus on emotional benefits."

**Advanced:** "Draft a persuasive email to convince a busy executive to take a 30-min call with you. No AI tools."

### Analysis Workout Examples

**Beginner:** "Manually calculate the average, median, and mode of this dataset: [10 numbers]. No spreadsheet formulas."

**Intermediate:** "Given this sales data [CSV link], identify the top 3 insights. Do your own analysis without AI."

**Advanced:** "Build a cohort retention analysis from this user data. Show your work step-by-step."

---

## References

[1] Survey data: Small businesses and AI skill concerns (Verizon 2025 State of Small Business Survey)  
[2] Research: AI agents and skill training effectiveness (DigiqT 2025)  
[3] Academic research: Illusion of competence and skill degradation (RSiS International 2025)  
[4] Industry analysis: Skill erosion concerns in AI era (Mitrix.io 2025)  
[5] Community discussions: Skill decay detection with AI (Pexelle LinkedIn 2025)  
[6] Enterprise adoption: AI training programs for employee skill retention (HighPeak SW 2025)  
[7] Consumer health tech analogy: AI-powered personal coaching models (Rise Science, Eight Sleep case studies)

---

**Document End**

*This PRD is a living document. Update as user research and market feedback emerges during MVP development.*

# SkillShield: Product Requirements Document (PRD) & MVP Spec

**Version:** 1.0  
**Date:** February 2, 2026  
**Author:** Product Strategy Team  
**Status:** MVP Planning

---

## Executive Summary

**SkillShield** is an AI-powered skill-decay detection and prevention platform that helps knowledge workers maintain professional competency in an age of AI over-reliance. While every other AI tool encourages maximum delegation, SkillShield tracks how AI usage affects your real skills and provides targeted "skill workouts" to prevent atrophy.

**Core Value Proposition:** "Stay competent, not just productive. SkillShield detects when AI is quietly eroding your skills and helps you rebuild them before it's too late."

**Target Market:** Individual knowledge workers (developers, writers, analysts, marketers) and teams concerned about long-term skill erosion from AI tool dependency[1][2].

**Business Model:** Freemium SaaS with subscription tiers (₹999/mo or $12/mo individual, ₹8,999/mo or $99/mo team plan).

---

## Problem Statement

### The Skill Decay Crisis

Research shows a documented phenomenon called "automation-induced deskilling"[3][4]:

- **Illusion of competence:** People feel productive using AI tools but their underlying skills quietly atrophy
- **Career risk:** As core skills decay, professionals become less hireable and more replaceable
- **No feedback loop:** Unlike physical fitness, skill decay is invisible until it's too late
- **Existing gap:** Every AI tool promotes *more* usage; zero tools help you stay sharp *despite* usage

### Market Evidence

- Growing awareness of "skill erosion" in developer communities[5]
- HR departments concerned about workforce deskilling[2][6]
- Individual anxiety about being "replaced by AI" driving demand for skill validation[1]

**Key insight:** The solution is not "stop using AI" (unrealistic) but "use AI strategically while exercising core skills regularly."

---

## Solution Overview

### Product Vision

SkillShield is a lightweight monitoring + intervention system that:

1. **Tracks** your work patterns (AI-assisted vs. self-work)
2. **Analyzes** which professional skills are active, fading, or decayed
3. **Intervenes** with micro-challenges to rebuild fading skills
4. **Measures** your skill health over time with clear metrics

Think: **Fitness tracker for professional competency**[7].

### Core User Experience

**For individual users:**

1. Install browser extension + optional desktop app
2. Grant permission to monitor work tools (IDE, docs, email, browser)
3. View personalized "Skill Health Dashboard" showing:
   - Active skills (exercised regularly)
   - Fading skills (declining activity)
   - Dormant skills (rarely used)
   - Recovery progress over time
4. Receive daily/weekly "Skill Workout" notifications:
   - 5-15 minute challenges targeting fading skills
   - E.g., "Write this email without AI," "Debug this code manually," "Summarize article yourself"
5. Complete workouts, see skill scores improve

**For team admins:**

- Aggregate view of team skill health (anonymized or role-based)
- Custom skill taxonomy for company-specific competencies
- Export reports for L&D and workforce planning

---

## Target Users & Personas

### Primary Persona: "Alex the AI-Dependent Developer"

- **Age:** 28-35
- **Role:** Full-stack developer, 3-7 years experience
- **Context:** Uses GitHub Copilot heavily, feels productive but worries about losing fundamental coding skills
- **Pain:** "I used to know algorithms cold. Now I can't solve a medium LeetCode without Copilot."
- **Goal:** Stay hireable and maintain technical depth despite AI assistance
- **Willingness to pay:** ₹999-1,499/mo ($12-18/mo) to protect career value

### Secondary Persona: "Priya the Content Strategist"

- **Age:** 26-32
- **Role:** Content writer/marketer
- **Context:** Uses ChatGPT for drafts, email, social posts
- **Pain:** "My writing voice is disappearing. Everything sounds AI-generated now."
- **Goal:** Maintain authentic creative voice and strategic thinking
- **Willingness to pay:** ₹799-999/mo ($10-12/mo)

### Tertiary Persona: "Rajesh the Engineering Manager"

- **Age:** 35-45
- **Role:** Team lead, 15-30 person team
- **Context:** Team heavily uses AI tools; concerned about junior developers never learning fundamentals
- **Pain:** "My juniors can ship features fast, but they can't debug without AI or explain how things work."
- **Goal:** Ensure team maintains core competencies for long-term success
- **Willingness to pay:** ₹8,999-14,999/mo ($99-199/mo) for team license

---

## MVP Feature Set (4-6 Week Build)

### Phase 1: Core Monitoring (Weeks 1-2)

**Feature 1.1: Browser Extension (Chrome/Edge)**

**What it does:**
- Tracks time spent on web-based work tools (VS Code Web, Google Docs, Gmail, Notion, ChatGPT, Claude, etc.)
- Detects AI tool usage patterns:
  - Copy/paste from AI chat interfaces
  - AI writing assistant usage (Grammarly, Jasper, etc.)
  - Time on AI tools vs. native work
- Logs activity data locally, syncs to backend

**Technical requirements:**
- Chrome Extension Manifest V3
- Content scripts for activity detection
- Local storage + periodic sync to backend API
- Privacy-first: no keystroke logging, only aggregate activity patterns

**Feature 1.2: Activity Classification Engine**

**What it does:**
- Maps detected activities to skill categories:
  - **Coding:** Time in IDE, commits, self-written vs. AI-generated code
  - **Writing:** Documents created, editing time, AI-assist usage
  - **Analysis:** Spreadsheets, dashboards, research tools
  - **Communication:** Email, Slack, meetings (tracked by integration)
- Assigns "self-work ratio" per skill per week

**Technical requirements:**
- Simple rule-based classifier (v1) with regex patterns
- Later: ML model for more accurate activity → skill mapping
- Skill taxonomy: 8-10 categories for MVP

**Feature 1.3: Skill Health Scoring**

**What it does:**
- Calculates skill health score (0-100) based on:
  - Self-work ratio trend (compared to baseline)
  - Frequency of skill usage
  - Recency of last self-work session
- Flags skills as: Active (80-100), Fading (50-79), Dormant (20-49), Decayed (0-19)

**Algorithm (simple MVP version):**
skill_score = (self_work_ratio * 0.5) + (usage_frequency * 0.3) + (recency_bonus * 0.2)

**Technical requirements:**
- Backend scoring service (Python/Node.js)
- Time-series data storage (PostgreSQL + TimescaleDB or similar)
- Daily batch scoring job

---

### Phase 2: Dashboard & Insights (Weeks 2-3)

**Feature 2.1: Skill Health Dashboard (Web App)**

**What it shows:**
- **Overview:** Overall skill health score + trend line
- **Skill breakdown:** List of tracked skills with individual scores and status badges
- **Weekly report:** "Skills exercised this week," "Skills at risk," "Recovery progress"
- **Activity timeline:** Visual representation of AI-usage vs. self-work over time

**Key visualizations:**
- Line chart: Skill health trends over 4-12 weeks
- Heat map: Skill activity by day/week
- Progress bars: Individual skill scores with targets

**Technical requirements:**
- React/Next.js web dashboard
- Chart library (Recharts or Chart.js)
- REST API for data fetching
- Responsive design (mobile-friendly)

**Feature 2.2: Insights & Recommendations**

**What it does:**
- Generates weekly insight messages:
  - "Your coding skills dropped 15% this week due to heavy Copilot usage"
  - "Great job! You completed 3 writing workouts and your writing score improved 8%"
- Suggests which skills need attention
- Celebrates progress and recovery

**Technical requirements:**
- Simple templated insight generation (v1)
- Later: LLM-generated personalized insights

---

### Phase 3: Skill Workouts (Weeks 3-5)

**Feature 3.1: Workout Generator**

**What it does:**
- Creates short (5-15 min) skill exercises tailored to fading skills:
  - **Coding:** "Implement this function without AI: [problem description]"
  - **Writing:** "Rewrite this AI-generated paragraph in your own voice"
  - **Analysis:** "Manually calculate this metric from raw data"
  - **Communication:** "Draft this email from scratch without AI assistance"
- Difficulty adapts based on user's baseline skill level

**Technical requirements:**
- Workout template library (20-30 templates for MVP)
- LLM API integration (OpenAI/Claude) for dynamic workout generation
- User profile: stores skill baselines and preferences

**Feature 3.2: Workout Delivery & Tracking**

**What it does:**
- Daily/weekly notifications: "Your writing skill needs attention. Try this 7-minute workout."
- In-app workout interface:
  - Challenge description
  - Input area (text editor, code sandbox, etc.)
  - Submit button
  - Simple validation (self-reported completion for MVP; automated checking v2)
- Logs completed workouts and updates skill scores

**Technical requirements:**
- Email + browser notification system
- Workout UI (modal or dedicated page)
- Completion tracking in database
- Score adjustment based on workout completion

**Feature 3.3: Workout Library**

**What it does:**
- Browse all available workouts by skill category
- Filter by difficulty, time commitment
- Save favorites
- Track completion history

**Technical requirements:**
- Simple catalog interface
- Search and filter functionality
- User workout history view

---

### Phase 4: Polish & Launch Prep (Weeks 5-6)

**Feature 4.1: Onboarding Flow**

**What it does:**
- Welcome screens explaining SkillShield's value
- Permission requests (browser monitoring, optional desktop access)
- Initial skill assessment: quick questionnaire to establish baseline
- First workout assignment

**Technical requirements:**
- Multi-step onboarding UI
- Baseline assessment logic
- User preferences storage

**Feature 4.2: Settings & Privacy Controls**

**What it does:**
- Toggle monitoring on/off
- Select which apps/sites to track
- Data retention settings
- Export personal data (GDPR compliance)
- Delete account

**Technical requirements:**
- Privacy-focused settings panel
- Data export API
- Account deletion workflow

**Feature 4.3: Basic Analytics & Gamification**

**What it does:**
- Streak tracking: "7-day workout streak!"
- Badges: "Skill Guardian" (30 workouts completed), "Coder's Edge" (maintained 80+ coding score for 4 weeks)
- Leaderboard (opt-in, anonymous): Compare your skill health percentile

**Technical requirements:**
- Achievement system (badge definitions + tracking)
- Leaderboard backend
- Social sharing (optional)

---

## Technical Architecture (MVP)

### Stack Recommendation

**Frontend:**
- **Extension:** Chrome Extension (Manifest V3), vanilla JavaScript + Webpack
- **Web Dashboard:** Next.js (React) + TypeScript + Tailwind CSS
- **Charts:** Recharts or Chart.js

**Backend:**
- **API:** Node.js (Express) or Python (FastAPI)
- **Database:** PostgreSQL (user data, skill scores) + TimescaleDB extension (time-series activity data)
- **Authentication:** Clerk or Auth0 for user management
- **Job Queue:** BullMQ or Celery for background scoring jobs

**AI/ML:**
- **Workout generation:** OpenAI GPT-4 or Anthropic Claude API
- **Activity classification:** Rule-based (v1) → simple ML classifier (scikit-learn or TensorFlow Lite) (v2)

**Infrastructure:**
- **Hosting:** Vercel (frontend) + Railway/Render (backend) for MVP
- **Monitoring:** Sentry (error tracking) + PostHog (product analytics)

**Storage:**
- User activity data: encrypted at rest
- Minimal PII collection (email only for MVP)

### Data Flow

1. Extension monitors activity → local storage
2. Periodic sync (every 1-6 hours) → Backend API
3. Backend stores activity logs → PostgreSQL/TimescaleDB
4. Daily batch job calculates skill scores
5. Web dashboard fetches scores via API
6. User completes workout → score updated immediately
7. Weekly insight email generated + sent

### Privacy & Security

- **Privacy-first design:** No keystroke logging, no document content capture
- **User control:** Granular permissions, pause monitoring anytime
- **Data minimization:** Store only aggregate activity patterns, not raw content
- **Encryption:** All data encrypted in transit (HTTPS) and at rest
- **Compliance:** GDPR-ready (data export, right to deletion)

---

## User Acquisition Strategy (MVP Phase)

### Target Launch Channels

1. **Developer communities:**
   - Reddit: r/programming, r/cscareerquestions, r/learnprogramming
   - Hacker News: "Show HN: I built a tool to prevent AI from eroding your coding skills"
   - Dev.to, Hashnode: Blog post about skill decay problem + solution

2. **Product Hunt launch:**
   - "SkillShield – Fitness tracker for your professional skills in the AI age"
   - Target: Product of the Day

3. **Twitter/X & LinkedIn:**
   - Thought leadership content about skill decay
   - Case studies: "I used SkillShield for 30 days and here's what happened"
   - Target audience: tech workers, managers, HR/L&D professionals

4. **Direct outreach:**
   - Tech bootcamps and upskilling platforms (integration partnerships)
   - HR/L&D leads at tech companies (team plan beta)

### Pricing (MVP)

**Individual Plan:**
- **Free:** Basic skill tracking, 1 workout/week, 30-day history
- **Pro (₹999/mo or $12/mo):** Unlimited workouts, full history, advanced insights, priority support
- **Annual (₹9,999/yr or $99/yr):** 2 months free

**Team Plan:**
- **₹8,999/mo or $99/mo for up to 10 users**
- Team dashboard, admin controls, custom skill taxonomy, usage reports
- Volume discounts for larger teams

### Success Metrics (3-Month Horizon)

- **Acquisition:** 500 signups, 100 paying users
- **Activation:** 60% complete onboarding, 40% complete first workout
- **Engagement:** 3+ workouts/user/week (active users)
- **Retention:** 50% D7 retention, 30% M1 retention
- **Revenue:** ₹1L or $1.2K MRR by month 3

---

## Development Roadmap

### Week 1-2: Foundation
- [ ] Set up project structure (frontend, backend, extension)
- [ ] Implement browser extension activity tracking
- [ ] Build basic backend API (user auth, activity logging)
- [ ] Design database schema
- [ ] Create activity classification rules (v1)

### Week 3-4: Core Features
- [ ] Implement skill health scoring algorithm
- [ ] Build web dashboard (overview + skill breakdown)
- [ ] Create workout template library (20 templates)
- [ ] Integrate LLM API for workout generation
- [ ] Implement workout delivery system

### Week 5: Polish
- [ ] Design onboarding flow
- [ ] Add privacy settings
- [ ] Implement email notifications
- [ ] Create insights generation logic
- [ ] Basic gamification (streaks, badges)

### Week 6: Testing & Launch Prep
- [ ] Internal testing (5-10 beta users)
- [ ] Fix critical bugs
- [ ] Write launch blog post + social content
- [ ] Prepare Product Hunt launch
- [ ] Set up analytics and monitoring
- [ ] Soft launch to developer communities

---

## Risk Assessment & Mitigation

### Technical Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Inaccurate skill classification | High | Medium | Start with rule-based + user feedback loop; iterate |
| Browser extension breaks with updates | Medium | High | Automated testing, fast update cycle |
| Data privacy concerns | Medium | High | Privacy-first design, clear communication, compliance |
| LLM API costs exceed budget | Medium | Medium | Cache common workouts, rate limits, tiered access |

### Market Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Users don't perceive skill decay as urgent | Medium | High | Content marketing: educate on long-term career risk |
| Hard to prove ROI | High | Medium | Track skill score improvements, user testimonials |
| Competing products emerge | Low | Medium | First-mover advantage, community building |
| AI tool makers integrate similar features | Low | High | Focus on cross-tool tracking, deeper insights |

### Competitive Landscape

**Direct competitors:** None identified (as of Feb 2026)

**Adjacent products:**
- Learning platforms (Coursera, Udemy): Focus on acquiring *new* skills, not maintaining existing ones
- AI coding assistants (GitHub Copilot): No skill-decay detection
- Productivity trackers (RescueTime): Track time, not skill health
- Corporate L&D platforms: Focus on training delivery, not individual skill monitoring

**Competitive advantage:**
- First mover in skill-decay detection category
- Privacy-first individual focus (vs. corporate surveillance)
- Lightweight, non-intrusive monitoring
- Actionable interventions (workouts), not just dashboards

---

## Go-to-Market Narrative

### Positioning Statement

"SkillShield helps knowledge workers stay competent, not just productive, in the age of AI. We detect when AI tools are quietly eroding your professional skills and provide targeted workouts to rebuild them—so you stay hireable, confident, and in control of your career."

### Key Messages

1. **Problem:** "AI tools make you feel productive, but your real skills are fading. You just don't notice until it's too late."
2. **Solution:** "SkillShield tracks your work patterns, detects skill decay early, and gives you micro-challenges to rebuild fading skills."
3. **Benefit:** "Maintain your professional edge. Use AI strategically without becoming dependent."
4. **Proof:** "Like a fitness tracker for your career—see your skill health improve week by week."

### Launch Story Hooks

- **Developer angle:** "I used Copilot for 6 months and almost forgot how to code. So I built SkillShield."
- **Research angle:** "Science says AI is quietly making us less competent. Here's how to fight back."
- **Career angle:** "Want to stay hireable in the AI age? You need to exercise your skills, not just outsource them."

---

## Post-MVP Roadmap (Months 2-6)

### v2 Features (Month 2-3)
- Desktop app for deeper IDE/app monitoring (VS Code, JetBrains, etc.)
- Advanced ML classification (activity → skill mapping)
- Automated workout validation (e.g., code execution, writing quality scoring)
- Mobile companion app (iOS/Android)

### v3 Features (Month 4-6)
- Team features: Manager dashboard, skill gap analysis, team challenges
- Integrations: Slack, Microsoft Teams, Linear, Jira
- Custom skill taxonomies (user-defined skills)
- Skill certification: Export verified skill profiles (e.g., for resumes, LinkedIn)
- Community features: Share workouts, leaderboards, skill challenges

### Long-term Vision (Year 2+)
- Enterprise plan: Custom deployments, SSO, compliance reporting
- B2B partnerships: Integrate with HR systems (Workday, BambooHR)
- Educational partnerships: Integrate with bootcamps and universities
- Skill marketplace: Connect users with projects that exercise specific skills
- AI skill coach: Personalized learning paths based on career goals and skill gaps

---

## Success Criteria (MVP)

**Validation that this is a viable business:**

1. **User interest:** 500+ signups in first month
2. **Willingness to pay:** 10%+ conversion to paid plans
3. **Engagement:** 40%+ weekly active users complete at least 1 workout
4. **Retention:** 30%+ users still active after 30 days
5. **Qualitative feedback:** 5+ strong testimonials about career impact

**If achieved → proceed to v2 and seed fundraising**  
**If not achieved → pivot messaging or target audience, or consider shutdown**

---

## Team & Resources (MVP Build)

### Recommended Team (Lean Startup)

**Solo founder path:**
- You (full-stack developer) + contract designer (UI/UX) + occasional LLM/ML consultant

**2-person founding team:**
- Technical co-founder (backend, ML, extension)
- Product/growth co-founder (frontend, design, marketing)

### Budget Estimate (6-week MVP)

| Item | Cost (INR) | Cost (USD) |
|------|------------|------------|
| Development time (opportunity cost) | ₹0-3L | $0-3.6K |
| Design (freelance, 2 weeks) | ₹40K-60K | $500-750 |
| OpenAI API credits (testing) | ₹5K | $60 |
| Infrastructure (dev + 3mo production) | ₹15K | $180 |
| Domain, logo, misc | ₹5K | $60 |
| **Total** | **₹65K-3.65L** | **$800-4.6K** |

*(Lower end assumes solo founder doing all dev work; higher end assumes some contractor help)*

### Tools & Services

- **Code:** VS Code, GitHub
- **Design:** Figma (free tier)
- **Project mgmt:** Linear or Notion
- **Communication:** Slack or Discord
- **Analytics:** PostHog (free tier), Google Analytics
- **Monitoring:** Sentry (free tier)
- **Email:** Resend or SendGrid (free tier)

---

## Appendix: Sample Workouts

### Coding Workout Examples

**Beginner:** "Implement a function that reverses a string without using built-in methods. Do not use AI. Time: 7 minutes."

**Intermediate:** "Given an array of integers, find two numbers that add up to a target sum. Implement in O(n) time. No AI assistance."

**Advanced:** "Design and implement a basic LRU cache with get() and put() operations in O(1) time. No AI tools."

### Writing Workout Examples

**Beginner:** "Rewrite this AI-generated paragraph in your own voice: [AI text]. Aim for authenticity and personality."

**Intermediate:** "Write a 200-word product description for [random product] without AI assistance. Focus on emotional benefits."

**Advanced:** "Draft a persuasive email to convince a busy executive to take a 30-min call with you. No AI tools."

### Analysis Workout Examples

**Beginner:** "Manually calculate the average, median, and mode of this dataset: [10 numbers]. No spreadsheet formulas."

**Intermediate:** "Given this sales data [CSV link], identify the top 3 insights. Do your own analysis without AI."

**Advanced:** "Build a cohort retention analysis from this user data. Show your work step-by-step."

---

## References

[1] Survey data: Small businesses and AI skill concerns (Verizon 2025 State of Small Business Survey)  
[2] Research: AI agents and skill training effectiveness (DigiqT 2025)  
[3] Academic research: Illusion of competence and skill degradation (RSiS International 2025)  
[4] Industry analysis: Skill erosion concerns in AI era (Mitrix.io 2025)  
[5] Community discussions: Skill decay detection with AI (Pexelle LinkedIn 2025)  
[6] Enterprise adoption: AI training programs for employee skill retention (HighPeak SW 2025)  
[7] Consumer health tech analogy: AI-powered personal coaching models (Rise Science, Eight Sleep case studies)

---

**Document End**

*This PRD is a living document. Update as user research and market feedback emerges during MVP development.*
