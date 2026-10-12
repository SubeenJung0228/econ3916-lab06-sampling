# Sampling for Machine Learning — Train-Test Splits

## Objective
I treated the train-test split as a sampling problem and checked how the way a sample is drawn affects whether the results can be trusted.

## Methodology
- Loaded the Titanic dataset (891 passengers) and used survival as the target, looking at how survival differed by passenger class.
- Split the data into training and test sets in two ways, a naive random split and a split stratified on survival, and compared the survival rate and the class shares in each half.
- Stratified on both passenger class and survival together, so that both shares stay the same in the training and test sets.
- Found the data leakage in a StandardScaler step and a SimpleImputer step that were fit on all the rows, and fixed them by fitting on the training rows only and then transforming the test rows with what was learned.
- Wrote a function, split_by_share(), that splits a table using a test share and a seed, and checked that it returns the same rows as the lab's own split.
- Simulated the 1936 Literary Digest poll on a population of 10 million voters, where the chance of being sampled depended on income, and compared a large biased sample with a random sample of 50,000.
- Computed Meng's data defect correlation to measure how strongly being in the sample was tied to the vote.
- Ran 100 replications of both samples to compare their average error and their spread.

## Key Findings
- **Stratification:** Stratifying on survival kept the survival rate the same in the training and test sets, which a naive split only does by chance.
- **Data leakage:** Fitting a scaler or imputer on all the rows lets test information into the training data. Fitting on the training rows only keeps the test set unseen.
- **Sample design beats sample size:** The biased sample of 4,382,503 responses was less accurate than the random sample of 50,000. A data defect correlation of 0.1475 produced an error of 8.3 percentage points.
- **Replications:** Across 100 replications, the biased sample gave nearly the same wrong answer every time, while the random sample stayed centered on the truth. A large biased sample makes us confident in the wrong answer.
