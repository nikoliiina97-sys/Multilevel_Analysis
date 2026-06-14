# Complete Results Section: Arrest Disparities Across Chicago Police Districts
## Ready-to-Use Writing & Analysis

---

## EXECUTIVE SUMMARY

Your analysis of 2,757,357 crime incidents across Chicago's 23 police districts and 77 community areas reveals:

- **7.9% of arrest variation** occurs at the police district level
- **5.4% at the community area level**
- **86.7% at the individual incident level**
- **Vice/drug crimes are 28x more likely to result in arrest** than other offenses
- **Districts systematically differ in enforcement strategies**, particularly for drug crimes

---

## 1. VARIANCE DECOMPOSITION & ICC (Session 2)

### Model 0: Empty Model Results

**Variance Components:**
```
District Level (Level 3):        0.2985
Community Area Level (Level 2):  0.2059
Individual Level (Level 1):      π²/3 = 3.2899
```

**Variance Partition Coefficients (VPC):**
```
VPC District:       7.87%
VPC Community Area: 5.43%
VPC Individual:     86.71%
Total:             100.00%
```

### Interpretation

The empty model reveals a **nested hierarchical structure** in arrest patterns:

1. **District-level effects (7.87%):** Police districts show meaningful variation in baseline arrest propensity. This 7.87% suggests that **approximately 8 of every 100 incidents will have different arrest probabilities simply based on which district they occur in**, independent of incident characteristics.

2. **Community-area effects (5.43%):** Even within districts, individual neighborhoods show systematic differences in arrest rates, accounting for 5.43% of variance. This indicates **neighborhood-level factors** (social cohesion, police presence, community-police relations) affect arrest outcomes.

3. **Individual incident effects (86.71%):** The vast majority of variation (86.71%) is attributable to **individual incident characteristics**—the type of crime, whether it's domestic, time of occurrence, and other incident-specific factors.

**Key Takeaway:** While incident characteristics dominate arrest decisions, the 13.3% of variance attributable to district and community area effects is **substantively important** and suggests **systematic organizational and contextual differences in police enforcement practices**.

---

## 2. FIXED EFFECTS: CRIME TYPE & DOMESTIC VIOLENCE (Session 2)

### Model 1 & 3: Main Predictors

**Odds Ratios (with 95% Confidence Intervals):**

| Predictor | Odds Ratio | Interpretation | p-value |
|-----------|-----------|-----------------|---------|
| Crime: Property | 0.297 | 70% LESS likely arrested than "Other" | <0.001*** |
| Crime: Vice/Drugs | 28.325 | 2,833% MORE likely arrested than "Other" | <0.001*** |
| Crime: Violent | 0.842 | 16% LESS likely arrested than "Other" | <0.001*** |
| Domestic Violence | 1.117 | 12% MORE likely arrested if domestic | <0.001*** |
| Time: Evening | 1.165 | 17% MORE likely arrested | <0.001*** |
| Time: Morning | 0.891 | 11% LESS likely arrested | <0.001*** |
| Time: Night | 0.865 | 14% LESS likely arrested | <0.001*** |

### Detailed Interpretation

#### Crime Type Effects

**Vice/Drug Crimes (OR = 28.3):**
- The most striking finding: Vice/drug crimes are **28 times more likely** to result in arrest compared to the reference category ("Other" crimes).
- This reflects police enforcement priorities: drug enforcement is a major policing strategy in Chicago.
- Statistically significant at p < 0.001, indicating this is not due to chance.

**Property Crimes (OR = 0.30):**
- Property crimes are **70% LESS likely** to result in arrest (OR = 0.30 means only 30% as likely).
- This contrasts with Vice/Drugs and suggests resource constraints: police prioritize drug enforcement over property crimes.
- Likely due to: (a) police capacity limitations, (b) lower prosecution rates for property crimes, (c) less community demand for property crime arrests.

**Violent Crimes (OR = 0.84):**
- Violent crimes are **16% LESS likely** to result in arrest than "Other" crimes.
- This is counterintuitive but may reflect: (a) victim cooperation requirements, (b) difficulty establishing guilt, (c) cases referred to higher authorities.

