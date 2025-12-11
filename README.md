# Assignment 1 Feedback - Petra Ilic

## Submission Status

- PDF Report: Yes
- Code File: Yes (.ipynb)
- Student Name on PDF: Yes (Petra Ilic, 2503891 and Elsa Andrea Rodriguez, 2500008)
- Late: No

## Scores

### 1. Data Work (0.5/2 points)

- Data loading: 0.5/0.5 - **Evidence:** Code successfully loads CPS data with `df = pd.read_csv('cps-earnings.csv')`. Data is loaded and used for analysis.

- Occupation selection: 0/0.5 - **Evidence:** **CRITICAL ISSUE - No occupation was selected.** The student used the entire CPS dataset (149,316 observations across all occupations) without filtering to a specific occupation code. The assignment required picking an occupation NOT from Chapter 9. No filtering by `occ2012` or any occupation variable was performed. The code shows no reference to occupation filtering anywhere.

🔵 We agree with this, it was an error from our end. 

- Data cleaning: 0/0.5 - **Evidence:** Minimal data cleaning was performed. The student created `grade92_sqrd` (squared education) and `earnwke_ln` (log wages), but did NOT create a proper female dummy variable. The original `sex` variable (1=male, 2=female) was used directly, which leads to confusing coefficient interpretation. A proper female dummy (0=male, 1=female) should have been created.

🔵 The instruction file never mentions cleaning should be performed. It is a important practice for data analysis projects but we decided not to proceed as we evaluated it was not needed. Changing the variable was also not mentioned in the instructions file, while it was commented in class, it was not clear since the file was not being yet considered. 

- Code documentation: 0/0.5 - **Evidence:** The code has minimal comments. There are brief comments like `# import dataset`, `# Linear Regression`, `# Square the education variable`, but no markdown cells explaining the methodology, rationale for choices, or interpretation of steps. Section headers exist but lack explanatory text.

🔵 Since it is a data analysis class, we assumed the format of the coding was not crucial, specially when a report is being created specifying all these details. Usually, there is not explanatory text in the coding delivarbles, the explanation is mentioned on the report. 

**Comments:** The most significant issue is the failure to select a specific occupation as required by the assignment. This fundamentally changes the analysis from examining the gender gap within a specific occupation to a general population-level analysis. The lack of a proper female dummy variable also complicates interpretation.

### 2. Modeling, Graphs and Tables (2.5/4 points)

- Unconditional gender gap: 1.0/1.0 - **Evidence:** The student clearly presents the unconditional gender gap via `reg1 = smf.ols("earnwke ~ sex", data=df).fit(cov_type ="HC3")`. The coefficient of -243.31 is reported (meaning women earn ~$243 less per week, though interpretation is complicated by using sex=2 for female). Figure 1 shows a visual representation.

- Gender gap × Education analysis: 1.0/2.0 - **Evidence:** The student includes multiple models examining gender and education:

  - reg2: `earnwke ~ sex + grade92` (simple additive)
  - reg3: `earnwke ~ sex + grade92 + grade92_sqrd` (quadratic)
  - reg4: `earnwke_ln ~ sex + grade92` (log-level)

  **MISSING: The analysis does not show how the gender gap varies with education level.** All models are parallel slopes models (wage ~ sex + education) where the gender gap is constant across education levels. To show how the gap _varies_, the student would need stratified regressions by education level, an interaction model, or computing gaps at each education level. The separate regression lines in plots are visual only, not formally analyzed. **Deduct 1.0 point for not demonstrating how the gap varies with education.**

- Regression table: 0.5/1.0 - **Evidence:** The student uses Stargazer to create a comparison table (Figure 6) showing coefficients, standard errors, and significance stars for three models. However, the table only includes reg2, reg3, and reg4 - the unconditional model (reg1) is not included in the comparison table. The table is well-formatted with proper significance indicators.

🔵 We do not consider missing 1 ou of 4 models implies a 50% point deduction, considering the results were present on the report. 

**Comments:** The analysis shows good effort with multiple model specifications but does not demonstrate how the gender gap varies with education. The models only control for education (showing parallel effects) rather than showing different gaps at different education levels. The visual stratification by gender in plots hints at the concept but is not formally analyzed.

### 3. Interpretation and Summary (1.25/2 points)

