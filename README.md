# GEO Carry-On Adaptation Benchmark

A small e-commerce benchmark for studying whether carry-on suitcase product pages changed in ways that affect **ChatGPT-style shopping answers**, product citations, and recommendation prominence.

This project compares three versions of product-page text:

1. **2023/2024 original archived product pages**
2. **2026 current product pages**
3. **2023/2024 GEO-style rewrites** generated from the archived pages

The project does **not** claim that firms intentionally optimized for GEO. It instead tests whether product-page text changes are associated with changes in generated shopping answers, product citations, recommendation prominence, and answer-ready product evidence.

---

## 1. Research Question

**Main question**

> Do current 2026 carry-on suitcase product pages produce different ChatGPT-style shopping answers compared with older 2023/2024 product pages, and do those changes resemble a hypothetical GEO-style rewrite direction?

**Operational version**

This benchmark asks a shopping assistant to answer realistic consumer questions using only provided product-page text. It then measures which products are cited, recommended, placed earlier, and described with more product-specific evidence.

---

## 2. Benchmark Overview

| Component | Description |
|---|---|
| Product category | Carry-on suitcases |
| Product count | 5 products |
| Historical period | 2023/2024 archived pages |
| Current period | 2026 current pages |
| Synthetic condition | GEO-style rewrite of each older page |
| Main unit of analysis | Generated shopping answers with product citations |
| Main outcome | Change in product citation and recommendation behavior |
| Current query scope | 5 consumer-style shopping questions |
| Interpretation level | Pilot content-level signal, not evidence of firm intent |

---

## 3. Selected 5-Product Benchmark Group

The sample uses comparable hardshell or hardshell-centered carry-on suitcases for short-trip and overhead-bin travel. The goal is not strict airline-size compliance, but a comparable product group with similar luggage category, feature language, and enough visible text for website adaptation analysis.

| Product | Archive date | Benchmark role | Product-level notes |
|---|---:|---|---|
| **Monos Carry-On** | 2023-03-19 | Central modern DTC hardshell carry-on baseline | 22 × 14 × 9 in; 7.01 lb; 39.9 L; 2–5 day trip language; polycarbonate shell; TSA lock; 360-degree spinner wheels; compression pad; laundry and shoe bags |
| **BÉIS The Carry-On Roller** | 2024-03-26 | Marketing-rich DTC comparison | 22.8 × 15.7 × 9.8 in exterior; 8.36 lb; 49–61 L; expandable capacity; TSA lock; weight indicator; compression straps; organization pouches |
| **Travelpro Platinum Elite Carry-On Hardside Spinner** | 2024-04-14 | Traditional luggage-brand durability / engineering comparison | 23 × 14.5 × 9.5 in overall; 8.2 lb; 46 L; polycarbonate shell; aluminum corner guards; PrecisionGlide spinner system; TSA lock; USB-A/C ports; 2-inch expansion |
| **Delsey Chatelet Air 2.0 Carry-On Plus Spinner** | 2024-07-13 | Premium/traditional luggage-brand comparison | Carry-On Plus; about 22.75 × 15 × 10 in; 44 L; 3–5 day use; SECURITECH zipper; TSA lock; corner protection; USB port; 10-year warranty |
| **INUSA Ally Hardside 20-Inch Carry-On Spinner** | 2023-09-29 | Budget-to-mid boundary case | 20 in; 5.9 lb; 37.72 L; PC/ABS shell; 360-degree wheels; TSA/Travel Sentry lock; telescopic handle; 10-year warranty language in current page |

---

## 4. Benchmark Restrictions

| Criterion | Restriction |
|---|---|
| Category | Standard carry-on suitcase |
| Type | Hardshell or hardshell-centered carry-on luggage |
| Size range | Roughly 21–23 inches including wheels/handles; slightly larger carry-on-plus cases accepted if marketed as carry-on |
| Use case | Short trips, overhead-bin travel, airline carry-on use |
| Core features | Spinner wheels, hard shell, TSA lock or secure-lock language, durability language, packing organization |
| Price tier | Mostly mid-range to upper-mid-range; one lower-price archive-available boundary case included |
| Website requirement | Product page must include enough visible text for description, features, specs, durability, organization, and travel-use analysis |

---

## 5. Repository Structure

```text
code/
└── data/
    ├── filtered/
    │   ├── old/
    │   └── current/
    ├── geo_rewrites/
    ├── prompts/
    ├── raw_2023_2024/
    ├── raw_2026/
    ├── docs/
    └── results/
        ├── shopping_answers/
        │   ├── baseline/
        │   │   └── baseline.txt
        │   ├── 01_2023_2024_original_vs_2026_current/
        │   ├── 02_2023_2024_original_vs_2023_2024_geo_rewrite/
        │   └── 03_2026_current_vs_2023_2024_geo_rewrite/
        └── tables/
```

