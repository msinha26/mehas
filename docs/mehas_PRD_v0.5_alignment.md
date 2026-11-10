# Mehas PRD v0.5 — alignment with the clickable prototype

> **What this is.** The prototype (Mehas mood board, Claude Design canvas) changed a lot between 4 and 10 November 2026 in design reviews with Meha [DR-2]. This document records every place where the prototype and the earlier documents disagree, and which one now holds.
>
> **Precedence rule.** Where this document differs from `claude/mehas_PRD.md` (v0.4, 4 Nov 2026) or `Mehas_MVP_Scope (3).docx` (2 Nov 2026), **this document wins**. Section numbers below refer to the PRD. Anything not mentioned here is unchanged.
>
> **Status:** Draft v0.5 · Owner: Meha · Updated 10 Nov 2026

| Tag | Source |
|---|---|
| [DR-2] | Design reviews with Meha on the clickable prototype, 4–10 Nov 2026 |

---

## 1. Terminology (applies to every document and screen)

| Old term | New term | Why |
|---|---|---|
| eggs / egg | **oocytes / oocyte** | Clinical wording; already used across all screens |
| Patient copy, patient instruction sheet | **Doctor instructions** | One name for what the doctors told the patient, visit by visit; the front desk prints it |
| Clinic admin | **Clinic operations coordinator** | Same person also checks Due today and Daily completeness, sets clinic rules and prices, and manages users |
| Clinical champion (in the product) | **Senior doctor** | The word "champion" is not shown anywhere in the product. Approvals land in the senior doctor's **Approvals** tab. The PRD's champion duties (rules, evidence set, sources, gold cases) stay with a named senior doctor; only the label changes |
| Metropolis (on screens) | **Lab report** | Screens never name the lab. Reports arrive by email (Q-12 decided) |
| Clinic ID | **Patient ID** | See R-30 |
| Folder (patient folder) | **Patient record** | Used in all navigation and links |

---

## 2. Roles and what each sees (replaces the roles table in 5.3 and the home screens in Flow 11)

Every person signs in to **Mehas** (not to a named clinic) with their own login, either **Continue with Google** or email/phone and password. The operations coordinator adds each person in Users and roles first; signing in with Google works only for an email she has added. The clinic and the role come from the login (no role picker, no self sign-up). **Scope change (11.2): Google sign-in moves into scope;** other single sign-on stays out.

| Role | Lands on | Tabs | Can change |
|---|---|---|---|
| Senior doctor | Patients | Patients · Approvals · Insights | Scan entry and plan in the patient record; agrees with or changes Mehas's suggestion; approves everything in Approvals |
| Junior doctor (sees patients) | Patients | Patients · Past records · Insights | Same as senior for her own patients; may **ask a senior to approve** (optional); approves digitized past files |
| Junior doctor · assisting (new, on rotation) | Patients (all patients today, with status) | Patients | Patient record is read-only with **no chat**; can edit **Injection sheet**, **Doctor instructions** and the **current cycle's Bill** (e.g. when the senior gives instructions verbally). Every change shows "Changed by [name], for [senior]" |
| Nurse coordinator | Patients (read-only patient details) | Patients · Injection sheet · Vitals · New registration · Lab reports | Records doses given, vitals, registration and KYC; checks only the lab reports Mehas could not read clearly or match to a patient |
| Front desk (new) | Today (appointments) | Today · New registration | Marks arrivals; prints doctor instructions for consulted patients |
| Data-entry operator | Past records | Past records | Digitizes paper files; each file goes to a junior doctor for approval |
| Anesthetist | Anesthesia | Anesthesia | Enters the anesthesia record (**Q-94 decided: logs in**) |
| Embryologist | Embryology | Embryology | Enters oocytes, fertilization and embryo records (**Q-94 decided: logs in**) |
| Clinic operations coordinator (replaces clinic admin) | Due today | Due today · Daily completeness · Clinic rules · Costing sheet · Users and roles | Checks and calls; end-of-day sign-off; creates and changes rules and prices (each needs senior approval); adds users, assigns roles, switches users off or deletes them, sets the on-call rota |
| Owner / medical director | Insights | Insights | Reads only |

Screens removed after review: nurse "Today", nurse "Today's schedule", the patient copy screens (front desk and junior), the "Screen map", and the separate "Due today" for doctors. Doctors no longer see Due today; the on-call doctor still gets an alert for a missed trigger.

