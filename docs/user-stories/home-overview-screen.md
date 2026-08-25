# User Story — Home Overview Screen

## User Story

**As a** MoneyMate user,
**I want to** see a monthly financial overview on my home screen,
**So that** I can quickly understand how much I can safely spend, where my money is going, and how my spending trends over time.

## Acceptance Criteria

- [ ] The screen displays the current month and year (e.g. "July 2026") in a bg/brand gradient header banner.
- [ ] A "Safe to Spend" card shows the remaining spendable amount in the user's local currency (e.g. S$857.70) with a "Updated just now" timestamp.
- [ ] A "How is this calculated?" link opens an explanation of the safe-to-spend formula.
- [ ] An Income vs. Spent summary displays total income and total spent for the current month, with a "Remaining this month" balance and an icon/success checkmark when positive.
- [ ] A "Spending by Category" section shows a donut chart with a month selector and a breakdown list of categories (Food & Drink, Bills & Utilities, Transport, Shopping, Entertainment, Other) each displaying amount and percentage.
- [ ] A "Spending Trend" section shows a 6-month bar chart distinguishing complete months from the in-progress month via brand/primary (complete) and brand/primary-subtle (in-progress) colour coding and a legend.
- [ ] A "Summary Insight" text block provides a contextual month-over-month comparison (e.g. "Jul is currently S$147.70 (7.4%) below Jun. Peak spending was May at S$2,210.00.").
- [ ] A bottom navigation bar provides access to Home, Transactions, Budget, and Profile tabs with "Home" highlighted as active.
- [ ] A notification bell icon is accessible from the top-right of the header.

## Tech Notes

- **API endpoints required:**
  - `GET /overview` — safe-to-spend, income, spent, remaining
  - `GET /spending/categories?month=YYYY-MM`
  - `GET /spending/trend?months=6`
- Safe-to-spend calculation is server-side; the "How is this calculated?" CTA should open a bottom sheet or navigate to a detail screen.
- Currency formatting must respect user locale (e.g. S$ for SGD). Use `locale/currency` from user profile settings.
- Charts can be rendered with a library (e.g. Victory Native, react-native-chart-kit) or custom SVG components.
- "Updated just now" timestamp reflects the last data sync. Support pull-to-refresh and/or background polling.
- Summary insight copy is generated server-side using month-over-month comparison logic.
- Category colour mapping (`category/food` = Food & Drink, `category/bills` = Bills & Utilities, `category/transport` = Transport, `category/shopping` = Shopping, `category/entertainment` = Entertainment, `category/other` = Other) should live in a shared theme config for consistency across all screens.
- The in-progress month bar in the trend chart needs distinct visual treatment (`brand/primary-subtle` shade or pattern) with a corresponding legend entry.

## Design Notes

- Header banner uses a `brand/primary`-to-`brand/secondary` gradient with `text/on-brand` colored text for the current month.
- Cards use ~16px corner radius, subtle drop shadows, and `bg/card` backgrounds on a `bg/primary` page.
- Donut chart uses distinct category color variables (`category/food`, `category/bills`, `category/transport`, `category/shopping`, `category/entertainment`, `category/other`) with a hollow center; ensure adequate contrast between adjacent segments.
- Active bottom nav tab ("Home") is differentiated with a filled `icon/brand` icon and `text/brand` highlighted label.
- Spending trend bars use `brand/primary` for completed months and `brand/primary-subtle` for the in-progress month.
- Typography hierarchy: header month uses `heading-lg`, "Safe to Spend" amount uses `heading-xl`, section headings use `heading-sm`, body text uses `body`.
- `icon/success` checkmark beside "Remaining this month" reinforces positive financial status — consider `status/error` / `status/warning` states when balance is low or negative.

## Design Reference

- **Figma frame:** [Home Overview Screen](https://figma.com/design/RcHnpN8r0H8tdMQzHlUO5G?node-id=2-5)
- **Figma Debug UUID:** `a2307efc-47d2-4737-86ec-5f31b45fbd7c`
