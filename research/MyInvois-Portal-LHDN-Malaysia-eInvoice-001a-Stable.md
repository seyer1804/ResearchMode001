# MyInvois Portal — LHDN Malaysia e-Invoice Deep Research

**Stable ID:** MyInvois-Portal-LHDN-Malaysia-eInvoice-001a-Stable  
**Research date:** 27 October 2026 (Asia/Manila)  
**Scope:** MyInvois Portal User Guide surface (`myinvois.hasil.gov.my`) plus the surrounding Malaysia e-Invoice mandate, mechanisms, lifecycle, and MSME tooling.  
**Sources of record:** HASiL / LHDNM official pages, e-Invoice Guideline PDF, Portal FAQ (9 Mar 2026), General FAQs, SDK microsite, Phase 4 / MyInvois e-POS media releases.

---

## Verdict

Malaysia’s e-Invoice system is a **Continuous Transaction Control (CTC)** clearance model run by LHDNM (HASiL / IRBM). Every covered transaction document must be submitted to LHDNM for near real-time validation; only then is it a valid e-Invoice, with an IRBM Unique Identifier (UUID), validation timestamp, and QR/validation link.

There are exactly **two official transmission mechanisms**:

1. **MyInvois Portal** (free) — individual form entry, Excel batch upload, mobile app after portal profile activation. Designed especially for MSMEs and taxpayers without ERP API integration. Digital signing is handled by the Portal (no taxpayer digital certificate required for Portal submissions).
2. **API / SDK** — direct ERP integration, Peppol providers, or non-Peppol intermediaries. Requires Client ID/Secret, OAuth 2.0 client credentials, signed XML/JSON documents, TLS, and polling for async validation results.

The screenshot’s User Guide page accurately describes the Portal: free MSME-oriented platform; seller and buyer roles; submit / review / cancel / reject; search validated documents; profile, ERP, intermediary, notifications, and document-type coverage including credit, debit, refund, self-billed, and consolidated documents.

**As of the HASiL timeline page last updated 30 August 2026:** phased mandate runs from 1 Aug 2024 (>$100m) through 1 Jan 2026 (up to RM5m), and taxpayers with annual turnover/revenue **less than RM3,000,000 are exempted**. Phase 4 (1 Jan–31 Dec 2026) has a **12-month transition** allowing consolidated e-Invoices (with stated conditions) and no penalties when those conditions are met. A separate free product, **MyInvois e-POS**, covers eligible businesses up to RM5m turnover with sales/inventory/reporting plus e-Invoice support.

**Product implication (research lock only):** for low-volume / non-ERP businesses, Portal (and optionally e-POS) is the compliance path. For volume systems (store platforms, POS, ERP, billing), build or attach via the official SDK API or a registered intermediary — do not invent a third clearance path.

---

## 1. What the screenshot is

| Item | Fact |
| --- | --- |
| Site | `myinvois.hasil.gov.my` — MyInvois Portal User Guide / content |
| Operator | LHDNM (Lembaga Hasil Dalam Negeri Malaysia) / HASiL / IRBM |
| Product named | MyInvois Portal |
| Stated audience | MSMEs; also usable by all taxpayers needing a non-API path |
| Stated access | Computers, laptops, smartphones |
| Stated actions | Submit, review, cancel, reject; view/display/search LHDNM-verified transactions |
| Features listed | Digital profile; ERP & intermediaries; invoices / credit / debit / refund notes & self-billed; retrieval; validation; notifications |

Official about-page wording (HASiL): Portal is free; aimed especially at taxpayers **not using a business ERP** to issue e-Invoices; also available via MyInvois mobile app (App Store / Google Play / AppGallery) **after** profile activation on the Portal.

---

## 2. Access path and environments

