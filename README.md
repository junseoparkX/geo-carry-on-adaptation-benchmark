# GEO Carry-On Adaptation Benchmark

A small e-commerce benchmark for studying whether carry-on suitcase product pages changed in ways that affect **ChatGPT-style shopping answers**, product citations, recommendation prominence, and product-specific evidence use.

This project compares three versions of product-page text:

1. **2023/2024 original archived product pages**
2. **2026 current product pages**
3. **2023/2024 GEO-style rewrites** generated from the archived pages

The project does **not** claim that firms intentionally optimized for generative engine optimization (GEO). It instead tests whether product-page text changes are associated with changes in generated shopping answers, product citations, recommendation prominence, and answer-ready product evidence.

---

## 1. Key Results

The expanded benchmark uses **20 consumer-style shopping prompts** across four prompt sets:

```text
Q1-Q5; Q6-Q10; Q11-Q15; Q16-Q20
```

Each comparison uses a **one-product replacement design**. For a target product, four products remain in the baseline condition and only the target product is replaced by the comparison condition. This replacement is repeated across all five products.

| Comparison label | Exact setup | Purpose | Interpretation |
|---|---|---|---|
| **Current over old** | 4 archived 2023/2024 pages + 1 current 2026 page | Measure the observed 2026 current-page replacement effect | Actual current-page movement |
| **GEO over old** | 4 archived 2023/2024 pages + 1 GEO-style rewrite | Measure the hypothetical GEO-style rewrite effect | Hypothetical GEO direction |
| **GEO over current** | 4 current 2026 pages + 1 GEO-style rewrite | Directly compare a GEO rewrite against the 2026 current page | Direct GEO-vs-current contrast |

Positive values mean that the replacement condition produced stronger answer behavior for the target product relative to the relevant baseline. Negative values mean that the baseline condition produced stronger answer behavior.

For **Comparison 03**, positive values mean that the GEO-style rewrite outperformed the 2026 current page. Negative values mean that the 2026 current page outperformed the GEO-style rewrite.

---

### 1.1 Comparison 01: Current over old

**Question:** What happens when one archived 2023/2024 product page is replaced with its actual 2026 current page?

**Effect definition:**

```text
current-over-old effect for product p
= metric(p in one-current + four-old replacement run)
  - metric(p in all-old baseline)
```

<div style="overflow-x:auto">

| Product | Direction label | Current-page advantage score | Δ rank score proxy | Δ citation rate | Δ first citation score | Δ top-1 cited share | Δ feature coverage | Δ PAIS | Matched prompts |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **Monos** | `current_2026_stronger` | **0.213** | 0.30 | 0.10 | 0.307 | 0.30 | 0.024 | 0.091 | 20 |
| **BÉIS** | `current_2026_stronger` | **0.078** | 0.06 | 0.15 | 0.081 | 0.10 | -0.013 | 0.027 | 20 |
| **Travelpro** | `current_2026_stronger` | **0.064** | 0.04 | 0.00 | 0.100 | 0.15 | 0.071 | 0.047 | 20 |
| **INUSA** | `similar_or_small_change` | 0.019 | 0.06 | 0.00 | 0.033 | 0.00 | -0.008 | -0.016 | 20 |
| **Delsey** | `baseline_2023_2024_stronger` | -0.079 | -0.10 | -0.10 | -0.087 | -0.05 | -0.034 | -0.057 | 20 |

</div>

**Working interpretation.** The 2026 current-page replacement strengthened answer behavior for Monos, BÉIS, and Travelpro, produced a small positive movement for INUSA, and reduced answer behavior for Delsey relative to the all-old baseline.

---

### 1.2 Comparison 02: GEO over old

**Question:** What happens when one archived 2023/2024 product page is replaced with a controlled GEO-style rewrite of that older page?

**Effect definition:**

```text
GEO-over-old effect for product p
= metric(p in one-GEO + four-old replacement run)
  - metric(p in all-old baseline)
```

<div style="overflow-x:auto">

