# INTRODUCTION 

In the age of data-driven decision-making, the complexities of multidimensional datasets necessitate advanced analytical techniques. Our endeavor revolves around the creation of a CardioRiskAnalyzer Streamlit app, leveraging data mining to predict heart disease likelihood. This report chronicles our journey from data sourcing and cleaning to model selection, aiming to empower users with personalized health risk assessments. Through this innovative application, we aspire to revolutionize proactive health management and decision-making processes.
Data Source
The dataset for the CardioRiskAnalyzer Streamlit app is sourced from Kaggle and originates from the Behavioral Risk Factor Surveillance System (BRFSS) by the CDC. It includes a wide range of health attributes, habits, and demographic details of individuals, covering physical and mental health indicators, lifestyle factors, and demographic information like age, gender, state of residence, and race/ethnicity.

## DATA CLEANING 

A.	Restate the question

To enhance our understanding of heart disease variables, we'll employ diverse data-cleaning methods. Our goal is to refine the dataset systematically, pinpointing essential features associated with heart disease. This approach enables a thorough analysis, revealing insights that enrich our understanding of heart-related conditions.

B.	Techniques used for data cleaning

Upon initial exploration of our dataset, we identified 6 variables containing missing data, with one falling into the categorical and 5 into the numerical category. Addressing this, we implemented three prominent techniques for handling missing values. 

1.	Handling Missing Values
•	Imputing Missing Values in Tetanus, Pneumovax, and Flu Vaccination Columns Columns with Missing Values: 'tetanuslast10tdap', 'pneumovaxever', 'fluvaxlast12'
•	Imputation Strategy: Mode imputation (replacing missing values with the most frequent value)
•	Imputing Missing BMI Values: Predict missing 'bmi' values using linear regression based on weight in kilograms.
•	Dropping Rows with Missing Values in Specified Columns: Dropping rows with missing values in the specified columns.


Columns: 'hadheartattack', 'haddepressivedisorder', 'hadcopd', 'hadasthma', 'hadstroke', 'physicalactivities', 'haddiabetes' 

•	Imputing Missing Values for Other Categorical Variables: Replace missing values with the mode for each respective column.
Columns: 'difficultyconcentrating', 'difficultywalking', 'agecategory', 'mentalhealthdays', 'sleephours', 'physicalhealthdays', 'alcoholdrinkers', 'ecigaretteusage', 'smokerstatus'


2.	Handling Data Types


•	Convert float values to integers where appropriate.


C.Defend How You Got the Conclusion and How That Resonates with the Business Problem:


1.	Mode Imputation for Categorical Variables with Missing Values:
•	Method Chosen: Mode imputation was used to replace missing values in categorical variables such as 'tetanuslast10tdap', 'pneumovaxever', and 'fluvaxlast12'.
•	Reasoning: Mode imputation is a simple and effective technique for handling missing values in categorical variables. Since these variables represent categorical responses (e.g., vaccination status), using the mode (most frequent value) preserves the distribution of responses and is suitable for categorical data. we have used the most frequent state in simple imputer because the vaccine can then predict the most common one.


2.	Linear Regression for BMI Imputation:
•	Method Chosen: Linear regression was employed to predict missing 'bmi' values based on the weight in kilograms.
•	Reasoning: Linear regression is a suitable method when there is a linear relationship between the predictor and target variables. In this case, weight in kilograms is expected to have a linear relationship with BMI. Using linear regression allows us to impute missing BMI values based on a continuous predictor variable, which is more accurate than simple imputation methods. I have used bmi and weight relation because of the coorleation heat map.


3.	Dropping Rows with Missing Values:
•	Method Chosen: Rows with missing values in specified columns such as 'hadheartattack', 'haddepressivedisorder', etc., were dropped.
•	Reasoning: Dropping rows with missing values is a straightforward approach to handling missing data when the number of missing values is relatively small compared to the dataset size. Since the missing values were in key columns related to the health conditions of individuals, it was deemed appropriate to drop these rows to ensure the integrity of the data for analysis.


