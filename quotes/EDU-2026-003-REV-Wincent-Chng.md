# Quotation: BM Sukukata Phonics Learning Web Portal

**Quote Ref:** EDU-2026-003-REV  
**Client:** Wincent Ch'ng Winn Shern  
**Revision:** Initial

---

## A. Executive Summary

- **Quote Date:** 2026-04-09
- **Validity:** 30 calendar days
- **Portal Configuration:** Single Portal (user-facing web portal only, 1.0×)
- **Target Budget:** RM 25,000
- **Pre-Buffer Development Budget:** RM 20,833
- **Budget Utilization:** 96.3%
- **Estimated Project Duration:** 64.25 Days (total effort across all roles)
- **Total Estimated Price:** RM 24,084
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, or ongoing maintenance beyond the quoted scope.*
- **Included Services:** *Requirements discussion and gathering with the client, and all UI/UX design (wireframes, mockups) are included in the quoted scope.*

**Project Overview:**
A web-based Bahasa Malaysia Sukukata (syllable phonics) learning portal, inspired by the Jolly Phonics Lessons App. The platform delivers structured lesson plans, audio playback for each sukukata/letter sound, songs, animated letter/syllable formation, flash cards, word bank, assessment tests, and interactive games — all adapted for BM Sukukata pedagogy.

---

## B. Module Breakdown

| Module Name | Priority | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost | Status |
| :--- | :---: | :--- | ---: | ---: | ---: | ---: | :---: |
| User & Role Management | P1 | Medium (1.5×) | 4.5 | 3 | 1.25 | RM 2,770 | ✅ Included |
| Sukukata Content Management | P1 | Medium (1.5×) | 4.5 | 3 | 1.25 | RM 2,770 | ✅ Included |
| Audio & Media Playback Engine | P2 | Hard (2.0×) | 4 | 6 | 1.5 | RM 3,540 | ✅ Included |
| Lesson Plan Module | P2 | Medium (1.5×) | 3 | 3 | 0.75 | RM 2,130 | ✅ Included |
| Flash Cards & Word Bank | P3 | Simple (1.0×) | 1 | 2 | 0.5 | RM 1,060 | ✅ Included |
| Assessment & Quiz Engine | P3 | Medium (1.5×) | 3 | 3 | 0.75 | RM 2,130 | ✅ Included |
| Interactive Games | P3 | Hard (2.0×) | 4 | 6 | 1.5 | RM 3,540 | ✅ Included |
| Student Progress Dashboard | P4 | Medium (1.5×) | 3 | 3 | 0.75 | RM 2,130 | ✅ Included |
| | | **Totals** | **27** | **29** | **8.25** | **RM 20,070** | |
| | | **+ 20% Buffer** | | | | **RM 24,084** | |

### Module Scope Notes

- **User & Role Management** — Authentication, user profile CRUD, role-based access control (e.g., teacher, student roles), session management.
- **Sukukata Content Management** — CRUD for sukukata/syllable entries, associated audio file references, action images, lesson content metadata, and word bank data.
- **Audio & Media Playback Engine** — Letter sound / sukukata audio playback, songs for each sound, animated stroke-order formation (SVG/Canvas), media file serving.
- **Lesson Plan Module** — Structured daily lesson plans, lesson sequencing, curriculum progression through sukukata groups.
- **Flash Cards & Word Bank** — Browsable flash card interface, word bank display grouped by sukukata, flip-card interactions.
- **Assessment & Quiz Engine** — Assessment tests with scoring, multiple question types (match sound, identify syllable), result tracking per student.
- **Interactive Games** — Educational mini-games (drag-and-drop matching, syllable building, timed challenges) with scoring and audio integration.
- **Student Progress Dashboard** — Completion tracking per sukukata/lesson, performance summary, progress visualization.

---

## C. Resource Capacity Note

> *Reminder for internal planning:* Ensure frontend workload is balanced — the team operates with heavier backend capacity. Modules with heavy UI/UX requirements may become the schedule bottleneck.

> ⚠️ **Capacity Warning:** This project's frontend workload (29 days) exceeds backend (27 days). Given the team's ~3:1 BE-to-FE capacity ratio, frontend delivery is the likely bottleneck. Consider augmenting FE resources or phasing UI-heavy modules (Audio & Media Playback, Interactive Games).

---

## D. Next Steps for Client

We are pleased to confirm that all eight modules fit within the RM 25,000 budget with a 96.3% budget utilization. To proceed, we invite you to review and approve this quotation so that requirements gathering sessions can be scheduled and development can begin. Should you have any questions on scope or priorities, we are happy to discuss adjustments.

---

## E. Missing Technical Clarifications

The following questions MUST be answered before this estimate can be converted into a fixed-price contract:

1. **Sukukata syllable count & curriculum structure** — How many sukukata/syllables need to be covered? Is there a specific BM Sukukata curriculum or textbook to follow?
   - *Modules affected:* Sukukata Content Management, Lesson Plan Module, Audio & Media Playback.
   - *Cost impact:* If the syllable count exceeds ~100 unique entries with individual audio/animation assets, content setup effort may increase Module 2 and Module 3 estimates by 1–2 days each (+RM 1,000–2,000). This could push the project over budget, requiring Module 8 to be deferred.

2. **Audio & song content source** — Will the client provide pre-recorded audio for each sukukata sound and songs, or does the team need to source/produce audio assets?
   - *Modules affected:* Audio & Media Playback Engine.
   - *Cost impact:* If audio production is required (recording, editing, mastering), a separate **Audio Production** module would be needed (~RM 2,000–4,000), which would exceed the current budget.

3. **Target audience & user roles** — Is the portal for teachers only (delivering lessons to a class), for students to self-learn, or both? Are there parent accounts?
   - *Modules affected:* User & Role Management, Lesson Plan Module, Student Progress Dashboard.
   - *Cost impact:* Additional distinct user roles with separate dashboards could increase Module 1 and Module 8 by ~RM 500–1,000 each.

4. **Animated letter formation fidelity** — What level of animation is expected? Simple stroke-order guides (SVG path animation) or fully animated characters/hand demonstrations?
   - *Modules affected:* Audio & Media Playback Engine.
   - *Cost impact:* Full character animation would push this module's complexity higher and could add 2–4 adjusted FE days (+RM 600–1,200).

5. **Interactive game types & count** — How many distinct game types are expected? The reference app mentions "a selection" — is 3–4 game types sufficient, or are 8–10+ expected?
   - *Modules affected:* Interactive Games.
   - *Cost impact:* Each additional game type beyond 4 adds ~0.5–1 adjusted day in BE + FE (+RM 300–660 per game type). More than 6 types could require deferring Module 8 to stay within budget.

6. **Content management workflow** — Who will manage and update sukukata content, lessons, and audio after launch? If the client needs a content management admin interface, this would require a **Dual Portal** configuration (1.5× FE multiplier), significantly increasing the estimate.
   - *Modules affected:* All modules with FE component.
   - *Cost impact:* Switching to Dual Portal would increase total FE days by ~50%, pushing the estimate well beyond the RM 25,000 budget. A separate Phase 2 admin panel would need to be quoted.

7. **Offline / PWA support** — Does the web portal need to work offline (Progressive Web App) for use in areas with limited internet connectivity?
   - *Modules affected:* All frontend modules.
   - *Cost impact:* PWA with offline caching and service workers would add a dedicated module (~RM 1,500–2,500), exceeding the current budget.

---

*Generated by /pricing_skill (reverse) on 2026-04-09 | Constitution v2.1.0 | Rates: BE=RM360, FE=RM300, PM/QA=RM200 | Budget cap: RM 25,000*