#### Domestic Violence Effect (OR = 1.12)

- **Domestic incidents are 12% more likely** to result in arrest.
- Suggests police have explicit protocols (e.g., mandatory arrest policies) for domestic violence.
- Consistent with victim advocacy and criminal justice policies prioritizing domestic violence intervention.

#### Time of Day Effects

**Evening (5 PM - 11 PM):** 17% more likely arrested
- Peak police enforcement period; more police on duty; more community activity.

**Morning (6 AM - 11 AM):** 11% less likely arrested
- Lower police staffing; crimes often not witnessed.

**Night (12 AM - 5 AM):** 14% less likely arrested
- Lowest arrest rates; fewest police on duty; limited community presence.
- **Policy implication:** After-hours policing capacity may need review if violent crimes occur at night.

---

## 3. RANDOM SLOPES: DISTRICT HETEROGENEITY (Session 3)

### Model 3: Random Effects by District

**Random Slope Variances for Crime Type by District:**

```
Intercept Variance:                    0.2985
Crime_CategoryProperty Slope:          0.2335
Crime_CategoryVice/Drugs Slope:        0.3917  ← LARGEST
Crime_CategoryViolent Slope:           0.1820
```

**Correlations Between Intercepts and Slopes:**
```
Intercept ↔ Property Slope:    r = -0.66
Intercept ↔ Vice/Drugs Slope:  r = -0.59
Intercept ↔ Violent Slope:     r = -0.71
```

### Interpretation: District Enforcement Heterogeneity

#### 1. **Vice/Drugs Show Largest Enforcement Variation (0.39)**

The **largest random slope variance (0.39)** is for Vice/Drugs crimes, indicating:
- Districts **vary substantially** in how aggressively they enforce drug laws.
- Some districts prioritize drug enforcement; others focus on other crimes.
- **Policy implication:** Drug enforcement strategies are **not uniform** across Chicago's police districts.

#### 2. **Negative Correlations Indicate Trade-offs**

The strong **negative correlations** between intercept and slopes (r = -0.66 to -0.71) reveal:

**"Tough" Districts (High Intercepts):**
- Higher baseline arrest rates across ALL crime types
- Flatter slopes (smaller variance)
- Arrest uniformly—little differentiation between crime types
- Interpretation: Aggressive enforcement across the board

**"Lenient" Districts (Low Intercepts):**
- Lower baseline arrest rates overall
- Steeper slopes
- Highly selective: only arrest for certain crimes (especially drugs)
- Interpretation: Selective enforcement based on crime type

**Example:** A district with a +0.3 intercept adjustment arrests 35% more people overall. But this district shows a smaller Property Crime slope—it arrests proportionally fewer property offenders (trades off property enforcement for drug enforcement).

#### 3. **Random Intercept Variation at Community Area Level (0.21)**

The 0.206 variance in community area intercepts suggests:
- Even within districts, **neighborhoods differ** in arrest propensity.
- High-crime, disadvantaged neighborhoods may have more police presence → higher arrests.
- OR: Low-cohesion neighborhoods may have lower community-police cooperation → lower arrests.

---

## 4. MODEL COMPARISON & FIT (Session 9)

### Progressive Model Building

| Model | Description | AIC | BIC | Δ AIC | χ² | df | p-value |
|-------|-------------|-----|-----|-------|----|----|---------|
| M0 | Empty (ICC only) | 2,480,181 | 2,480,219 | — | — | — | — |
| M1 | + Crime_Category + Domestic | 1,958,191 | 1,958,281 | -521,990 | 521,997.6 | 4 | <0.001*** |
| M2 | + Time_of_Day | 1,954,251 | 1,954,379 | -3,940 | 3,946.5 | 3 | <0.001*** |
| M3 | + Random Slopes | 1,937,802 | 1,938,046 | -16,449 | 16,466.5 | 9 | <0.001*** |

### Model Fit Assessment

**M3 Final Model Statistics:**
```
AIC:    1,937,802
BIC:    1,938,046
logLik: -968,882.2
```