4.	Mode Imputation for Other Categorical Variables:
•	Method Chosen: Mode imputation was used for other categorical variables like 'difficultyconcentrating', 'agecategory', etc.
•	Reasoning: Mode imputation is a robust method for handling missing values in categorical variables when there is no strong relationship between the predictor and target variables. It preserves the original distribution of the data and is suitable for variables with discrete categories. After checking there isn’t any relationship between categorical maximum found 0.51 as high score. I have Mode simple imputer instead of normal mode imputation because an algorithm approach would give us more accurate values and it wouldn’t repeat values because I have used age as a dependent variable for this approach to make a difference.


## Feature Engineering
1.	Smoker status
•	A new feature called 'smoking_status'. This new feature aims to capture the combined information about an individual's smoking behavior, considering both traditional smoking and e-cigarette usage.
•	The rationale behind this feature engineering is to create a more comprehensive representation of smoking behavior. By consolidating these two related variables into a single feature, we can simplify the dataset and potentially uncover more meaningful insights about the relationship between smoking habits and other factors in the dataset.
•	Overall, this feature engineering technique helps streamline the dataset while preserving important information about smoking habits, which could be valuable for subsequent analysis and modeling tasks.


2.	Vaccination Status
•	This code snippet combines three columns, 'fluvaxlast12', 'pneumovaxever', and 'tetanuslast10tdap', into a new feature called 'vaccination_status'. This new feature aims to provide a consolidated representation of an individual's vaccination history across different types of vaccines.
•	The rationale behind this feature engineering is to simplify the dataset by aggregating related information into a single variable. By combining the vaccination status for different diseases into one feature, we can reduce the dimensionality of the dataset while retaining the essential information about an individual's immunization status.
•	For example, if an individual has received the flu vaccine in the last 12 months, the pneumonia vaccine ever, and the tetanus vaccine in the last 10 years, their vaccination status in the new 'vaccination_status' column would be represented as 'Yes_Yes_Yes'.
•	This approach allows us to capture the overall vaccination status comprehensively, considering multiple vaccines simultaneously. It can facilitate subsequent analysis and modeling tasks by providing a more concise and informative representation of vaccination history.



## EXPLORATORY DATA ANALYSIS

**A. Restate the Question**


In this analysis, we delve into the distribution of both age categories and smoker statuses within our dataset. By scrutinizing these variables, we aim to uncover discernible patterns or correlations that could potentially serve as indicators for predicting heart attack risks among individuals.  


**B. Techniques Used**
•	For our analysis, we’ve employed a combination of a bar chart and an overlaid line graph. The bar chart provides a clear, visual representation of the frequency of individuals within distinct age brackets. The line graph, in turn, allows us to track trends and fluctuations across these categories, lending insight into the data's distribution and central tendencies.
•	A bar chart serves as the chosen visualization tool, depicting the frequency of individuals within distinct smoker status categories: ‘Never smoked’, ‘Current smoker - now smokes some days’, ‘Former smoker’, and ‘Current smoker - now smokes every day’. The bar chart is particularly effective in offering a straightforward comparison of prevalence rates across these categories.


**C.Defend How You Got the Conclusion and How That Resonates with the Business Problem:**
Upon examining the visual data, we observe that the age groups “50 to 54” and “55 to 59” exhibit higher frequencies. This prominence could imply a greater prevalence of heart attack cases within these demographics, or it might simply reflect a larger population count within the sample. In contrast, the “80 or older” category shows a marked decrease in frequency, hinting at a smaller population within this age range or a lower incidence of heart attacks. Notably, the middle-aged segment appears to be more represented in the dataset, aligning with the established medical understanding that this age group bears a heightened risk of heart attacks. The findings from this EDA are valuable for guiding focused medical interventions and preventative measures in populations that are statistically more susceptible.


The data presented in the bar chart indicates a predominant number of individuals who have ‘Never smoked’, with ‘Former smokers’ representing a smaller portion of the population. The categories for ‘Current smoker - now smokes some days’ and ‘Current smoker - now smokes every day’ have even fewer individuals. This pattern points to a predominance of non-smokers in the dataset, potentially skewing the overall heart attack risk profile toward lower incidence rates. Understanding the distribution of smoking habits is vital in assessing heart attack risk, as smoking is a well-known risk factor. Thus, the representation of smoker statuses in the dataset is imperative for constructing a nuanced, predictive model for heart attack occurrences. This model, while informed by the current findings, would benefit from incorporating more detailed patient data to enhance its predictive accuracy and relevance to health-related business problems.