Important paths:

| Path | Purpose |
|---|---|
| [`code/data/raw_2023_2024/`](code/data/raw_2023_2024/) | Raw archived visible text |
| [`code/data/raw_2026/`](code/data/raw_2026/) | Raw current visible text |
| [`code/data/filtered/old/`](code/data/filtered/old/) | Lightly filtered 2023/2024 product text |
| [`code/data/filtered/current/`](code/data/filtered/current/) | Lightly filtered 2026 product text |
| [`code/data/geo_rewrites/`](code/data/geo_rewrites/) | GEO-style rewrites of older product pages |
| [`code/data/prompts/`](code/data/prompts/) | Prompt files used for rewriting and shopping-answer generation |
| [`code/data/results/shopping_answers/baseline/baseline.txt`](code/data/results/shopping_answers/baseline/baseline.txt) | All-original 2023/2024 baseline shopping-answer output |
| [`code/data/results/shopping_answers/01_2023_2024_original_vs_2026_current/`](code/data/results/shopping_answers/01_2023_2024_original_vs_2026_current/) | One-product-current replacement shopping-answer outputs |
| [`code/data/results/shopping_answers/02_2023_2024_original_vs_2023_2024_geo_rewrite/`](code/data/results/shopping_answers/02_2023_2024_original_vs_2023_2024_geo_rewrite/) | One-product-GEO replacement shopping-answer outputs |
| [`code/data/results/tables/`](code/data/results/tables/) | Generated CSV analysis outputs |

---

## 6. Text Processing Strategy

Raw product-page text often contains page noise such as navigation, cart text, repeated titles, image modal text, footer menus, reviews, and recommendation modules. The main benchmark therefore uses **lightly filtered product-content text**.

Filtering rule:

> Preserve original product wording, claims, and section order where possible. Remove webpage boilerplate, repeated UI text, reviews, unrelated recommendation modules, footer/navigation, and obvious scraping artifacts.

The filtering step is intended to reduce webpage noise while avoiding rewriting or artificially improving the original product text.

---

## 7. GEO-Style Rewrite Strategy

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
| [`geo_rewrite_prompt_ecommerce_ca.txt`](code/data/prompts/geo_rewrite_prompt_ecommerce_ca.txt) | Main GEO-style rewrite prompt |
| [`geo_rewrite_prompt_source_notes.txt`](code/data/prompts/geo_rewrite_prompt_source_notes.txt) | Notes linking prompt design to prior GEO / e-commerce GEO literature |
| [`carry_on_shopping_answer_prompt.txt`](code/data/prompts/carry_on_shopping_answer_prompt.txt) | Shopping-answer prompt used to generate answer outputs |

---

## 8. Shopping-Answer Evaluation Design

The benchmark currently uses five consumer-style carry-on questions.

| Question | Shopper intent |
|---|---|
| Q1 | 3–5 day trip and carry-on suitability |
| Q2 | Durability and protection |
| Q3 | Mobility through airports, streets, and crowded spaces |
| Q4 | Packing capacity and organization |
| Q5 | Purchase confidence: size, lock/security, warranty/trial, and limitations |

Generated answers include product-label citations such as `[Monos]`, `[BEIS]`, `[Travelpro]`, `[Delsey]`, and `[INUSA]`.

Important note:

> The current analysis is based on only five shopping questions. These results should be treated as preliminary. Future runs should add more consumer queries, different trip-use cases, and prompt variations before making stronger claims.

---

## 9. Experimental Conditions

### 9.1 Baseline

| Condition | Input setup | Output file |
|---|---|---|
| All-original baseline | All five products use 2023/2024 original filtered text | [`baseline.txt`](code/data/results/shopping_answers/baseline/baseline.txt) |

### 9.2 Comparison 01: Original vs Current

Purpose:

> Check how much the actual product page changed over time.

Design:

| File pattern | Meaning |
|---|---|
| `beis_2023vs2026.txt` | BÉIS uses 2026 current text; the other four products use 2023/2024 original text |
| `delsey_2023vs2026.txt` | Delsey uses 2026 current text; the other four products use 2023/2024 original text |
| `inusa_2023vs2026.txt` | INUSA uses 2026 current text; the other four products use 2023/2024 original text |
| `monos_2023vs2026.txt` | Monos uses 2026 current text; the other four products use 2023/2024 original text |
| `travel_2023vs2026.txt` | Travelpro uses 2026 current text; the other four products use 2023/2024 original text |

Effect definition:

```text
current effect for product p
= metric(p in one-product-current run) - metric(p in all-original baseline)
```

