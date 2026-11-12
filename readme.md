# Loqma Cloud Kitchens — Delivery Operations & Profitability Analysis (Power BI)

**Loqma Data Story Challenge | End-to-End Operational & Financial Analytics Case Study**  
*Tools Used: Power BI Desktop (Power Query M, Star-Schema Data Modeling, DAX), Excel*

---

## 1. Executive Summary & Business Problem

**Loqma (لقمة)** is a virtual delivery-only cloud kitchen chain operating **4 branches** across Greater Cairo and Giza (**Nasr City `B01`**, **Maadi `B02`**, **Dokki `B03`**, and **Fifth Settlement `B04`**) serving **8 delivery zones (`Z01`–`Z08`)** across **3 ordering channels (`APP`, `AGG`, `PHONE`)**.

Between **April 1, 2026 and September 30, 2026** (with customer support tickets tracked through **October 1, 2026**), monthly order volume grew **2.5x** (from **1,000** to **2,500 orders/month**, totaling **10,000 placed orders** and **9,717 delivered orders**). However, customer support complaints surged **15.8x** (from **34** to **536 tickets/month**, totaling **1,273 tickets** across **1,040 distinct delivered orders**).

### Management's Core Question
> *"Does order growth mean Loqma is improving? Should we continue expanding promotions and delivery coverage next month, or pause to fix operations first? Where should we intervene, why, and what KPIs should we monitor afterward?"*

### Executive Verdict
**Pause aggressive discounting and geographic expansion immediately and prioritize targeted operational fixes in Dokki (`B03`) and Fifth Settlement (`B04`).**  
While total 6-month operating profit reached **670,307 EGP** (growing from **42,785 EGP** in April to **190,474 EGP** in September as volume absorbed **640,000 EGP** in branch fixed costs), **growth quality deteriorated sharply starting in June and July**:
- **Unit Contribution Margin Eroded by -16.3%:** Contribution per delivered order fell from **149.26 EGP** (April) to **124.99 EGP** (September).
- **SLA Delays Multiplied 27x in Rate:** Orders exceeding promised delivery times jumped from **1.13%** (April) to **30.72%** (September), totaling **1,557 delayed orders** (**16.02%** overall).
- **Complaints & Refunds Surged:** The complained order rate jumped nearly **5x** (from **3.51%** to **17.38%**), driving **28,035.88 EGP** in customer refunds (**100% of refunds** occurred on the **1,040 complained orders**).

---

## 2. Six-Month Performance Scorecard (April – September 2026)

| Month | Total Orders | Delivered Orders | Cancel Rate | Net Revenue (EGP) | Order Contrib. (EGP) | Contrib. / Order (EGP) | Fixed Costs (EGP) | Operating Profit (EGP) | Avg Prep (min) | Avg Delivery (min) | Delay Rate (%) | Complaint Rate (%) | Avg Rating |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Apr 2026** | 1,000 | 970 | 3.00% | 321,365 | 144,785 | 149.26 | 102,000 | 42,785 | 18.07 | 21.11 | 1.13% | 3.51% | 4.35 |
| **May 2026** | 1,200 | 1,173 | 2.25% | 390,714 | 172,115 | 146.73 | 102,800 | 69,315 | 18.14 | 21.47 | 1.53% | 4.01% | 4.24 |
| **Jun 2026** | 1,450 | 1,413 | 2.55% | 456,267 | 194,103 | 137.37 | 106,600 | 87,503 | 20.53 | 21.22 | 6.94% | 5.59% | 4.02 |
| **Jul 2026** | 1,750 | 1,692 | 3.31% | 539,508 | 225,115 | 133.05 | 107,400 | 117,715 | 21.02 | 24.87 | 17.49% | 12.59% | 3.79 |
| **Aug 2026** | 2,100 | 2,041 | 2.81% | 659,196 | 270,715 | 132.64 | 108,200 | 162,515 | 21.36 | 25.05 | 19.01% | 12.00% | 3.73 |
| **Sep 2026** | 2,500 | 2,428 | 2.88% | 758,663 | 303,474 | 124.99 | 113,000 | 190,474 | 24.48 | 23.47 | 30.72% | 17.38% | 3.43 |
| **Total / Avg** | **10,000** | **9,717** | **2.83%** | **3,125,712** | **1,310,307** | **134.85** | **640,000** | **670,307** | **21.24** | **23.24** | **16.02%** | **10.70%** | **3.81** |

