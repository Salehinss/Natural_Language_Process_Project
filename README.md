Job Advertisement Category Classification (NLP)
A machine-learning NLP project that predicts the category of a job advertisement from its job title and description. The project compares text preprocessing choices, Bag of Words (BoW), TF-IDF, and average Word2Vec features with Multinomial Naive Bayes and Logistic Regression.

This notebook was developed as a CSC4233 Natural Language Processing midterm project.
Categories
The model predicts one of six categories:
- IT
- Finance
- Marketing
- Education
- Engineering
- Other
The Other label groups all source job categories that are not mapped to one of the five named categories. This leads to substantial class imbalance.
Dataset
- Source: SEEK job advertisements CSV
- Raw rows used: Up to the first 15,000 rows
- Rows after cleaning: 13,833 (one empty text and 1,166 duplicate texts removed)
- Input columns: job_title, job_description
- Target: Derived from the original category column
- Class distribution: IT 1,309; Finance 1,055; Marketing 327; Education 572; Engineering 359; Other 10,211
Dataset rights: The original dataset's licence has not been confirmed. Verify the rights and any required permission before publishing or submitting a local copy of the data. For this reason, the data CSV is not packaged with this repository.

The notebook tries to load the dataset from the source URL. If this fails, it looks in the working directory for jobs_first_15000_rows.csv, then jobs.csv.
Method
1. Combine job title and description; remove blank and exact-duplicate documents.
2. Explore class counts, document lengths, and frequent words.
3. Clean HTML, URLs, emoji, numbers, and punctuation; compare basic cleaning, stop-word removal, and stemming.
4. Use a stratified 70% training / 15% validation / 15% test split with seed 42.
5. Compare BoW, TF-IDF, and average Word2Vec text features. Vectorizers and Word2Vec are trained only on the training split.
6. Tune Multinomial Naive Bayes and Logistic Regression using validation macro-F1; include a majority-class baseline.
7. Evaluate on the held-out test set with accuracy, macro precision, macro recall, macro-F1, a confusion matrix, and classification reports.
8. Review 20 misclassified advertisements to understand common errors.
Selected preprocessing: stop-word removal (without stemming).

Selected TF-IDF features: unigrams and bigrams.
Results
The best model was chosen using validation macro-F1:
Measure	Result
Best model	Logistic Regression + TF-IDF
Best regularization setting	C = 5.0
Validation macro-F1	0.8300
Test accuracy	0.9239 (92.39%)
Test macro-F1	0.8365
Test macro recall	0.8765
Test examples	2,075


These scores were reported in the supplied notebook's saved output; they have not been independently rerun as part of packaging.
Test comparison (macro-F1)
Model	Test macro-F1
Majority-class baseline	0.1415
Multinomial Naive Bayes + BoW	0.8023
Multinomial Naive Bayes + TF-IDF	0.8097
Logistic Regression + BoW	0.8136
Logistic Regression + TF-IDF	0.8365
Logistic Regression + average Word2Vec	0.7185
