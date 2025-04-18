1. Aligning Bootstrap Logic with the Linear Model Output
Challenge:
It took some attention to detail to ensure the bootstrap process matched the linear model structure. The goal was to resample rows of the dataset with replacement and fit the exact same formula (logHR ~ logBM) repeatedly. Forgetting to use as.formula() or mismatching variable names could easily cause the loop to fail or misestimate coefficients.

Thought:
This reinforced the importance of reproducible modeling. Automating repeated analysis using replicate() made me appreciate how often simple errors—like mismatched variable names or not transposing arrays—can snowball in statistical workflows.

2. Comparing Bootstrap vs. lm() Standard Errors
Challenge:
At first, I expected the bootstrap standard errors and confidence intervals to match those from lm() closely, but they didn’t align perfectly. The differences were subtle but consistent—bootstrap SEs were slightly smaller in this case.

Thought:
This highlighted how bootstrapping gives an empirical approximation of variability that doesn't rely on the same assumptions (like normality) as analytical solutions. It’s more flexible, but also more sensitive to sample size and variation.

3. Creating a General-Purpose Bootstrapping Function
Challenge:
Writing a flexible function (boot_lm) that takes a model formula as a string and works on any dataset introduced a few design choices. I had to make sure the function didn’t break when passed other formulas, handled column name parsing robustly, and returned results in a consistent, readable format.

Thought:
This gave me practical experience in writing clean, reusable code for data analysis—a skill that's useful beyond statistics homework. The ability to wrap logic into a general function helps standardize analysis across different projects or datasets.

4. Visualizing Bootstrap Convergence
Challenge:
It was tricky to summarize how coefficient estimates and their confidence intervals converge as the number of bootstrap replicates increases. Managing data reshaping, faceting, and ribbons with ggplot2 was a bit tedious, especially when ensuring each panel had the correct y-scale.

Thought:
The plot was super helpful! It made it easy to see when additional bootstraps stop adding meaningful precision to the estimates. I now see how convergence visualization can be a diagnostic tool—not just a pretty extra.

5. Interpreting Differences in Confidence Intervals
Challenge:
Explaining why bootstrap CIs might be narrower than those from lm() was more conceptual than computational. Since bootstrap CIs are based on empirical distributions, they're sensitive to skew or outliers, and might not behave like symmetric t-distribution intervals.

Thought:
This made me reflect on the assumptions behind different methods. Bootstrap methods are more robust when model assumptions are violated but may behave differently even in well-behaved datasets. It’s important to interpret these CIs in context, not just trust numbers blindly.
