# Letter Brief — first-session plan (v1 slice)

> Phase: **plan**. Skills: `brainstorming`, `writing-plans`, `spec`, `jobs-to-be-done`, `journey-map`, `user-flow-diagram`. Tool: plan mode. Repo: `~/Desktop/plainpaper-ios` only.
> Path classification (brainstorming skill): **architectural** — new project, no existing flow to change. Full process: JTBD → journey → flow → spec → plan.
> Build lock: `docs/CLAUDE_HANDOFF.md` (identical to `~/agent-tools/plainpaper/CLAUDE_HANDOFF.md`, verified with `cmp`). If anything below conflicts with it, the handoff wins.

## Context

Owner decided on 2026-10-01 to build "a scanner that explains a letter and lets you sign it" (section 2 item 1 of the 1 Oct study). Comparable scanner apps are crowded (guideline 4.3 risk medium), so the new thing App Review and users must see first is the **five-line brief**, not the crop tool. This session delivers the whole v1 sample flow on the simulator plus the listing and design docs, with proof (`xcodebuild` success line and `~/agent-tools/plainpaper/proof/brief.png`). No store, no TestFlight, no GitHub, no other app's folder.

### What exists today (verified 2026-10-01 13:16 Dubai)

| Item | State |
|---|---|
| `~/Desktop/plainpaper-ios` | `CLAUDE.md` (routing table), `docs/CLAUDE_HANDOFF.md`, `.claude/settings.local.json` (model fable). No Xcode project, no git repo. |
| `~/agent-tools/plainpaper/` | `CLAUDE_HANDOFF.md`, empty `proof/`, empty `promo/` |
| Xcode | 26.2 (17C52), `xcodegen` 2.44.1 at `/opt/homebrew/bin/xcodegen` |
| Simulators (via XcodeBuildMCP, `list_sims`) | **iPhone 16 Pro, iOS 18.5, id `36199439-2AB1-4E07-AF48-FF0BEBAD739A`** (the handoff's preferred device, present). Also iPhone 17 / iOS 26.2 and iPhone 15 Pro / iOS 17.5. |
| `xcrun simctl` from Bash | Blocked by the sandbox (CoreSimulatorService "Connection refused", log file "Operation not permitted"). XcodeBuildMCP works. Use it for boot/build/run/screenshot. |
| `higgsfield` CLI | Not on PATH (confirmed). The **Higgsfield MCP** (`claude_ai_Haggsfeild_ai`, `generate_image`) is connected in this session. |
| Mobbin MCP | Connected (`mcp__mobbin__search_screens`, `search_flows`, `search_sections`). |
| `research/2m-month-ideas-2026-10-01.md` | **Not found** under `~/agent-tools` or `~/Desktop` (depth 3). The handoff's summary of it is the only source; nothing in this plan depends on the file. |
| Plan-phase skills `jobs-to-be-done`, `journey-map`, `user-flow-diagram` | Not invocable by the Skill tool under those names. They live at `~/Developer/designer-skills/design-research/skills/{jobs-to-be-done,journey-map}/SKILL.md` and `~/Developer/designer-skills/prototyping-testing/skills/user-flow-diagram/SKILL.md`; read and applied directly. |
| `spec` skill | Resolves to the gstack `/spec`, whose terminal step files a **GitHub issue**. That step is skipped (hard rule: no GitHub). Its quality standards (verified state, acceptance criteria, file table, out-of-scope) are applied in this document instead. |

---

## 1. Jobs to be done

**Core job:** *When a paper lands on me (citation, notice, bill, form) and I don't understand it, I want to know in seconds what it is, what it wants, by when, how much, and what happens if I ignore it, so I can act or sign without reading the whole thing.*

| Dimension | Job | Outcome expectation | Design implication |
|---|---|---|---|
| Functional | Get the five facts out of the page, then sign and file it | Correct date and amount, never invented. "Not found" is acceptable; a wrong number is not. | Template extractor with evidence spans; every section is `found` or `notFound`, never a guess. |
| Emotional | Stop the dread of official mail | Relief in under 30 seconds. No wall of text, no chatbot. | One card, five rows, big date and amount, plain words. |
| Social | Look organized and in control (to a landlord, a court clerk, a partner) | A clean signed PDF, in Files, with a sensible name. | Export names the file `Letter Brief – <kind> – <date>.pdf`. |

**Job stages → screens:** locate (Home) → prepare (Camera/Import, Crop) → confirm (Brief card) → execute (Signature) → conclude (Export to Files).

**How people hire today:** general scanner apps (crop + OCR, no explanation), Notes/Camera, asking a friend, pasting the text into a chatbot (privacy cost). **Underserved:** the explanation step, and the privacy of keeping the page on the phone.

## 2. Journey map (one persona, one scenario)

Persona: US renter, 30s, got a city parking citation in the mail. Scenario: evening, kitchen table, phone in hand.

| Stage | Goal | Actions | Emotion (−2…+2) | Pain / moment of truth | Design response |
|---|---|---|---|---|---|
| 1 Open | Deal with this paper | Opens app from a search for "explain a letter" | −1 anxious | First screen must say what it does in one line | Home: "Scan a page. Get the five facts. Sign and save." Two buttons + "Try a sample citation". |
| 2 Capture | Get the page in | Points camera, auto-capture, or imports a photo | 0 | Blurry or skewed capture | VisionKit document camera (auto edge detection, perspective fix). Import goes through the crop screen. |
| 3 Crop | Make sure the whole page is in | Drags four corners, taps Use | 0 | Corners hard to hit | Big 44 pt handles, magnifier not needed in v1, "Use page" primary button. |
| 4 Brief | Understand it | Reads the card | **+2 (moment of truth)** | A wrong amount destroys trust; an empty card feels broken | Five fixed rows, "Not found on the page" when absent, evidence line under each found fact, no essay. |
| 5 Sign | Acknowledge / sign the form | Draws a signature, places it | +1 | Ugly signature, wrong spot | Signature sheet (name, draw, clear, one primary button, per the Fresha structure), then drag-to-place on the page. |
| 6 Export | File it | Saves PDF to Files | +1 | Where did it go? | `fileExporter` to Files with a readable default name, success toast. |
| 7 Second page | Do it again next month | Hits the paywall | −1 → 0 | Dark patterns break trust | Annual price largest, trial facts before the button, real close. |

Prioritized opportunities: (1) brief accuracy and honesty, (2) capture reliability, (3) paywall clarity.

## 3. User flow (screen level)

```
[Home] ──Scan──▶ [Document camera (VisionKit)] ──page captured──▶ [Crop]
  │  └──Import──▶ [PhotosPicker] ──photo chosen──▶ [Crop]
  └──Try sample──▶ (bundled fictional citation image) ──▶ [Crop]

[Crop] ──Use page──▶ ◇ gate: freeDocumentUsed && !entitled ?
                        ├─ yes ──▶ [Paywall]  ──close──▶ [Home]  (document discarded)
                        │                    ──purchase/restore ok──▶ continue ▼
                        └─ no  ──▶ [Processing: Vision OCR → BriefComposer]
                                       ├─ OCR < 20 chars or 0 lines ──▶ [Alert: "Couldn't read this page"] ──Retry──▶ [Crop]   (free doc NOT consumed)
                                       └─ ok ──▶ mark freeDocumentUsed (first time only) ──▶ [Brief card]
[Brief card] ──Sign──▶ [Signature sheet] ──Done──▶ [Place signature on page] ──Save PDF──▶ [Files exporter] ──saved──▶ [Brief card + toast]
[Brief card] ──Done──▶ [Home]
[Paywall] ──Restore──▶ AppStore.sync → currentEntitlements ──▶ entitled? continue : "Nothing to restore"
```

Rules encoded by the gate: one free *successful* explanation; a failed OCR never consumes it; the same document stays unlocked for signature and export in that session; the second document is gated **before** its explanation; close on the paywall is real and returns Home.

## 4. Spec

### 4.1 Product facts (copied from the lock)
- iOS 17.0+, SwiftUI, StoreKit 2, Swift 5 language mode, US-first, iPhone only (`TARGETED_DEVICE_FAMILY = 1`).
- Bundle id `com.shuhratjon.letterbrief`. Display name **Letter Brief**. Product name/scheme `LetterBrief`. Team `4MJ97BQM65` set in `project.yml`; simulator builds run with `CODE_SIGNING_ALLOWED=NO`.
- "Plainpaper" appears only in `docs/APP_STORE_LISTING.md`. Never in any identifier.
- Brief = exactly: What it is · What it asks · The date · The amount · What happens if you ignore it. Missing part → "Not found on the page".
- Forbidden words in code strings, docs, and the sample: fax, lawyer, legal advice, medical, treatment, notarized, certified, legally binding, any competitor name. Signature is "ink on your PDF".
- Privacy: Vision OCR on device; image never leaves the phone; no network code in v1 at all (no API key path is built this session — the local template is the v1 default and the only path).
- Build output: `-derivedDataPath ~/Library/Developer/LetterBriefDerivedData`.

### 4.2 Paywall facts (section 2 of the lock)
| Product id | Plan | Price (StoreKit config) | Intro offer | Weight |
|---|---|---|---|---|
| `com.shuhratjon.letterbrief.annual` | Annual | $49.99 / 1 year | 7-day free trial | Largest price on screen, preselected |
| `com.shuhratjon.letterbrief.weekly` | Weekly | $6.99 / 1 week | none | Smaller |
| `com.shuhratjon.letterbrief.monthly` | Monthly | $14.99 / 1 month | none | Smaller |

One subscription group "Letter Brief Pro". All prices on screen come from `Product.displayPrice`; trial length from `product.subscription?.introductoryOffer` (paymentMode `.freeTrial`, `period`). Selected-plan line above the button: annual → "7 days free, then $49.99/year"; weekly → "$6.99/week"; monthly → "$14.99/month". Button: annual → "Start 7-day free trial — $49.99/year after"; others → "Subscribe — $6.99/week". Under the button: auto-renew sentence, then Restore · Terms (Apple standard EULA URL) · Privacy (in-app sheet with the local-only privacy text; no hosted URL exists yet). Close (`xmark`) top trailing, always visible, dismisses. No toggles, no timers.

### 4.3 Architecture (units with one job each)

```
project.yml                              xcodegen spec → LetterBrief.xcodeproj (generated, not hand-edited)
LetterBrief/
  App/
    LetterBriefApp.swift                 @main; starts EntitlementStore.listenForTransactions()
    AppModel.swift                       @Observable: route state, current DocumentSession, gate decisions
    RootView.swift                       NavigationStack over the flow
  Features/
    Home/HomeView.swift                  Scan / Import / Try sample; menu with Restore + Privacy
    Capture/DocumentCameraView.swift     UIViewControllerRepresentable over VNDocumentCameraViewController
    Capture/PhotoImport.swift            PhotosPicker → UIImage
    Crop/CropView.swift                  4 draggable corners over the image, "Use page"
    Crop/PerspectiveCorrector.swift      CIPerspectiveCorrection → UIImage (pure function)
    Brief/BriefView.swift                The card: 5 rows + evidence + Sign / Done
    Brief/ProcessingView.swift           Progress while OCR runs
    Signature/SignatureSheet.swift       Name field, draw canvas, Clear, "Use signature"
    Signature/SignatureCanvas.swift      PencilKit-free Path drawing (DragGesture → Path), renders UIImage
    Signature/PlaceSignatureView.swift   Drag/scale signature over the page, "Save PDF"
    Export/PDFBuilder.swift              UIGraphicsPDFRenderer: page image + signature → Data (pure)
    Export/PDFDocument.swift             FileDocument for .fileExporter
    Paywall/PaywallView.swift            3 plan cards, selected-plan line, button, legal row, close
    Paywall/PlanCopy.swift               Pure formatter: (displayPrice, period, trial) → strings (tested)
    Paywall/PrivacySheet.swift           Local-only privacy text
  Services/
    OCR/OCRService.swift                 Vision VNRecognizeTextRequest (.accurate, en-US) → [OCRLine]
    Brief/BriefComposer.swift            [OCRLine] → Brief (5 BriefSection values); pure, no UIKit
    Brief/Extractors/DocumentKindExtractor.swift   "What it is"
    Brief/Extractors/AskExtractor.swift            "What it asks"
    Brief/Extractors/DateExtractor.swift           NSDataDetector + cue words
    Brief/Extractors/AmountExtractor.swift         currency regex + cue words
    Brief/Extractors/ConsequenceExtractor.swift    "if unpaid / failure to / may result …"
    Store/EntitlementStore.swift         StoreKit 2: products, purchase, restore, currentEntitlements, updates
    Gate/FreeDocumentGate.swift          Protocol-backed flag store; Keychain impl + in-memory impl for tests
    Sample/SampleCitation.swift          SwiftUI view of a fictional citation → ImageRenderer → UIImage
  Resources/
    Assets.xcassets                      AccentColor, AppIcon placeholder slot (icon art deferred)
    PrivacyInfo.xcprivacy                tracking=false, no collected data, no required-reason APIs beyond none used
    LetterBrief.storekit                 3 products above
    Localizable.xcstrings                en only in v1 (strings live here so forbidden-word scan is one file)
LetterBriefTests/                        Swift Testing
docs/
  APP_STORE_LISTING.md                  ASO phase output
  DESIGN-MOBBIN.md                      Design phase output (real mobbin_url links)
  superpowers/specs/2026-10-01-letter-brief-v1-design.md   this spec, copied in
  superpowers/plans/2026-10-01-letter-brief-v1.md          this plan, copied in
```

Decisions made here (flag to owner, override by saying so):
1. **Camera = VisionKit `VNDocumentCameraViewController`.** Full-bleed, auto edge detection, perspective-corrected output, zero custom AVFoundation. Its output still passes through our Crop screen with corners defaulted to the full page so the user sees one consistent "obvious crop" step. A custom AVFoundation camera is more work and more review risk for no v1 gain.
2. **Free-document flag in Keychain**, not UserDefaults, so a reinstall does not reset the free document. Entitlement truth is `Transaction.currentEntitlements`.
3. **Gate before OCR for the second document.** Cheaper and matches "before its explanation".
4. **PDF = the signed page only** (one page). The brief stays in the app. Keeps v1 small.
5. **Privacy link opens an in-app sheet**, Terms opens Apple's standard EULA. No hosted privacy URL exists; nothing fake is linked.
6. **Local `git init` with no remote.** Needed for commits and worktrees. Not a GitHub repo.
7. **Sample page**: fictional "City of Fairhollow" parking citation, rendered from a SwiftUI view at launch (no binary asset), run through the real Vision OCR so the proof screenshot exercises the real pipeline. Sample facts: Notice No. PC-2026-04417, issued Sep 22 2026, amount due $65.00, pay by Oct 22 2026, "If unpaid by Oct 22, 2026 the amount increases to $130.00 and a hold may be placed on vehicle registration renewal." (Confirm "Fairhollow" matches no real US municipality before shipping; swap if it does.)
8. **App icon art is deferred.** Not required for the simulator proof. The screenshot phase this session covers `brief.png` only.
9. **Promo stills via the Higgsfield MCP**, since "Higgsfield inside Claude" is connected and the CLI is not. Runs only after the proof exists, capped at 3 stills, stops immediately if the MCP reports unauthenticated or no credits. It spends Higgsfield credits.

### 4.4 Acceptance criteria (pass/fail)
1. `xcodebuild build` for `platform=iOS Simulator,name=iPhone 16 Pro,OS=18.5` ends with `** BUILD SUCCEEDED **`; command and line pasted in the final report and in `~/agent-tools/plainpaper/proof/BUILD.txt`.
2. `xcodebuild test` on the same destination: all Swift Testing tests pass (count reported).
3. Launching the app with argument `--sample-brief` shows the brief card for the fictional citation with: What it is = "A parking citation from the City of Fairhollow", The date = "October 22, 2026", The amount = "$65.00", consequence row non-empty, ask row non-empty. Screenshot at `~/agent-tools/plainpaper/proof/brief.png`, light mode.
4. Second document (after the sample) on a fresh install shows the paywall before any OCR; close returns Home; the brief is never shown.
5. Paywall shows three prices from StoreKit; annual price is the largest type size; "7 days free, then $49.99/year" is visible above the button in the simulator with the local StoreKit config; weekly/monthly show no trial text.
6. Paywall and brief render without clipping the price or the close button at `dynamicTypeSize .accessibility3` (SwiftUI preview snapshot checked by eye, noted in the report).
7. `grep -riE "fax|lawyer|legal advice|medical|notariz|certified|binding|plainpaper" LetterBrief/ project.yml docs/DESIGN-MOBBIN.md` returns nothing (Plainpaper is allowed only in `docs/APP_STORE_LISTING.md`).
8. No `URLSession`, `URLRequest`, or network entitlement in `LetterBrief/`. No `.env`, no key string.
9. `docs/DESIGN-MOBBIN.md` holds ≥ 3 real `mobbin.com` links from this session's MCP calls plus the Fresha signature reference.
10. `docs/APP_STORE_LISTING.md`: title ≤ 30 chars, subtitle ≤ 30 and no word shared with title, keyword field ≤ 100 chars with no spaces and no word from title or subtitle, no "fax", no competitor name, no price.
11. Nothing on the Desktop outside `~/Desktop/plainpaper-ios` is modified; no App Store Connect, TestFlight, GitHub, `asc-*`, RevenueCat.

### 4.5 Out of scope (this session)
Server explanation path and any API key; fax; iPad; multi-page documents; brief inside the PDF; app icon art; App Store screenshots beyond `brief.png`; localization beyond en; release prep / submission; Apple Search Ads test; account/sync of any kind.

### 4.6 Risks
- Vision OCR on the simulator is slower than device but works; the rendered sample is high-contrast so accuracy is high. If OCR returns garbage for the sample, the composer tests still pass on fixture text and the report says so.
- `VNDocumentCameraViewController` is unavailable on the simulator; the Scan button shows "Camera needs a real iPhone" there. Import and Sample paths cover the simulator.
- StoreKit local config in the simulator requires the scheme's `storeKitConfiguration`; xcodegen supports it under `schemes.LetterBrief.run.storeKitConfiguration` (same pattern as the sibling project's `project.yml`).
- Writing to `~/agent-tools/plainpaper/proof/` from sandboxed Bash is denied (write allow-list is cwd + `$TMPDIR`). The screenshot is taken with XcodeBuildMCP `screenshot` and copied with one explicitly approved unsandboxed `cp`, or written with the Write/Read tools. The report states which.