| Product | Direction label | GEO-rewrite advantage score | Δ rank score proxy | Δ citation rate | Δ first citation score | Δ top-1 cited share | Δ feature coverage | Δ PAIS | Matched prompts |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **Monos** | `geo_rewrite_stronger` | **0.076** | 0.12 | 0.10 | 0.074 | 0.05 | 0.008 | 0.028 | 20 |
| **Travelpro** | `geo_rewrite_stronger` | **0.051** | 0.04 | 0.05 | 0.057 | 0.05 | 0.076 | 0.043 | 20 |
| **INUSA** | `similar_or_small_change` | 0.011 | 0.02 | 0.00 | 0.019 | 0.00 | 0.018 | 0.001 | 20 |
| **BÉIS** | `similar_or_small_change` | 0.008 | 0.02 | 0.05 | 0.017 | -0.05 | -0.011 | -0.020 | 20 |
| **Delsey** | `baseline_2023_2024_stronger` | -0.109 | -0.15 | -0.25 | -0.060 | 0.00 | -0.045 | -0.051 | 20 |

</div>

**Working interpretation.** The GEO-style rewrite improved answer behavior for Monos and Travelpro, produced small movements for INUSA and BÉIS, and reduced answer behavior for Delsey relative to the all-old baseline.

---

### 1.3 Comparison 03: GEO over current

**Question:** What happens when one 2026 current product page is replaced with its 2023/2024 GEO-style rewrite while the other four products remain current?

**Effect definition:**

```text
GEO-over-current effect for product p
= metric(p in one-GEO + four-current replacement run)
  - metric(p in all-current baseline)
```

<div style="overflow-x:auto">

| Product | Direction label | GEO-vs-current advantage score | Δ rank score proxy | Δ citation rate | Δ first citation score | Δ top-1 cited share | Δ feature coverage | Δ PAIS | Matched prompts |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **Travelpro** | `similar_or_small_change` | 0.021 | 0.02 | 0.05 | 0.042 | 0.00 | -0.032 | 0.009 | 20 |
| **Delsey** | `similar_or_small_change` | 0.011 | 0.03 | 0.00 | 0.019 | 0.00 | -0.018 | 0.016 | 20 |
| **BÉIS** | `similar_or_small_change` | -0.001 | 0.04 | 0.00 | 0.018 | -0.05 | -0.037 | -0.031 | 20 |
| **INUSA** | `similar_or_small_change` | -0.038 | -0.10 | -0.05 | -0.042 | 0.00 | 0.032 | 0.021 | 20 |
| **Monos** | `current_2026_stronger_than_geo_rewrite` | **-0.213** | -0.32 | -0.05 | -0.268 | -0.30 | -0.126 | -0.121 | 20 |

</div>

**Working interpretation.** In the direct GEO-vs-current comparison, Travelpro and Delsey show small positive GEO-over-current effects, BÉIS is nearly unchanged, INUSA slightly favors the 2026 current page, and Monos strongly favors the 2026 current page over the GEO-style rewrite.

---

### 1.4 Expanded 20-prompt pattern

The expanded 20-prompt benchmark suggests **heterogeneous product-level effects**:

- The 2026 current pages do **not** uniformly outperform the older pages.
- The GEO-style rewrites do **not** uniformly outperform the older pages.
- Monos shows the strongest positive current-over-old movement, but its GEO rewrite is weaker than its 2026 current page in the direct comparison.
- Travelpro shows positive movement under both current-over-old and GEO-over-old, plus a small positive GEO-over-current contrast.
- Delsey is negative under both current-over-old and GEO-over-old, suggesting that the older page may already have contained answer-ready cues.
- BÉIS shows stronger current-over-old movement than GEO-over-old movement.
- INUSA remains close to zero in the old-baseline comparisons and slightly favors the 2026 current page in the direct GEO-over-current comparison.
- The benchmark measures answer-behavior movement, not firm intent, causal GEO optimization, or general AI-search ranking changes.

---

## 2. Research Question

**Main question**

> Do current 2026 carry-on suitcase product pages produce different ChatGPT-style shopping answers compared with older 2023/2024 product pages, and do those changes resemble a hypothetical GEO-style rewrite direction?

