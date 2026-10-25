# DESIGN-MOBBIN.md — Letter Brief design references

Pulled from the Mobbin MCP (server `mobbin`) on 2026-10-01, iOS only, three searches. Each link is a structure reference. We borrow layout and interaction order, never colors, type, icons, or copy. No reference app is named anywhere in the product.

## Search 1 — scanner camera, crop corners, page review

| Reference | What we borrow | What we do not copy |
|---|---|---|
| [Apple Mail — captured page with four draggable corner handles on a dark canvas, close top-left, confirm top-right](https://mobbin.com/screens/4f73de4e-6461-44bb-9267-684f9264b638) | Crop screen: full-bleed dark canvas, page photo centered, four circular handles at the corners connected by a thin quad outline, close and confirm as circular buttons top-left / top-right. | Their accent color. |
| [Freeform — crop with the corners defaulted to the full page](https://mobbin.com/screens/e7cb91e1-8552-430d-bfcf-1c7c21671515) | Default corner positions = full page, so a good capture needs zero adjustment and one tap. | Nothing else. |
| [Google Drive — live camera with the detected page edge highlighted, Cancel top-left, flash and mode controls, round shutter](https://mobbin.com/screens/1e8afd16-6fe4-420f-b810-dca6f8234a5f) | Camera stage: full-bleed viewfinder, detected-edge overlay, single round shutter, text Cancel top-left. This is what VisionKit's document camera already provides, so our camera matches without custom code. | Toolbar icon set. |
| [Dropbox — page review with Retake and Add page, Edit/Delete/Arrange toolbar](https://mobbin.com/screens/564d678a-2987-4512-9277-24da01770e96) | The "retake" affordance idea on the review step. v1 keeps one page, so only Retake survives (as "Retake" on the crop screen). | Multi-page tools. |

## Search 2 — signature sheet, then export

| Reference | What we borrow | What we do not copy |
|---|---|---|
| [Fresha — "Add a signature": full name, Type/Draw segmented control, draw box with Clear, one black primary button](https://mobbin.com/screens/099dd522-1fc1-432d-b902-8ca8c40e1d1c) (the one confirmed in the handoff; also listed as `d6becd9c-f79e-4e33-8fa9-0f4921b1777b`) | Sheet structure: title + close, name field, draw area with "Clear" at its top-trailing, one full-width primary button at the bottom. | Their legal paragraph, colors, type, the Type tab (v1 is draw only). |
| [Apple Notes — signature pad with a baseline, "Sign your name using your finger" hint, Clear below](https://mobbin.com/screens/2081c297-9589-4290-838c-31721f84336b) | The baseline rule inside the pad and the hint text under it. Gives the hand a guide and makes the result sit straight on the page. | Nothing else. |
| [PayPal — large pad with "Sign here" placeholder, Apply primary button, Clear as a text link below](https://mobbin.com/screens/950f13a8-7199-4ae7-8867-b1e495da6d73) | Pad occupies most of the sheet; placeholder text disappears on first stroke. | Button copy. |

## Search 3 — paywall with one annual plan dominant, price before the button

| Reference | What we borrow | What we do not copy |
|---|---|---|
| [ABY Journal — selected annual card reads "1 week FREE trial / $129.98 yearly", button "Start free trial", Terms · Privacy · Restore row](https://mobbin.com/screens/65f1ef09-8067-43b6-a2d0-2210febda055) | Trial length and the billed yearly price shown on the selected card, above the button; legal row order. We go further: the button itself carries the yearly price. | "58% OFF" badge, "Best deal" badge, lifetime plan. |
| [The Outsiders — three equal cards, annual in the center marked "BEST OFFER", one pink primary button, "Cancel Anytime" under it](https://mobbin.com/screens/65112b07-4e73-4a48-a3f5-0a83e895108e) | Three cards in a row with annual as the visually heaviest; price inside each card. We put the annual price in the largest type on the screen. | Their button label (no price on it), badges, awards section. |
| [Liven — selected plan line "3 days free trial / then $7.99 per week" directly above the button](https://mobbin.com/screens/a612cffd-939d-471f-9b89-bf734058ab1a) | The "then <price> per <period>" line above the button. | The "Enable free trial" toggle (forbidden by the handoff), the weekly-trial pattern, testimonial header. |
| [pillowtalk — plain three-row plan list with annual preselected, one Continue button, "restore purchase" below](https://mobbin.com/screens/4139d31a-e861-4982-b075-7e8d5ffd1468) | Row list alternative; selected row has a filled check. Used for the Dynamic Type fallback layout (rows instead of three narrow cards at accessibility sizes). | Lifetime row, discount copy. |

## What this means for Letter Brief

- Camera: VisionKit document camera (matches the Google Drive reference out of the box).
- Crop: dark canvas, four 44 pt handles defaulted to full page, "Use page" primary, "Retake" secondary.
- Brief: not a reference from Mobbin; it is the new thing. One card, five rows, date and amount in the largest type.
- Signature: Fresha structure + Apple Notes baseline. Draw only. Button "Use signature".
- Paywall: three plan cards, annual preselected and largest; above the button "7 days free, then $49.99/year"; button "Start 7-day free trial — $49.99/year after"; weekly and monthly show price and period only; `xmark` close always visible; Restore · Terms · Privacy.
- At accessibility Dynamic Type sizes the three cards become three full-width rows (pillowtalk structure) so the price never clips.
