# Balance of Goods Audit Report

**Audit date:** 2026-11-02 (UTC)  
**Severity convention:** counts below are distinct finding classes; affected cells/records are itemized separately. A suspected title mismatch is not called a confirmed omission until technical equivalence is checked.

## 1. Executive summary

The repository contains one original workbook with **8 visible worksheets**: one consolidated balance and seven well/side-track source worksheets. The full workbook structure, formulas, dependencies, displayed cached results, item records, sheet names, merged ranges, print setup and formatting were inspected.

The audit identified a material consolidated-total discrepancy. After correcting seven incomplete well-summary formulas, the source-sheet totals recalculate to **$4,251,805.00**, while the master item-category rollup remains **$4,075,299.40**. The master is therefore **$176,505.60 below** the sum of the seven well/side-track totals. This remains clearly flagged in the corrected workbook; it was not concealed with a plug or fabricated item quantity. **The workbook does not yet fully reconcile.**

Seven well-level summary formulas omitted an entire material category; one formula in the F-20 sheet excluded a delivered quantity; 15 hard-coded zero calculation cells were restored as formulas; a malformed stray formula was removed; and 70 exact-title/unit matches missing a well-specific master formula were linked. Stale external workbook links/names were removed. Ambiguous technical-title differences and master/source mismatches remain for business-owner review.

### Finding counts (distinct finding classes)

| Severity | Identified | Fully corrected | Outstanding / partially corrected |
|---|---:|---:|---:|
| CRITICAL | 1 | 0 | 1 |
| HIGH | 4 | 3 | 1 (31 title records require technical confirmation) |
| MEDIUM | 4 | 1 | 3 |
| LOW | 1 | 1 | 0 |

The workbook contains **1,764 formulas originally** and **1,848 formulas** in the reference version after the formula restorations and removal of the malformed formula. This count includes formulas added to master cells, not just formula edits.

## 2. Original workbook and worksheet inventory

**Original/source workbook (unchanged):** `08. Total Material Balance OEOC-31.xlsx`  
**Consolidated/master worksheet:** `Total Material Balance` (184 rows x 50 used columns; its visible business table spans A:AQ).  
**Individual source worksheets (7):**

| Worksheet | Well / purpose inferred from title and worksheet data | Source final total cell |
|---|---|---|
| `Cost Breakdown-Material-12` | AZN12 | O14 (corrected to link to M24) |
| `Cost Breakdown-Material-075` | AZN075, standard | N29 (corrected to link to M37) |
| `Material Balance 127-113` | AZN113 | N19 (corrected to link to M29) |
| `Material Balance 166` | AZN166 | N16 (corrected to link to M26) |
| `Cost Breakdown-Material-F-20` | F-20 / 207 | N69 (corrected to link to M81) |
| `Cost Breakdown-Material-075 (2` | AZN075 extra work / side tracking | N21 (corrected to link to M27) |
| `Cost Breakdown-Material-122` | AZN-122 | N24 (corrected to link to M35) |

The master identifies columns for wells 12, 75, 113, 166, 207, Extra 75 and Extra 122. All seven source sheets are present. The source sheets are not structurally identical: they contain different well-specific materials, title variants, subtotal locations and side-track data. Their differences were not forcibly normalized.

## 3. Structural and data-integrity findings

### HIGH — well rollup cells omitted categories (corrected)

The master’s source-total formula at `Total Material Balance!AQ184` depends on one summary cell per source sheet. Seven of those helper summary formulas were incomplete. The cells now link to each sheet’s existing complete final total formula, preserving the original item calculations and keeping the master dynamically linked.