**Operational version**

This benchmark asks a shopping assistant to answer realistic consumer questions using only provided product-page text. It then measures which products are cited, recommended, placed earlier, and described with more product-specific evidence.

---

## 3. Benchmark Overview

| Component | Description |
|---|---|
| Product category | Carry-on suitcases |
| Product count | 5 products |
| Historical source | Wayback Machine snapshots from 2023/2024 |
| Current source | Official 2026 product pages |
| Synthetic condition | GEO-style rewrite of each older page |
| Main unit of analysis | Generated shopping answers with product-label citations |
| Query scope | 20 consumer-style shopping prompts across four prompt sets |
| Main outcome | Product-level replacement effects in citation, ranking, first-citation, top-cited share, feature coverage, PAIS, and composite advantage score |
| Interpretation level | Controlled content-level answer-behavior signal, not evidence of firm intent |

---

## 4. Product Sample

The sample uses comparable hardshell or hardshell-centered carry-on suitcases for short-trip and overhead-bin travel. The goal is not strict airline-size compliance, but a comparable product group with similar luggage category, feature language, and enough visible text for website adaptation analysis.

<div style="overflow-x:auto">

| Product | Current source | Archived source | Archive date | Benchmark role | Product-level notes |
|---|---|---|---:|---|---|
| **Monos Carry-On** | Current official page | Wayback Machine snapshot | 2023-03-19 | Central modern DTC hardshell carry-on baseline | 22 × 14 × 9 in; 7.01 lb; 39.9 L; 2-5 day trip language; polycarbonate shell; TSA lock; 360-degree spinner wheels; compression pad; laundry and shoe bags |
| **BÉIS The Carry-On Roller** | Current official page | Wayback Machine snapshot | 2024-03-26 | Marketing-rich DTC comparison | 22.8 × 15.7 × 9.8 in exterior; 8.36 lb; 49-61 L; expandable capacity; TSA lock; weight indicator; compression straps; organization pouches |
| **Travelpro Platinum Elite Carry-On Hardside Spinner** | Current official page | Wayback Machine snapshot | 2024-04-14 | Traditional luggage-brand durability / engineering comparison | 23 × 14.5 × 9.5 in overall; 8.2 lb; 46 L; polycarbonate shell; aluminum corner guards; PrecisionGlide spinner system; TSA lock; USB-A/C ports; 2-inch expansion |
| **Delsey Chatelet Air 2.0 Carry-On Plus Spinner** | Current official page | Wayback Machine snapshot | 2024-07-13 | Premium/traditional luggage-brand comparison | Carry-On Plus; about 22.75 × 15 × 10 in; 44 L; 3-5 day use; SECURITECH zipper; TSA lock; corner protection; USB port; 10-year warranty |
| **INUSA Ally Hardside 20-Inch Carry-On Spinner** | Current official page | Wayback Machine snapshot | 2023-09-29 | Budget-to-mid boundary case | 20 in; 5.9 lb; 37.72 L; PC/ABS shell; 360-degree wheels; TSA/Travel Sentry lock; telescopic handle; 10-year warranty language in current page |

</div>

---

## 5. Benchmark Restrictions

| Criterion | Restriction |
|---|---|
| Category | Standard carry-on suitcase |
| Type | Hardshell or hardshell-centered carry-on luggage |
| Size range | Roughly 21-23 inches including wheels/handles; slightly larger carry-on-plus cases accepted if marketed as carry-on |
| Use case | Short trips, overhead-bin travel, airline carry-on use |
| Core features | Spinner wheels, hard shell, TSA lock or secure-lock language, durability language, packing organization |
| Price tier | Mostly mid-range to upper-mid-range; one lower-price archive-available boundary case included |
| Website requirement | Product page must include enough visible text for description, features, specs, durability, organization, and travel-use analysis |

---

## 6. Repository Structure

The repository is organized around product-page text, generated shopping answers, result tables, and publication-style figures.

