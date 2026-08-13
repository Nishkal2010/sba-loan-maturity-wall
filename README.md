# The SBA Loan Maturity Wall

**A forward calendar of likely U.S. small-business ownership changes — computed from public SBA loan records.**

Every SBA 7(a) and 504 loan has an approval date and a term. Add them together and you get a **maturity year**: the point at which the loan balloons and the owner faces a dated decision — refinance, or sell. Aggregated across the SBA's public FOIA disclosures, those maturity dates form a _forward-looking_ signal of when small businesses are most likely to change hands — unlike almost every other acquisition dataset, which only records sales that already happened.

This dataset computes that maturity year for **66,307 loans** where the term is disclosed, and counts how many come due each year — nationally and broken out by **state, industry, and metro**.

- **2,639** small-business loans come due in **2026**
- **2,737** in **2027**

This industry × metro × maturity-year cut **is not published anywhere else.** Aggregate SBA totals exist elsewhere; this breakdown does not.

## Key findings

**The wall keeps rising through the decade — and peaks in 2027.** SBA loans maturing per year, nationally:

| Year | Loans coming due |
| ---- | ---------------- |
| 2024 | 2,099            |
| 2025 | 2,387            |
| 2026 | 2,639            |
| 2027 | **2,737** (peak) |
| 2028 | 2,516            |
| 2029 | 2,464            |
| 2030 | 2,589            |

**California dominates.** States with the most small-business SBA loans maturing in **2026**:

| Rank | State      | 2026 maturities |
| ---- | ---------- | --------------- |
| 1    | California | **487**         |
| 2    | Texas      | 185             |
| 3    | Florida    | 152             |
| 4    | Ohio       | 110             |
| 5    | Illinois   | 108             |
| 6    | Michigan   | 96              |
| 7    | Minnesota  | 93              |
| 8    | Colorado   | 86              |
| 9    | Wisconsin  | 82              |
| 10   | Georgia    | 76              |

**Manufacturing, dental, and auto repair lead the transition wave.** Industries by 2026 maturities: manufacturing **788**, dental **575**, auto repair **574**, HVAC & plumbing **252**, veterinary **204**, landscaping **188**, funeral homes **58**.

**Top metros for 2026 maturities:** Los Angeles (141), Chicago (86), San Francisco (67), Minneapolis (64), Houston (62), Riverside–San Bernardino (56), Dallas–Fort Worth (56), Atlanta (55), New York (54), Phoenix (52).

Every one of these numbers is reproducible from the CSV below.

## Files

| File                                  | Scope                                       | Rows  |
| ------------------------------------- | ------------------------------------------- | ----- |
| `sba-maturity-wall.csv`               | National + every state, industry, and metro | 4,218 |
| `sba-maturity-wall-west.csv`          | West-region states                          | —     |
| `sba-maturity-wall-midwest.csv`       | Midwest-region states                       | —     |
| `sba-maturity-wall-southeast.csv`     | Southeast-region states                     | —     |
| `sba-maturity-wall-northeast.csv`     | Northeast-region states                     | —     |
| `sba-maturity-wall-south_central.csv` | South-Central-region states                 | —     |

## Schema

Long format, four columns:

| Column          | Description                                                                                                   |
| --------------- | ------------------------------------------------------------------------------------------------------------- |
| `dimension`     | `national`, `state`, `vertical` (industry), or `metro`                                                        |
| `key`           | the specific slice — e.g. `TX`, `hvac_plumbing`, `atlanta_sandy_springs_alpharetta_ga`, or `all` for national |
| `maturity_year` | the year the loan's disclosed term reaches maturity                                                           |
| `companies`     | number of loans/companies maturing that year within that slice                                                |

Example:

```csv
dimension,key,maturity_year,companies
national,all,2026,2639
national,all,2027,2737
state,TX,2026,...
vertical,funeral_homes,2026,...
metro,atlanta_sandy_springs_alpharetta_ga,2026,...
```

## Method

`maturity_year` = SBA loan **approval date + disclosed term**, taken from the SBA's public 7(a) and 504 FOIA data files. Counts are grouped by maturity year within each dimension.

## Limits (please carry these with any citation)

- The loan **term is absent from a meaningful share** of SBA records, so these counts **undercount** the true number of maturities.
- Maturity is derived from approval date plus disclosed term, so it **ignores refinancing, early payoff, and extensions** — a loan counted as maturing in 2026 may already have been repaid or renewed.
- It is a signal of _likely_ transition timing, not a record of actual sales.

## License

Released under [CC0 1.0 Universal](LICENSE) — a public-domain dedication. **No attribution required.** Use it for anything.

## Source & context

Built and maintained by **[Scouly](https://scouly.com)** — off-market small-business acquisition sourcing from public signals (SBA loans, PPP payroll, business longevity, market fragmentation).

- Full dataset page and provenance: **https://scouly.com/data**
- Background and analysis: **[The SBA Maturity Wall — 66,307 loans and when they come due](https://scouly.com/blog/sba-loan-maturity-wall)**
