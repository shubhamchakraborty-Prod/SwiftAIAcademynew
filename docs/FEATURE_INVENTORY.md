# Swift AI Academy - Feature Inventory (from previous repos)

Source of truth for the rebuild in this repo. Compiled 28 Oct 2026.

## 1. Sources reviewed

| Repo | Content | Use for rebuild |
|---|---|---|
| `platformdemo` | `mvp_prd_doc.html` (11,422-line single-file clickable MVP, ~30 patch layers), `backend/` Course Finder API (Node, 26 tests), `docs/phase1-ux-audit.md`, contrast audit | **Primary.** All features below come from here |
| `Swift-AI-Academy` | README only | None |
| `Pathway-Engine` | Empty (no commits) | None |
| `SwiftAIAcademynew` | Empty (this repo) | Target |

## 2. Roles

| Role | Demo account | Lands on |
|---|---|---|
| Learner - new, college | Isha Joshi | Welcome |
| Learner - new, ITI | Sagar Pawar | Welcome |
| Learner - new, college onboarding | Ananya Mehta | Welcome |
| Learner - counselling | Rohan Kulkarni | Career counselling chat |
| Learner - existing, has progress | Sneha Kapoor / Aarav Sharma | Home |
| Learner - project under review | Karan Singh | Home |
| Institution admin - college | Priya Kapoor (AISHE C-41237) | Admin dashboard |
| Institution admin - ITI | Sunita Rao (NCVT MIS GR27000142) | Admin dashboard |
| Swift team (super admin) | team@swiftaiacademy.in | Institution admins console |
| Expert reviewer | Dr. Meera Shah | Reviews queue |

## 3. Learner features

### 3.1 Auth and account

| Feature | Detail |
|---|---|
| Login | Email + password, show/hide, demo-account dropdown, errors (wrong password, unknown email, not activated) |
| Invite activation | `#/invite/{token}` and `#/start`: set password from admin invite. Password rules by role (learner: 12+ chars) |
| Forgot / reset password | `#/reset/{token}`, simulated email |
| Signup | Self-signup route exists (`#/signup`); institution-linked is the main path |
| OTP | Demo OTP state present |
| Mock inbox | `#/inbox`, `#/inbox/{id}`: simulated mail client showing invite/reset emails (demo only) |
| Contact support | Canned support topics, simulated send to support@swiftaiacademy.in |

### 3.2 Onboarding (`#/onboarding/profile`)

| Step | Content |
|---|---|
| 1 Basic information | Prefilled by institution (locked fields with source): name, student ID, gender, DOB, email, mobile, address |
| 2 Institution information | Institution, programme, specialisation, year/semester; ITI: trade, NCVT reg no, scheme (CTS/DST/Flexi MoU), medium, apprenticeship status |
| 3 Consent | Required, explicit (audit D4: must not be pre-ticked) |
| 4 Awards and past experience | Optional |
| Profile completeness | % score, sections saved, edit later via `#/profile/edit/{0-7}` (8 sections: Basic, Institution & Academics, Skills & Baseline, Interests & Aspirations, Learning Preferences, Awards & Past Experience, ...) |

### 3.3 Welcome and product tour

`#/welcome` hero, then 5-step guided tour (Next, Previous, Skip, Finish; reopen from Help).

### 3.4 Home (`#/home`)

Resume current course (single Continue CTA), next step + time, weekly activity (days active, hours), notifications, news/"Did you know", events, alumni spotlight.

### 3.5 Career Counselling (`#/career`, `#/career/chat`, `#/career/report`, `#/career/compare`)

Embedded second app (212 KB, iframe). English / Hindi (Hinglish) chosen first.

| Stage | Detail |
|---|---|
| Greeting | Language pick, profile check (prefilled from onboarding) |
| Quick questions | Goal (start career, study further, own work, stable job), timeline urgency, weekly hours (2-3 / 4-6 / 7+), support needed, interests (multi-select), top priority |
| Picture-based test | Part 1 "What you enjoy" (interests, pick one of pictures), Part 2 "How you work" (personality statements, scale). 18 statements in learner build (40 in full spec). Listen (speech synthesis), Back, Save and pause, careless-pattern detection + retake |
| Report | Your type, personality + "what this means at work", areas of interest (top 3), strengths, skills to build, suitable career tracks, your answers, Download PDF, saved to profile, previous reports |
| Recommendations | 3 recommended pathways with fit, why it suits you; compare side by side (fit, duration, jobs, key skills, AI skills, where people get hired) |
| Handoff | "View your courses" -> pathway, report surfaced on Career page |

