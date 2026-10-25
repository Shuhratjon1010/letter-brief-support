# CLAUDE_HANDOFF.md — letter-brief iOS app

**Owner:** Shuhrat Soliev. **Written:** 2026-10-01, Dubai (UTC+4).
**Paste this whole file into a Claude Code Project (beta) for this app.** Not a one-off chat. Not a second product.

This file is the build lock. If a later message conflicts with it, stop and say so.

---

## 0. How to open the session

1. Create a **Claude Code Project (beta)** whose only job is this app. Do not reuse a chat, and do not work inside another app's folder (WorthSnap, Tallymile, Bidframe, Evenpace, HandCut, Scribewell, or anything else on the Desktop).
2. Model: the **strongest model** Project beta offers. Effort: **high**. On this Mac, Claude Code settings at 10:13 Dubai on 2026-10-01 were model `fable` and effort `high`. Do not switch to a smaller model or a lower effort.
3. **Plan mode before any large change.** First reply is a plan. Wait for the owner to accept it, then implement only the accepted slice.
4. The weekly Claude Code limit was expected to lift around **1:00 PM Dubai on 2026-10-01**. A non-spending check at **10:12 AM Dubai** showed `claude` **2.1.282 (Claude Code)** at `/Users/shuhratjon/.npm-global/bin/claude`. The quota was **not** opened. If the session is still refused, stop. Do not start a second session to "see if it works."
5. **Name the phase and its skill before doing that phase.** The map is section 8. If the phase changes and the skill for the new phase is not named, stop and name it before continuing.

---

## 1. What this is

US-first iOS app. SwiftUI. StoreKit 2. iOS 17+.

**Working title: Plainpaper.** Trademark and App Store name clearance are **UNKNOWN**. The 1 Oct 2026 study (`research/2m-month-ideas-2026-10-01.md`, section 2 item 1, and section 4) says not to put that name in a binary until it is checked.

- Allowed: the word Plainpaper in `docs/APP_STORE_LISTING.md` only (listing draft).
- Forbidden: Plainpaper inside the bundle id, an app group, a URL scheme, a keychain access group, a product identifier, or any reverse-DNS string.
- On-device display name until clearance is recorded: **Letter Brief**. Do not rename the binary to Plainpaper unless the owner writes that clearance is done.

**Bundle id (use this, do not invent another):** `com.shuhratjon.letterbrief`

Availability: **UNKNOWN**. App Store Connect was not queried. This project must not open App Store Connect to "check." `com.soliev.letterbrief` was the first candidate and was **not** adopted, because uniqueness could not be confirmed.

Apple team: the sibling apps on this Mac record team `4MJ97BQM65`. Use the team already signed in on this Mac. Do not create an App Store Connect app record.

**Product, v1 only.** Camera or import, then on-device crop and OCR, then a short plain-English brief, then a signature, then export a PDF to Files.

The brief has exactly these parts, in this order, and no extra essay:

1. What it is
2. What it asks
3. The date
4. The amount
5. What happens if you ignore it

If a part is not on the page, say **Not found on the page**. Do not invent a date, an amount, or a consequence.

**Out of v1, and out of the copy:** fax, a fax number, "free fax," legal advice, the word "lawyer," medical advice, treatment suggestions, "we read your medical record," another app's name, another app's icon, another app's sample document. Guideline 1.4.1 (medical) and 4.3 (crowded scanner category) are the review risks. The new thing App Review should see is the explanation card, not another crop tool.

A signature here is ink on a PDF the user exports. Do not call it legally binding, notarized, or certified.

---

## 2. Paywall (StoreKit 2, guideline 3.1.2)

One free document. The first **successful** explanation is free, including signature and PDF export of that same document. A failed scan does not use up the free document. The next document hits a **hard paywall** before its explanation. No account. No "skip" that still explains the second page.

Prices, implemented as StoreKit products, read back with `displayPrice` and `introductoryOffer`. Never hard-code the charged price on the button. Local StoreKit configuration file carries:

| Plan | Price | Trial | Visual weight |
|---|---|---|---|
| Annual | $49.99 | **7 days, this plan only** | Largest price on the screen |
| Weekly | $6.99 | none | Smaller |
| Monthly | $14.99 | none | Smaller |