| Source sheet | Old summary formula / value | Corrected summary formula | Recalculated value | Omitted category/value effect |
|---|---|---|---:|---|
| `Cost Breakdown-Material-12` | `O14 = SUM(M5,M8,M14)` = $153,455 | `=M24` | $175,955 | M19 Drilling Bit &mill: +$22,500 |
| `Cost Breakdown-Material-075` | `N29 = SUM(M5,M12,M22,M24,M29)` = $374,970 | `=M37` | $400,970 | M31 Drilling Bit &mill: +$26,000 |
| `Material Balance 127-113` | `N19 = SUM(M5,M7,M11,M19)` = $313,220 | `=M29` | $380,720 | M24 Drilling Bit &mill: +$67,500 |
| `Material Balance 166` | `N16 = SUM(M5,M8,M16)` = $1,050,280 | `=M26` | $1,134,280 | M21 Drilling Bit &mill: +$84,000 |
| `Cost Breakdown-Material-F-20` | `N69 = SUM(M69,M62,M29,M13,M7)` = $2,230,160 | `=M81` | $2,073,460 | M71 Drilling Bit &mill is a negative $156,700; omitted category caused overstatement |
| `Cost Breakdown-Material-075 (2` | `N21 = SUM(M5,M12,M14,M21)` = -$10,060 | `=M27` | $15,940 | M23 Drilling Bit &mill: +$26,000 |
| `Cost Breakdown-Material-122` | `N24 = SUM(M5,M7,M13,M22,M24)` = $24,980 | `=M35` | $70,480 | M28 Drilling Bit &mill: +$45,500 |

The net change to the sum of source totals is **+$114,800**. The old helper totals summed to $4,137,005; corrected totals sum to $4,251,805. The reference version’s grand-total cells now calculate from the complete source sheet totals.

### MEDIUM — blank mandatory values

`Cost Breakdown-Material-075!D16:E16` are blank for **“Stop Collar, 4 1/2", c/w nails and pins”** (unit is `ea.`). The original provides no unit price or contract quantity. These were not invented; the source row is preserved and needs an approved value or confirmation that the row is intentionally unused.

No hidden worksheets, rows or columns were found. The workbook has **184 source detail records** and **171 master item rows** (excluding section headings). Quantities are stored as numeric values where populated; dash/text markers occur in contract/no-price fields and are retained. Negative balance/cost values follow the workbook’s existing `(used + delivered) - contract` balance convention; they were not recast as input quantity errors.

## 4. Item-title and description reconciliation

Title comparison used raw text, case/space/punctuation-normalized text, unit and a conservative similarity screen. A normalized match was accepted only when the complete title remained the same after case/spacing/punctuation normalization; near matches are candidates, not automatic equivalences.

- Source detail records: **184**.
- Exact title matches (excluding whitespace variation): **135/184**.
- Same title after case/spacing/punctuation normalization: **153/184**.
- Source records with no normalized exact title in the master: **31** (table below).
- Master item-title rows without an exact normalized source title: **66**. Many are unpopulated catalogue or well-configuration rows, but exact source support cannot be established from this workbook alone. Review is required before treating them as contractual omissions or deleting them.
- The master has **11 repeated normalized title groups**; several are repeated Section A–D headings for different well categories. Product-title repeats include rows 49–50, 51–52, 104–105, 124–125, 128–129, 134–135, and repeated drill-pipe-dart lines at 141/147/153/159/165. These occur in well-specific columns/sets and were preserved rather than merged.

### Source titles without normalized exact master matches