Traits: Takes initiative, Careful and thorough, Creative thinker, Team player, Calm under pressure. Interests: Helping people, Figuring things out, Hands-on and machines, Creating and designing, Leading and selling, Organising.

### 3.6 Course Finder (backend, `platformdemo/backend`)

ITI population pack: 32 questions, 15 screens, 8 parts -> explained plan (`start`, `next[]`, `also[]`, path). 19 courses, 39 skills, 11 goals. EN/HI. Evidence rules, levels, eligibility, scoring, planner, explanations. Staff trace, course ingestion with validation, AES-256-GCM encryption at rest, retention, rate limit. Not yet wired to the bot.

### 3.7 Explore and pathways

| Feature | Detail |
|---|---|
| Explore (`#/explore`) | Search, filters by category (Data & Analytics, AI & ML, Software & IT, Communication, Business, Sales & Marketing, Healthcare), recommended first, partner rows (Google, ConveGenius.AI, AWS, Intel, + others), role cards, news |
| Pathway page (`#/pathways/{id}`) | Courses in order, estimate, roles, skills, OEM partner, enroll / start |
| Baseline test (`#/baseline/{track}`) | 8-question adaptive test from 12-item bank per track (4 Foundation / 4 Core / 4 Advanced), per-skill evidence, placement (Foundation / Core / Advanced) + explanation, sets course start point |
| Role page (`#/roles/{id}`) | Intro, tasks, core + good-to-have skills, progression (illustrative), entry routes, certs |

Pathways (3):

| ID | Name | Courses | Estimate | Partner | Roles |
|---|---|---|---|---|---|
| aiml | Applied AI/ML Practitioner | AI01-AI04 + MC4 elective | 18 wks, 4-6 h/wk | Google | ML Associate, Data Science Analyst, AI Support |
| analytics | Business Data Analyst | DA01-DA03 | 14 wks, 4-6 h/wk | AWS | Data Analyst, MIS Executive, BI Associate |
| comms | Workplace Communication Pro | CO01-CO03 | 8 wks, 2-3 h/wk | ConveGenius.AI | Customer Success Associate |

Courses (11): AI01 Python for data work, AI02 Data handling and statistics, AI03 ML foundations, AI04 Applied ML project (expert review), DA01 Spreadsheets to SQL, DA02 Dashboards, DA03 Analytics case studies (expert review), CO01 Spoken clarity, CO02 Written workplace English, CO03 Interviews and GD, MC4 Make It Stick (AAI-E-MC4). Each: overview, outcomes, skills, weeks, hours, mode, languages, 4-5 submodules, assessment, practical.

### 3.8 Course page and player (`#/courses/{id}`, `#/learn/{course}/{step}`)

| Feature | Detail |
|---|---|
| Course page | Units, status, duration, credit/NSQF (label "pending"), Start/Continue, locked units with reason |
| Step types | Video, reading + worked example, response task, checkpoint quiz (practice), module quiz (assessed) |
| MC4 asset types | video, reading, card, lab (structured forms), practice bot, peer exchange, section check (quiz, S02 = non-compensatory gate), resources, facilitator kit, portfolio form, final demonstration |
| MC4 segments | S01 Build the Method (5h), S02 Test and Harden It (5h, gate), S03 Demonstrate and Commit (5h), S04 Checkpoint Assessment (portfolio + demo) |
| MC4 rubric | Method clarity, Test coverage, Diagnosis & correction, Human checkpoint present, Limitations ... |
| Progress | Per-course status, completed submodules, checkpoint scores, quiz score/attempts |

### 3.9 Projects and expert review (`#/projects/{id}`, `#/reviews`)

Submit project (versions), status (submitted / under_review / returned / resubmitted / approved), reviewer comments, review queue for expert/institution.

### 3.10 Achievements and credentials

| Feature | Route |
|---|---|
| Achievements hub | `#/achievements`, `/pathways`, `/courses`: certificates, hackathons, competitions, projects, other achievements, stats |
| Certificate | `#/certificates/{id}` (e.g. SAA-2026-1001), QR, download, share |
| Public verify | `#/verify/{id}` (public route) |
| Skill passport | `#/skill-passport` |