```text
code/
├── carry_on_comparison01_baseline_based_current_vs_old_multi_prompt_BASELINE_TEXT_FIXED_v2.ipynb
├── carry_on_comparison02_baseline_based_geo_vs_old_FIXED.ipynb
├── carry_on_comparison03_baseline_chunks_current_vs_geo_rewrite_FIXED.ipynb
└── carry_on_make_publication_figures_from_tables_v4_one_product_replacement.ipynb

data/
├── filtered/
│   ├── old/
│   └── current/
├── geo_rewrites/
├── prompts/
├── raw_2023_2024/
├── raw_2026/
└── docs/

results/
├── shopping_answers/
│   ├── baseline/
│   ├── 01_2023_2024_original_vs_2026_current/
│   ├── 02_2023_2024_original_vs_2023_2024_geo_rewrite/
│   └── 03_2026_current_vs_2023_2024_geo_rewrite/
├── tables/
└── figures/
```

Important paths:

| Path | Purpose |
|---|---|
| `data/raw_2023_2024/` | Raw archived visible text from Wayback Machine snapshots |
| `data/raw_2026/` | Raw current visible text from official product pages |
| `data/filtered/old/` | Lightly filtered 2023/2024 product text |
| `data/filtered/current/` | Lightly filtered 2026 product text |
| `data/geo_rewrites/` | GEO-style rewrites of older product pages |
| `data/prompts/` | Prompt files used for rewriting and shopping-answer generation |
| `results/shopping_answers/baseline/` | All-old and all-current baseline answer chunks |
| `results/shopping_answers/01_2023_2024_original_vs_2026_current/` | One-product-current replacement shopping-answer outputs |
| `results/shopping_answers/02_2023_2024_original_vs_2023_2024_geo_rewrite/` | One-product-GEO replacement outputs under all-old baseline |
| `results/shopping_answers/03_2026_current_vs_2023_2024_geo_rewrite/` | One-product-GEO replacement outputs under all-current baseline |
| `results/tables/` | Generated CSV analysis outputs |
| `results/figures/` | Publication-style main and supplementary figures |

---

## 7. Source Collection and Wayback Machine Method

For each product, two webpage text sources were collected:

1. **Archived page** from the Wayback Machine, using a usable 2023 or 2024 snapshot.
2. **Current page** from the official brand website, observed on June 1, 2026.

Collection rules:

- Use the same product or the closest continuous product page when possible.
- Prefer snapshots with visible product description, feature highlights, specifications, warranty/trust language, and travel-use language.
- Exclude candidates with no usable Wayback snapshot, insufficient visible archived text, or nearly identical archived/current text for the intended adaptation comparison.
- Keep raw visible text in `raw_2023_2024/` and `raw_2026/`.
- Create lightly filtered product-content text for the main analysis.

The benchmark uses Wayback Machine snapshots only as historical webpage evidence. It does not infer company strategy or intent from the existence of page changes.

---

## 8. Text Processing Strategy

Raw product-page text often contains page noise such as navigation, cart text, repeated titles, image modal text, footer menus, reviews, and recommendation modules. The main benchmark therefore uses **lightly filtered product-content text**.

Filtering rule:

> Preserve original product wording, claims, and section order where possible. Remove webpage boilerplate, repeated UI text, reviews, unrelated recommendation modules, footer/navigation, and obvious scraping artifacts.

The filtering step is intended to reduce webpage noise while avoiding rewriting or artificially improving the original product text.

---

## 9. GEO-Style Rewrite Strategy

The GEO-style rewrite condition is a controlled hypothetical direction. Each older product page is rewritten using the same prompt.

| Constraint | Description |
|---|---|
| Format-preserving | Keep the original product title, major sections, and general layout where possible |
| E-commerce focused | Improve usefulness for generative shopping agents and product recommendation |
| Fact-preserving | Do not invent new specs, awards, reviews, ratings, warranty terms, or features |
| Comparison-ready | Surface concrete product details such as dimensions, capacity, material, lock, wheels, handle, organization, and warranty |
| Not universal templating | Do not force all brands into the same new structure |
| No fake citations | Do not add external citations, fabricated review quotes, or unsupported statistics |

Prompt files:

| File | Purpose |
|---|---|
| `geo_rewrite_prompt_ecommerce_ca.txt` | Main GEO-style rewrite prompt |
| `geo_rewrite_prompt_source_notes.txt` | Notes linking prompt design to prior GEO / e-commerce GEO literature |
| `carry_on_shopping_answer_prompt.txt` | Shopping-answer prompt used to generate answer outputs |

---

## 10. Shopping-Answer Evaluation Design

The benchmark uses **20 consumer-style carry-on shopping prompts**. The prompts are grouped into four prompt sets:

| Prompt set | Question IDs | Role |
|---|---:|---|
| Prompt set 1 | Q1-Q5 | Baseline shopping needs such as trip length, durability, mobility, packing organization, and purchase confidence |
| Prompt set 2 | Q6-Q10 | Expanded shopper scenarios and additional product-selection constraints |
| Prompt set 3 | Q11-Q15 | Additional comparison and decision-making prompts |
| Prompt set 4 | Q16-Q20 | Robustness prompts that vary shopper intent and product-selection framing |

Generated answers include product-label citations such as `[Monos]`, `[BEIS]`, `[Travelpro]`, `[Delsey]`, and `[INUSA]`.

---

## 11. Experimental Conditions

### 11.1 Baselines

| Condition | Input setup | Used for |
|---|---|---|
| All-old baseline | All five products use 2023/2024 original filtered text | Comparison 01 and Comparison 02 |
| All-current baseline | All five products use 2026 current filtered text | Comparison 03 |

The 20 prompts are stored in four chunks. The current-baseline chunks use names such as:

```text
baseline_1_curr
baseline_6_curr
baseline_11_curr
baseline_16_curr
```

These correspond to Q1-Q5, Q6-Q10, Q11-Q15, and Q16-Q20.

---

### 11.2 Comparison 01: Current over old

Purpose:

> Measure the observed 2026 current-page replacement effect.

For each product, only that product is replaced with its 2026 current page while the other four products remain in the 2023/2024 old-page condition.

Example:

| Replacement run | Input setup |
|---|---|
| Monos current replacement | Current Monos + old BÉIS + old Travelpro + old INUSA + old Delsey |
| BÉIS current replacement | Old Monos + current BÉIS + old Travelpro + old INUSA + old Delsey |

Effect definition:

```text
current-over-old effect for product p
= metric(p in one-current + four-old replacement run)
  - metric(p in all-old baseline)
```

Main output:

```text
results/tables/01_2023_2024_original_vs_2026_current_baseline_based/current_vs_baseline_delta_by_product.csv
```

---

### 11.3 Comparison 02: GEO over old

Purpose:

> Measure the hypothetical GEO-style rewrite effect.

For each product, only that product is replaced with its GEO-style rewrite while the other four products remain in the 2023/2024 old-page condition.

Example:

| Replacement run | Input setup |
|---|---|
| Monos GEO replacement | GEO Monos + old BÉIS + old Travelpro + old INUSA + old Delsey |
| BÉIS GEO replacement | Old Monos + GEO BÉIS + old Travelpro + old INUSA + old Delsey |

Effect definition:

```text
GEO-over-old effect for product p
= metric(p in one-GEO + four-old replacement run)
  - metric(p in all-old baseline)
```

Main output:

```text
results/tables/02_2023_2024_original_vs_2023_2024_geo_rewrite_baseline_based/geo_vs_baseline_delta_by_product.csv
```

---

### 11.4 Comparison 03: GEO over current

Purpose:

> Directly compare each GEO-style rewrite against the 2026 current page under an all-current baseline.

For each product, only that product is replaced with its GEO-style rewrite while the other four products remain in the 2026 current-page condition.

Example:

| Replacement run | Input setup |
|---|---|
| Monos GEO replacement under current baseline | GEO Monos + current BÉIS + current Travelpro + current INUSA + current Delsey |
| BÉIS GEO replacement under current baseline | Current Monos + GEO BÉIS + current Travelpro + current INUSA + current Delsey |

Effect definition:

```text
GEO-over-current effect for product p
= metric(p in one-GEO + four-current replacement run)
  - metric(p in all-current baseline)
```

