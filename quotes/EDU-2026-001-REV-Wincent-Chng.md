# Reverse Estimation Quotation — BM Sukukata Learning App

**Quote Ref:** EDU-2026-001-REV

---

## A. Executive Summary

- **Quote Date:** 2026-04-08
- **Validity:** 30 calendar days
- **Target Budget:** RM 25,000
- **Pre-Buffer Development Budget:** RM 20,833
- **Budget Utilization:** 90.8%
- **Estimated Project Duration:** 71.75 Days (adjusted, included modules only)
- **Total Estimated Price:** RM 22,697 *(within RM 25,000 cap)*
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, Apple/Google developer account fees, audio recording/licensing costs, or ongoing maintenance beyond the quoted scope.*

**Assumptions:**
- Client provides all BM Sukukata linguistic content (syllable lists, correct pronunciations, word lists, lesson sequencing).
- Audio assets (recordings of syllable sounds, songs) are provided by the client or recorded separately — this quote covers integration only, not studio recording.
- UI/UX design mockups are provided by the client or handled as a separate engagement.
- Target platforms: Android + iOS (using cross-platform framework, e.g., Flutter/React Native).

---

## B. Module Breakdown

### Included Modules

| Module Name | Priority | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost | Status |
| :--- | :---: | :--- | :---: | :---: | :---: | ---: | :---: |
| User Authentication & Profile | P1 | Medium (1.5×) | 3 | 2.25 | 0.75 | RM 1,613 | ✅ Included |
| Sukukata Sound Library & Audio Engine | P1 | Hard (2.0×) | 5 | 5 | 1.5 | RM 3,050 | ✅ Included |
| Animated Sukukata Formation | P2 | Hard (2.0×) | 2 | 6 | 1 | RM 2,300 | ✅ Included |
| Lesson Plan & Content Sequencing | P2 | Medium (1.5×) | 3 | 3 | 0.75 | RM 1,800 | ✅ Included |
| Word Bank & Flash Cards | P3 | Medium (1.5×) | 1.5 | 3 | 0.75 | RM 1,350 | ✅ Included |
| Interactive Learning Games | P3 | Hard (2.0×) | 3 | 7 | 1.5 | RM 2,950 | ✅ Included |
| Assessment & Progress Tracking | P3 | Medium (1.5×) | 3 | 2.25 | 0.75 | RM 1,613 | ✅ Included |
| Admin / Content Management Panel | P4 | Medium (1.5×) | 3 | 3 | 0.75 | RM 1,800 | ✅ Included |
| Push Notifications & Reminders | P5 | Simple (1.0×) | 1 | 0.75 | 0.25 | RM 538 | ✅ Included |
| Offline Mode & Data Sync | P5 | Hard (2.0×) | 4 | 2 | 1 | RM 1,900 | ✅ Included |
| | | | | | | | |
| **Totals (Included)** | | | **28.5** | **34.25** | **9** | **RM 18,914** | |
| **Grand Total (×1.20 buffer)** | | | | | | **RM 22,697** | |

> All 10 candidate modules fit within the RM 20,833 development budget. No modules deferred.
> Budget headroom remaining: RM 20,833 − RM 18,914 = **RM 1,919** (pre-buffer).

### Module Detail Notes

| # | Module | What's Included |
| :---: | :--- | :--- |
| 1 | **User Authentication & Profile** | Email/social login, child profile CRUD, avatar selection, parent/teacher role separation |
| 2 | **Sukukata Sound Library & Audio Engine** | Audio playback engine for all BM sukukata/syllable sounds, syllable-to-audio mapping, streaming + caching, playback controls |
| 3 | **Animated Sukukata Formation** | Stroke-by-stroke animation for writing each sukukata, touch-to-trace practice with feedback |
| 4 | **Lesson Plan & Content Sequencing** | Structured daily lesson plans, progressive difficulty sequencing, lesson completion tracking |
| 5 | **Word Bank & Flash Cards** | Vocabulary cards with image + audio + text, drill mode, categorization by lesson/topic |
| 6 | **Interactive Learning Games** | 3–4 mini-games (matching, drag-and-drop syllables, spelling builder, sound recognition) |
| 7 | **Assessment & Progress Tracking** | Quiz engine with multiple question types, scoring, progress dashboard for parents/teachers |
| 8 | **Admin / Content Management Panel** | Web-based CMS for managing syllables, audio, images, lessons, and game content |
| 9 | **Push Notifications & Reminders** | Daily learning reminders, streak notifications, configurable schedule |
| 10 | **Offline Mode & Data Sync** | Local content caching for offline use, background sync when connectivity returns |

---

## C. Resource Capacity Note

> *Reminder for internal planning:* Ensure frontend workload is balanced — the team operates with heavier backend capacity. Modules with heavy UI/UX requirements may become the schedule bottleneck.