---

## 5. Implementation plan

Executed after owner acceptance, task by task, TDD where there is logic, commit after each task. Every phase below starts by stating phase + skills + tool + repo (CLAUDE.md rule), and loading those skills.

### Phase A — setup (build phase skills: `swiftui-pro`, `swift-concurrency`, `ios-swiftui`, `swiftui-expert-skill`, `xcode-build-system`; tool `xcodebuild`)
- A1 `git init` in `~/Desktop/plainpaper-ios`, `.gitignore` (DerivedData, `*.xcodeproj` is **committed** since xcodegen output is deterministic? No: commit `project.yml`, ignore `LetterBrief.xcodeproj`, regenerate on checkout). Commit `CLAUDE.md`, `docs/`.
- A2 Create task-observer files under `~/.claude/projects/-Users-shuhratjon-Desktop-plainpaper-ios/skill-observations/` and log the three observations found during planning (skill names not invocable; `spec` → GitHub conflict; simctl sandboxed, XcodeBuildMCP works).
- A3 Copy this spec/plan into `docs/superpowers/specs/` and `docs/superpowers/plans/`.
- A4 `project.yml` (name LetterBrief, bundle id, display name, iOS 17.0, team, `storeKitConfiguration: LetterBrief/Resources/LetterBrief.storekit`, test target, Info.plist keys: `NSCameraUsageDescription` "Letter Brief uses the camera to scan a page you choose. The image stays on your iPhone.", `NSPhotoLibraryUsageDescription` "Letter Brief opens a photo you choose so it can read the page. The image stays on your iPhone.", `UISupportedInterfaceOrientations` portrait, `ITSAppUsesNonExemptEncryption` false). Empty `LetterBriefApp` + `RootView` "Letter Brief". `xcodegen generate`, then the simulator build command. **Checkpoint: BUILD SUCCEEDED on an empty app.**