---

## 3. Approvals (replaces "There is no approval step" in 5.3, R-07, R-20, Flow 3 and 16.4)

The senior doctor's **Approvals** tab holds four kinds of request, each with an optional comment from the senior on approve or send back:

| Type | Comes from | Required? | Shows |
|---|---|---|---|
| Prescriptions | Junior doctor ("Ask Dr. X to approve") | **Optional** for the junior, except a dose above a clinic cap, which always needs approval | Patient name and ID, key numbers, the junior's prescription and reason, an amber "Above the clinic dose cap" warning when it applies |
| Clinic rule changes | Operations coordinator (Clinic rules) | Required | Now vs proposed, created by and the date and time (recorded automatically) |
| Price changes | Operations coordinator (Costing sheet) | Required | Each component old → new, new total, applies-from date, reason, created by and time |
| Patient bills | Assisting junior doctor (current cycle's Bill) | Required when any amount differs from the price list | Item, price list, proposed; bill total and difference; reason; that the estimate was explained to the patient |

Departure flags (a junior's plan differing from the senior's) remain, but there is no separate approval step for routine prescriptions.

---

## 4. The suggestion (replaces the U1 layout in 18.3.2 and parts of R-05, R-15, 15 and 18.3.1)

What the doctor sees on the patient record, under **Chat with Mehas about [patient]**:

1. **What to do**, as one line (e.g. "Continue Gonal-f 225 IU, start Cetrotide tomorrow (day 7), scan day 8").
2. **Reason:** one short line, then a **See why** link. No source chips on the card.
3. **Also today:** any other medicines or injections that are not stimulation (e.g. a vitamin D3 injection, a change of tablets), each with a one-line "Why".
4. **Agree and save**, and a **"This showed me something new"** tick (kept because it feeds a primary pilot metric, 9.3).
5. **No "Tell the patient" line.** The doctor decides what to tell the patient.
6. **No "Checks passed" chip.** A clinic-rule warning appears **only** when a dose is above the cap (U7 changed: green confirmation is no longer shown; failures still are, and E-31 still blocks when checks did not run).

**See why** (pop-up) has three parts:

| Part | Contents | Source label |
|---|---|---|
| The patient so far | Current and past cycles in plain lines | None — the doctor knows it is her record |
| Similar patients at this clinic | Group definition and N; what happened to them; 3 closest matches (name, patient ID, what was done, outcome) each with **Open record**; "See all N in Similar patients" | Counts always shown |
| Guidelines and research | One line per source with a linked citation and, where relevant, availability in India | Linked citation per item |

This replaces rule 3 of 18.3.1 ("every claim has a visible source") with: **every claim has its source one click away in See why.** The old "See what happened to these N patients" link is removed (the Similar patients tab already does this).

**Disagreeing with the suggestion (replaces thumbs up / thumbs down / Give feedback in R-15):** the doctor types what she will do instead in the chat (Enter sends; no send button, no canned question chips, no reason dropdown). Mehas records it as today's plan, uses her words as the reason, and shows a warning if a dose is above the clinic cap. The junior can also ask a senior to approve. Metrics in 9.3: "Thumbs-up rate" becomes **agreement rate**; "feedback completeness" becomes **agreed, or a different plan recorded, for 100% of suggestions**.

---

## 5. Patient record (refines R-03, R-08, R-21 and 15)

- Tabs: **Current cycle · Past cycles · Similar patients** (no separate Reports tab).
- Patient ID sits directly under the name everywhere (small text, no "Patient ID" label).
- Current cycle: record buttons **Reports · Injection sheet · Doctor instructions · Vitals · Bill**. Past cycles add **Anesthesia · Embryology · Discharge summary**. Records open in a pop-up.
- Visit table: Day, right and left ovary, lining, prescription (injections, with tablets as a subtext), prescribed by, Notes ("Report available" plus key values, opening that day's report), Scan ("View" opens the photo; a dash when there is no photo). No E2 column.
- Follicle chart: no legend and no medicine lanes; hovering a day shows that day's medicines.
- Past cycles: each cycle is a card that expands and collapses; the newest opens by default.
- Editing: Injection sheet and Doctor instructions are editable by doctors (and the assisting junior) in the current cycle, with every change flagged by name; everything else is read-only.

---

## 6. Daily monitoring (changes R-09, R-26(5), U6, U11, Flow 9)

- **Due today** (operations coordinator): today and tomorrow's triggers, pick-ups, injections and blood tests, with status. For anything missing she **calls the patient or the staff member** (no "ask to update" messages). At the end of the day she adds an optional comment and clicks **Mark today as reviewed**; her name and the date and time are recorded automatically.
- **Daily completeness** (operations coordinator): what is missing from today's records (visit not entered, prescribed not recorded, advised but no record, test ordered with no result, **past file not digitized or not yet approved**), with a Call button for the person responsible. She marks the day complete with an optional comment; date and time are recorded automatically. Open gaps carry over to the next day.
- The WhatsApp notification rules (counts only, no names) are unchanged.

---

## 7. Clinic rules (R-06) and Users and roles (R-27)

- Clinic rules are **created and changed by the operations coordinator**; each change goes to a senior doctor's Approvals with "Created by [name] · [date, time]". Not in force until approved.
- Users and roles is managed by the **operations coordinator** (not the owner): add a person, assign roles, switch off (power icon) or delete (bin icon, with confirmation), who is on call today, and a weekly on-call rota. Role list adds **Junior doctor · assisting** and **Clinic operations coordinator**.

---

## 8. New requirements

| ID | Requirement | Priority | Done when |
|---|---|---|---|
| **R-28** | **Costing sheet and patient bills.** (a) Price list of procedures and packages, each broken into components (surgeon, anesthesia, equipment, procedure, theatre and lab, freezing, embryo transfer) with a total; packages show the saving against booking items separately. Sample items: intra-ovarian PRP; intra-ovarian exosome; PRP + exosome package; ovum pick-up; embryo freezing; pick-up + embryo freezing; pick-up + fresh embryo transfer. (b) The coordinator changes a price with an applies-from date and a reason; it goes to Approvals. (c) Each cycle (current and past) has a **Bill**: items with dates and amounts, payments received (date, mode, amount), total paid, and balance due or "Fully paid". The current cycle's bill is made from the doctor's plan and the price list; the assisting junior can change amounts or add items; anything off the price list goes to Approvals. Payments are taken by the front desk | P0 proposed (in the prototype; Meha to confirm) | Every price change and every off-list bill change has an approval record with who and when; bill totals equal the sum of items; balance = billed − paid |
| **R-29** | **Vitals.** Nurse records weight, blood pressure and heart rate at check-in, with who took them; shown in the patient record per cycle | P1 | Every reading shows who took it and when |
| **R-30** | **Patient ID.** Created by Mehas at registration with the clinic's code as prefix (e.g. KH-2611-0142). Shown with the patient's name on every list, record, sheet, report, bill, discharge summary and approval | P0 | No screen shows a patient name without the ID (except a new patient before registration) |

**Scope change (11.2):** the out-of-scope row "Billing, scheduling, inventory — not planned" now reads: **"Scheduling, inventory and payment collection — not planned. Mehas keeps the clinic's price list and each cycle's bill estimate and payments received (R-28)."**

---

## 9. Other screens and changes

- **Welcome / sign-in:** headline "Your AI companion for every IVF decision" (the only mention of AI; kept subtle, like Harvey's homepage). Line under it: "Built for IVF clinics. Plan every cycle with confidence, and spend your time on patients, not paperwork." Five short points: prescription suggestions at every step of the cycle; personalised to each patient; insights at your fingertips to help your clinic grow; fewer missed doses, safer prescriptions; seamless and paperless. Value only, not how it works; no claims about prediction or time saved.
- **Lab reports** (nurse): shows today's count (received, added automatically, to check) and only the reports that need a check (see Q-12).
- **Insights** (one screen for doctors and the owner) merges the outcomes dashboard (R-16), "What's new" (R-23, as "Around the world" with "AI summary · not yet reviewed") and the clinic-wide Ask Mehas chat (R-14). Charts use oocytes and count days from the first injection to trigger. Under each answer: "How did we answer your question? Rate us" with 1–5 stars (new metric: average answer rating, reported weekly with the lowest-rated questions for review).
- **Front desk Today:** each consulted patient has **Print instructions**, which opens her doctor instructions read-only with name and ID.
- **Past records:** the operator digitizes each paper file into a register (name, patient ID, file, last visit, date digitized, approver); a **junior doctor approves or sends back** each file (adds to Flow 10; the 10% second check and senior spot-checks remain).
- **Discharge summary** (R-12): prepared by the junior doctor; every field editable; print preview.
- **Due today and Daily completeness** for doctors: removed (see 2 and 6).

---

## 10. Evidence set citations (confirms 25.1)

| Source in 25.1 | Confirmed citation | Link |
|---|---|---|
| ESHRE ovarian stimulation guideline, 2025 update | ESHRE Guideline Group on Ovarian Stimulation. ESHRE guideline: ovarian stimulation for IVF/ICSI: an update in 2025. *Human Reproduction* 2026;41(4):498–514 | https://doi.org/10.1093/humrep/deag018 |
| ASRM 2023 OHSS guideline | Practice Committee of ASRM. Prevention of moderate and severe ovarian hyperstimulation syndrome: a guideline. *Fertility and Sterility* 2024;121:230–45 | https://doi.org/10.1016/j.fertnstert.2023.11.013 |
| (added) Cochrane review on antagonist protocols | Al-Inany HG et al. Gonadotrophin-releasing hormone antagonists for assisted reproductive technology. *Cochrane Database Syst Rev* 2016;(4):CD001750 | https://doi.org/10.1002/14651858.CD001750.pub4 |

The prototype's "See why" links point to these three. Guideline licensing (NFR-09, OD-28) still applies before any paid rollout.

---

## 11. Open questions added or changed

| ID | Question | Owner | Status |
|---|---|---|---|
| Q-07 (changed) | Mehas creates the patient ID at registration with the clinic code (R-30). Does the clinic already have an ID scheme Mehas must follow? | Clinic | Open |
| Q-12 | How do lab reports reach Mehas? | Meha + clinic | **Decided 10 Nov 2026: by email.** The lab emails each report to the patient and to the clinic's Mehas address; Mehas reads it, matches the patient and adds it to her record automatically. Only reports with a value it could not read clearly, or a patient it could not match, go to the nurse's Lab reports screen to check |
| Q-94 | Do the embryologist and anesthetist get logins? | Meha + clinic | **Decided 10 Nov 2026: yes** |
| Q-97 (new) | Real prices and components for the costing sheet; who at the clinic owns them | Clinic | Open |
| Q-98 (new) | India availability tags shown in "See why" (e.g. "Cetrotide and ganirelix available in India"): who verifies them, and how often? | Meha + senior doctor | Open |
| Q-99 (new) | Sample "Also today" regimen (vitamin D3 6,00,000 IU injection, calcium with D3) is demo content. Replace with the clinic's own protocol | Senior doctor | Open |
| Q-100 (new) | Should the senior doctor's comment on an approval show on the junior's and coordinator's screens? (Not built yet) | Meha | Open |

---

## 12. Known limits of the prototype (not product decisions)

- Each screen keeps its own state: approving a bill in Approvals does not update the bill inside the patient record.
- "Open record" for a similar patient always opens one sample record (Anita G.).
- Sample patients, prices, doses and staff names are made up for the demo.

---

## 13. What is still in sync (checked)

The prototype matches the PRD on: no patient-facing app; role comes from the login; doctor decides every order; AI never reads scan images; KYC kept separate; clinic rules versioned and approved; similar patients always shown with counts and "Limited data" below the minimum; cohorts by age and reserve; scan photos as "View" only when a photo exists; WhatsApp counts only; paper stays the legal record.

## 14. Change log entry (add to PRD Section 43)

| Date | Change | Reason | By |
|---|---|---|---|
| 2026-11-10 | v0.5: prototype alignment. Approvals tab (prescriptions optional, rules, prices, patient bills); suggestion shows reason + See why (patient, similar patients with records, guidelines with citations) + Also today; Agree and save, chat to say what you will do instead; no thumbs, no source chips, no "Tell the patient", no "Checks passed". New roles: assisting junior doctor, front desk, clinic operations coordinator (replaces clinic admin); anesthetist and embryologist log in. Due today and Daily completeness moved to the coordinator with end-of-day sign-off and comment. New R-28 costing sheet and bills, R-29 vitals, R-30 patient ID. Terminology: oocytes, Doctor instructions, patient record, no "champion" or lab brand on screens. Welcome rewritten: "Your AI companion for every IVF decision", value only; sign-in card says "Sign in to Mehas" with Continue with Google. Lab reports by email, added automatically (Q-12). Star rating on Insights answers | Design reviews [DR-2] | Claude, for Meha |