Before the purchase button, the selected plan shows the billed price and, for annual only, the trial length. The annual button may not say only "Start free trial." It has to be readable as **$49.99/year after 7 days** (wording can be tighter, the facts cannot move). Weekly and monthly buttons show their price and period and do not mention a trial.

Close button is real and dismisses the paywall. No fake close, no timer that hides it, no free-trial toggle. Restore, Terms (EULA), and Privacy are on the paywall.

No "free fax." No fax in v1 at all. Do not copy a darker weekly-trial pattern from scanner ads.

The 1 Oct study's $500 Apple Search Ads test is **not** this session. Do not buy ads. Do not change the prices above to match a competitor.

---

## 3. Privacy

On-device OCR by default: Apple Vision. Crop stays on device.

Do not upload the document image. Ever, in v1.

A server call is allowed only if the user explicitly asks for the explanation **and** an API key already exists outside the app. The payload is the extracted text only, never the image. If no key exists, use a **local template** over the Vision text (dates, amounts, due language). That is the v1 default. Ship that path first.

Do **not** embed an Anthropic key, or any other model key, in the app, the repo, a plist, a screenshot, or this chat. No `.env` committed. No training on user papers.

`PrivacyInfo.xcprivacy`, the camera string, the photo-library string, and the App Privacy answers must match a local-only v1: camera and photos to scan a page the user picked, files export, no tracking, no document image leaving the phone.

---

## 4. Design bar

Mobbin quality or it does not ship. The Mobbin MCP is already connected in Claude Code (server name `mobbin`). Before drawing, call it and **look at the images**. Pull real references in three searches, iOS only:

- document scanner camera, crop corners, page review
- sign a PDF / signature pad, then export
- subscription paywall with one annual plan visually dominant and the price visible before the button

Write the chosen `mobbin_url` links into `docs/DESIGN-MOBBIN.md`. One layout reference already confirmed, signature sheet only, not a brand to copy: Fresha "Add a signature" (`https://mobbin.com/screens/d6becd9c-f79e-4e33-8fa9-0f4921b1777b`). Use it for structure (name, draw, clear, one primary button). Do not copy Fresha's colors, type, or legal paragraph.

Ship only screens that would sit next to those references: full-bleed camera, obvious crop, a short brief card (not a chat transcript), a signature sheet, a paywall with the annual price largest. Light and dark. Dynamic Type does not clip the price or the close button.

Original fictional sample only. A made-up city parking citation with a date and an amount is enough. Not a real person's letter. Not an explanation of benefits. Not a medical bill.

---

## 5. ASO is part of v1

Write `docs/APP_STORE_LISTING.md` in the first session. Local file only. Do not upload it. Do not open App Store Connect.

- **Title** (30 characters). Working title Plainpaper is allowed **here only**.
- **Subtitle** (30). Must not repeat title words.
- **Keyword field**, 100 characters, comma-separated, no spaces. Do not repeat any word already in the title or the subtitle. No competitor names. No "fax" (the app does not fax; that would be a misleading metadata claim).
- **Description** leads with the words people type: scan document, sign pdf, explain a letter. First sentences say what the brief contains. No lawyer. No medical claim. No free fax. No prices in the title, subtitle, or screenshots (guideline 2.3.7).

Draft to beat, not to paste blindly (re-run the ASO skills; the keyword line is 98 characters and repeats nothing in the title "Plainpaper" or the subtitle below):

- Title: `Plainpaper`
- Subtitle: `Explain a letter. Sign PDF.`
- Keywords: `scan,document,scanner,camera,ocr,form,bill,notice,citation,signature,files,export,pages,mail,paper`
- Description opener: `Scan a document. Sign a PDF. Explain a letter in plain English: what it is, what it asks, the date, the amount, and what happens if you ignore it.`

---

## 6. Promo stills (Higgsfield)

After the app's own UI exists, generate **original** promo stills of that UI. Not frames copied from iScanner, CamScanner, FAX from iPhone, or Scanner App. Not their icons, not their sample pages.

Use the Higgsfield skills already on this Mac: `higgsfield` and, for stills, `higgsfield-product-photoshoot` (under `~/.claude/skills/higgsfield-official`). Read the skill files before prompting. Do not invent model names.