### Phase B — design (skills: `swiftui-pro`, `swiftui-expert-skill`, `ios-swiftui`, `hig`, `swiftui-liquid-glass`, `impeccable`, `ios-micro-interactions`, `ios-design-review`, `design-review`, `platform-conventions`, `camera-first-apps`, `visual-hierarchy`, `color-system`, `typography-scale`; tool Mobbin MCP)
- B1 Three `mcp__mobbin__search_screens` / `search_flows` calls (iOS only): document scanner camera + crop corners + page review; sign a PDF / signature pad then export; subscription paywall with one annual plan dominant and price visible before the button. Look at the returned images. Write chosen `mobbin_url`s with one line each on what is borrowed (structure only) into `docs/DESIGN-MOBBIN.md`, plus the Fresha signature link already confirmed.
- B2 Design tokens in code: `Theme.swift` (accent, paper surface, ink text, success, warning; light + dark via asset catalog colors), type scale (largeTitle for amount/date, title3 row labels, body text), 44 pt minimum targets, Dynamic Type everywhere, no fixed heights on text rows.

### Phase C — core logic, TDD (build phase skills + test phase skills: `test-driven-development`, `swift-testing-expert`, `swift-testing-framework`)
Each task: write failing test → run (`xcodebuild test … -only-testing:LetterBriefTests/<Suite>`) → implement → pass → commit.
- C1 `Brief` / `BriefSection` models (`enum BriefSection { case found(text: String, evidence: String?), notFound }`; `Brief` has `whatItIs, whatItAsks, date, amount, consequence`, `displayText` returns "Not found on the page" for `.notFound`).
- C2 `AmountExtractor`: tests — "$65.00" found; "Total due $1,250.00 … late fee $25" prefers the amount nearest "due"/"total"; no currency → `.notFound`; "$" with no digits ignored.
- C3 `DateExtractor`: tests — "Pay by October 22, 2026" → that date with cue "Pay by"; "Issued 09/22/2026 … due 10/22/2026" prefers the due date; no date → `.notFound`; returns formatted "October 22, 2026".
- C4 `ConsequenceExtractor`: tests — "If unpaid by … the amount increases to $130.00" found; "failure to respond may result in …" found; plain thank-you letter → `.notFound`.
- C5 `AskExtractor`: tests — "You must pay the amount due by …" found; "Please return the enclosed form" found; page with no imperative → `.notFound`; result trimmed to ≤ 160 chars ending at a sentence boundary.
- C6 `DocumentKindExtractor`: tests — "PARKING CITATION … City of Fairhollow" → "A parking citation from the City of Fairhollow"; "INVOICE" → "A bill from <sender>"; "NOTICE" → "A notice from <sender>"; unknown → "A letter" (+ "from <sender>" when a sender line is found), never `.notFound` for this row unless OCR is empty.
- C7 `BriefComposer.compose(lines:)` integration test on the full fictional citation text fixture → all five rows found with the expected values; empty input → every row `.notFound`.
- C8 `FreeDocumentGate`: protocol `FreeDocumentFlagStore { var used: Bool }`, `InMemoryFlagStore`, `KeychainFlagStore` (service `com.shuhratjon.letterbrief.gate`). Tests on the in-memory store: first document allowed; after `markUsed()` second is blocked when not entitled; entitled bypasses; `markUsed()` idempotent.
- C9 `PlanCopy`: tests — annual with 7-day trial → selected line "7 days free, then $49.99/year", button "Start 7-day free trial — $49.99/year after"; weekly no trial → "$6.99/week", button "Subscribe — $6.99/week"; monthly → "$14.99/month". Input is a small struct `(displayPrice: String, unit: Product.SubscriptionPeriod.Unit, trialDays: Int?)` so no StoreKit mocking is needed.
- C10 `PDFBuilder.build(page: UIImage, signature: UIImage?, signatureRect: CGRect?) -> Data`: test that the output starts with `%PDF` and `PDFDocument(data:)` has exactly 1 page.

