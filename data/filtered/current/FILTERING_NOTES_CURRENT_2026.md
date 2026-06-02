# Filtering notes for 2026 current carry-on product-page texts

Purpose:
These files are lightly filtered versions of the 2026 current raw product-page text for the GEO carry-on adaptation benchmark.

Filtering principle:
Raw files are preserved separately for traceability. The benchmark should use lightly filtered product-content text so that similarity metrics are not dominated by navigation, cart modules, customer reviews, repeated media text, recommendation widgets, or footer boilerplate.

Preserved:
- Product title and core product identification
- Price or review count when directly attached to the product header
- Brand-written description
- Product feature highlights
- Product specifications, measurements, materials, capacity, and weight
- Product-specific warranty or return claims
- Brand-written detail modules that describe the product

Removed:
- Navigation menus
- Add-to-cart and quantity UI
- Payment-plan boilerplate unless part of the product header
- Media modal text and image alt-text galleries
- Bundle/complementary product cards
- Similar-style and “you may also like” modules
- Customer reviews and individual review text
- Review filters and rating distributions
- AI-generated customer-review summaries
- Footer navigation, newsletter signup, social media, payment methods, privacy/terms links
- Delsey “Concierge” chatbot prompt module, because it is a page UI/search-assistant feature rather than product-content wording

Important caution:
The filtered files are not paraphrased GEO rewrites. Original wording is preserved as much as possible. Only noise, repeated UI text, and non-product modules were removed.
