# UK Healthy Life Expectancy 2012–14 to 2022–24: age-band decomposition

An interactive decomposition of the UK ONS *Healthy Life Expectancy* release of 19 February 2026 (covering 2011–13 to 2022–24), showing which age groups' changes in self-reported "good" health prevalence drove the headline fall in HLE at birth.

**[👉 Open the dashboard](https://amcunningham.github.io/hle-decomposition/)** *(after enabling GitHub Pages — see Setup below)*

## What it does

UK healthy life expectancy at birth fell by roughly 2–3 years between 2012–14 and 2022–24. The [Health Foundation's watershed paper](https://www.health.org.uk/reports-and-analysis/analysis/healthy-life-expectancy-trends-in-the-uk-a-watershed-moment) flagged the 25–49 working-age band via a counterfactual, but a full age-band decomposition hasn't been published. This page fills that gap: for each constituent country, it apportions the observed change in HLE at birth across life-stage bands, holding mortality at 2022–24 levels.

Charts in the dashboard:

1. **Contribution by life stage** — bar chart of how much each life-stage band's change in "good" health prevalence added to or subtracted from the country's HLE at birth.
2. **Prevalence trajectory** — five-life-stage prevalence trends across all 12 three-year periods.
3. **Cross-nation comparison** — UK as locked reference, with toggleable nations alongside.
4. **HLE at birth across periods, four nations** — full 12-period trajectories for UK / England / NI / Scotland / Wales.
5. **NI 25–49 prevalence vs the rest of the UK** — full 12-period series, by sex.
6. **NI HLE at birth: ONS (APS-based) vs DoH NI (HSNI-based)** — cross-survey validation.
7. **Deprivation gradient (England 10 deciles, Wales 5 quintiles)** — HLE by IMD/WIMD decile/quintile, 2013–15 vs 2022–24, plus per-decile change. Shows the headline 2-year fall against the within-population gradient.

## Methodology in brief

- **Source data:** ONS modelled "good" general health prevalence (Sheet 3 of `hleinputs.xlsx`) and HLE outputs with proportion-in-good-health (Sheet 1 of `healthylifeexpectancyuk.xlsx`), from the [19 February 2026 release](https://www.ons.gov.uk/peoplepopulationandcommunity/healthandsocialcare/healthandlifeexpectancies/bulletins/healthstatelifeexpectanciesuk/between2011to2013and2022to2024).
- **Calculation:** Standard Sullivan method. Cohort person-years per 5-year band were back-solved from published HLE(x) and proportion-in-good-health(x) using the recursion HLE(x) = π_x · u_x + ρ_x · HLE(x+5). The Sullivan reconstruction of HLE at birth replicates the published ONS value to within 0.01 years across all country × sex × period combinations.
- **Decomposition:** Symmetric Arriaga at the 5-year-band level, aggregated to five life-stage bands. Mortality is held at 2022–24 levels throughout, so the bars reflect the morbidity (self-reported health) component only. The aggregate mortality contribution is small (UK Male −0.02 yrs, Female +0.06 yrs).
- **Under-15s** are excluded from charts because their prevalence is parent-proxy via Census, not self-rated. The under-15 contribution is shown as a small footnote.
- **External methodology check:** The analytical approach was sense-checked against an independent description of how a Tetzlaff-style replication on ONS data should be set up (Perplexity AI, May 2026). No substantive methodological gaps identified.

## Key findings

1. The largest single negative contribution to HLE at birth comes from the **25–49 working-age band** (UK Male −0.95 yrs, Female −1.24 yrs). This matches the age pattern [Tetzlaff et al. (Eur J Public Health 2026)](https://academic.oup.com/eurpub/article-pdf/36/3/ckag059/68087747/ckag059.pdf) reported for Germany — younger working-age health driving the fall, older working-age health stable or improving.
2. **NI has the smallest HLE-at-birth fall of the four UK nations.** It also has the highest rate of working-age economic inactivity due to long-term sickness (10.1% vs 6.6% UK-wide). The two findings sit alongside each other and don't yet add up to a coherent story.
3. **Two independent surveys (ONS APS and DoH NI HSNI) give the same NI pattern**: small male fall, larger female fall, absolute levels within ~1.5 yrs. Cross-instrument validation strengthens the finding.
4. **Mental health is plausibly part of the SRH signal.** The Adult Psychiatric Morbidity Survey shows common mental health conditions in 16–24 year olds rose from 17.5% (2007) to 25.8% (2023/24). UKHLS GHQ data show the steepest rise in 16–18s and the economically inactive. Blanchflower et al. (NBER 2024) argue the U-shaped age curve of mental ill-being has flattened or inverted in the UK.

## Files

```
hle-decomposition/
├── index.html                          # The interactive dashboard (self-contained, Chart.js inlined)
├── README.md                           # This file
├── LICENSE                             # CC BY 4.0
└── data/
    ├── dashboard_data.json             # Full dashboard payload (all charts use this)
    ├── life_table_back_solved.csv      # Back-solved cohort person-years by age × sex × country × period
    ├── decomposition_age_band.csv      # Per-5-year-band Arriaga decomposition
    ├── decomposition_summary.csv       # Country × sex headline summary
    ├── prev_country.csv                # ONS modelled "good" health prevalence (extracted)
    └── hle_country.csv                 # ONS HLE values (extracted)
```

## Setup: publishing to GitHub Pages

After pushing this repository to GitHub:

1. Go to **Settings → Pages** in your repository.
2. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
3. Set **Branch** to `main` and folder to `/ (root)`.
4. Click **Save**.
5. Within a minute or two, the dashboard will be live at `https://amcunningham.github.io/hle-decomposition/`.

## Sources

- Office for National Statistics. *Healthy life expectancy, UK: between 2011 to 2013 and 2022 to 2024* (19 February 2026).
- Tetzlaff J et al. *Eur J Public Health* 2026;36(3):ckag059. doi:10.1093/eurpub/ckag059.
- Mooney A, Alarilla A, Cavallaro F. *Healthy life expectancy trends in the UK: a watershed moment*. The Health Foundation, 26 April 2026.
- Tracey F, Finch D, Bibby J. *Socioeconomic disadvantage and self-reported health*. The Health Foundation, 9 March 2026.
- Commission for Healthier Working Lives. *Action for healthier working lives* (final report, March 2025).
- Marmot M et al. *Health Equity in England: The Marmot Review 10 Years On* (Institute of Health Equity, 2020).
- Browne J, Crowley-Carbery K, Langengen T. *An Emergency Handbrake for UK Welfare*. Tony Blair Institute for Global Change, 28 April 2026.
- McManus S et al. *Adult Psychiatric Morbidity Survey: Survey of Mental Health and Wellbeing, England 2023/24* (NHS England Digital, 2025).
- Egan M et al. Regional trends in mental health inequalities in young people aged 16–25 in the UK. *Soc Sci Med* 2024.
- Blanchflower D et al. *The Declining Mental Health of the Young in the UK*. NBER WP 32879, 2024.
- Department of Health NI. *Life Expectancy in Northern Ireland 2022-24* (9 December 2025).

Full source list inline in the dashboard.

## Licence

Code and analysis: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Underlying ONS data: Open Government Licence v3.0.

## Author

Anne Marie Cunningham, May 2026.