At 10:13 Dubai on 2026-10-01 the `higgsfield` CLI was **not** on `PATH`. Do not pipe a remote install script. Do not paste an API key into the app or the chat. If the CLI is missing or logged out, stop the promo step, say so, and leave the app build intact.

Save stills under `~/agent-tools/plainpaper/promo/`. They are marketing images of our screens, not a substitute for the App Store screenshot set in `proof/`.

---

## 7. First session — done means all of this

Create `~/Desktop/plainpaper-ios`. Nothing else on the Desktop gets edited.

Inside it:

- An Xcode project (xcodegen from `project.yml` is fine) that **builds for the simulator**.
- Bundle id `com.shuhratjon.letterbrief`. Display name Letter Brief.
- One sample flow: import or camera, crop, on-device brief of the fictional citation, signature, export PDF toward Files.
- `CLAUDE.md` copied from section 8 of this handoff.
- `docs/DESIGN-MOBBIN.md` with real Mobbin links from this session.
- `docs/APP_STORE_LISTING.md` as in section 5.
- A StoreKit configuration with the three products in section 2. Prices on screen come from StoreKit.
- Local template explanation. No API key.
- Build output **not** on the Desktop. `-derivedDataPath` under `~/Library` or `/tmp`.

Proof, required before saying done:

- `xcodebuild build` for an installed iPhone simulator (iPhone 16 Pro if present, otherwise the newest iPhone simulator that is installed). Paste the command and the success line.
- One screenshot of the sample brief, saved at `~/agent-tools/plainpaper/proof/brief.png`. Light mode is enough for this session. If the simulator name differed, write the exact destination into `~/agent-tools/plainpaper/proof/BUILD.txt`.

Do not submit to the App Store. Do not archive for TestFlight. Do not touch App Store Connect. Do not create or push a GitHub repo. Do not open another app's project. Do not run `asc`, fastlane deliver, or any submit script.

Promo stills (section 6) are v1, but they are not allowed to block this proof. If Higgsfield is not authenticated, ship the proof and report promo as blocked.

---

## 8. CLAUDE.md routing table

Write the following into `~/Desktop/plainpaper-ios/CLAUDE.md` unchanged, then follow it. Every skill name below was found on this Mac on 2026-10-01 (`~/.claude/skills`, `~/.claude/plugins`, `~/Developer/ios-skills`, and the skill tables in `~/Desktop/worthsnap-ios/CLAUDE.md` and `~/smart-kids-ai/CLAUDE.md`). Do not invent a skill name. Invoke with the Skill tool by these exact names.

**Standing line:** If Claude changes phase without naming the skill, stop and name it before continuing.

Owner rule (2026-09-27, restated 2026-10-01): the project `CLAUDE.md` lists which skills and tools Claude must use at each build step. State the phase, the skill names, the tool, and the repo at the start of the task, then load that row before writing code. One repo for the app: `~/Desktop/plainpaper-ios`. Do not work inside another app's folder.