### Phase D — UI flow (build phase skills)
- D1 `AppModel` + `RootView` routing per the flow diagram; `DocumentSession { image, croppedImage, brief, signature, unlocked }`.
- D2 `HomeView` (three actions, menu with Restore and Privacy). Launch argument `--sample-brief` routes straight to Crop with the sample image and auto-confirms, for the proof screenshot.
- D3 `SampleCitation` view + `ImageRenderer` at scale 3 → UIImage.
- D4 `DocumentCameraView` (VisionKit) with simulator fallback alert; `PhotoImport` with `PhotosPicker`.
- D5 `CropView` + `PerspectiveCorrector` (CIPerspectiveCorrection, orientation-normalized input).
- D6 `OCRService` (async, `VNRecognizeTextRequest`, `.accurate`, `en-US`, lines sorted top→bottom by boundingBox) + `ProcessingView`.
- D7 `BriefView` card: five rows, evidence in secondary text, "Sign" and "Done", honest footer "A summary of the words on this page. Check the original before you act." (no legal wording).
- D8 `SignatureSheet` + `SignatureCanvas` + `PlaceSignatureView` (drag + pinch, default bottom-trailing) → `PDFBuilder` → `.fileExporter` with `PDFDocument`, default name `Letter Brief – <kind> – <yyyy-MM-dd>.pdf`, success toast.
- D9 Gate wiring: `AppModel.proceedFromCrop()` checks `FreeDocumentGate` + `EntitlementStore.isEntitled`; failed OCR alert with Retry does not call `markUsed()`; `markUsed()` is called exactly when the brief first appears.

