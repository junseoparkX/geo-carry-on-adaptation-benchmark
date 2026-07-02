GEO Nike Product Page Detection Package

Folder structure

original_text/
Stores raw original text captures for reproducibility.
Includes restriction notes explaining why raw text should not be used directly as the main cosine similarity input.

filtered_text/
Stores cleaned, same-topic, product-specific text after excluding likely scraping noise and duplicated boilerplate.
These are the recommended inputs for cosine similarity and feature comparison.

prompts/
Stores prompts that use only filtered text as input.
The 2023 prompt creates a GEO-consistent reference rewrite.
The 2026 prompt extracts GEO-relevant features without rewriting.
The difference-only prompt compares only meaningful product-specific differences.

output/
Empty folder reserved for generated outputs.
Suggested future output file:
2023_Nike_Air_Force_1_GEO_reference_rewrite_output.txt

Recommended workflow

1. Keep original_text unchanged for reproducibility.
2. Use filtered_text as the analysis input.
3. Run prompts/01_2023_filtered_text_to_GEO_reference_rewrite_prompt.txt to generate the 2023 GEO-reference rewrite.
4. Save the generated rewrite into output/2023_Nike_Air_Force_1_GEO_reference_rewrite_output.txt.
5. Compute cosine similarity:
   - 2026 filtered current vs 2023 filtered original
   - 2026 filtered current vs 2023 GEO-reference rewrite output
6. Use prompts/03_difference_only_filtered_comparison_prompt.txt for feature-level interpretation.