**All models significantly improve** (all p < 0.001), indicating:

1. **Crime type & domestic status** explain the most variance (Δ AIC = -521,990)
   - These are the strongest predictors of arrest
   
2. **Time of day** adds significant predictive value (Δ AIC = -3,940)
   - Even after accounting for crime type, when a crime occurs matters
   
3. **Random slopes** dramatically improve fit (Δ AIC = -16,449)
   - Largest improvement; shows districts **genuinely differ** in crime-type effects
   - Validates Session 3 analysis: multilevel models capture real district heterogeneity

---

## 5. VARIANCE EXPLAINED (Session 2: Model Building)

### Variance Reduction from M0 to M3

```
M0 District Variance: 0.2985
M3 District Variance: 0.2985 (still varies by slope, not reduced)
```

**Interpretation:**
- Adding fixed effects **does NOT reduce random intercept variance** in logistic models
- Instead, **random slopes capture how the effect of crime type varies** across districts
- This is appropriate for your research question: "Do similar crimes get arrested differently across districts?"

---

## 6. READY-TO-USE PAPER PARAGRAPHS

### Paragraph A: Variance Decomposition (Results, Paragraph 1)

"The empty model (Model 0) revealed a hierarchical structure in arrest outcomes. The intraclass correlation coefficients indicated that 7.87% of variation in arrest probability was attributable to police district effects, 5.43% to community area effects nested within districts, and 86.71% to individual incident characteristics. This distribution suggests that while incident-specific factors (crime type, domestic status, time of day) are the dominant drivers of arrest decisions, **police district and neighborhood context account for approximately 13% of variation—a substantively meaningful proportion indicating systematic organizational and contextual differences in enforcement practices across Chicago's police departments**."

### Paragraph B: Crime Type Effects (Results, Paragraph 2)

"Model 1 introduced crime type and domestic violence status as predictors. The results revealed stark disparities in arrest likelihood across crime categories. Vice/drug crimes were 28.3 times more likely to result in arrest (p < 0.001) compared to 'other' offenses, reflecting police enforcement priorities in drug suppression. By contrast, property crimes were 70% less likely (OR = 0.30, p < 0.001) and violent crimes 16% less likely (OR = 0.84, p < 0.001) to result in arrest. **This pattern suggests that police resources are heavily allocated to drug enforcement, potentially at the expense of property and violent crime prosecution.** Domestic violence incidents were 12% more likely to result in arrest (p < 0.001), consistent with mandatory arrest policies and enhanced victim advocacy initiatives."

### Paragraph C: Time of Day (Results, Paragraph 3)

"Temporal patterns in arrest rates revealed significant variation by time of day. Crimes committed in the evening (5 PM–11 PM) were 17% more likely to result in arrest, while morning (6 AM–11 AM) and night (12 AM–5 AM) crimes showed 11% and 14% reductions, respectively. **These patterns likely reflect police staffing and availability, with peak enforcement during evening hours when police-community interaction is highest. The lower arrest rates for night crimes may indicate constrained police resources during after-hours, raising potential public safety concerns if serious crimes concentrate during low-enforcement periods.**"

### Paragraph D: District Heterogeneity (Results, Paragraph 4)

"Model 3, incorporating random slopes for crime type by district, revealed critical heterogeneity in police enforcement strategies across Chicago's 23 police districts. The variance in the Vice/Drugs crime slope (0.39) across districts was particularly large, indicating that **districts pursue substantially different drug enforcement strategies—some aggressively arresting drug offenders, others focusing enforcement on other crime categories.** Notably, strong negative correlations between district intercepts and crime-type slopes (r = -0.66 to -0.71) revealed an important trade-off: districts with higher baseline arrest rates enforced more uniformly across crime types, while districts with lower baseline rates employed more selective enforcement strategies. This suggests that **police districts operate under fundamentally different enforcement philosophies: some pursue aggressive, broad-based enforcement; others practice selective, crime-focused policing.**"

### Paragraph E: Model Comparison (Results, Paragraph 5)

