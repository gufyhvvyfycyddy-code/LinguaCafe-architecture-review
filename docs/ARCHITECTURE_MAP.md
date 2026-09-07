# Architecture Map — source baseline 190e7ab9

This map is a reviewer orientation aid. It does not replace current code and ADRs.

## 1. Repository shape

Single source repository:
- Laravel backend;
- Vue 2 / Vuex / Vuetify Web/PC;
- mobile shared source;
- Android native project;
- iOS native project.

Mobile clients call the central server. They do not own an independent Anki-style authoritative collection.

## 2. Formal learning data

### WordSense
Concrete learning meaning/content.

### ReviewCard
Scheduled object. New product work uses sense cards as the formal path.

### ReviewLog
Historical fact of a real rating. Reporting, preview and browsing must not fabricate it.

### WordSenseOccurrence
Evidence that a particular sense occurred in a source context.

### EncounteredWord
Reading/display/compatibility state. It is not the long-term formal scheduling authority.

## 3. Main product flows

### Reader

Current major orchestration surface:
- `resources/js/components/Text/TextBlockGroup.vue`
- current size: about 2,141 lines.

Review questions:
- rendering versus mutation ownership;
- lookup request ownership;
- selection/phrase behavior;
- semantic spaces;
- source occurrence binding;
- failure states.

Size alone is not a refactor mandate.

### Sense Review

- `resources/js/components/Senses/SenseReview.vue`
- current size: about 1,389 lines.

Review questions:
- Question → Answer → rating flow;
- formal rating endpoint;
- ReviewLog ownership;
- undo;
- lifecycle eligibility;
- keyboard/mobile navigation.

### Legacy Review

- `resources/js/components/Review/Review.vue`
- current size: about 1,025 lines.

Treat as compatibility surface until dependency/data audit proves retirement is safe.

### AI Study Card

- `resources/js/components/Text/AiStudyCardDesktopWorkflow.vue`
- current size: about 447 lines.

The project has already moved much of the AI-study workflow toward a bounded feature surface. External review should check whether actual writes still follow the formal WordSense/ReviewCard boundaries.

## 4. Backend high-impact services

### Dictionary import

- `app/Services/DictionaryImportService.php`
- current size: about 1,886 lines.

This is the largest current service in this quick hotspot sample.

Risk is not “too many lines” by itself. Risk comes from:
- multiple formats;
- replacement/rollback semantics;
- data validation;
- failure recovery;
- user/language isolation.

Any future import work should first check whether one responsibility can be isolated without creating a second truth source.

### TextBlock service

- `app/Services/TextBlockService.php`
- current size: about 1,077 lines.

Review as Reader/import compatibility boundary.

### Custom Study state

- `app/Services/CustomStudy/CustomStudySessionState.php`
- current size: about 1,176 lines.

Advanced product path, not a reason to expose Custom Study in the ordinary-user first-level UI.

## 5. Mobile

Directories:
- `mobile/src`
- `mobile/android`
- `mobile/ios`

Architecture invariants to verify:
- server remains authoritative;
- offline package is bounded;
- queued formal operations are idempotent;
- retry does not duplicate rating/ReviewLog;
- conflicts are explicit;
- restart preserves pending operations;
- device revocation removes local authority.

## 6. Cross-cutting high-risk boundaries

- authentication / user isolation;
- language isolation;
- WordSense mutation;
- ReviewCard mutation;
- ReviewLog writes;
- FSRS;
- Finish Reading settlement;
- import;
- sync;
- backup/restore;
- account deletion;
- secret/environment management.

## 7. Review method

Use this order:
1. current source SHA;
2. applicable ADR/module contract;
3. tests;
4. real caller/data flow;
5. current runtime evidence.

Do not turn every large file into a refactor project. Extract only where current evidence shows mixed ownership, duplicate truth, repeated bugs, or an untestable seam.
