# Letter Brief v1 decisions locked by Claude.ai (Opus 5.5) on 2026-10-01

Source chat: https://claude.ai/chat/7ecc34b2-704a-4c88-9333-5f470281777f
Owner: treat these as locked. Do not reopen the visual world, icon, or title unless a test fails.

## 1. Visual world
Facts Panel, motion kept to a minimum. Base on a US Nutrition Facts label: heavy black rules, tight type, plain data rows. One accent color, only where something is urgent.

Tokens:
- Paper #FAF8F3 (dark #121212)
- Ink #111111 (dark #F2F0EA)
- Hairline #D9D5CC
- Urgent accent #E5484D only for dates under 7 days and consequence text
- CTA: ink-black button, paper-colored text

Type: SF Pro Display Heavy titles, SF Pro Text body, SF Mono for amounts and dates. Dynamic Type including AX5. No custom font in v1.

Rules: 8pt top rule, 4pt section rules, 1pt row rules. Corner radius 4 except CTA 14. No gradients, shadows, glass, or emoji.

Motion, exactly three, all off under Reduce Motion:
- Brief rows reveal top to bottom, 40ms stagger, 180ms each
- haptic .success when the brief is ready
- matchedGeometry of the document thumbnail into the Brief screen

## 2. Home
- "Letter Brief" Heavy 34pt left, 8pt rule under it. Gear top right.
- Hero 220pt: "Got a letter?" Heavy 28. Subline "Get the five facts in seconds." 17pt.
- Black primary Scan (camera.viewfinder). Outlined secondary Import (doc).
- Section "RECENT" 13pt caps tracking 1.2, 4pt rule.
- Rows 72pt: 44x56 thumb, type in bold, due date mono (red if under 7 days), amount mono right, swipe to delete.
- Empty: one sample brief at 40% opacity labeled Example.
- No tab bar. Settings is a sheet from the gear.

## 3. Brief
Header: thumbnail (tap full screen), "Brief" Heavy 34, 8pt rule.
Exactly five rows: WHAT IT IS, WHAT THEY ASK, DATE (mono; red + days-left chip if under 7 days), AMOUNT (mono with currency), IF YOU DON'T.
13pt caps label over 22pt semibold value. 1pt rules, 4pt closing rule.
Missing fields: "Not found in this letter." Never guess.
Tap a row highlights source text on the scanned page.
Footer: "Summary of the text on the page. Check the original."
Sticky bar: Sign and Export PDF. Export opens share sheet with Save to Files first.

## 4. Paywall
- X top left, 44pt, immediately visible, returns Home.
- Headline "Understand every letter." Heavy 32, 8pt rule.
- Benefits: Unlimited briefs. Sign and export PDFs. Stays on your iPhone.
- Annual first, largest, preselected: "7 days free, then $49.99/year"
- Monthly "$14.99/month". Weekly "$6.99/week"
- Above the button, updates with selection: "Free for 7 days, then $49.99/year. Cancel anytime in Settings."
- Annual button "Start 7-day free trial". Monthly/Weekly "Continue".
- Restore Purchases, Terms, Privacy, auto-renew disclosure.
- Product IDs: annual_4999_trial7, monthly_1499, weekly_699. Keep existing IDs if already created; do not invent a second set. If IDs already differ, keep the existing IDs and note the difference.
- Free-brief flag in Keychain so reinstall does not reset it.
- Prices unchanged: annual $49.99 with 7-day trial only on annual. One free explanation then hard paywall.

## 5. Icon
Upright off-white #FAF8F3 sheet, folded top-right corner, on deep ink-navy #0E1B3D. One thick yellow #FFD60A highlighter bar on the upper third, two thin gray lines below. No text, envelope, pen, magnifier, or gradient. Check 29pt, 60pt, and grayscale. Provide dark and tinted iOS 18 variants.

## 6. App Store
Title (27): Letter Brief: Mail Explainer
Subtitle (29): Scan Bills, Forms & Sign PDF.
Keywords (97, no spaces): summary,understand,document,paperwork,notice,ocr,deadline,due,amount,invoice,tax,insurance,ai,owe
Screenshot captions: "What does this letter want?" / "Due date and amount, instantly." / "Sign and save as PDF." / "Stays on your iPhone."
No fax, lawyer, legal advice, medical, notarized, certified, legally binding, competitor names, or prices in the keyword field.
Working title Plainpaper is not trademark-cleared. Do not submit to the App Store.

## 7. Done means all of this passes
Real iOS 17 device and latest iOS. OCR: 30 varied docs, correct date and amount on at least 28/30, zero invented values. Auto-crop 9/10; manual crop, rotate, multipage reorder and delete. Signature survives PDF export; PDF opens in Files, Mail, and Preview; text selectable; filename Type_YYYY-MM-DD.pdf. Paywall sandbox: free brief, reinstall, trial, all products, restore, cancel, Ask to Buy, offline, refund, family sharing, X close. Price and trial above the button. Camera denied, limited photos, empty and error states, no blank screens. No crash on airplane, full storage, 50-page import, bad PDF, backgrounding, incoming call. VoiceOver, AX5, contrast 4.5:1, Reduce Motion, dark mode, SE and Pro Max. Brief ready under 3s on iPhone 12. Cold launch under 1.5s. Zero leaks across 20 scans. On-device only. Privacy manifest. Copy audit clean. UI tests: scan, brief, paywall, export. Do not claim done without the command output.
