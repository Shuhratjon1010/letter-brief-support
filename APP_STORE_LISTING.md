# APP_STORE_LISTING.md — Letter Brief, US English, draft, local only

Rewritten 2026-10-01 in the ASO / listing phase with `aso-app-store-optimization-deep` and `app-store-description-copywriting`. This is a local file. Nothing here was entered in App Store Connect.

Name note: the working title Plainpaper is not trademark-cleared and is not used in the app, the bundle id, the product ids, or this listing.

Sources: `docs/CLAUDE_AI_DECISIONS.md` sections 3, 4, and 6, and the owner's 2026-10-01 keyword instruction, which overrides section 6 for the keyword field.

Every count below was measured with `printf %s '<text>' | wc -m` (characters, not bytes). Multi-line blocks were counted on the exact text between the fences, newlines included.

## 1. Metadata

| Field | Value | Count | Limit |
|---|---|---|---|
| Title | `Letter Brief: Mail Explainer` | 28 | 30 |
| Subtitle | `Scan Bills, Forms & Sign PDF.` | 29 | 30 |
| Keywords | `summary,understand,document,paperwork,notice,ocr,deadline,due,amount,invoice,tax,insurance,payment` | 98 | 100 |
| Primary category | Productivity | | |
| Secondary category | Utilities | | |

Notes:
- The decisions doc lists the title as 27 characters. `wc -m` measures 28. The title text is unchanged; only the count in that doc is off by one.
- The keyword field follows the owner's 2026-10-01 instruction. It replaces the decisions doc's ending `...,insurance,ai,owe` (97) with `...,insurance,payment` (98). `ai` and `owe` are dropped; `payment` is added.
- No keyword repeats a word from the title (letter, brief, mail, explainer) or subtitle (scan, bills, forms, sign, pdf). Apple already combines the three fields, so repeats would waste characters.
- No spaces in the keyword field. No price in the title, subtitle, keywords, promotional text, or captions.

## 2. Promotional text

Editable without a new build.

```
Scan a letter and see what it wants: the date, the amount, and what happens if you don't. Tap any answer to see the words on your page. Nothing is uploaded.
```

Count: 156 / 170.

## 3. Description

The first three lines are what people see before "more".

```
What does this letter want? Scan it and get five plain answers: what it is, what they ask, the date, the amount, and what happens if you don't.

Letter Brief reads the page on your iPhone. If a fact is not on the page, the brief says "Not found in this letter." It never guesses a date or an amount.

THE BRIEF
• WHAT IT IS: the kind of letter, in a few words
• WHAT THEY ASK: the action the letter asks of you
• DATE: the key date on the page
• AMOUNT: the amount on the page, with its currency
• IF YOU DON'T: what the letter says happens next

Tap any row to see the words it came from, highlighted on your scanned page. A date less than 7 days away turns red, but only when the date on the page is clear.

SCAN OR IMPORT
• Scan with the camera, one page or many
• Or import photos and PDFs, including multi-page files
• Rotate, crop, reorder, or delete pages
• Text is read on your iPhone with Apple's Vision text recognition

SIGN AND SAVE
• Sign with your finger
• Save a separate signed PDF and keep the original as it was
• Files get clear names, like Bill_2026-10-01.pdf
• Export PDF opens the share sheet with Save to Files first

STAYS ON YOUR IPHONE
• Your page image is never uploaded
• No account
• No tracking

YOUR FIRST BRIEF IS FREE
After that, a subscription unlocks unlimited briefs. The price and the free-trial length are shown in the app before you subscribe.

Letter Brief summarizes the text on the page. It is a reading aid, not advice. Check the original letter before you act.

Subscriptions renew automatically unless canceled at least 24 hours before the end of the current period. Manage or cancel them in Settings under your Apple Account.

Terms of Use (Apple standard EULA): https://www.apple.com/legal/internet-services/itunes/dev/stdeula/
Privacy Policy: https://shuhratjon1010.github.io/letter-brief-support/privacy.html
```

Count: 1,858 / 4000.

## 4. What's New (first release)

```
First release. Scan or import a letter, get a five-row brief, sign it, and save the PDF. Everything stays on your iPhone.
```

Count: 121 / 4000.

## 5. Screenshot captions (locked)