| Phase | Skill | Tool | Repo |
|---|---|---|---|
| plan | `brainstorming`, `writing-plans`, `spec`, `jobs-to-be-done`, `journey-map`, `user-flow-diagram` | Plan mode. No code until the owner accepts the plan. | `~/Desktop/plainpaper-ios` only. Not WorthSnap, Evenpace, Tallymile, Bidframe, HandCut, Scribewell, or smart-kids-ai. |
| design | `swiftui-pro`, `swiftui-expert-skill`, `ios-swiftui`, `hig`, `swiftui-liquid-glass`, `impeccable`, `ios-micro-interactions`, `ios-design-review`, `design-review`, `platform-conventions`, `camera-first-apps`, `visual-hierarchy`, `color-system`, `typography-scale` | Mobbin MCP, server name `mobbin`. Call it and look at the images before drawing. | `~/Desktop/plainpaper-ios`. Write links in `docs/DESIGN-MOBBIN.md`. |
| build | `swiftui-pro`, `swift-concurrency`, `ios-swiftui`, `swiftui-expert-skill`, `xcode-build-system` | `xcodebuild`. `-derivedDataPath` under `~/Library` or `/tmp`, never the Desktop. | `~/Desktop/plainpaper-ios` |
| paywall | `storekit2-subscriptions`, `storekit`, `ios-paywall-design-specific`, `paywall-optimization`, `subscription-economics`, `paywalls`, `pricing` | StoreKit 2, local configuration file. Prices from `displayPrice` and `introductoryOffer`. | `~/Desktop/plainpaper-ios` |
| ASO / listing | `aso-app-store-optimization-deep`, `metadata-optimization`, `app-store-keyword-research`, `aso-audit`, `app-store-description-copywriting`, `aso` | None. Local markdown only. | `~/Desktop/plainpaper-ios/docs/APP_STORE_LISTING.md` |
| screenshots | `app-store-screenshots-design`, `screenshot-optimization`, `applekit-simulator-utils`, `ios-app-icon-design`, `app-icon-optimization` | Installed iPhone simulator (iPhone 16 Pro if present). | App in `~/Desktop/plainpaper-ios`. Proof in `~/agent-tools/plainpaper/proof/`. |
| promo images | `higgsfield`, `higgsfield-product-photoshoot` | Higgsfield inside Claude. At 10:13 Dubai on 2026-10-01 the `higgsfield` CLI was not on `PATH`. Do not pipe a remote install script. If it is missing or logged out, stop this phase and leave the build intact. | `~/agent-tools/plainpaper/promo/` |
| test | `verification-before-completion`, `test-driven-development`, `swift-testing-expert`, `swift-testing-framework`, `xcuitest-ui-testing`, `ios-testing`, `systematic-debugging`, `ios-qa`, `mobilebuildmcp-cli` | XcodeBuildMCP, for the simulator test. | `~/Desktop/plainpaper-ios` |
| release prep | `app-store-preflight`, `app-store-review`, `release-review`, `app-rejection-recovery`, `xcode-build-system`, `finishing-a-development-branch` | None. Do not submit. | `~/Desktop/plainpaper-ios`. Do not create or push a GitHub repo. |

`asc-cli-usage`, `asc-metadata-sync`, `asc-release-flow`, `asc-shots-pipeline`, `asc-testflight-orchestration`, and `asc-xcode-build` are on this Mac. They are **not** in the table. Do not call them. Do not open App Store Connect. Do not archive for TestFlight. `revenuecat-paywall` and `integrate-revenuecat` are also on this Mac. This app uses StoreKit 2, not RevenueCat. Do not invoke them.

Where the names live: `swiftui-pro`, `swift-concurrency`, `swift-testing-expert`, `app-store-preflight`, `app-store-review`, and `mobilebuildmcp-cli` are symlinked from `~/Developer/ios-skills/skills/` into `~/.claude/skills/`. `paywalls`, `pricing`, and `aso` are symlinked from `~/Developer/marketingskills` (github.com/coreyhaines31/marketingskills). `platform-conventions` is symlinked from `~/Developer/designer-skills` (github.com/Owl-Listener/designer-skills). `brainstorming`, `writing-plans`, `verification-before-completion`, `test-driven-development`, `systematic-debugging`, and `finishing-a-development-branch` are the superpowers plugin skills. `higgsfield-product-photoshoot` is under `~/.claude/skills/higgsfield-official/`. The rest of the table is under `~/.claude/skills/`.