*Note on Ratings: Customer ratings cover **34.27%** of delivered orders (`3,330 / 9,717`). Delayed orders exhibit higher rating participation (**46.56%** coverage, **1.99** avg rating) than on-time orders (**31.92%** coverage, **4.32** avg rating), reflecting negative self-selection bias.*

---

## 3. Dashboard Architecture & Interactive Features

The Power BI report is structured into **4 main story pages** plus **2 hidden analytical helper pages**:

1. **Page 1 — Executive Growth & Quality Scorecard (`نظرة عامة: هل النمو صحي؟`):**
   - 6 KPI cards with reference labels comparing volume, net revenue, order contribution, operating profit, delay rate, and complaint rate.
   - Dual-axis combo chart contrasting monthly revenue/operating profit growth against eroding unit contribution per order (`149.26 → 124.99 EGP`).
   - Service quality deterioration timeline annotated with management policy events (`V02`, `V03`, `V04`).
   - Expandable Branch & Zone Scorecard Matrix with conditional formatting and data bars.
2. **Page 2 — Operational Bottlenecks: Kitchen vs. Delivery (`التشغيل: المطبخ أم التوصيل؟`):**
   - Stacked bar breakdown of **Kitchen Prep Time (`ready_at - placed_at`)** vs. **Delivery Time (`delivered_at - ready_at`)** across all 4 branches and 8 zones.
   - 2×2 Small Multiples monthly trajectory isolating `B03`'s June kitchen spike from `B04`'s July delivery spike and `B02`'s September recovery.
   - Shift Capacity Utilization Heatmap (`Dinner` vs. `Lunch`) and Support Ticket Reason breakdown.
3. **Page 3 — Channel, Promotion & Unit Economics (`اقتصاديات القنوات والعروض`):**
   - 8-component unit economics breakdown per delivered order across channels (`PHONE`, `APP`, `AGG`) and promotions (`NONE`, `WELCOME10`, `APP20`).
   - Side-by-side comparison of **Contribution per Delivered Order** vs. **Contribution per Total Order Placed** (accounting for pre-prep cancellations).
   - Zone-level comparison of **Customer Delivery Fee Collected** vs. **Variable Rider Trip Cost**.
4. **Page 4 — Action Plan, Proof of Concept & Monitoring Matrix (`خطة التدخل والمؤشرات`):**
   - Timeline of Management Decisions (`V01`–`V04`), Maadi (`B02`) September `V04` Before/After Proof of Concept chart, Verified Facts vs. Testable Hypotheses callout, and 3-Row Action & KPI Monitoring Table.
5. **Hidden Page 5 — `Tooltip_Diagnosis` (Custom Report Page Tooltip):**
   - Appears dynamically on hover over any branch or zone to display `Prep (m)`, `Deliv (m)`, `Kitchen %`, `Delivery %`, and a live bar chart of complaint reasons.
6. **Hidden Page 6 — `Drillthrough_Zone_Orders` (Order-Level Audit):**
   - Right-click drill-through page exposing individual order timestamps, SLA promises, net contributions, and refunds sorted by highest financial leakage.

---

## 4. The Data Story — Four-Stage Narrative Arc

### Act I: The Illusion of Healthy Growth (Page 1)
- **Hook:** Did 2.5x order volume growth make Loqma a healthier business?
- **Evidence:** Top-line scale masked severe unit-level and operational decay. Between April and September, promotional discounts surged **8.2x** (`4,470 → 36,758 EGP/month`) and customer refunds jumped **8.4x** (`1,286 → 10,804 EGP/month`), cutting unit contribution from **149.26 EGP** to **124.99 EGP** per delivered order while SLA delays hit **30.72%** in September.