### 9.3 Comparison 02: Original vs GEO-Style Rewrite

Purpose:

> Check how a GEO-style rewrite changes the older page.

Design:

| File pattern | Meaning |
|---|---|
| `beis_2023_2024vsGEO.txt` | BÉIS uses GEO-style rewrite; the other four products use 2023/2024 original text |
| `delsey_2023_2024vsGEO.txt` | Delsey uses GEO-style rewrite; the other four products use 2023/2024 original text |
| `inusa_2023_2024vsGEO.txt` | INUSA uses GEO-style rewrite; the other four products use 2023/2024 original text |
| `monos_2023_2024vsGEO.txt` | Monos uses GEO-style rewrite; the other four products use 2023/2024 original text |
| `travel_2023_2024vsGEO.txt` | Travelpro uses GEO-style rewrite; the other four products use 2023/2024 original text |

Effect definition:

```text
GEO rewrite effect for product p
= metric(p in one-product-GEO run) - metric(p in all-original baseline)
```

### 9.4 Comparison 03: Current vs GEO-Style Rewrite

Purpose:

> Check whether the current 2026 page moved closer to the GEO-style rewrite.

This comparison is the main detection test and can be added after Comparisons 01 and 02 are finalized.

---

## 10. Metrics

The notebooks convert generated shopping answers into product-level metrics.

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

Composite score:

```text
advantage_score =
0.25 * delta_rank_score_proxy
+ 0.20 * delta_citation_rate
+ 0.20 * delta_first_citation_score
+ 0.15 * delta_top1_cited_share
+ 0.10 * delta_feature_coverage
+ 0.10 * delta_PAIS
```

This score is descriptive, not causal. It summarizes observed answer-behavior movement after replacing one product page with either its 2026 current version or its GEO-style rewrite.

---

## 11. Notebooks

| Notebook | Purpose | Main output |
|---|---|---|
| [`carry_on_comparison01_baseline_based_current_vs_old.ipynb`](code/carry_on_comparison01_baseline_based_current_vs_old.ipynb) | Compare all-original baseline against one-product 2026 current replacements | `current_vs_baseline_delta_by_product.csv` |
| [`carry_on_comparison02_baseline_based_geo_vs_old.ipynb`](code/carry_on_comparison02_baseline_based_geo_vs_old.ipynb) | Compare all-original baseline against one-product GEO-style rewrite replacements | `geo_vs_baseline_delta_by_product.csv` |

---

## 12. Preliminary Results

### 12.1 Comparison 01: 2023/2024 Original Baseline vs 2026 Current

| Product | Direction label | Advantage score | Note |
|---|---|---:|---|
| Monos | `current_2026_stronger` | 0.163 | 2026 current text increased answer prominence |
| BÉIS | `current_2026_stronger` | 0.132 | 2026 current text increased citation and answer visibility |
| INUSA | `similar_or_small_change` | -0.007 | Little observed change |
| Travelpro | `similar_or_small_change` | -0.014 | Little observed change; older page may already have been answer-ready |
| Delsey | `baseline_2023_2024_stronger` | -0.082 | Older page produced stronger answer behavior |

### 12.2 Comparison 02: 2023/2024 Original Baseline vs GEO-Style Rewrite

| Product | Direction label | Advantage score | Note |
|---|---|---:|---|
| Monos | `geo_rewrite_stronger` | 0.137 | GEO rewrite improved answer prominence |
| BÉIS | `geo_rewrite_stronger` | 0.121 | GEO rewrite improved answer visibility |
| Travelpro | `geo_rewrite_stronger` | 0.102 | GEO rewrite improved answer behavior |
| INUSA | `similar_or_small_change` | -0.006 | Little observed change |
| Delsey | `baseline_2023_2024_stronger` | -0.467 | GEO rewrite substantially reduced answer prominence |

---

## 13. Notes

These preliminary results suggest several working observations.

1. **The 2026 current pages do not uniformly outperform the older pages.**  
   Monos and BÉIS gain answer prominence relative to the all-original baseline, while INUSA and Travelpro remain close to baseline and Delsey declines.

2. **The GEO-style rewrite is also product-dependent.**  
   Monos, BÉIS, and Travelpro improve under the GEO-style rewrite condition, INUSA remains close to baseline, and Delsey declines strongly.

3. **Original page quality matters.**  
   Delsey’s older page already contains direct, concrete, answer-ready information such as trip length, volume, organization details, zipper/security language, warranty language, and airline-fit warnings. A rewrite may reduce performance if it weakens or redistributes those useful cues.

4. **The current query set is small.**  
   The current shopping-answer results are based on five consumer questions only. More queries are needed before making stronger claims about product-page adaptation, GEO-style movement, or category-level patterns.