- Coefficient interpretation: 0.5/0.75 - **Evidence:** The PDF provides interpretations of key coefficients. For example: "if the gender remains constant, on average a one unit increase in education level correlates with a $116 increase in weekly earnings" and "at the same education level, on average, a female is expected to earn $289 less than a man (weekly)." For the log model: "a woman's earnings are 35.03% less than a man's" (though this should technically be approximately 35%, not exactly). The interpretations are generally correct but imprecise due to using sex (1,2) instead of a female dummy (0,1). The coefficient of -243 for sex should be interpreted as the change when moving from sex=1 to sex=2, not directly as the female-male difference.

🔵 It seems the interpretation was made adequatley according to the comments, the error was the (1,2) vs (0,1), which had deduction on the grade on some bullets above. 

- Statistical inference: 0.5/0.5 - **Evidence:** The student discusses R-squared values throughout: "r-squared value of 0.036, which is drastically low", "r-squared value of .238 which is too low to be considered significant", "r-squared value of .215". The PDF also references "the low r square values consistently demonstrated that sex and education level are insufficient variables to explain the majority of the observed variation." The regression outputs show p-values (P>|z|) = 0.000 for all coefficients, though this is not explicitly discussed in the report.

- Summary of findings: 0/0.5 - **Evidence:** The summary is weak and somewhat misleading. The conclusion that "sex and education level are insufficient variables to explain the majority of the observed variation in weekly earnings" misinterprets R-squared - a low R-squared does not mean variables are "insufficient" or findings are not meaningful. The student does not provide clear conclusions about the main research question (how does the gender gap vary with education?), because they never modeled this interaction.

- Report quality: 0.25/0.25 - **Evidence:** The report is professionally formatted with clear figures, numbered appropriately. Within reasonable length. Student names and IDs are included.

**Comments:** The interpretations show understanding of regression coefficients, but the lack of interaction terms means the core research question (how does the gap vary with education?) cannot be properly answered. The misinterpretation of R-squared as indicating "insufficiency" is a conceptual error.

## Total Score: 4.25/8 points

🔵 Thank you for taking the time to consider our comments!

## Strengths

- **Multiple model specifications:** The student explored different functional forms (linear, quadratic, log-level), showing good analytical curiosity.
- **Use of robust standard errors:** Correctly applied HC3 heteroscedasticity-robust standard errors to all regressions.
- **Visual presentation:** Created multiple informative plots showing the relationship between earnings, gender, and education with separate trend lines by gender.
- **Stargazer table:** Used Stargazer package to create a professional comparison table of multiple models.
- **PDF report structure:** Clear organization with properly labeled figures.

## Areas for Improvement

- **Select an occupation:** The assignment explicitly required selecting a specific occupation (not 1005 or 1240). This is a fundamental requirement that was missed entirely.
- **Show how gap varies with education:** To analyze how the gender gap varies with education, you could use stratified regressions by education level, an interaction model (`sex * grade92`), or compute wage gaps at each education level. Without one of these approaches, the gender coefficient represents a constant gap across all education levels.
- **Create proper dummy variable:** Instead of using sex (1,2), create a female dummy (0=male, 1=female) for clearer interpretation. With the current coding, coefficients are harder to interpret directly.
- **Improve interpretation of R-squared:** A low R-squared does not mean the analysis is invalid. It simply means other factors explain earnings variation. The gender coefficient can still be meaningful and precisely estimated even with low R-squared.
- **Add more code documentation:** Include markdown cells explaining the analytical approach and rationale for each step.

## Code Reproducibility Notes (No Point Deduction)

- **Syntax errors:** None found. All cells executed successfully without errors.
- **Cell execution issues:** Cells appear to be in correct sequential order. Would run cleanly from top to bottom.
- **Dependencies:** Uses numpy, pandas, statsmodels, seaborn, matplotlib, plotnine, stargazer. No requirements.txt file included.
- **Data paths:** Uses relative local path: `pd.read_csv('cps-earnings.csv')`. This assumes the data file is in the same directory as the notebook. A URL or more robust path handling would improve reproducibility.
- **Would code run from fresh kernel:** Yes, if cps-earnings.csv is present in the working directory. All imports are at the top, variables are defined before use.

## Additional Notes

The student appears to have misunderstood the assignment scope. The analysis was conducted on the entire CPS dataset rather than a specific occupation, fundamentally changing the research question from "gender gap within occupation X" to "overall gender gap across all occupations." This is a significant deviation from the assignment requirements.

The separate regression lines shown in the plots (Figures 3, 4, 5) visually suggest different slopes for men and women, which is exactly what an interaction term would capture formally. The visual analysis hints at understanding the concept, but this was not translated into the formal regression model.