| Source worksheet | Source row | Item title | Unit | Master-sheet status | Required action |
|---|---:|---|---|---|---|
| Cost Breakdown-Material-075 | 13 | Centralizer, 5 " x 8 1/2", Non weld, Bow spring type, c/w nails | ea. | No normalized exact match; possible candidate master row 92 (Centralizer, 5 " x 8 1/2", Non0weld, Bow0 spring type, c/w nails), similarity 98% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-075 | 33 | 6 1/8" Rock Bit | each | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-F-20 | 15 | Casing, 7", 110S, 32 ppf Premium Conn.,seamless, R3, PLS-3. | m | No normalized exact match; possible candidate master row 41 (Casing, 7", 110S, 32 ppf Premium Conn.,seamless, R3, PLS03.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 16 | Casing, 7", TP110S, 35 ppf, TPCQ, R3 | Jt. | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-F-20 | 21 | Casing Pup Joint, 9 5/8", 110SS, 53.5 PPF, Gas Tight Conn.,seamless, 1.5m long, PSL3. | ea. | No normalized exact match; possible candidate master row 55 (Casing Pup Joint, 9 5/8", 110S, 53.5 PPF, Gas Tight Conn.,seamless, 1.5m long, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 22 | Casing Pup Joint, 9 5/8", 110SS, 53.5 PPF,Gas Tight Conn.,seamless, 3m long, PSL3. | ea. | No normalized exact match; possible candidate master row 56 (Casing Pup Joint, 9 5/8", 110S, 53.5 PPF,Gas Tight Conn.,seamless, 3m long, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 24 | Tubing pup joint, 4 1/2", L-80 type 1, 18.9 PPF, Gas Tight Conn, seamless, 1.5m, PSL3. | ea. | No normalized exact match; possible candidate master row 62 (Tubing pup joint, 4 1/2", L080 type 1, 18.9 PPF, Gas Tight Conn, seamless, 1.5m, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 25 | Crossover, 4-1/2" 18.9 PPF Box × 3-1/2" 10.2 PPF Pin, Gas Tight Conn, L-80 type1 1.2m long, PSL3. | ea. | No normalized exact match; possible candidate master row 64 (Crossover, 4 1/2" 18.9 PPF Box × 3 1/2" 10.2 PPF Pin, Gas Tight Conn, L080 type1 1.2m long, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 26 | Tubing pup joint, 3 1/2", L-80 type 1, 10.2 PPF, Gas Tight Conn, seamless, 1.5m long, PSL3. | ea. | No normalized exact match; possible candidate master row 63 (Tubing pup joint, 3 1/2", L080 type 1, 10.2 PPF, Gas Tight Conn, seamless, 1.5m long, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 27 | Tubing pup joint, 4 1/2", L-80,Gas Tight  Connection 18.9 ppf, seamless,1.5 m long , PSL3 | ea. | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-F-20 | 28 | Tubing pup joint, 3 1/2", L-80,premium Connection 10.2 ppf,13CR-1 MO, seamless,3 m long , PSL3 | ea. | No normalized exact match; possible candidate master row 67 (Tubing pup joint, 3 1/2", L080,premium Connection 10.2 ppf,13CR01 MO, seamless,3 m long , PSL3), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 41 | Float Collar, 9 5/8", 110S, premium connection, 53.5 ppf, Special drift, c/w non-rotating profile, PDC drillable, PSL3. | ea. | No normalized exact match; possible candidate master row 89 (Float Collar, 9 5/8", 110S, premium connection, 53.5 ppf, Special drift, c/w non0rotating profile, PDC drillable, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 42 | Centralizer, 9 5/8" x 12 1/4", Non-weld,Bow-spring type, c/w nails | ea. | No normalized exact match; possible candidate master row 90 (Centralizer, 9 5/8" x 12 1/4", Non0weld,Bow0spring type, c/w nails), similarity 98% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 46 | Centralizer, Bow type, 7" x 8-3/8", Non-welded | ea. | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-F-20 | 51 | Cement Plug, Top, for 9 5/8" 47-53.5#casing, oil and PH resistance element, Non- rotating type | ea. | No normalized exact match; possible candidate master row 109 (Cement Plug, Top, for 9 5/8" 47-53.5#casing, oil and PH resistance element, Non0 rotating type), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 52 | Cement Plug, Bottom, for 9 5/8" 47-53.5#casing, oil and PH resistance element, Non- rotating type | ea. | No normalized exact match; possible candidate master row 110 (Cement Plug, Bottom, for 9 5/8" 47-53.5#casing, oil and PH resistance element, Non0 rotating type), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 59 | Drift Gauge, API, for 7" 35# casing | ea. | No normalized exact match; possible candidate master row 119 (Drift Gauge, API, for 7" 32# casing), similarity 96% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 63 | Rotating liner hanger, hydraulic set, tandem cone, with integral/split, weight set top packer, 7" 32# x 9 5/8" 47-53.5#, 110S, PREMIUM connection, 10 ft PBR, load capacity 2,000KN, packer seal capacity 10,000 psi, Temperature 150 ºC | set | No normalized exact match; possible candidate master row 137 (Rotating liner hanger, hydraulic set, tandem cone, with integral/split, weight set top packer, 7" 29 32# x 9 5/8" 47 53.5#, 110S, PREMIUM connection, 10 ft PBR,load capacity 2,000KN, packer seal capacity 5000 psi, Temperature 150 ºC), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 64 | Float shoe, reamer type, 7", 32#, 110S,PREMIUM connection, PDC drillable | ea. | No normalized exact match; possible candidate master row 138 (Float shoe, reamer type, 7", 29 32#, 110S, PREMIUM connection, PDC drillable), similarity 98% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 65 | Float collar, 7", 32#, 110S, PREMIUM connection, PDC drillable | ea. | No normalized exact match; possible candidate master row 139 (Float collar, 7", 29 32#, 110S,PREMIUM connection, PDC drillable), similarity 98% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 66 | Landing collar c/w setting ball, 7", 32#, 110S,PREMIUM connection, PDC drillable | ea. | No normalized exact match; possible candidate master row 140 (Landing collar c/w setting ball, 7", 29 32#, 110S, PREMIUM connection, PDC drillable), similarity 98% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-F-20 | 72 | 26" Rock Bit | each | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-F-20 | 73 | 17-1/2" Rock Bit | each | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-F-20 | 74 | 17-1/2" PDC Bit | each | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-075 (2 | 26 | 6 1/8" Rock Bit | each | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |
| Cost Breakdown-Material-122 | 8 | Tubing pup joint, 4 1/2", L-80 type 1, 18.9 PPF, Gas Tight Conn, seamless, 1.5m, PSL3. | ea. | No normalized exact match; possible candidate master row 62 (Tubing pup joint, 4 1/2", L080 type 1, 18.9 PPF, Gas Tight Conn, seamless, 1.5m, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-122 | 9 | Tubing pup joint, 3 1/2", L-80 type 1, 10.2 PPF, Gas Tight Conn, seamless, 1.5m long, PSL3. | ea. | No normalized exact match; possible candidate master row 63 (Tubing pup joint, 3 1/2", L080 type 1, 10.2 PPF, Gas Tight Conn, seamless, 1.5m long, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-122 | 10 | Crossover, 4-1/2" 18.9 PPF Box × 3-1/2" 10.2 PPF Pin, Gas Tight Conn, L-80 type1 1.2m long, PSL3. | ea. | No normalized exact match; possible candidate master row 64 (Crossover, 4 1/2" 18.9 PPF Box × 3 1/2" 10.2 PPF Pin, Gas Tight Conn, L080 type1 1.2m long, PSL3.), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-122 | 11 | Tubing pup joint, 4 1/2", L-80,premium Connection 18.9 ppf,13CR-1 MO, seamless,3 m long , PSL3 | ea. | No normalized exact match; possible candidate master row 66 (Tubing pup joint, 4 1/2", L080,premium Connection 18.9 ppf,13CR01 MO, seamless,3 m long , PSL3), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-122 | 12 | Tubing pup joint, 3 1/2", L-80,premium Connection 10.2 ppf,13CR-1 MO, seamless,3 m long , PSL3 | ea. | No normalized exact match; possible candidate master row 67 (Tubing pup joint, 3 1/2", L080,premium Connection 10.2 ppf,13CR01 MO, seamless,3 m long , PSL3), similarity 99% | Human confirmation required: verify dimensions/specification/unit before linking or normalizing. |
| Cost Breakdown-Material-122 | 34 | 3-1/8" Mill | each | No defensible exact/normalized master match identified | Confirm whether a master line is missing; add only with approved technical description and identifier. |

Examples of close but non-identical items include the source’s `Casing, 7", 110S, 32 ppf Premium Conn.,seamless, R3, PLS-3.` (`Cost Breakdown-Material-F-20!B15`) versus master row 41 (`... PLS03.`), and the source’s 7-inch liner-hanger / float-equipment specifications which differ in rating, pressure or packer details from nearby master rows. These are not treated as the same material without technical sign-off.

**No technical descriptions, well codes or quantities were silently rewritten.** The 70 newly inserted master formulas use only unique normalized title plus matching-unit pairs; ambiguous or non-exact records were left unresolved.

## 5. Formula and dependency audit

### Corrected formulas

- Seven source grand-total helper formulas now refer to the complete final total formulas shown above (`=M24`, `=M37`, `=M29`, `=M26`, `=M81`, `=M27`, `=M35`).
- In `Cost Breakdown-Material-F-20`, row 6 previously used `I6=G6-F6` and `K6=J6-E6`, despite H6/L6 being part of the workbook’s regular calculation logic. They are now `I6=(H6+G6)-F6` and `K6=(J6+L6)-E6`; `M6` is now `=-(K6)*D6` instead of hardcoded 0. At current values these calculate to 0, but they now respond correctly to changes in inputs.
- Fifteen numeric hardcodes in calculated fields I/K/M on the F-20 and AZN-122 sheets were restored as row formulas, including F-20 `I9:I16`, `K16`, `M16`, `K46`, `M46`, `K59`, `M59`, `M6`, and AZN-122 `I30`. Existing values were zero; those cells now recalculate if inputs change.
- Seventy previously blank master cells received direct references where title and unit matched uniquely. Example: `Total Material Balance!O59 = 'Cost Breakdown-Material-075'!J6`; corresponding contract and F/PEDEC-used fields link to source E6 and G6 where applicable. Existing formulas were not overwritten.
- The malformed stray formula `Cost Breakdown-Material-075 (2!K112` contained `='Cost Breakdown-Material-075 (2'!E17q` and evaluated as `#NAME?`. It was outside the source table and has been cleared; no supported data depended on it.
- Fourteen defined names pointing to external workbooks or `#REF!` were removed, along with seven obsolete external-workbook link records. There were no remaining external references or `#REF!` formula tokens in the corrected workbook.

### Outstanding formula and aggregation risk — master does not reconcile

The master rollup `Total Material Balance!AQ183` sums category/item balances and recalculates to **$4,075,299.40**. The source total `Total Material Balance!AQ184` sums the seven corrected sheet totals and recalculates to **$4,251,805.00**. The difference `AP184 = AQ184-AQ183` is **+$176,505.60** (source sheets exceed master rollup). The master therefore fails the requested reconciliation despite the source total fixes and 70 formula links. The corrected workbook labels/highlights this variance instead of forcing the totals to agree.

The difference is not confidently attributable to one item from the available workbook because many master descriptions have no exact source title, and repeated/near-match titles contain material-specification differences. Do not approve the master total for contractual reporting until a materials owner reviews the 31 unmatched source titles, the 66 master-only title rows, and the row-by-row well allocation/receipt/use mapping, then resolves the remaining $176,505.60 variance.

## 6. Quantity and total reconciliation

The source grand totals were recalculated using a Python Excel-formula calculation engine and independently summed in Python across the seven source summary cells after the rollup formulas were repaired. Python also recalculated 165 numeric source F/PEDEC balance rows and 55 numeric contract-balance and cost rows from their inputs; no arithmetic differences were found in these applicable rows.

| Source worksheet / identifier | Recalculated final total (USD) |
|---|---:|
| AZN12 — `Cost Breakdown-Material-12` | $175,955.00 |
| AZN075 — `Cost Breakdown-Material-075` | $400,970.00 |
| AZN113 — `Material Balance 127-113` | $380,720.00 |
| AZN166 — `Material Balance 166` | $1,134,280.00 |
| F-20 / 207 — `Cost Breakdown-Material-F-20` | $2,073,460.00 |
| AZN075 extra work — `Cost Breakdown-Material-075 (2` | $15,940.00 |
| AZN-122 — `Cost Breakdown-Material-122` | $70,480.00 |
| **Source total, `AQ184`** | **$4,251,805.00** |
| **Master item/category total, `AQ183`** | **$4,075,299.40** |
| **Unreconciled variance, `AP184`** | **+$176,505.60 source over master** |

The seven source totals now include all existing source category subtotal cells. No missing item quantity was fabricated. Although the formula engine recalculated all formula results successfully, the master’s item-level allocations and individual-well quantities cannot be certified as reconciled until the variance and title mismatches are resolved.

## 7. Formatting and presentation

### LOW — print/navigation issues (corrected)

- Original master freeze pane was `X85`, leaving 84 rows above the frozen split and freezing many columns; corrected to `F4` so the headers and identifying columns remain visible.
- Original master print area ended at `A1:AQ182` and omitted the grand-total/reconciliation rows 183–184. It now includes `A1:AQ184`, with rows 1–3 repeated when printed.
- Each source print area ended one row before its visible total line. The reference version’s print areas include the respective bottom total rows; source header rows 1–4 repeat. Freeze panes are consistent at `A5` (including F-20, originally `A36`).
- Existing professional layout, merged title/header cells, fonts, borders, column widths, landscape orientation and sheet order were otherwise retained. No merges were found inside item-detail tables that would block calculations.

## 8. Corrections implemented vs. not implemented

### Implemented

1. Corrected all seven incomplete well summary totals by linking to each sheet’s existing complete final-total formula.
2. Corrected F-20 row-6 calculation logic and restored 15 hardcoded derived calculation cells as formulas.
3. Added 70 missing source links to unique exact-title/unit matches in the master.
4. Removed the invalid K112 formula and stale external links/defined names.
5. Updated master/source print areas and freeze panes; added a visible formula-driven variance label/alert at `AP183:AP184`.
6. Set automatic full recalculation on workbook open.

### Not implemented without additional information

1. No edits to the 31 unresolved source-title discrepancies or 66 master-only titles.
2. No invented value for `Cost Breakdown-Material-075!D16:E16`.
3. No balancing plug or arbitrary master row adjustment for the $176,505.60 variance.
4. No merging of repeated titles where well-specific technical/quantity allocations could be different.

## 9. Independent validation of the corrected workbook

- Opened and parsed all **8 worksheets**; all seven source sheets remain included.
- Checked formulas and references: **1,848 formulas**, no formula-cell `#REF!` tokens, no remaining external-link records/names and no `#NAME?` results in the full calculation-engine run.
- Recalculated the complete corrected workbook with the Python `formulas` calculation engine. It evaluated without formula errors; key totals and source formula cells were checked against an independent Python sum of the seven source totals.
- Performed a live dependency test in a temporary copy: increased `Cost Breakdown-Material-075!J6` from 0 to 1. The linked master cell `Total Material Balance!O59` recalculated from 0 to 1, and `AQ183` changed from $4,075,299.40 to $4,074,949.40. `AQ184` also recalculated with the source total, so the variance formula remained live.
- Workbook formulas are set to recalculate automatically when opened. No Microsoft Excel or LibreOffice executable was available in this environment, so a native Excel/LibreOffice open-save recalculation was not performed. The `formulas` Python engine result and test-copy dependency test are reported as such, not as an Excel runtime check.
- Corrected workbook loads successfully through openpyxl; original workbook remains unchanged.
- **Final reconciliation validation: FAIL / outstanding** — master and corrected source totals differ by $176,505.60.

## 10. Deliverables and repository state

- Original retained unchanged: `08. Total Material Balance OEOC-31.xlsx`
- Audit report: `Balance_of_Goods_Audit_Report.md`
- Corrected reference workbook: `Balance_of_Goods_Audited_and_Corrected.xlsx`

The reference workbook is a corrected, formula-linked working version, but it is **not certified as fully reconciled** pending human review of the outstanding item mapping and variance.