| Environment | Gateway | Notes |
| --- | --- | --- |
| Production | `https://mytax.hasil.gov.my` → MyInvois Portal | Real submissions; User Guide also at `https://myinvois.hasil.gov.my/content/` |
| Testing (Sandbox) | `https://preprod-mytax.hasil.gov.my` | Not connected to production; sandbox data is not stored in HASiL production DB and is not migrated |

Roles (Business Owner / Company Director / Organization Administrator / Estate Administrator, plus appointed representatives) must be applied **separately** for Production and Testing in MyTax. First-time representatives must complete sandbox MyTax login before appointment in sandbox.

---

## 3. Mandate timeline (official HASiL table)

| Targeted taxpayers (annual turnover / revenue) | Implementation date |
| --- | --- |
| More than RM100 million | 1 August 2024 |
| More than RM25 million and up to RM100 million | 1 January 2025 |
| More than RM5 million and up to RM25 million | 1 July 2025 |
| Up to RM5 million | 1 January 2026 |

**Exemption (timeline page, updated 30 Aug 2026):** annual turnover or revenue **less than RM3,000,000** — exempted from e-Invoice implementation.

**Threshold determination (Guideline):** based on FY2022 audited turnover/revenue (or YA2022 tax return if no audited FS). Once the cohort date is fixed from 2022 figures, later turnover changes do **not** move the obligation date. Voluntary early adoption is allowed.

**Note on older Guideline text:** Section 1.6.1(e) in the English Guideline PDF still lists an exemption for turnover **less than RM1,000,000**. The public timeline page updated **30 August 2026** states **less than RM3,000,000**. Treat the timeline page as the current public mandate/exemption statement until a matching Guideline revision is confirmed; do not invent a third number.

**Phase 4 transition (Jan 2026 announcements):** 1 Jan–31 Dec 2026 — consolidated e-Invoices (including stated Specific Guideline cases), consolidated self-billed where provided, flexible product/service description field use; **no penalties** if stated conditions are met.

---

## 4. Model: CTC clearance, not PDF-as-invoice

| Concept | Locked fact |
| --- | --- |
| What is an e-Invoice | Structured machine-readable file in **XML or JSON** per IRBM SDK — not PDF/JPG as the legal e-Invoice itself |
| Model | Continuous Transaction Control (CTC): IRBM validates submissions |
| Validation speed | Near real-time; FAQ states generally **less than two seconds** |
| After validation | IRBM Unique Identifier Number (UUID), validation date/time, validation link; supplier invoice number remains as a separate internal field |
| Sharing to buyer | Until further notice, validated e-Invoice **and/or** visual representation with embedded QR is allowed |
| Covers | B2B, B2C, B2G; also cross-border applicability per FAQs |

---

## 5. Two mechanisms (only)

| | MyInvois Portal | API (SDK) |
| --- | --- | --- |
| Cost to use LHDN channel | Free | Integration/build cost on taxpayer or intermediary side |
| Best for | MSMEs, no ERP, low/medium volume | High volume, ERP, POS/platform products |
| Create path | Individual form **or** Excel batch upload | Signed XML/JSON submissions |
| Digital certificate | **Not** required — Portal signs | Required on each submitted document |
| API paths | N/A | (i) Direct ERP (ii) Peppol providers (iii) Non-Peppol providers |
| Portal print PDF | Available for Portal-submitted docs | Print in Portal **not** available for API-submitted docs — get PDF from seller/system |

Taxpayers may use either or both mechanisms provided there is **no duplication** of the same e-Invoice.

---

## 6. Document types on the Portal

From the official User Guide module list:

- Invoice  
- Credit Note  
- Debit Note  
- Refund Note  
- Self-Billed Invoice / Credit / Debit / Refund  
- Consolidated e-Invoice  
- Scan Taxpayer QR code (buyer/taxpayer identity assist)

Guideline framing: Invoice documents income; Credit/Debit/Refund adjust; self-billed documents certain expenses (e.g. foreign supplier who does not use MyInvois).

---

## 7. Lifecycle (Portal and API — same rules)