### Phase E — paywall (skills: `storekit2-subscriptions`, `storekit`, `ios-paywall-design-specific`, `paywall-optimization`, `subscription-economics`, `paywalls`, `pricing`; tool StoreKit 2 local config)
- E1 `LetterBrief.storekit` with the three products in one group, annual intro offer free trial 1 week.
- E2 `EntitlementStore` (@Observable): `loadProducts()`, `purchase(_:)`, `restore()`, `isEntitled` from `Transaction.currentEntitlements`, `listenForTransactions()` task started at launch, `checkVerified`.
- E3 `PaywallView`: three `PlanCard`s (annual preselected, largest price), selected-plan line, button, auto-renew sentence, Restore · Terms · Privacy, close `xmark` always visible. Dynamic Type previews at `.accessibility3`, light and dark previews.
- E4 Manual check in the simulator: purchase annual via the StoreKit test environment → brief unlocks; "Restore" with nothing purchased → "Nothing to restore" message; close → Home.

### Phase F — privacy and copy audit (skills: `mobile-security-privacy` agent not required; use `verification-before-completion`)
- F1 `PrivacyInfo.xcprivacy` (tracking false, no data collected, no tracking domains, required-reason APIs: none, since Keychain and `fileExporter` need none; add `NSPrivacyAccessedAPICategoryUserDefaults` only if UserDefaults ends up used).
- F2 Forbidden-word grep (criterion 7) and network grep (criterion 8).