> ⚠️ **Capacity Warning:** This project's frontend workload (34.25 days) exceeds backend (28.5 days). Given the team's ~3:1 BE-to-FE capacity ratio, frontend delivery is the likely bottleneck. Consider augmenting FE resources or phasing UI-heavy modules (Animated Formation, Interactive Games, and Sound Library are the heaviest FE modules at 6, 7, and 5 FE days respectively).

---

## D. Next Steps for Client

We invite Wincent to review and approve this quotation so that development planning can begin. All 10 modules fit within the RM 25,000 budget including contingency — no scope cuts are required at this stage. Upon approval, we will proceed with a detailed project kickoff covering content requirements, timeline, and milestone delivery schedule.

---

## E. Missing Technical Clarifications

The following information is required to convert this estimate into a fixed-price contract. Each item identifies the affected module(s) and potential cost impact.

1. **BM Sukukata Syllable Inventory & Taxonomy** *(Modules: Sound Library, Animation, Word Bank, Games)*
   - How many unique sukukata/syllables need to be supported? (Jolly Phonics covers 42 letter sounds; BM sukukata combinations could range from ~30 to 200+.)
   - **Cost impact:** If >100 unique syllables with individual audio + animation, Sound Library and Animation modules may each increase by RM 500–1,500 (more content integration work).

2. **Audio Asset Source** *(Modules: Sound Library, Lesson Plan)*
   - Will the client provide professionally recorded audio files, or does the team need to integrate a text-to-speech engine?
   - **Cost impact:** TTS integration would escalate Sound Library from Hard to Hard+ and add ~RM 1,000–2,000. Studio recording coordination is out of scope but would require PM overhead.

3. **Target Platforms & Minimum OS Versions** *(All Modules)*
   - Android only, iOS only, or both? Minimum Android API / iOS version?
   - **Cost impact:** Single-platform reduces FE effort by ~25%. Native (non-cross-platform) development would approximately double FE costs.

4. **Existing Brand / UI Design Assets** *(Modules: Animation, Games, Flash Cards)*
   - Are there existing character designs, illustrations, or a brand style guide? Or does the team need to create the visual identity?
   - **Cost impact:** Original illustration/character design is NOT included in this quote. If required, add RM 2,000–4,000 for design work (separate engagement).

5. **Songs / Music Content** *(Modules: Sound Library, Lesson Plan)*
   - Jolly Phonics includes songs for each letter sound. Will the BM Sukukata app include original songs?
   - **Cost impact:** Song integration is included; song creation/recording is NOT. If original compositions are needed, that is a separate creative engagement.

6. **Number and Type of Mini-Games** *(Module: Interactive Games)*
   - The estimate covers 3–4 mini-game types. How many distinct game mechanics are required?
   - **Cost impact:** Each additional game type beyond 4 adds approximately RM 500–750 (Hard complexity).

7. **User Roles & Multi-Tenancy** *(Modules: Auth, Admin, Assessment)*
   - Is this for individual parents/children only, or also for schools/classrooms with teacher accounts managing multiple students?
   - **Cost impact:** Multi-tenant school/classroom support would add RM 1,000–2,000 to Auth + Admin modules.

8. **Monetization Model** *(Modules: Auth, potentially new module)*
   - Free app, one-time purchase, freemium with in-app purchases, or subscription?
   - **Cost impact:** In-app purchase / subscription integration is NOT included. Would add a new Hard-tier module at RM 1,500–2,500.

9. **Analytics & Reporting Depth** *(Module: Assessment)*
   - Basic progress bars, or detailed reporting with exportable PDF reports for teachers/parents?
   - **Cost impact:** PDF report generation would add RM 500–800 to Assessment module.

10. **Content Update Frequency** *(Modules: Admin CMS, Offline Mode)*
    - How often will content be updated post-launch? Does the CMS need versioned content releases or simple CRUD?
    - **Cost impact:** Versioned content releases with rollback would add RM 500–1,000 to Admin + Offline modules.

---

### Derivation Summary

| Parameter | Value |
| :--- | ---: |
| Target Budget | RM 25,000 |
| ÷ 1.20 (strip 20% buffer) | RM 20,833 |
| Sum of included modules | RM 18,914 |
| × 1.20 (apply buffer) | RM 22,697 |
| Budget headroom | RM 2,303 |
| Budget utilization | 90.8% |
| Total adjusted BE days | 28.5 |
| Total adjusted FE days | 34.25 |
| Total adjusted PM/QA days | 9.0 |
| Total adjusted days | 71.75 |

---

*Generated by /pricing_skill (reverse) on 2026-04-08 | Constitution v1.1.0 | Rates: BE=RM300, FE=RM250, PM/QA=RM200 | Budget cap: RM 25,000*