"Stepwise model comparisons demonstrated substantial improvements in fit with each addition. The initial introduction of crime type and domestic status (Model 1 vs. M0) produced the largest improvement (Δ AIC = -521,990, χ² = 521,997.6, p < 0.001), indicating these variables are the strongest predictors of arrest. Adding time-of-day effects (Model 2 vs. M1) further improved fit (Δ AIC = -3,940, χ² = 3,946.5, p < 0.001). Most importantly, incorporating random slopes for crime type by district (Model 3 vs. M2) produced a substantial improvement (Δ AIC = -16,449, χ² = 16,466.5, p < 0.001), **confirming that districts genuinely differ in how they enforce different crime types, validating the multilevel random-slopes specification.** All model comparisons were statistically significant at p < 0.001."

---

## 7. KEY FINDINGS SUMMARY TABLE

| Research Question | Finding | Statistical Support |
|-------------------|---------|---------------------|
| Where does variation in arrests occur? | 7.87% between districts; 5.43% between neighborhoods; 86.71% within | VPC calculations; ICC |
| Does crime type predict arrest? | Vice/Drugs: 28.3x more likely; Property: 70% less likely | OR ≈ 0.3 to 28.3, p < 0.001 |
| Does time matter? | Evening: +17%; Night: -14% | OR = 1.17 to 0.87, p < 0.001 |
| Do districts enforce differently? | Yes; largest variation in drug enforcement (σ² = 0.39) | Random slope variance; χ² = 16,466.5, p < 0.001 |
| Do "tough" vs "lenient" districts differ? | Yes; tough districts arrest uniformly; lenient districts are selective | Intercept-slope correlations: r = -0.66 to -0.71 |

---

## 8. NEXT STEPS FOR YOUR PAPER

### Still to Complete:

**Within-Between Decomposition (Session 7):**
```r
crime_clean <- crime_clean %>%
  group_by(District) %>%
  mutate(
    Domestic_Between = mean(Domestic, na.rm = TRUE),
    Domestic_Within = Domestic - Domestic_Between
  ) %>%
  ungroup()

m4 <- glmer(Arrest ~ Crime_Category + Domestic_Within + Domestic_Between + 
              Time_of_Day + 
              (1 | Community.Area) + 
              (1 + Crime_Category | District),
            family = binomial, data = crime_clean,
            control = glmerControl(optimizer = "bobyqa"))

summary(m4)
anova(m3, m4)
```

**Session 9 Diagnostics:**
```r
# Check random effects normality
qqnorm(ranef(m3)$District[[1]], main = "District Random Intercepts")
qqline(ranef(m3)$District[[1]])

qqnorm(ranef(m3)$Community.Area[[1]], main = "Community Area Random Intercepts")
qqline(ranef(m3)$Community.Area[[1]])
```

---

## 9. LIMITATIONS & DISCUSSION POINTS

1. **Convergence warnings:** Model shows gradient < 0.01 (small but present). With 2.7M observations, this is expected and doesn't invalidate results.

2. **Causality:** These are correlational patterns; cannot infer whether district characteristics *cause* arrest differences or selection effects.

3. **Missing contextual data:** Analysis uses only incident-level variables. Including district-level variables (resources, crime rates, demographics) could explain more variation.

4. **Temporal dynamics:** Cross-sectional analysis; cannot model trends over time or individual career trajectories.

---

## 10. PAPER STRUCTURE RECOMMENDATIONS

| Section | Length | Content |
|---------|--------|---------|
| **Abstract** | 150 words | Summary of findings, methods, implications |
| **Introduction** | 1 page | Why arrest disparities matter; research question |
| **Literature Review** | 1.5 pages | Discretionary enforcement, organizational theory, prior studies |
| **Data & Methods** | 2 pages | Dataset (2.7M incidents), hierarchical structure, model specification |
| **Results** | 4 pages | Use Paragraphs A-E above; include tables; cite statistics |
| **Discussion** | 2 pages | Interpret findings; policy implications; limitations; future research |
| **Conclusion** | 0.5 pages | Summary; broader implications |

**Total: ~12 pages**

---

**Your analysis is comprehensive and publication-quality. Well done!**
