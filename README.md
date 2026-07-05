# AI_Fairness

Hey, welcome to my little fairness project
This repo is basically me messing around with a resume‑screening dataset to see:

how well a model can predict who gets shortlisted

whether the model treats people with different education levels fairly

and what the model is actually thinking when it makes decisions

How to get started
If you want to run this yourself:

bash
git clone https://github.com/Loopinlogix/AI_Fairness.git
cd AI_Fairness
You’ll need the usual ML stuff:

pandas

numpy

scikit‑learn

fairlearn

shap

lime

seaborn

matplotlib

Install them however you normally do. I used pip.

Step 1: Load the data
The dataset is a resume‑screening CSV. First thing I checked was the class balance.

From the notebook:

“Yes: 20966, No: 9034”
“Yes 0.698867, No 0.301133”

This is pretty imbalanced. Most people are “Yes”.

I encoded the target, one‑hot encoded education level, scaled everything, and split into train/test.

Step 2: Train the model
I used a logistic regression model with class_weight='balanced' because of the imbalance.

The model actually did really well.

From the output:

“Accuracy: 0.8903”
“ROC AUC: 0.9650”

So the model is solid.

 Step 3: Fairness check
This is where things get interesting.

I looked at fairness across education levels using:

selection rate

TPR

FPR

precision, recall, F1

Some numbers from the notebook:

“PhD selection rate: 0.810403”
“High School selection rate: 0.489149”

That’s a pretty big gap.

Fairness differences
From your output:

Demographic Parity Difference: 0.3213

TPR Difference: 0.0949

FPR Difference: 0.0398

So yeah — the model definitely treats education groups differently.

Step 4: Visualizing fairness
I made bar charts for:

selection rate

TPR

FPR

They make the differences way easier to see. High School candidates get picked way less often.

Step 5: Explainability (SHAP + LIME)
SHAP (manual version)
I calculated SHAP values using the model’s coefficients.

From the notebook:

“years_experience: +3.6416”
“project_count: +3.0982”
“edu_PhD: +1.1112”

So experience and projects matter a lot. Education level also nudges things.

LIME
LIME gives simple rule‑based explanations.

From your output:

“years_experience > 0.97: +0.3067”
“project_count > 0.72: +0.2464”

Both SHAP and LIME agree on the big features.

SHAP global plot
I also generated a SHAP summary plot to see which features matter overall.

Step 6: SHAP vs LIME
I compared both explainers side‑by‑side.

Example from your table:

“years_experience SHAP: 3.575538, LIME: 0.306716”

SHAP gives bigger numbers because it works in log‑odds space. LIME gives smaller, more interpretable numbers.

Final thoughts (super casual)
The model is strong.

It’s not perfectly fair — education level definitely affects predictions.

SHAP and LIME help explain what’s going on under the hood.

Experience, project count, and skills score are the big drivers.

Education level still plays a noticeable role, which is something you’d want to address if this were a real hiring system.

How to run it
Just open the notebook in Colab or Jupyter, upload the CSV, and run the cells top to bottom.
