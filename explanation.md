## Car Breakdown Prediction Explanation

### Goal

👉 Predict whether a car will break down within the next 30 days.

It uses past car data to learn patterns and then predicts future breakdown risk.

## Big Picture

Think of it like this:

You give the system information about cars.

- Mileage
- Engine hours
- Age of vehicle
- Oil quality
- Cleanliness score
- Other features

You also tell it:

- Which cars broke down
- Which cars did not break down

The system learns patterns:

- Do older cars break more?
- Does low oil quality increase breakdown risk?
- Does high mileage increase failure?

After learning, it predicts:  
👉 For new cars → Will they break down in 30 days? (Yes / No)

## Workflow

### 1. Importing Tools

It loads libraries that help with:

- Reading data
- Cleaning data
- Creating graphs
- Building AI models
- Evaluating predictions

Think of libraries as tools in a toolbox.

### 2. Loading the Data

It loads:

- Training data → Used to teach the model
- Test data → Used to make final predictions

Training data includes the correct answers (did it break down or not).

Test data does NOT include the answer — the model must predict it.

### 3. Understanding the Data

They check:

- How many rows?
- What columns exist?
- What are the data types?
- Is the dataset balanced?

They also check target distribution.

Target = Breakdown (Yes/No)

They found:  
👉 Only ~17% break down  
👉 83% do NOT break down

This is important because:

If a model always predicts “No breakdown,” it would be 83% accurate — but useless.

So accuracy alone is not enough.

They focus more on:

- Recall
- F1-score
- ROC-AUC

### 4. Visualizing Target Distribution

They make a bar chart to see:

- How many cars broke down
- How many did not

This helps understand imbalance.

### 5. Data Cleaning

Real-world data is messy.

They fix:

- Negative mileage → corrected
- Negative values → clipped
- Percent values → limited between 0 and 100

👉 This makes data realistic and clean.

### 6. Splitting Data

They split training data into:

- Training set → Model learns from this
- Validation set → Model is tested on this

Important:  
They test performance on unseen data to check if it generalizes.

### 7. Preprocessing

Before AI can learn:

- Numbers → Filled with median values if missing
- Categories (like vehicle type) → Converted into numbers using One-Hot Encoding

Why?

Machines only understand numbers.

So text categories must be transformed into numerical form.

### 8. Random Forest Model

They use a model called:

🌲 Random Forest

Concept:

- It builds many decision trees
- Each tree makes a prediction
- The system combines all trees
- Final decision = majority vote

Why?

Because:

- It handles nonlinear patterns
- Works well with tabular data
- Reduces overfitting

They also use:  
`class_weight="balanced"`

Why?  
Because breakdown cases are rare — so the model must pay attention to them.

### 9. Threshold Tuning

The model outputs probabilities like:

- 0.75 → 75% chance of breakdown
- 0.20 → 20% chance

They choose a threshold:

- If probability > 0.4 → Predict breakdown

Why not 0.5?

Because lowering threshold increases recall — meaning:  
👉 We catch more breakdown cases.

In this project, catching breakdowns is more important than avoiding false alarms.

### 10. Evaluation

They measure:

- Accuracy
- ROC-AUC
- Confusion Matrix
- Classification Report

These metrics tell:

- How many breakdowns were correctly predicted?
- How many were missed?
- How many false alarms?

The confusion matrix shows prediction mistakes clearly.

### 11. Feature Importance

This step answers:

👉 Which features influenced predictions the most?

Example:  
Maybe mileage contributed more than oil quality.

This helps understand:

- What factors increase breakdown risk?
- What matters most?

Very important for business insight.

### 12. Logistic Regression Comparison

They test another model:

📊 Logistic Regression

Why?

To compare performance.

If Random Forest performs better → They choose it.

Model comparison ensures they pick the best model.

### 13. Final Prediction (Kaggle Submission)

Now they:

- Use the trained model
- Apply it to test data
- Predict breakdown probability
- Convert probability into 0 or 1 using threshold
- Save results in `submission.csv`

This file is uploaded to Kaggle.