Main output:

```text
results/tables/03_2026_current_vs_2023_2024_geo_rewrite_baseline_current_chunked_based/geo_vs_current_delta_by_product.csv
```

---

## 12. Metrics

The notebooks convert generated shopping answers into product-level metrics.

<div style="overflow-x:auto">

| Metric | Definition | Interpretation |
|---|---|---|
| `citation_rate` | Share of question answers where a product is cited at least once | How often the product is selected as supporting evidence |
| `mean_ref_count` | Average number of product citations per question | Citation intensity |
| `first_citation_score` | `1 / first_citation_index`; uncited products receive 0 | Whether the product appears early in the answer |
| `rank_score_proxy` | Citation-order-based recommendation prominence proxy | Higher means more central answer placement |
| `top1_cited_share` | Share of answers where the product is the first cited product | First-position prominence |
| `feature_coverage` | Share of predefined carry-on feature categories used in cited sentences | How much product-specific evidence appears in answers |
| `PAIS` | Product Answer Influence Score combining reference count, citation position, feature coverage, TF-IDF similarity, and n-gram overlap | Descriptive proxy for answer-level use of product text |
| `advantage_score` | Weighted composite of delta metrics | Summary of whether replacement text improved answer behavior |

</div>

### 12.1 General replacement-effect formula

For a product `p`, comparison condition `c`, baseline condition `b`, and metric `m`:

```text
Delta_m(p, c | b)
= m_p(Run[p <- c, others <- b]) - m_p(Baseline[b])
```

Where:

```text
Run[p <- c, others <- b]
= product p is replaced by condition c,
  while the other four products remain in baseline condition b.
```

Applied to the three comparisons:

```text
Current over old:
Delta_m(p, current | old)
= m_p(one-current + four-old run) - m_p(all-old baseline)

GEO over old:
Delta_m(p, GEO | old)
= m_p(one-GEO + four-old run) - m_p(all-old baseline)

GEO over current:
Delta_m(p, GEO | current)
= m_p(one-GEO + four-current run) - m_p(all-current baseline)
```

### 12.2 Composite advantage score

The benchmark summarizes product-level movement using a descriptive weighted composite:

```text
advantage_score(p) =
0.25 * Delta_rank_score_proxy(p)
+ 0.20 * Delta_citation_rate(p)
+ 0.20 * Delta_first_citation_score(p)
+ 0.15 * Delta_top1_cited_share(p)
+ 0.10 * Delta_feature_coverage(p)
+ 0.10 * Delta_PAIS(p)
```

This score is descriptive, not causal. It summarizes observed answer-behavior movement after replacing one product page with either its 2026 current version or its GEO-style rewrite.

For Comparison 03, positive values indicate that the GEO-style rewrite produced stronger answer behavior than the 2026 current page. Negative values indicate that the 2026 current page produced stronger answer behavior than the GEO-style rewrite.

---

## 13. Observed-Hypothetical GEO Alignment

To evaluate whether observed 2026 page movement resembles the hypothetical GEO-style rewrite direction, the benchmark compares the product-level **current-over-old** advantage score with the **GEO-over-old** advantage score.

In the observed-hypothetical alignment scatter plot:

```text
x-axis = GEO-over-old advantage score
y-axis = Current-over-old advantage score
point = one product
```

Interpretation:

| Region | Meaning |
|---|---|
| Upper-right | Product improves under both actual 2026 current text and hypothetical GEO-style rewrite |
| Near origin | Limited movement under both conditions |
| Opposite regions | Actual current-page movement and hypothetical GEO-style rewrite movement diverge |
| Lower-left | Both current and GEO replacement weaken answer behavior relative to the old baseline |

Current pattern:

- Monos and Travelpro show positive movement under both current-over-old and GEO-over-old comparisons.
- Delsey is negative under both current-over-old and GEO-over-old comparisons.
- BÉIS shows stronger current-over-old movement than GEO-over-old movement.
- INUSA remains close to zero.

---

## 14. Figures

Publication-style figures are generated from the result tables.

