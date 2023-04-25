# glassdoor-salary-prediction

Employing Supervised Machine Learning Models to predict average salary of Data Science Glassdoor jobs. 

## About dataset

This dataset is sourced from Kaggle (https://www.kaggle.com/datasets/rashikrahmanpritom/data-science-job-posting-on-glassdoor). The dataset scrapes information about Data Science job posts from Glassdoor's. It contains the following fields:

Job Title: Title of the job posting
Salary Estimation: Salary range for that particular job
Job Description: This contains the full description of that job
Rating: Rating of that post
Company: Name of company
Location: Location of the company
Headquarter: Location of the headquater
Size: Total employee in that company
Type of ownership: Describes the company type i.e non-profit/public/private farm etc
Industry, Sector: Field applicant will work in
Revenue: Total revenue of the company
Competitors: List of competitors
Founded: year founded
Index: index

## Data Cleaning / Feature Engineering

Dataset needs to undergo extensive data cleaning and feature engineering. 

Summary of data cleaning and preprocessing steps:
- Dropping redundant index column
- Dropping duplicate rows
- Removing rating from 'Company Name': 'Google\n4.4' --> "Google'
- Extracting min, max, avg, and range from 'Salary Estimation' column
- Replacing '-1' with Nan values, dropping sparse column 'Competitors'
- Imputing Nan values in Rating with mean values
- Calculating 'company age' based on 'Founded' column
- Generating 'seniority' boolean column if 'Job Title' contains key workds like 'Sr', 'Senior', 'VP' etc. 
- Extracting skills from job description column. Creating boolean columns for 'python', 'sql', 'aws', 'tableau', 'deep_learning', 'big_data', 'stats', 'cuda' , 1 if exists in description else 0
- Using Ordinal Encoder to encode 'Company Name', 'industry', 'Job Title', 'Location' into numeric features for ML modeling. 

Engineered Features:

min_salary,max_salary,salary_range, avg_salary: Refers to the minimum, maximum, given range, and average salary for that post
company_age: Age of company
'python', 'sql', 'aws', 'tableau', 'deep_learning', 'big_data', 'stats', 'cuda': Some most appeared skills in boolean columns form
seniority: if job type is senior or not (0/1)
'company_name_code', 'industry_code', 'job_title_code', 'location_code': encoded categorical columns 

## Modeling

Objective: Create a model that predicts 'avg_salary'.

Following features selected for modeling: 'company_name_code', 'industry_code', 'job_title_code', 'location_code', 'Rating', 'salary_range', 'company_age', 'seniority', 'python', 'sql', 'aws', 'tableau', 'big_data', 'deep_learning', 'cuda', 'stats'

Target variable: 'avg_salary'

Models used:
- Linear Regression
- Decision Tree 
- Random Forest 
- XGBoost

Performance Metrics:
- Root Mean Square Error
- Mean Absolute Error
- R^2

## Summary of results

Random Forest model was able to predict 'avg_salary' with the best, R^2, MAE, and RMSE scores. XGBoost was the second best predictor. Linear regression, performed worst. 'Rating' was the most important feature. 

## Next possible steps...

To improve the project, the dataset could be scraped again to include more types of job postings (eg SDE, PM, DA), more meta information (job benefits, reviews) collected over wider date range. Timestamps could be used to gather inights over season trends in job postings and salaries and allow us to account for seasonality (recessions, booms, periods of low hiring etc). 

In terms of modeling, due to the relative small size of the dataset, it is prone to overfitting as ML models generalize patterns in training data.  One could improve quality of predictions by removing outliers. It could also be beenficial to combine the predictions of several models or the same model with different hyperparameters to reduce variance and enhance generalization. This could be done by obtaining a weighted avergae of various predictions. 