### Act II: Isolating Localized Hotspots vs. Systemic Performance (Page 2)
- **Question:** Is the operational breakdown chain-wide or concentrated in specific branches and shifts?
- **Evidence:** The crisis is **strictly localized to two branches (`B03` Dokki and `B04` Fifth Settlement) and peaks during the Dinner shift (`18:00–22:00`, which carries 68.3% of all demand)**:
  - **`B01` (Nasr City)** is Loqma's #1 profit engine (**209,957 EGP** operating profit on **2,321** delivered orders, **1.64%** delay rate, **4.24** rating).
  - **`B02` (Maadi)** generated **193,544 EGP** operating profit (**2.84%** overall delay rate) and achieved **0.00% delays in September**.
  - **`B03` (Dokki)** and **`B04` (Fifth Settlement)** together account for **93.3% of all delayed orders (`1,453 / 1,557`)** and **83.5% of all complaint tickets (`1,063 / 1,273`)**.

| Branch & Zone | Typical Distance | Promised SLA | Delivered Orders | Net Revenue (EGP) | Order Contrib. (EGP) | Contrib. / Order (EGP) | Fixed Costs (EGP) | Operating Profit (EGP) | Avg Prep (min) | Avg Deliv (min) | Delay Rate (%) | Complaint Rate (%) | Primary Diagnosis |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **B01 Nasr City** | **2–6 km** | **50 min** | **2,321** | **781,042** | **356,957** | **153.79** | **147,000** | **209,957** | **18.03** | **18.89** | **1.64%** | **3.96%** | **#1 Profit Benchmark** |
| ↳ `Z01` المنطقة الأولى | 2 km | 50 min | 1,751 | 592,790 | 275,855 | 157.54 | — | — | 18.06 | 16.87 | 0.00% | 3.08% | Fast kitchen & delivery |
| ↳ `Z02` الحي العاشر | 6 km | 50 min | 570 | 188,252 | 81,102 | 142.28 | — | — | 17.94 | 25.08 | 6.67% | 6.67% | Minor 6-km transit friction |
| **B02 Maadi** | **2–7 km** | **53.3 min** | **2,321** | **774,963** | **350,544** | **151.03** | **157,000** | **193,544** | **18.02** | **24.29** | **2.84%** | **4.39%** | **0.0% Sep Delays (V04 Fix)** |
| ↳ `Z03` المعادي القديمة | 2 km | 50 min | 1,806 | 605,359 | 277,405 | 153.60 | — | — | 18.05 | 22.10 | 3.65% | 4.71% | Fixed in Sep (`16.9m` deliv) |
| ↳ `Z04` زهراء المعادي | 7 km | 65 min | 515 | 169,603 | 73,139 | 142.02 | — | — | 17.93 | 31.95 | 0.00% | 3.30% | Realistic 65-min SLA buffer |
| **B03 Dokki** | **2–5 km** | **50 min** | **3,115** | **920,930** | **355,858** | **114.24** | **171,000** | **184,858** | **28.14** | **18.46** | **27.93%** | **16.79%** | **Kitchen Overload + APP20** |
| ↳ `Z05` الدقي | 2 km | 50 min | 2,406 | 716,659 | 282,601 | 117.46 | — | — | 28.06 | 17.09 | 21.86% | 13.80% | Sep prep hit `35.4m` (`37.1m` Dinner) |
| ↳ `Z06` المهندسين | 5 km | 50 min | 709 | 204,271 | 73,257 | 103.32 | — | — | 28.40 | 23.13 | 48.52% | 26.94% | Kitchen (`28.4m`) + road (`23.1m`) > 50m |
| **B04 Fifth Settlement** | **3–10 km** | **57.6 min** | **1,960** | **648,777** | **246,947** | **125.99** | **165,000** | **81,947** | **17.90** | **34.76** | **29.74%** | **16.48%** | **Delivery Bottleneck + Z08 Loss** |
| ↳ `Z07` داخل النطاق | 3 km | 50 min | 967 | 318,539 | 129,852 | 134.28 | — | — | 17.83 | 24.64 | 19.86% | 11.79% | Rider spillover (`33.2m` deliv Jul–Sep) |
| ↳ `Z08` امتداد القاهرة الجديدة | 10 km | 65 min | 993 | 330,238 | 117,095 | 117.92 | — | — | 17.97 | 44.61 | 39.38% | 21.05% | `47.2m` deliv (Jul–Sep) + 42 EGP cost |