### 3.11 Opportunities (`#/opportunities`)

Govt portals first (PMIS, NCS, Skill India Digital Hub, NAPS, ... with ministry, who can apply, how-to steps), competitions, internships, jobs, hackathons, partner companies (Myntra, OLA, PepsiCo, Reliance, Samsung, Snapdeal, Tata), coding sprint challenges, eligibility by pathway/placement, deadlines.

### 3.12 Community, notifications, profile, help

| Feature | Detail |
|---|---|
| Community | Posts (Thought / Project / Achievement), like, comment, report |
| Notifications / Updates | Types: opportunity, action required, platform update; tabs learning / certs / account; mark read |
| My profile | `#/profile` (about, report, tracks, learning, readiness) |
| Help | FAQ, reopen tour, contact support |
| i18n | English + Hindi toggle across app (`T(en, hi)`) |
| Theme | system / light / dark setting (audit: decide) |

## 4. Institution admin features

| Feature | Detail |
|---|---|
| Admin dashboard (`#/admin/dashboard`) | Invite funnel (Added -> Invited -> Delivered -> Email opened -> Link clicked -> Password set -> Profile done -> Tour done), "Needs a nudge" list, stream popularity, avg progress, notifications, project review queue, seminars |
| Learners (`#/admin/learners`) | Table + filters, add single learner, bulk CSV upload (sample CSVs for college and ITI, header aliasing), edit invite subject/message, invite, resend |
| Field schemas | College: ID, name, gender, DOB, email, mobile, programme, specialisation, year, semester, batch, city, state. ITI adds NCVT reg no, trade, scheme, medium, apprenticeship, guardian |
| Institution types | ITI (NCVT MIS code), Degree college / University / Polytechnic (AISHE code) |
| Admin roles | ITI: Principal, Training officer, Placement officer, Group instructor, Office superintendent. College: Principal/director, TPO, Dean/HoD, Faculty coordinator, Registrar |
| Cohorts, reports, performance | `#/institution/*` (folded into dashboard in latest layer) |
| Institution registration | `#/institution/register`: contact, cohort scope, goals, delivery, access (SSO), funding, reporting/credit recognition; activation log Draft -> Submitted -> Verification pending -> Scope confirmed -> Configuration complete -> Active |

Reference data: 12 programmes (Diploma, B.Tech, B.Sc, BCA, B.Com, BBA, BA, B.Ed, B.Pharm, MBA, M.Sc, MCA) with specialisations; ITI trades list; 12th streams; boards; mediums.

## 5. Swift team (super admin)

`#/admin/institutions`: create institution admins (type, institution name + code, admin name, role), issue login, list admins.

## 6. Demo-only items (do not ship as real)

Demo console (`#/demo`), demo account dropdown, "skip to results" in test, simulated email/PDF/video/QR, mock inbox.

## 7. Known defects to avoid (from Phase 1 audit)

| # | Defect | Rule for rebuild |
|---|---|---|
| D1 | One click completes a course | Gated Next per step; response cannot be empty |
| D2 | Empty quiz passes and issues certificate | Pass mark, score, feedback, attempts, retry |
| D3 | Reload logs out, login resets progress | Real session + persisted state |
| D4 | Consent pre-ticked | Explicit opt-in, blocks finish |
| D5 | Certificate modal ignores Esc, persists across routes | Modal: Esc, focus trap, closes on route change |
| D6 | Demo buttons in learner test | No demo controls in learner UI |
| D7 | Internal production metadata shown | Hide PC codes, asset status |
| D8 | Placeholder lesson/quiz content | Real or clearly labelled content |
| D9 | Progress mismatch (8% vs 4%) | One progress source |
| D10 | Mobile tab bar covers content | Safe-area padding |

Brand rules (v1.0): Royal Blue `#3D5AFE`, Deep Navy `#0E1B5C`, Gold `#FBB034` (verified moments only), Cabinet Grotesk + JetBrains Mono, no serifs, no emoji icons, one line icon family, no hype copy, no exclamation marks.

## 8. Missing components the audit requires

Video player (play, pause, seek, subtitles, speed, resume), audio recorder (record, stop, playback, re-record, submit), quiz item (check, feedback), assessment shell (pass mark, attempts, timer, time-up reattempt, resume), hint ladder, Next/Previous bar, loading/error states, interrupted-session resume.