5. **The results should be interpreted as answer-behavior signals.**  
   They show how provided product-page text affects generated shopping answers under this prompt setup. They do not prove firm intent, causal optimization, or general AI-search ranking changes.

Suggested wording:

> These preliminary results suggest mixed product-level effects in ChatGPT-style shopping answers. Some 2026 current pages and GEO-style rewrites increase answer prominence, but the effect is not uniform and appears sensitive to how answer-ready the original page already was.

---

## 14. How to Run

### Step 1: Verify answer files

Make sure these files exist:

```text
code/data/results/shopping_answers/baseline/baseline.txt
code/data/results/shopping_answers/01_2023_2024_original_vs_2026_current/
code/data/results/shopping_answers/02_2023_2024_original_vs_2023_2024_geo_rewrite/
```

### Step 2: Run Comparison 01

Open and run:

```text
code/carry_on_comparison01_baseline_based_current_vs_old.ipynb
```

Main output:

```text
code/data/results/tables/01_2023_2024_original_vs_2026_current_baseline_based/current_vs_baseline_delta_by_product.csv
```

### Step 3: Run Comparison 02

Open and run:

```text
code/carry_on_comparison02_baseline_based_geo_vs_old.ipynb
```

Main output:

```text
code/data/results/tables/02_2023_2024_original_vs_2023_2024_geo_rewrite_baseline_based/geo_vs_baseline_delta_by_product.csv
```

### Step 4: Compare observed vs hypothetical movement

After both CSVs are available, compare:

```text
current_page_advantage_score
vs
geo_rewrite_advantage_score
```

This helps evaluate whether observed 2026 changes resemble the hypothetical GEO rewrite direction.

---

## 15. Limitations

| Limitation | Why it matters |
|---|---|
| Small sample | Five products are enough for a pilot benchmark but not for broad industry claims |
| Small query set | Current results use five shopping questions only; more consumer queries are needed |
| One product category | Results may not generalize beyond carry-on suitcases |
| One model/prompt setup | Shopping-answer outputs may vary across models, prompts, and runs |
| Manual/product-page text extraction | Filtered text may omit some webpage context |
| No claim of intent | The analysis cannot prove that brands intentionally optimized for GEO |
| Composite score is descriptive | The advantage score summarizes answer behavior but is not causal evidence |
| Product-level heterogeneity | A strong original page may not benefit from rewriting, while a weaker or less structured page may benefit more |

---

## 16. Next Steps

Potential extensions:

- Add more consumer shopping queries beyond the current five.
- Add **Comparison 03**: 2026 current vs 2023/2024 GEO-style rewrite.
- Compute **Observed-Hypothetical Directional Alignment** between current-page movement and GEO-rewrite movement.
- Add semantic answer similarity metrics between baseline, current, and GEO answer sets.
- Repeat the benchmark with another product category such as shoes, backpacks, toys, or grocery products.
- Test multiple shopping-answer prompts to check robustness.
- Compare generated answers across multiple LLMs.
- Add repeated runs to estimate output variability.

---

## 17. Appendix: Candidate Links Not Used

Some candidate products were considered but excluded because they lacked usable archived text, had insufficient Wayback capture quality, or showed too little text-level change for the intended comparison.

| Product | Link | Reason not used |
|---|---|---|
| LEVEL8 Hegent Carry-On Luggage 20 in | [Product page](https://www.level8cases.com/products/hegent-carry-on-luggage-20?variant=44474106052831) | No reliable usable 2023/2024 Wayback snapshot for the planned historical comparison |
| Victorinox Spectra 3.0 Frequent Flyer Carry-On | [Product page](https://www.victorinox.com/en-US/Products/Travel-Gear/Carry-On-Bags/Spectra-30-Frequent-Flyer-Carry-On/p/611756/) | Archived/current text was not as clean for the 2023/2024 vs 2026 comparison, and the main sample already includes traditional/premium luggage-brand cases |
| July Carry On | [Current page](https://july.com/us/luggage/carry-on/?moss=) / [Wayback snapshot](https://web.archive.org/web/20231127143310/https://july.com/us/luggage/carry-on/?moss=) | 2023 and 2026 text appeared too similar, or the Wayback capture did not provide enough detailed visible product text |

---

## 18. Status

Current status:

- Product sample finalized
- Raw and filtered texts collected
- GEO-style rewrites generated
- Shopping-answer prompt created
- Baseline answer file added
- Comparison 01 notebook created
- Comparison 02 notebook created
- Preliminary result tables generated
- More consumer queries still needed for stronger robustness

Current pages observed: **June 1, 2026**.