### Act III: Opposite Operational Root Causes & Commercial Margin Leakage (Pages 2 & 3)
1. **Diagnosis 1 — `B03` (Dokki) Suffered Promo-Induced Kitchen Overload (`Event V02`):**
   - On **June 1, 2026 (`V02`)**, management launched `APP20` (20% food discount + free delivery) exclusively in `B03` and raised local marketing from `2,000` to `5,000 EGP/month`.
   - `APP20` cut unit contribution in half to **86.76 EGP per delivered order** (**84.07 EGP per total order placed**), compared to **170.99 EGP** on unpromoted `B03` app orders. Consequently, `B03` cooked **800 more delivered orders** than `B01` (`3,115` vs. `2,321`) yet earned **25,099 EGP less operating profit** (`184,858 EGP` vs. `209,957 EGP`).
   - Operationally, `B03` kept kitchen staffing fixed at **6 hours/shift (18 planned orders)**. By September, **Dinner kitchen utilization hit 118.15%** (`21.3` delivered orders/night vs. `18` capacity, exceeding capacity on **21 of 30 nights**), driving Dinner prep time from **18.40 min to 37.14 min** and Dinner delays to **71.47%**, while delivery time remained completely unchanged at **18.31 min**.
2. **Diagnosis 2 — `B04` (Fifth Settlement) Suffered Unfunded Range Expansion & Rider Spillover (`Event V03`):**
   - On **July 1, 2026 (`V03`)**, `B04` expanded order intake from the 10-km `Z08` zone (`امتداد القاهرة الجديدة`) while keeping delivery staffing fixed at **5 hours/shift (15 planned orders)**.
   - Sending riders on long `Z08` trips pushed `Z08` delivery time from **32.8 min (Apr–Jun) to 47.2 min (Jul–Sep)** (**48.0% delay rate**).
   - Worse, rider queuing spilled over into the local 3-km `Z07` zone: while `B04` kitchen prep time stayed rock-solid at **~17.9 min**, `Z07` delivery time jumped from **19.1 min (Apr–Jun) to 33.2 min (Jul–Sep)**, pushing `Z07` delays from **0.0% to 50.5%**!
   - Simultaneously, variable rider trip payouts in `B04` rose by **+8 EGP/trip** in July (`Z07`: `20 → 28 EGP`; `Z08`: `34 → 42 EGP`) against a fixed **25 EGP** customer fee—creating a direct **-17 EGP delivery loss on every `Z08` order**.
3. **Internal Proof of Concept — `B02` (Maadi) Proved Capacity Investment Works (`Event V04`):**
   - On **September 1, 2026 (`V04`)**, management increased `B02` planned delivery hours from **8 to 12 hours/shift** (`+4,000 EGP` monthly payroll).
   - Immediately in September, `B02` average delivery time dropped from **25.77 min to 19.11 min**, `B02` delays fell from **4.40% to 0.00%**, and monthly operating profit increased from **48,194 EGP to 51,211 EGP**.

---

## 5. Verified Dataset Facts vs. Testable Hypotheses