### Phase G — ASO / listing (skills: `aso-app-store-optimization-deep`, `metadata-optimization`, `app-store-keyword-research`, `aso-audit`, `app-store-description-copywriting`, `aso`; local file only)
- G1 Write `docs/APP_STORE_LISTING.md`: title (Plainpaper, 10 chars, flagged "working title, not cleared"), subtitle, 100-char keyword field with the no-repeat rule checked by a small script in the doc, description opening with "Scan a document. Sign a PDF. Explain a letter in plain English: what it is, what it asks, the date, the amount, and what happens if you ignore it." then what the brief contains, privacy line, subscription line without prices. Start from the handoff's draft and beat it; record character counts.

### Phase H — test and proof (skills: `verification-before-completion`, `test-driven-development`, `swift-testing-expert`, `swift-testing-framework`, `xcuitest-ui-testing`, `ios-testing`, `systematic-debugging`, `ios-qa`, `mobilebuildmcp-cli`; tool XcodeBuildMCP). Screenshot phase skills `app-store-screenshots-design`, `screenshot-optimization`, `applekit-simulator-utils` for the capture.
- H1 Full `xcodebuild build` and `xcodebuild test` on iPhone 16 Pro / iOS 18.5 with the derived data path above; paste the success lines.
- H2 XcodeBuildMCP: `boot_sim` 36199439-…, `build_run_sim` with launch arg `--sample-brief`, wait for the brief, `screenshot` → `~/agent-tools/plainpaper/proof/brief.png`; write `BUILD.txt` with the exact destination, command, and success line.
- H3 Light mode only is required; capture dark as a bonus if quick.