| # | Caption | Count | Screen to show |
|---|---|---|---|
| 1 | What does this letter want? | 27 | Brief with all five rows filled |
| 2 | Due date and amount, instantly. | 31 | Brief with DATE in red and the days-left chip, AMOUNT in mono |
| 3 | Sign and save as PDF. | 21 | Signature on the page, then the export sheet with Save to Files first |
| 4 | Stays on your iPhone. | 21 | Home with Recent rows |

Captions have no hard App Store limit; keep each to one line on the screenshot. No price on any screenshot.

## 6. Review-risk notes

Guidelines named are from the App Review Guidelines; each note is a check to run before any submission, not a claim that it passes.

- **2.3.1 accuracy.** Every feature in the description must be in the build that ships: multi-page camera scan, multi-page photo and PDF import, rotate / crop / reorder / delete, the five rows, tap-to-highlight source text, the red date rule, finger signature, the separate signed PDF, the `Type_YYYY-MM-DD.pdf` name, and Save to Files first. If any one slips, cut its line before submitting.
- **2.3.7 price in metadata.** No price in title, subtitle, keywords, promotional text, or captions. The description says only that price and trial length are shown in the app.
- **3.1.2 subscriptions.** The paywall shows the billed amount and the trial length above the button, has a real close, and puts Restore Purchases, Terms (Apple's standard EULA, a `Link`) and Privacy (the public policy, a `Link`) next to the button. Below the plans, the selected plan's disclosure names the title, length, price, auto-renewal, when payment is taken, and how to cancel. Settings has Restore Purchases, Manage subscription, Privacy Policy, Terms of Use (EULA), and Support. The description ends with both links.
- **5.1.1 privacy.** "Never uploaded", "No account", and "No tracking" must match the privacy label (Data Not Collected) and the privacy manifest. If any analytics or crash SDK is added later, these lines change first.
- **Advice wording.** The brief summarizes the page, says "Not found in this letter." for missing facts, and never guesses. The description calls it a reading aid, not advice. Keep the IF YOU DON'T row quoting the letter, not predicting outcomes.
- **Keyword relevance.** `tax` and `insurance` describe kinds of letters people scan. Screenshots should show a neutral sample (a utility bill or a parking notice) so neither word reads as a promise of tax or insurance help.
- **Title word "Mail".** It means paper mail. Some searchers expect email. That is a conversion risk, not a review risk; watch the search-to-install rate after launch.
- **Copy audit.** The words banned by `docs/CLAUDE_AI_DECISIONS.md` section 6 and `CLAUDE.md` hard rule 4 were grepped out of this file (result recorded in the session report).

## 7. Not done here

- No App Store Connect entry. Nothing was uploaded, no metadata was synced, no build was submitted, and no TestFlight build was sent. The API key cannot create the app record (see section 9), so the subscriptions are not in App Store Connect either.
- No keyword volume data. That needs Apple Search Ads or a paid ASO tool.
- No localization beyond US English.
- No screenshots or preview video. Those belong to the screenshots phase.
- No trademark search for "Letter Brief".

## 8. App Store Connect fields (2026-10-01, release-prep phase)

Filled from the code on branch `worktree-letter-brief-v1`. Enter by hand once the app record exists. Nothing here was sent to App Store Connect.

### URLs

| Field | Value |
|---|---|
| Privacy Policy URL | https://shuhratjon1010.github.io/letter-brief-support/privacy.html |
| Support URL | https://shuhratjon1010.github.io/letter-brief-support/ |
| Marketing URL | (leave empty) |
| License Agreement | Apple's standard EULA (leave the custom EULA field empty). Linked in the description and in the app. |

Both URLs returned HTTP 200 on 2026-10-01. Source: public repo `Shuhratjon1010/letter-brief-support`, GitHub Pages from `main` /.

### Age rating: 4+

Answer None or No to every content descriptor in the questionnaire. Also No for unrestricted web access (the two policy links open Safari; there is no in-app browser), user-generated content or messaging, gambling and contests, and parental controls. Not made for kids (not in the Kids category). Expected result: 4+.

### App Privacy: Data Not Collected

- Tracking: No. `NSPrivacyTracking` is false and there are no tracking domains.
- Data collection: "No, we do not collect data from this app." The page image, the recognized text, the brief, and the signature stay on the iPhone. The app has no server and no analytics, crash, or ad SDK.
- Purchases go through Apple's StoreKit. Apple, not the developer, collects the payment data.
- `PrivacyInfo.xcprivacy`: no collected data types and no required-reason API types. The code calls none of those APIs: no `UserDefaults`, no file timestamps, no system boot time, no disk space. It was checked and needs no change.

### Subscriptions (group "Letter Brief Pro")

Product IDs are unchanged. They match `LetterBrief/Resources/LetterBrief.storekit`.

| Reference name | Product ID | Duration | Price (USD) | Introductory offer |
|---|---|---|---|---|
| Annual | `com.shuhratjon.letterbrief.annual` | 1 year | 49.99 | Free trial, 1 week (7 days), new subscribers |
| Monthly | `com.shuhratjon.letterbrief.monthly` | 1 month | 14.99 | None |
| Weekly | `com.shuhratjon.letterbrief.weekly` | 1 week | 6.99 | None |

Display names (en-US): Annual, Monthly, Weekly. The in-app disclosure uses the display name as the title, for example "Annual subscription: 1 year, $49.99/year after a 7-day free trial."

In-app subscription disclosure (3.1.2), built from StoreKit for the selected plan:

```
<Display name> subscription: <1 year|1 month|1 week>, <price>/<period>[ after a 7-day free trial]. Renews automatically at <price>/<period> until canceled. Payment is charged to your Apple Account <when the free trial ends | when you confirm the purchase>. To cancel, open the Settings app, tap your name, then Subscriptions, at least 24 hours before the current period ends.
```

Each subscription also needs a review screenshot of the paywall. Use `~/agent-tools/plainpaper/proof/policy/paywall-annual.png`.

### Export compliance

- `ITSAppUsesNonExemptEncryption` = `false` in `LetterBrief/Info.plist` (also set in `project.yml`). This is true for this app.
- Why: the app has no networking code of its own (no `URLSession`, no sockets, no crypto library). The only encryption is what iOS provides: HTTPS inside Apple's StoreKit, Keychain storage, and Data Protection on saved files. That is exempt, so no export compliance documents are needed.

### Review notes (paste into App Review Information)

```
No login. Letter Brief has no account and no sign-in, so there is nothing to sign in to and no demo account.

How to test: tap Scan to photograph any printed letter or bill, or tap Import to pick a photo or PDF. Text is read on the iPhone with Apple's Vision framework. The page image and its text are never uploaded. The app has no server.

The first successful brief is free. Starting a second letter opens the subscription screen: Annual $49.99/year with a 7-day free trial, Monthly $14.99, or Weekly $6.99. Restore Purchases, Terms of Use (Apple's standard EULA), and the Privacy Policy are next to the purchase button. Settings (gear on Home) also has Restore Purchases, Manage subscription, Privacy Policy, Terms of Use, and Support.

Account deletion: not applicable. The app has no account. Saved letters live only on the iPhone and are deleted by swiping them away or deleting the app.

The brief summarizes the words printed on the page. It is a reading aid, not advice. Missing facts show "Not found in this letter."

Contact: Shuhrat Soliev, shuhrat.soliev@gmail.com, +1 914 650 2041.
```

### Contact for App Review

Shuhrat Soliev · shuhrat.soliev@gmail.com · +1 914 650 2041

## 9. App Store Connect status

- On 2026-10-01 the API key `Q8VZ7JJU3M` (team issuer `0c13dc0a-…`) found no app record and no registered bundle ID for `com.shuhratjon.letterbrief`.
- `POST /v1/apps` returned **403 FORBIDDEN_ERROR**: "The resource 'apps' does not allow 'CREATE'. Allowed operations are: GET_COLLECTION, GET_INSTANCE, UPDATE". The App Store Connect API cannot create an app record.
- Subscriptions hang off the app record, so the three products could not be created either.
- Owner steps:
  1. Register the bundle ID `com.shuhratjon.letterbrief` (Certificates, Identifiers & Profiles, or an Xcode archive with automatic signing).
  2. In App Store Connect, go to Apps, then + and New App: iOS, name "Letter Brief", primary language English (U.S.), bundle ID `com.shuhratjon.letterbrief`, SKU of your choice.
  3. Check that the Paid Apps agreement and the tax and banking details are active.
  4. After that, the same API key can create the subscription group, the three subscriptions, their prices, and the annual free trial without a browser.