```markdown
# CLAUDE.md — Letter Brief (working title Plainpaper, listing draft only)

## Project facts
- iOS 17+, SwiftUI, StoreKit 2, US-first. Folder `~/Desktop/plainpaper-ios`.
- Bundle id `com.shuhratjon.letterbrief`. Display name **Letter Brief**. Team already on this Mac (`4MJ97BQM65` if that is the signed-in team).
- Working title Plainpaper is allowed only in `docs/APP_STORE_LISTING.md`. It is not trademark-cleared. Never put it in a bundle id or product id.
- v1: camera or import, on-device crop, Vision OCR, local template brief, signature, PDF to Files. One free successful explanation, then a hard paywall.
- Prices: annual $49.99 with a 7-day trial (annual only), weekly $6.99, monthly $14.99. Annual is the largest price. Price and trial length visible before the button. Real close. No fax.
- No server upload of the page image. No embedded API key. Local explanation if no key exists.
- Build with `-derivedDataPath` under `~/Library` or `/tmp`, never the Desktop / iCloud.
- Do not create a GitHub repo. Do not touch App Store Connect, TestFlight upload, or any other app.

## Phase → skill / tool / repo (mandatory)
State the phase, the skill names, the tool, and the repo before any work in that phase. Load the row before writing code. If the phase changes and the skill is not named, stop and name it before continuing.

| Phase | Skill | Tool | Repo |
|---|---|---|---|
| plan | `brainstorming`, `writing-plans`, `spec`, `jobs-to-be-done`, `journey-map`, `user-flow-diagram` | Plan mode. No code until the owner accepts the plan. | `~/Desktop/plainpaper-ios` only |
| design | `swiftui-pro`, `swiftui-expert-skill`, `ios-swiftui`, `hig`, `swiftui-liquid-glass`, `impeccable`, `ios-micro-interactions`, `ios-design-review`, `design-review`, `platform-conventions`, `camera-first-apps`, `visual-hierarchy`, `color-system`, `typography-scale` | Mobbin MCP (`mobbin`). Look at the images. | `~/Desktop/plainpaper-ios` |
| build | `swiftui-pro`, `swift-concurrency`, `ios-swiftui`, `swiftui-expert-skill`, `xcode-build-system` | `xcodebuild`, derived data off the Desktop | `~/Desktop/plainpaper-ios` |
| paywall | `storekit2-subscriptions`, `storekit`, `ios-paywall-design-specific`, `paywall-optimization`, `subscription-economics`, `paywalls`, `pricing` | StoreKit 2 local configuration | `~/Desktop/plainpaper-ios` |
| ASO / listing | `aso-app-store-optimization-deep`, `metadata-optimization`, `app-store-keyword-research`, `aso-audit`, `app-store-description-copywriting`, `aso` | Local file only. No App Store Connect. | `docs/APP_STORE_LISTING.md` in this repo |
| screenshots | `app-store-screenshots-design`, `screenshot-optimization`, `applekit-simulator-utils`, `ios-app-icon-design`, `app-icon-optimization` | iPhone simulator | This repo, proof in `~/agent-tools/plainpaper/proof/` |
| promo images | `higgsfield`, `higgsfield-product-photoshoot` | Higgsfield inside Claude. CLI was not on PATH. Do not install it from a remote script. | `~/agent-tools/plainpaper/promo/` |
| test | `verification-before-completion`, `test-driven-development`, `swift-testing-expert`, `swift-testing-framework`, `xcuitest-ui-testing`, `ios-testing`, `systematic-debugging`, `ios-qa`, `mobilebuildmcp-cli` | XcodeBuildMCP | `~/Desktop/plainpaper-ios` |
| release prep | `app-store-preflight`, `app-store-review`, `release-review`, `app-rejection-recovery`, `xcode-build-system`, `finishing-a-development-branch` | None. Do not submit. | `~/Desktop/plainpaper-ios`. No GitHub repo. |

If Claude changes phase without naming the skill, stop and name it before continuing.

Do not invoke `asc-*`, `revenuecat-paywall`, or `integrate-revenuecat`. Do not submit.

## Hard rules
1. Plan mode before any large change. Strongest model. High effort. Name the phase skill first.
2. No App Store Connect, no submit, no TestFlight upload, no other app's repo.
3. Paywall facts are section 2 of `~/agent-tools/plainpaper/CLAUDE_HANDOFF.md`. StoreKit prices, not hard-coded buttons.
4. No lawyer copy. No medical advice. No fax. No competitor name, icon, or sample.
5. No secrets in the project, the screenshot, or the chat.
6. Do not say done without `xcodebuild` output and `~/agent-tools/plainpaper/proof/brief.png`.
7. If the phase changes and the matching skill is not named, stop and name it before continuing.
```

---

## 9. What the owner already decided

Agreed 2026-10-01: build the section 2 item 1 idea from `2m-month-ideas-2026-10-01.md`. Scanner that explains a letter and lets you sign it. Fax is not v1. Conditional business case in that file is about 45% and is not a reason to add fax, ads, or a backend in this session.

Comparables (do not copy): iScanner Business #6, Scanner App Business #5, FAX from iPhone Business #7, CamScanner Productivity #7, as ranked in that file on 2026-10-01. They are why 4.3 risk is medium. Differentiation is the five-line brief.
