# Reverse Estimation Quotation — BM Sukukata Learning Portal

**Quote Ref:** EDU-2026-002-REV

---

## A. Executive Summary

- **Quote Date:** 2026-04-09
- **Validity:** 30 calendar days
- **Portal Configuration:** Single Portal (Web)
- **Target Budget:** RM 25,000
- **Pre-Buffer Development Budget:** RM 20,833
- **Budget Utilization:** 99.2%
- **Estimated Project Duration:** 66.5 person-days (adjusted, included modules only)
- **Total Estimated Price:** RM 24,804 *(within RM 25,000 cap)*
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, audio recording/licensing costs, or ongoing maintenance beyond the quoted scope.*

**Assumptions:**
- Platform: Web (browser-based learning portal — desktop and mobile browser compatible). No native iOS/Android app is included in this scope.
- Client provides all BM Sukukata linguistic content (syllable lists, correct sequences, word lists, lesson sequencing).
- Audio assets (recordings of syllable sounds) are provided by the client or recorded separately — this quote covers integration only, not studio recording.
- UI/UX design mockups are provided by the client or handled as a separate engagement.

---

## B. Module Breakdown

### Included Modules

| Module Name | Priority | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost | Status |
| :--- | :---: | :--- | :---: | :---: | :---: | ---: | :---: |
| User & Role Management | P1 | Medium (1.5×) | 4.5 | 3.0 | 1.25 | RM 2,770 | ✅ Included |
| CRUD Content Management (Syllable & Lesson) | P1 | Medium (1.5×) | 4.5 | 3.75 | 1.25 | RM 2,995 | ✅ Included |
| Sukukata Sound Library & Audio Engine | P2 | Hard (2.0×) | 6.0 | 6.0 | 1.75 | RM 4,310 | ✅ Included |
| Animated Sukukata Formation | P2 | Hard (2.0×) | 3.0 | 8.0 | 1.75 | RM 3,830 | ✅ Included |
| Lesson Plan & Content Sequencing | P3 | Medium (1.5×) | 3.0 | 3.0 | 1.0 | RM 2,180 | ✅ Included |
| Word Bank & Flash Cards | P3 | Medium (1.5×) | 2.25 | 3.75 | 1.0 | RM 2,135 | ✅ Included |
| Assessment & Progress Tracking | P4 | Medium (1.5×) | 3.75 | 3.0 | 1.0 | RM 2,450 | ✅ Included |
| | | | | | | | |
| **Totals (Included)** | | | **27.0** | **30.5** | **9.0** | **RM 20,670** | |
| **Grand Total (×1.20 buffer)** | | | | | | **RM 24,804** | |
| | | | | | | | |
| ~~Interactive Learning Games~~ | P5 | Hard (2.0×) | ~~5.0~~ | ~~9.0~~ | ~~2.0~~ | ~~RM 4,900~~ | ⛔ Deferred |
| ~~Push Notifications & Reminders~~ | P6 | Simple (1.0×) | ~~1.0~~ | ~~0.5~~ | ~~0.25~~ | ~~RM 560~~ | ⛔ Deferred |
| ~~Offline Mode & Data Sync~~ | P6 | Hard (2.0×) | ~~5.0~~ | ~~3.0~~ | ~~1.25~~ | ~~RM 2,950~~ | ⛔ Deferred |

> All P1–P4 modules fit within the RM 20,833 development budget.
> Budget headroom remaining: RM 20,833 − RM 20,670 = **RM 163** (pre-buffer).
> Deferred modules total RM 8,410 pre-buffer and are recommended as a Phase 2 engagement.

### Cost Verification

| Module | Formula | Subtotal |
| :--- | :--- | ---: |
| User & Role Management | (4.5×360) + (3.0×300) + (1.25×200) | RM 2,770 |
| CRUD Content Management | (4.5×360) + (3.75×300) + (1.25×200) | RM 2,995 |
| Sukukata Sound Library & Audio Engine | (6.0×360) + (6.0×300) + (1.75×200) | RM 4,310 |
| Animated Sukukata Formation | (3.0×360) + (8.0×300) + (1.75×200) | RM 3,830 |
| Lesson Plan & Content Sequencing | (3.0×360) + (3.0×300) + (1.0×200) | RM 2,180 |
| Word Bank & Flash Cards | (2.25×360) + (3.75×300) + (1.0×200) | RM 2,135 |
| Assessment & Progress Tracking | (3.75×360) + (3.0×300) + (1.0×200) | RM 2,450 |

### Module Detail Notes