1. **Create & submit** immediately after the sale/transaction (or adjustment).  
2. **Validate** near real-time → UUID + timestamp + link.  
3. **Notify** supplier and buyer (Portal + email from configured taxpayer profile).  
4. **Share** validated document and/or visual with QR.  
5. **Reject / Cancel window — 72 hours from validation time:**  
   - Buyer may **request rejection** (with reason).  
   - Supplier may **cancel** (own error or accepting buyer rejection).  
   - If not cancelled within 72 hours, cancellation is closed.  
6. **After 72 hours:** issue Credit Note / Debit Note / Refund Note e-Invoice referencing the original UUID; then issue a new invoice if needed. CN/DN/RN may also be used *inside* the 72-hour window if preferred instead of cancel.  
7. **Store & search** on IRBM database; Portal search limits apply (see §8).

---

## 8. Portal operational limits (Portal FAQ, updated 9 Mar 2026)

| Topic | Limit / rule |
| --- | --- |
| Recent document search | Up to **10 days** within last **31 days** |
| Search all documents | Window of **31 days** within last **2 years** |
| Export from Documents | Max **100** documents |
| Excel batch upload | Max **100** documents per file; max **25 MB**; max **1,000** drafts stored per taxpayer |
| Digital cert for Portal submit | Not required |
| Print button | Portal-submitted only |
| Copy as Draft | Portal / MyInvois mobile submissions only |
| ERP systems registrable | No maximum count |
| Intermediary delete | Cannot delete once registered; deactivate via “Delegation Until” / status |
| Individual as Intermediary | Not allowed — business/company/organisation only |
| API vs Portal timestamps | API/batch use UTC; Portal displays Malaysia Standard Time (UTC+8) |

---

## 9. API / SDK (for product builders)

Official SDK: `https://sdk.myinvois.hasil.gov.my`

- REST APIs; JSON control plane; documents XML or JSON.  
- OAuth 2.0 **client_credentials**; Bearer JWT; renew on expiry.  
- Intermediary login: `POST /connect/token` with header `onbehalfof` = taxpayer TIN (or TIN:ROB).  
- Submit: `POST /api/v1.0/documentsubmissions/` with format, base64 document, documentHash, codeNumber.  
- Cancel: within 72 hours of validation; after that use CN/DN/RN.  
- Async validation with polling.  
- TLS required; each document digitally signed.  
- Rate guidance example: ~12 RPM per Client ID on login endpoint docs.  
- Prerequisite: taxpayer digital profile + ERP/intermediary registered on Portal.

---

## 10. MyInvois e-POS (adjacent free product)

Not the same as the Portal User Guide page, but part of the same HASiL MSME stack:

- Free digital POS: sales, inventory, financial reporting, e-Invoice support.  
- Eligibility (FAQ updated 9 Jan 2026): Malaysian-citizen owner/director; business operates in Malaysia; annual turnover/revenue **up to RM5 million**.  
- Not for tax agents / intermediaries as their tool for client work — for businesses selling directly on premises.  
- If turnover later exceeds RM5m eligibility band, free e-POS ends; transition to commercial POS at taxpayer cost.  
- Uses Client ID / Client Secret (renewable) tied to MyInvois Portal registration.

---

## 11. Profile, roles, notifications

- MyTax roles gate Portal access; switch taxpayer profile inside Portal.  
- Representative types: User (appointed), ERP system, Intermediary.  
- Permissions include View/Send/Cancel/Reject documents; edit profile; manage user/ERP/intermediary; visual template; notifications.  
- Notification emails come from configured **Taxpayer Profile** addresses (not the seller/buyer fields on the invoice form); whitelist `@myinvois.hasil.gov.my` / `@hasil.gov.my`.  
- Taxpayer QR code generation supported for identity/scan flows.  
- Visual templates customisable for Portal print (logo PNG 400×400, 10–250 KB, no background, etc.).

---

## 12. Sources (primary)

