# FashionHero Reach — Smoke Test Landing · Project Config

PROJECT: FashionHero Reach — Smoke Test Landing
ROLE: Buduje single-page smoke-test landing page dla "FashionHero Reach" — productized sponsored listings + Offsite Ads dla sellersów FashionHero. Cel: walidacja czy sellersi opt-in'ują się przy transparent take-rate model.

## Cel aplikacji

Landing page kierowany do sellersów FashionHero (B2B, ~4 200 niezależnych sklepów modowych w PL). Zbiera waitlist emails dla early access do FH Reach. Page NIE buduje funkcjonalności sponsored-ads — tylko testuje desirability (czy seller zostawia email).

## Wytyczne designu

- Czysta, nowoczesna estetyka marketplace. Think Zalando, nie Allegro.
- Mobile-first responsive (320px → 1920px).
- Brand tokens spójne z FashionHero Plus prototype: tło `#FAFAF7`, navy primary `#1F2940`, brass accent `#B8956A`, ink `#1A1A1F`, muted `#5C5C66`, line `#E6E4DC`.
- System font stack + Inter fallback. Generous whitespace. Soft shadows.
- Reuse design tokens z Q1.3 (Plus). Same vibe, różny audience (sellersi, nie kupujący).

## Granice

### ALWAYS
- Polish UI only, no English placeholders, no Lorem Ipsum.
- Form intercept przez JS, success state inline (Q1.3 pattern).
- LocalStorage logging dla future PostHog wiring (Q4.1): zapisuj `{email, timestamp, source: "hero" | "cta-band"}`.

### ASK FIRST
- Przed dodaniem zewnętrznych integracji (Stripe, real analytics) — to smoke test, nie real product.
- Przed zmianą core value prop (16-18% take rate na paid traffic vs 22% standardowa) — to jest hypothesis.

### NEVER
- Nie buduj rzeczywistej funkcjonalności sponsored ads — page tylko zbiera intent.
- Nie dodawaj seller dashboard / account creation / payment flow — out of scope smoke test.
- Nie używaj real imion sellersów w testimonialach — fictional brands only (credible-but-fabricated case-study cards).

## Reguły domenowe

- Sellersi FashionHero to niezależne sklepy modowe (4 200 globally), nie pracownicy.
- Średnia prowizja standard 22%; top sellerzy (~150 z 4 200) negocjują do 14-18%.
- **Reach take rate proposal:** 16% (top tier, dla GMV > 35K) lub 18% (volume tier, GMV 5-35K) **na sprzedaży z paid traffic** — vs 22% standardowa prowizja.
- Quoted: "z 696K PLN/mies. obecnego marketing_spend, 80% sellersów nie potrafi przypisać efektu" (Q2.1 finding #3, własna analiza CSV).

## Model danych

- Single waitlist table (localStorage only, no backend): `{email: string (PK), entry_timestamp: ISO, source_page_section: "hero" | "cta-band"}`.
- No real DB integration for smoke test.

## Feature Spec (do wklejenia jako pierwszy prompt po Plan→Build switch)

Patrz `../../decisions/11-spec-q3.1.md` sekcja 3 dla pełnej Feature Spec ≤200 słów.

## Success / Kill thresholds (z Q2.4 OST, AT-1)

- **Sukces:** ≥15% email conversion (75 emails na 500 impressions).
- **Kill:** <5% (zatrzymanie hipotezy FH Reach).
- **Iterate:** 5-15% — popraw value prop / pricing anchor / dowody (A/B test).