| Finding / Observation | Classification | Exact Dataset Evidence | Operational & Analytical Implication |
| :--- | :--- | :--- | :--- |
| **100% of customer refunds (`28,035.88 EGP`) occur on the 1,040 complained orders** | **Verified Fact** | Cross-tabulating `refund_egp > 0` with `has_complaint` yields an exact `1,040 / 1,040` match (`0` uncomplained orders received refunds). Delayed orders account for `767` complained orders (`18,258.16 EGP` in refunds). | Eliminating SLA delays in `B03` and `B04` directly removes **65.1%** of all refund leakage. |
| **All 233 "Cold Food" (`الطعام بارد`) tickets are secondary tickets on delayed orders** | **Verified Fact** | Every single `الطعام بارد` ticket (`233`) was logged on an order that also logged a `تأخر التوصيل` ticket (`233` delayed orders × 2 tickets = `466` tickets). | Cold food is not a kitchen cooking temperature failure—it is a byproduct of excessive wait/transit delays (`78.6%` of all `1,273` tickets are delay-driven). |
| **`B03`'s bottleneck is 100% in kitchen prep (especially Dinner), whereas `B04`'s is 100% in delivery** | **Verified Fact** | `B03` Dinner prep rose `18.4m → 37.1m` (`118.1%` util) while delivery stayed `18.3m`. `B04` prep stayed `17.9m` while delivery jumped to `47.2m` (`Z08`) and `33.2m` (`Z07`). | Adding riders in `B03` or kitchen staff in `B04` would misallocate capital; interventions must match each branch's specific constraint. |
| **Cause of `Z07` order volume dip in July (`219` in Jun → `106` in Jul)** | **Hypothesis to Test** | `Z07` delivered volume fell `-51.6%` in July the exact month `V03` expanded `Z08` (`70 → 213`), before partially recovering to `153` in September. | *Hypothesis:* Either dispatch/app visibility favored `Z08` when `B04` riders were saturated, or `Z07` repeat customers churned due to sudden 50% delays. Requires app session/dispatch logs to verify. |
| **Demand retention when restructuring `APP20` and repricing `Z08` delivery fees** | **Hypothesis to Test** | Observational data shows `B03` grew from `321` delivered orders (May) to `915` (Sep) (`473` `APP20`, `382` `NONE`, `60` `WELCOME10`). | *Hypothesis:* Restricting `APP20` to off-peak Lunch shifts (or a 10% cap) and raising `Z08` delivery fees to `40 EGP` will retain `70%–80%` of volume at positive unit economics. Requires A/B testing. |

---

## 6. Top 3 Prioritized Recommendations & Monitoring Plan