1. MyInvois Portal content / User Guide — https://myinvois.hasil.gov.my/content/  
2. About MyInvois Portal — https://www.hasil.gov.my/en/e-invois/portal-myinvois/mengenai-portal-myinvois/  
3. e-Invoice implementation timeline — https://www.hasil.gov.my/en/e-invois/pelaksanaan-e-invois-di-malaysia/garis-masa-pelaksanaan-e-invois/ (updated 30 Aug 2026)  
4. Overview of e-Invoice model — https://www.hasil.gov.my/en/e-invois/pelaksanaan-e-invois-di-malaysia/gambaran-keseluruhan-model-e-invois/  
5. Guidelines index — https://www.hasil.gov.my/e-invois/rujukan-pelaksanaan-e-invois/garis-panduan/ (Guideline v4.8 30 Aug 2026; Specific Guideline v4.9 7 Sep 2026)  
6. IRBM e-Invoice Guideline PDF — https://www.hasil.gov.my/wp-content/uploads/irbm-e-invoice-guideline.pdf  
7. Portal FAQ (9 Mar 2026) — https://www.hasil.gov.my/wp-content/uploads/soalan-lazim-portal-myinvois.pdf  
8. General e-Invoice FAQs — https://www.hasil.gov.my/wp-content/uploads/lhdnm-e-invoice-general-faqs.pdf  
9. SDK — https://sdk.myinvois.hasil.gov.my / https://sdk.myinvois.hasil.gov.my/start/  
10. MyInvois e-POS FAQs (9 Jan 2026) — https://www.hasil.gov.my/wp-content/uploads/Guideline-myinvois-epos-faqs.pdf  

---

## Detail by Detail

### The page in the phone shot is the official free invoice portal

**Meaning**  
The government built a free website so small businesses can send tax e-Invoices without buying ERP software.

**On the page**  
LHDN says MyInvois Portal is free. It works on computers and phones. Sellers and buyers can submit, check, cancel, or reject invoices. They can also search invoices LHDN already checked.

**Example**  
A small shop with no accounting system logs into MyTax, opens MyInvois, and types one invoice at a time.

**Your move**  
Treat the Portal as the official MSME path. Do not invent a private “tax invoice PDF only” path for covered sales.

**Check**  
Can you name the site operator? Answer: LHDN / HASiL / IRBM.

---

### There are only two ways to send an e-Invoice to LHDN

**Meaning**  
You either use the free Portal, or you connect a system through the official API.

**Research**  
HASiL lists MyInvois Portal and API. API can be direct ERP, Peppol, or another registered tech provider. You may use both, but you must not send the same invoice twice.

**Example**  
A big chain wires its ERP to the SDK. A sole prop uses the Portal form. Both still need LHDN validation.

**Your move**  
Pick Portal for low volume. Pick API or an intermediary for high volume product software.

**Check**  
Is a pretty PDF alone a valid e-Invoice? Answer: No. The legal file is structured XML or JSON that LHDN validates.

---

### LHDN checks each invoice almost at once

**Meaning**  
This is a live clearance system. The tax office stamps the invoice before it is treated as a finished e-Invoice.

**Research**  
Validation is near real-time, often under two seconds. LHDN returns a unique ID, a time stamp, and a check link or QR.

**Example**  
You submit. Seconds later the Portal shows Validated. The buyer can later scan the QR to confirm it.

**Your move**  
Build product flows around “submit → wait for valid UUID → share.” Do not treat “saved locally” as done.

**Check**  
What model name do the FAQs use? Answer: Continuous Transaction Control (CTC).

---

### Cancel is only open for 72 hours after validation

**Meaning**  
Fix mistakes fast, or use credit / debit / refund notes later.

**Research**  
Buyer can ask to reject within 72 hours. Supplier can cancel within 72 hours. After that window, cancel is closed. Adjust with a credit note, debit note, or refund note that points to the old UUID.