| Figure | File | Purpose |
|---|---|---|
| Figure 1 | `results/figures/main/figure1_product_effect_heatmap.pdf` | Product-level advantage scores across the three replacement comparisons |
| Figure 2 | `results/figures/main/figure2_observed_geo_alignment_scatter_single_column.pdf` | Observed current-over-old movement versus hypothetical GEO-over-old movement |
| Figure 2, full-width version | `results/figures/main/figure2_observed_geo_alignment_scatter_full_width.pdf` | Wider version for two-column LaTeX layouts |
| Figure S1 | `results/figures/supplementary/figureS1_metric_delta_heatmaps_no_colorbar.pdf` | Metric-level decomposition of replacement effects |
| Figure S2 | `results/figures/supplementary/figureS2_geo_vs_current_bar.pdf` | Direct GEO-over-current comparison |

Figure-generation notebook:

```text
code/carry_on_make_publication_figures_from_tables_v4_one_product_replacement.ipynb
```

---

## 15. Notebooks

| Notebook | Purpose | Main output |
|---|---|---|
| `carry_on_comparison01_baseline_based_current_vs_old_multi_prompt_BASELINE_TEXT_FIXED_v2.ipynb` | Compare all-old baseline against one-product 2026 current replacements | `current_vs_baseline_delta_by_product.csv` |
| `carry_on_comparison02_baseline_based_geo_vs_old_FIXED.ipynb` | Compare all-old baseline against one-product GEO-style rewrite replacements | `geo_vs_baseline_delta_by_product.csv` |
| `carry_on_comparison03_baseline_chunks_current_vs_geo_rewrite_FIXED.ipynb` | Compare all-current baseline against one-product GEO-style rewrite replacements | `geo_vs_current_delta_by_product.csv` |
| `carry_on_make_publication_figures_from_tables_v4_one_product_replacement.ipynb` | Generate publication-style main and supplementary figures from CSV tables | PDF/PNG figures under `results/figures/` |

---

## 16. Notes

These expanded 20-prompt results suggest several working observations.

1. **Current-page effects are product-specific.**  
   Monos shows the strongest current-over-old gain, followed by BÉIS and Travelpro.

2. **GEO-style rewrite effects are also product-specific.**  
   Monos and Travelpro improve under GEO-over-old, while BÉIS and INUSA remain close to zero and Delsey declines.

3. **Direct GEO-vs-current results do not show uniform GEO superiority.**  
   Travelpro and Delsey show small positive GEO-over-current effects, BÉIS is nearly unchanged, INUSA slightly favors current, and Monos strongly favors the 2026 current page.

4. **Observed current-page movement only partially aligns with hypothetical GEO-style rewrite movement.**  
   Some products move in similar directions under current and GEO replacements, while others show divergence.

5. **Original page quality may matter.**  
   A product page that already contains concrete, answer-ready information may not benefit from rewriting and may even lose useful cues.

6. **The results should be interpreted as answer-behavior signals.**  
   They show how provided product-page text affects generated shopping answers under this prompt setup. They do not prove firm intent, causal optimization, or general AI-search ranking changes.

Suggested wording:

> These expanded 20-prompt results suggest mixed product-level effects in ChatGPT-style shopping answers. Some 2026 current pages and GEO-style rewrites increase answer prominence, but the effect is not uniform and appears sensitive to how answer-ready the original page already was.

---

## 17. How to Run

### Step 1: Verify answer files

Make sure these folders exist:

```text
results/shopping_answers/baseline/
results/shopping_answers/01_2023_2024_original_vs_2026_current/
results/shopping_answers/02_2023_2024_original_vs_2023_2024_geo_rewrite/
results/shopping_answers/03_2026_current_vs_2023_2024_geo_rewrite/
```

The baseline folder should contain all-old baseline chunks and all-current baseline chunks, including:

```text
baseline_1_curr
baseline_6_curr
baseline_11_curr
baseline_16_curr
```

### Step 2: Run Comparison 01

Open and run:

```text
code/carry_on_comparison01_baseline_based_current_vs_old_multi_prompt_BASELINE_TEXT_FIXED_v2.ipynb
```

Main output:

```text
results/tables/01_2023_2024_original_vs_2026_current_baseline_based/current_vs_baseline_delta_by_product.csv
```

### Step 3: Run Comparison 02

Open and run:

```text
code/carry_on_comparison02_baseline_based_geo_vs_old_FIXED.ipynb
```

Main output:

```text
results/tables/02_2023_2024_original_vs_2023_2024_geo_rewrite_baseline_based/geo_vs_baseline_delta_by_product.csv
```

### Step 4: Run Comparison 03

Open and run:

```text
code/carry_on_comparison03_baseline_chunks_current_vs_geo_rewrite_FIXED.ipynb
```

Main output:

```text
results/tables/03_2026_current_vs_2023_2024_geo_rewrite_baseline_current_chunked_based/geo_vs_current_delta_by_product.csv
```

### Step 5: Generate figures

Open and run:

```text
code/carry_on_make_publication_figures_from_tables_v4_one_product_replacement.ipynb
```

Main outputs:

```text
results/figures/main/figure1_product_effect_heatmap.pdf
results/figures/main/figure2_observed_geo_alignment_scatter_single_column.pdf
results/figures/main/figure2_observed_geo_alignment_scatter_full_width.pdf
results/figures/supplementary/figureS1_metric_delta_heatmaps_no_colorbar.pdf
results/figures/supplementary/figureS2_geo_vs_current_bar.pdf
```

---

## 18. Limitations

| Limitation | Why it matters |
|---|---|
| Small product sample | Five products are enough for a pilot benchmark but not for broad industry claims |
| One product category | Results may not generalize beyond carry-on suitcases |
| Prompt scope | The benchmark uses 20 prompts, but results may still vary under different shopper intents, prompt wording, and model settings |
| One model/prompt setup | Generated answers may vary across LLMs, decoding settings, and repeated runs |
| Manual/product-page text extraction | Filtered text may omit some webpage context |
| Wayback snapshot quality | Historical pages vary in capture completeness and visible text quality |
| No claim of intent | The analysis cannot prove that brands intentionally optimized for GEO |
| Composite score is descriptive | The advantage score summarizes answer behavior but is not causal evidence |
| Metric weighting | The composite score depends on the chosen metric weights |
| Product-level heterogeneity | A strong original page may not benefit from rewriting, while a weaker or less structured page may benefit more |

---

## 19. Next Steps

Potential extensions:

- Add repeated LLM runs to estimate output variability.
- Test alternative shopping-answer prompts.
- Compare generated answers across multiple LLMs.
- Add text-length and feature-density controls.
- Add semantic answer similarity metrics between baseline, current, and GEO answer sets.
- Repeat the benchmark with another product category such as shoes, backpacks, toys, or grocery products.
- Explore whether product-page structure, not just content length, predicts answer-behavior gains.

---

## 20. Appendix: Candidate Links Not Used

Some candidate products were considered but excluded because they lacked usable archived text, had insufficient Wayback capture quality, or showed too little text-level change for the intended comparison.

<div style="overflow-x:auto">

| Product | Link | Reason not used |
|---|---|---|
| LEVEL8 Hegent Carry-On Luggage 20 in | Product page | No reliable usable 2023/2024 Wayback snapshot for the planned historical comparison |
| Victorinox Spectra 3.0 Frequent Flyer Carry-On | Product page | Archived/current text was not as clean for the 2023/2024 vs 2026 comparison, and the main sample already includes traditional/premium luggage-brand cases |
| July Carry On | Current page / Wayback snapshot | 2023 and 2026 text appeared too similar, or the Wayback capture did not provide enough detailed visible product text |

</div>

---

## 21. Status

Current status:

- Product sample finalized
- Wayback Machine snapshots selected
- Raw and filtered texts collected
- GEO-style rewrites generated
- 20 shopping prompts prepared
- All-old baseline answer files generated
- All-current baseline answer files generated
- Comparison 01 completed
- Comparison 02 completed
- Comparison 03 completed
- Product-level result tables generated
- Publication-style main and supplementary figures generated

Current pages observed: **June 1, 2026**.