**D.	Key insights from EDA**
BMI vs Physical Health Days: The data shows that individuals with a lower BMI generally report a consistent number of healthy days, but this varies more widely as BMI increases. This pattern is important for predicting heart attack risk since a higher BMI can be associated with greater health complications, which may influence the occurrence of heart attacks.
Age Category vs Sleep Hours: Sleep duration is relatively consistent across all age groups, with most adults getting around 7 hours, despite some outliers reporting more. Since sleep is a critical factor in overall cardiovascular health, understanding that sleep duration does not significantly vary with age can help refine risk predictions for heart attacks, as it suggests other factors may be more indicative of risk in different age groups.



## Building and finalizing the model

**A. Models we have tried**
•	Logistic Regression: We initiated our analysis with Logistic Regression, chosen for its aptness in binary classification tasks, making it ideal for predicting heart disease presence. Its simplicity and interpretability are advantageous for discerning the intricate relationship between health attributes, habits, and demographic factors regarding heart disease risk. Through Logistic Regression, we aim to gain precise insights into the factors influencing heart disease likelihood.
•	Random Forest Classifier: We also explored the Random Forest Classifier, chosen for its capability to handle complex datasets with high dimensionality. Unlike Logistic Regression, Random Forest can capture intricate non-linear relationships between features and the target variable, potentially improving predictive accuracy. By leveraging ensemble learning techniques, Random Forest mitigates overfitting and generalizes well to unseen data, ensuring reliable heart disease risk predictions. Through this exploration, we aimed to assess its effectiveness and suitability for our business problem.

**B. Finalizing the model to build an app**

Both Logistic Regression and Random Forest Classifier exhibited similar accuracy scores, highlighting their comparable performance in predicting heart disease likelihood. However, to make an informed decision on the model to finalize for the CardioRiskAnalyzer app, we delved deeper into the confusion matrices. Upon closer inspection, it became evident that Random Forest Classifier outperformed Logistic Regression in minimizing false negatives. In the context of predicting heart disease, false negatives—instances where the model incorrectly predicts no heart disease when it is present—carry significant implications as they may lead to undetected risks and potential health complications for individuals. Given Random Forest's ability to reduce false negatives, it offers enhanced sensitivity in identifying individuals at risk of heart disease, thereby making it the preferred choice for finalizing the model to be integrated into the CardioRiskAnalyzer app.



**## Product Overview and User Guide**

**A.	Overview**

The CardioRiskAnalyzer is an innovative tool designed to provide personalized risk assessments for heart disease. By leveraging advanced data analytics and machine learning algorithms, the app aims to empower individuals with valuable insights into their cardiovascular health. From analyzing physical and mental health indicators to considering lifestyle habits and demographic details, the CardioRiskAnalyzer offers a comprehensive approach to assessing heart disease risk. Whether for preventive care or proactive management, the product serves as a valuable resource for individuals seeking to understand and address their heart health.

**B.	User Guide**

1.	Parameter Selection: Begin by selecting various parameters relevant to your health profile, including physical health days, mental health days, sleep hours, physical activities, medical history (e.g., had a stroke, had asthma), BMI, alcohol consumption, vaccination history, age range, and smoking status. Input your information accordingly using the provided fields or dropdown menus.


2.	Error Handling: Ensure to enter all required parameters accurately before clicking on the “Predict” button. In case you forget to input your BMI value, the app will prompt an error message, requesting you to enter your BMI before proceeding with the prediction process.


3.	Prediction Process: Once all parameters are entered, click on the “Predict” button to initiate the prediction process. The CardioRiskAnalyzer will utilize the input data to generate a personalized risk assessment for heart disease.


4.	Review Results: After the prediction process is complete, the app will display the results on the screen. Review the prediction outcome, which will indicate whether you are at low, moderate, or high risk of developing heart disease based on the entered parameters.



## Conclusion

The CardioRiskAnalyzer app empowers users to proactively manage their cardiovascular health through personalized risk assessments. Leveraging advanced analytics and machine learning, the app provides valuable insights into potential heart disease risks. With user-friendly features and robust error-handling mechanisms, it ensures seamless usability and accuracy. Continuous refinement and updates are prioritized to enhance capabilities, ultimately facilitating better health outcomes and informed decision-making for users.