**Example**  
Wrong buyer TIN noticed the next day: cancel and reissue. Wrong amount noticed next week: issue a credit note, then a new invoice if needed.

**Your move**  
Put a 72-hour clock on cancel UX. After that, only adjustment documents.

**Check**  
Does the 72 hours start at submit or at validation? Answer: From validation date and time.

---

### The mandate came in phases by business size

**Meaning**  
Bigger firms had to start first. Smaller firms came later. Very small firms can be exempt.

**Research**  
Official dates: Aug 2024 (>RM100m), Jan 2025 (>RM25m–RM100m), Jul 2025 (>RM5m–RM25m), Jan 2026 (up to RM5m). Timeline page updated 30 Aug 2026 says under RM3m turnover is exempt. Phase 4 also got a full-year 2026 soft landing for consolidated invoices under stated rules.

**Example**  
A firm that was already large in 2022 still follows the early date even if sales later fell.

**Your move**  
Read the taxpayer’s 2022 size first. Then check the RM3m exemption line on the current HASiL timeline page.

**Check**  
Does later turnover change move the start date? Answer: No, once fixed from 2022 figures.

---

### Portal users do not need their own digital certificate

**Meaning**  
On the free website, LHDN handles the digital signature for you.

**Research**  
Portal FAQ: no taxpayer digital certificate for Portal submission. API users must sign each document themselves.

**Example**  
MSME clicks Submit on the Portal. The system signs. An ERP product must attach a proper digital signature before API submit.

**Your move**  
Portal path: skip cert setup. API product path: plan signing and Client ID/Secret renewal.

**Check**  
Can an individual register as an Intermediary? Answer: No. Only a business/organisation can.

---

### Batch Excel and search limits matter for real work

**Meaning**  
The Portal is free, but it is not built like a full ERP.

**Research**  
Excel batch: max 100 invoices per file, 25 MB, up to 1,000 drafts. Search and export windows are capped. Print works for Portal docs, not for API docs.

**Example**  
A shop uploading 250 invoices must split into three Excel files.

**Your move**  
If volume will pass these limits often, move to API or e-POS/ERP, not bigger Portal spreadsheets.

**Check**  
How many documents can one Excel upload hold? Answer: 100.

---

### e-POS is a free shop system next to the Portal

**Meaning**  
HASiL also offers a free point-of-sale tool for eligible MSMEs, with e-Invoice support built in.

**Research**  
MyInvois e-POS is for Malaysian-citizen owners/directors, Malaysia operations, turnover up to RM5m. It records sales, stock, reports, and helps with e-Invoice. It is not for tax agents acting as intermediaries.

**Example**  
A retail MSME runs the till on e-POS instead of only typing invoices in the Portal after hours.

**Your move**  
Do not confuse e-POS with the Portal User Guide page. They are related free tools in the same program.

**Check**  
What happens if turnover later exceeds RM5m for e-POS eligibility? Answer: Free e-POS ends; move to a commercial POS.

---

### Sandbox and live are separate doors

**Meaning**  
Practice and real filing do not share data.

**Research**  
Sandbox is preprod MyTax. Production is live MyTax. Roles must be set in each. Sandbox submissions do not move to production.

**Example**  
Staff practice cancel flows in sandbox. Real January sales go only to production.

**Your move**  
Train in sandbox. Never point a live product at preprod for real invoices.

**Check**  
Are the two environments linked? Answer: No.

---

### Bottom line in simple words

**Meaning**  
The phone screenshot is the government free Portal for Malaysia e-Invoices. Covered businesses must get LHDN validation. Small shops can use the Portal or e-POS. Product systems should use the official API or a registered intermediary. Mistakes have a short cancel window, then only adjustment notes.

**Your move**  
Lock this Stable before building any Malaysia e-Invoice feature. Follow these mechanisms only. Do not add extra tech the research did not name.

**Check**  
What are the only two official send paths? Answer: MyInvois Portal and API.