### Phase I — promo stills (skills: `higgsfield`, `higgsfield-product-photoshoot`; tool Higgsfield MCP). After H only.
- I1 Read both skill files. Check `balance`/auth via the MCP. If unauthenticated or no credits → stop, report "promo blocked", build intact.
- I2 Otherwise generate ≤ 3 original stills of our own brief card and camera screens (device mockup in a lifestyle scene; our UI only; no other app's frames or icons). Save under `~/agent-tools/plainpaper/promo/` (same write-path note as the proof).

### Not this session
Release prep phase (no submit), app icon art, App Store screenshot set.

## 6. Verification (end to end)
1. `xcodegen generate && xcodebuild build -project LetterBrief.xcodeproj -scheme LetterBrief -destination 'platform=iOS Simulator,name=iPhone 16 Pro,OS=18.5' -derivedDataPath ~/Library/Developer/LetterBriefDerivedData CODE_SIGNING_ALLOWED=NO` → `** BUILD SUCCEEDED **`.
2. Same with `test` → all tests pass.
3. Sample flow in the simulator → `proof/brief.png` shows the five rows with the expected values.
4. Second document → paywall; prices from StoreKit; close works; restore message works.
5. Greps for forbidden words, network, and "Plainpaper" placement.
6. Report: commands, success lines, test count, screenshot path, Mobbin links count, listing character counts, promo status, and the list of decisions 1–9 for the owner to confirm or reverse.