| Priority & Target | Concrete Intervention (Where & Why) | Supporting Dataset Evidence | Conditional Expected Impact (Monthly) | Primary Monitoring KPIs |
| :--- | :--- | :--- | :--- | :--- |
| **1. De-bottleneck `B03` (Dokki) Kitchen & Restructure `APP20`** | **A)** Expand `B03` Dinner kitchen staffing from `6h` (`18` cap) to `10–12h` (`30–36` cap), partially reallocating idle Lunch hours (`51.3%` Sep util). **B)** Restrict `APP20` to Lunch shifts or a 10% discount cap (charging normal `25 EGP` delivery at Dinner) and reduce `B03` local marketing from `5,000` to `2,000 EGP`. | `B03` Dinner kitchen hit `118.15%` utilization in Sep (`37.14m` prep, `71.47%` delay rate, `5,959 EGP` refunds). `APP20` yields `86.76 EGP/delivered order` (`84.07 EGP/total order`) vs `170.99 EGP` on unpromoted `B03` App orders. | *Assuming `+4,000 EGP/mo` payroll (modeled on `B02` `V04`) and 70% retention of `APP20` volume at `WELCOME10` margins:* Cuts `B03` prep time to `~19m` and delays to `<5%`, saves `~4,500 EGP/mo` in refunds + `3,000 EGP` marketing, and adds **`+15,000 to +22,000 EGP/month`** in net operating profit. | • `B03 Dinner Kitchen Util %` (`<80%`) • `B03 Avg Prep Minutes` (`<20 min`) • `B03 Contrib. / Delivered Order` (`>135 EGP`) |
| **2. Expand `B04` (Fifth Settlement) Delivery Fleet & Reprice `Z08`** | **A)** Increase `B04` delivery shift hours from `5h` (`15` cap) to `9–10h` (`27–30` cap), prioritizing Dinner (`70.2%` util with 10-km trips). **B)** Raise `Z08` (10 km) delivery fee from `25 EGP` to `40 EGP` (matching the `42 EGP` rider trip cost) or cap `Z08` intake during Dinner peak. | `V03` pushed `Z08` delivery time to `47.28m` (Sep) and spilled over to `Z07` (`19.1m → 33.2m`, `50.5%` Jul–Sep delays, `3,256 EGP` Sep refunds). Every `Z08` order loses `-17 EGP` on delivery (`25 EGP` fee vs `42 EGP` cost = `-5,525 EGP` loss in Sep). | *Assuming `+4,000 EGP/mo` rider payroll and 80% `Z08` retention at a `40 EGP` fee:* Eliminates `Z07` rider spillover (`0%` `Z07` delays), cuts overall `B04` delays from `49%` to `<5%`, and recovers **`~6,400 EGP/month`** in delivery deficits and delay refunds. | • `Z07 & Z08 Avg Delivery Mins` (`<22m` / `<35m`) • `B04 Delay Rate %` (`<5%`) • `Z08 Net Delivery Margin` (`Charge - Cost >= -2 EGP`) |
| **3. Optimize Channel Mix (`AGG` → Direct) & Pre-Dispatch QA** | **A)** Discontinue `WELCOME10` discounts on `AGG` (where 10% discount + 22% commission reduces contribution to `70.02 EGP/order` in `B04`) and place in-bag flyers migrating repeat `AGG` users to `APP`/`PHONE`. **B)** Introduce a pre-dispatch bag-check checklist for multi-meal baskets. | `AGG` charges `243,198.56 EGP` in commissions (22% of gross basket), yielding `104.62 EGP/delivered order` vs `144.26 EGP` on `APP` and `175.00 EGP` on `PHONE`. The `273` on-time accuracy/packaging complaints cost `9,777.72 EGP` in avoidable refunds. | *Assuming 15% migration of `AGG` orders to direct `APP` (no promo) and 50% reduction in packing/accuracy errors:* Gains `+39 to +65 EGP` per migrated order (**`+8,000 to +12,000 EGP/month`**) and saves **`~800 EGP/month`** in non-delay refunds. | • `Direct Channel Share % (APP + PHONE)` (`>70%`, up from `63.6%`) • `Non-Delay Quality Complaint Rate %` (`<1.5%`, down from `2.81%`) |

---

## 7. Data Model & Key DAX Engineering Highlights

To prevent multi-grain double-counting across the 4 fact tables (`Orders` at order grain, `Complaints` at ticket grain, `Staffing` at daily-shift grain, and `Branch_Costs` at monthly-branch grain), the Power BI model enforces strict star-schema best practices:

- **Ticket-to-Order Pre-Aggregation:** Because `233` delayed orders generated `2` support tickets each (`1,273` tickets across `1,040` unique complained orders), `Complaints` is linked `1:*` from `Orders[order_id]`, and `Complained Orders` uses `CALCULATE(DISTINCTCOUNT(Complaints[order_id]), Orders[status] = "Delivered")`.
- **Fixed-Cost Grain Guardrail (`Branch_Costs`):** Since `Branch_Costs` (`640,000 EGP`) is recorded strictly at the `Branch × Month` level, `Branch Fixed Costs (EGP)` and `Operating Result (EGP)` automatically return `BLANK()` when filtered by unallocated dimensions (`Channel`, `Promo`, `Zone`, `Shift`, or `Customer Segment`), preventing false fixed-cost allocation.
- **Shift-Level Capacity Binding (`TREATAS`):** Passes filter context from `Orders[shift]` (`Lunch` vs. `Dinner`) to `Staffing[shift]` via `TREATAS(VALUES(Orders[shift]), Staffing[shift])`, accurately exposing `B03`'s **118.15% Dinner kitchen utilization** in September.