| # | Module | What's Included |
| :---: | :--- | :--- |
| 1 | **User & Role Management** | Email/social login, user profile CRUD, student/parent/teacher role separation, session management, RBAC |
| 2 | **CRUD Content Management** | Web-based CMS for managing syllables, audio mappings, images, lesson content, and flash card data |
| 3 | **Sukukata Sound Library & Audio Engine** | Audio playback engine for all BM sukukata/syllable sounds, syllable-to-audio mapping, streaming + caching, playback controls |
| 4 | **Animated Sukukata Formation** | Stroke-by-stroke animation for writing each sukukata in browser, mouse/touch-to-trace practice with visual feedback |
| 5 | **Lesson Plan & Content Sequencing** | Structured daily lesson plans, progressive difficulty sequencing, lesson completion tracking |
| 6 | **Word Bank & Flash Cards** | Vocabulary cards with image + audio + text, drill mode, categorization by lesson/topic |
| 7 | **Assessment & Progress Tracking** | Quiz engine with multiple question types, scoring, progress dashboard for parents/teachers |

---

## C. Resource Capacity Note

> *Reminder for internal planning:* Ensure frontend workload is balanced — the team operates with heavier backend capacity. Modules with heavy UI/UX requirements may become the schedule bottleneck.

> ⚠️ **Capacity Warning:** This project's frontend workload (30.5 days) exceeds backend (27.0 days). Given the team's ~3:1 BE-to-FE capacity ratio, frontend delivery is the likely bottleneck. The Animated Sukukata Formation module (8.0 FE days) and Sound Library (6.0 FE days) carry the heaviest FE concentration — consider sequencing these as early milestones to surface integration risks and augmenting FE resources if needed.

---

## D. Next Steps for Client

We are pleased to present this quotation for the BM Sukukata Learning Portal. All P1–P4 modules fit comfortably within the RM 25,000 budget. Upon approval, we will proceed with content requirements gathering, UI/UX mockup alignment, and Sprint 1 planning — with the Sound Library and Animated Formation modules prioritised as the earliest milestones. The three deferred modules (Interactive Learning Games, Push Notifications, Offline Mode) are recommended as a Phase 2 engagement and can be quoted separately upon successful delivery of Phase 1.

---

## E. Missing Technical Clarifications

The following information is required to convert this estimate into a fixed-price contract. Each item identifies the affected module(s) and potential cost impact.

1. **BM Sukukata Syllable Inventory** *(Modules: Sound Library, Animation, Word Bank)*
   - How many unique BM sukukata/syllables need to be supported? (BM syllable combinations could range from ~30 to 200+.)
   - **Cost impact:** If >100 unique syllables each with individual audio + animation, Sound Library and Animation modules may each increase by RM 500–1,500.

2. **Audio Asset Source** *(Modules: Sound Library, Lesson Plan)*
   - Will the client provide professionally recorded audio files, or does the team need to integrate a text-to-speech engine?
   - **Cost impact:** TTS integration would escalate Sound Library from Hard to Hard+ and add ~RM 1,000–2,000.

3. **User Roles & Multi-Tenancy** *(Modules: User & Role Management, Assessment)*
   - Is this for individual parents/children only, or also for schools/classrooms with teacher accounts managing multiple students?
   - **Cost impact:** Multi-tenant school/classroom support would add RM 1,000–2,000 to Auth + Assessment modules.

4. **Browser & Device Support** *(All FE Modules)*
   - Target browsers (Chrome, Safari, Firefox)? Is mobile browser compatibility (responsive web) required?
   - **Cost impact:** Wide cross-browser and responsive compatibility adds approximately 10–15% FE overhead across all modules.

5. **Monetization Model** *(Modules: User & Role Management, potentially new module)*
   - Free, one-time purchase, subscription, or school/institutional licensing?
   - **Cost impact:** Subscription or payment integration is NOT included in this quote. Would add a new Hard-tier module at RM 2,500–4,000.

6. **Songs / Music Content** *(Modules: Sound Library, Lesson Plan)*
   - Will the app include original BM Sukukata songs (similar to the Jolly Phonics song-per-sound feature)?
   - **Cost impact:** Song playback integration is included; original song creation/recording is NOT. If original compositions are needed, that is a separate creative engagement.

---

### Derivation Summary

| Parameter | Value |
| :--- | ---: |
| Target Budget | RM 25,000 |
| ÷ 1.20 (strip 20% buffer) | RM 20,833 |
| Sum of included modules | RM 20,670 |
| × 1.20 (apply buffer) | RM 24,804 |
| Budget headroom (post-buffer) | RM 196 |
| Budget utilization | 99.2% |
| Total adjusted BE days | 27.0 |
| Total adjusted FE days | 30.5 |
| Total adjusted PM/QA days | 9.0 |
| Total adjusted days | 66.5 |

---

*Generated by /pricing_skill (reverse) on 2026-04-09 | Constitution v2.0.0 | Rates: BE=RM360, FE=RM300, PM/QA=RM200 | Budget cap: RM 25,000*
