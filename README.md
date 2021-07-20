# Diagnosing Patient’s Stroke Risk Using Health Data
According to the CDC, 1 in every 6 deaths from cardiovascular disease is due to stroke -- our goal is to create a model that helps inform a patient about their personal risk for enduring a stroke. This model could take a generalized process and produce something much more personal for each patient. A common complaint about the current state of the healthcare system in the US is the lack of personalization and the overwhelming amount of generalization occurring from patient to patient. With statistics such as someone having a stroke every 40 seconds in the US, it seems like the obvious choice to make sure we are taking the time to accurately diagnose a patient’s risk for stroke so that the patient can take the appropriate steps to reduce their risk. 

# 1. Data 
The stroke prediction dataset contains patient information pulled from a kaggle dataset. The dataset aims to predict whether a patient is likely to suffer a stroke based on input parameters such as gender, age, hypertension, smoking status, and a few lifestyle type statuses. We pulled in the data from .csv format and read it in as a DataFrame.
* [Kaggle Dataset] (https://www.kaggle.com/fedesoriano/stroke-prediction-dataset)

# 2. Data Cleaning and Wrangling 
Data from this dataset did not require any cleaning. The data was read in as a DataFrame
with 5110 rows and 12 columns. Most work was done during Exploratory Data Analysis.

# 3. Exploratory Data Analysis (EDA) and Initial Findings 
## Missing Values 
The primary step taken during Exploratory Data Analysis was to address missing values found in the data set.

#### _BMI_
During EDA, we found that 3.93% of values in the BMI column were missing. To address this issue, we imputed the average BMI of 28.89 for each missing value. This imputation did not change the overall mean of the column but did bring a slight shift to the standard deviation bringing it from 7.85 to 7.70. The shift was considered negligible.

#### _Distributions_
The distribution for each feature was checked for both stroke positive and stroke negative patients.


1. Marital Status 

![Screen Shot 2021-07-18 at 7 48 07 PM](https://user-images.githubusercontent.com/79958096/126095570-1a454e7c-5326-43f7-bddd-a04228b3e3f6.png)

The marital status distribution comparison showed that more people in the stroke positive group were married (88%); this was also true for the stroke negative patients but at a lower percentage (64.5%). Resulting in a wider difference between groups in the stroke positive group.

2. Work Type 

![Screen Shot 2021-07-18 at 7 48 51 PM](https://user-images.githubusercontent.com/79958096/126095624-1cad531c-f728-4caf-960d-085f618509bd.png)

For both the stroke positive and stroke negative groups, patients who worked a private job were the highest population -- 59.8% for the stroke positive group and 57.1% for the stroke negative group. The private job employees were followed by those who were self-employed. This distribution was expected since most of the general population tends to be privately employed. The most significant difference between the two distributions was that none of the patients from the “Never worked” population appeared in the stroke positive group. This difference could be due to such a small sample of those who had never worked ( only 0.43% of the entire dataset’s population).

3. Residence Type 

![Screen Shot 2021-07-18 at 7 50 29 PM](https://user-images.githubusercontent.com/79958096/126095742-a9e102a6-339b-449b-b7f8-5a93a12a06fa.png)


For both the stroke positive and negative groups, the Urban populations hold the majority -- 54.2% in stroke positive groups and 50.6% in the stroke negative groups.

4. Smoking Status

![Screen Shot 2021-07-18 at 7 51 00 PM](https://user-images.githubusercontent.com/79958096/126095778-0de92206-07cd-4ef7-8e37-d20e6d1e0652.png)


Patients that reported as “Never Smoked” held the majority in both populations -- 36.2% in the stroke positive group and 37.1% in the stroke negative group. Interestingly enough, the smallest population for the stroke positive group was the patients who reported as smokers (16.9%). This feature group did have 30.2% of its data categorized as “Unknown” which could play a part in the unexpected results found during EDA.

5. Gender 

![Screen Shot 2021-07-18 at 7 51 33 PM](https://user-images.githubusercontent.com/79958096/126095822-8e433237-c9b0-45f0-811a-c7157c07f146.png)


Females were the majority in both the stroke positive and stroke negative groups -- 56.6% in the stroke positive group and 58.7% in the stroke negative group. This feature group was imbalanced with 17% more females than there were males.

6. Age 
 
![Screen Shot 2021-07-18 at 7 52 42 PM](https://user-images.githubusercontent.com/79958096/126095910-95ec8fb0-7b4f-4a5b-97a3-95faccff1ef3.png)


Patients who reported as stroke positive were generally found in the older groups. Distributions showed that 75% of patients in the stroke positive group were above the age of 59 with an average age of 68 years.

7. Average Glucose Levels

![Screen Shot 2021-07-18 at 7 53 36 PM](https://user-images.githubusercontent.com/79958096/126095979-e5287285-2874-4dbc-8b91-2ce1631d7b10.png)


For our dataset as whole, the average value fell at 132.54 which is a normal glucose reading. 24.6% of patients were within the diabetic range (75th percentile = 196.71) and 10.8% of patients were within the prediabetic range (25th percentile = 79.9). When analyzing patients from the stroke positive and stroke negative groups separately, it was found that 48.1% of stroke positive patients had abnormal glucose readings.

8. BMI 

![Screen Shot 2021-07-18 at 7 54 10 PM](https://user-images.githubusercontent.com/79958096/126096024-d5a74c50-c65c-4994-a7d5-d06318fa7dec.png)


A majority of stoke positive patients were reported to be either overweight or obese (84.7%) with a larger percentage (46.2%) of this group falling within the overweight range (BMI 25.0-29.9).

9. Hypertension

![Screen Shot 2021-07-18 at 7 55 01 PM](https://user-images.githubusercontent.com/79958096/126096096-e614dc7e-9a23-4184-8cda-ee8705f47495.png)


There was a noticeable difference between stroke positive patients with hypertension and stroke negative patients with the same diagnosis. While the majority for both groups was those who did not have hypertension, the distribution of people in the stroke positive group with hypertension showed as 26.5%, while those with hypertension in the stroke negative group only reported at 8.8%.

10. Heart Disease 

![Screen Shot 2021-07-18 at 7 55 46 PM](https://user-images.githubusercontent.com/79958096/126096148-89978b27-df10-462e-a84f-d11c8db3d596.png)


There was a noticeable difference in the heart disease distributions as well. 18.9% of patients with heart disease appeared in the stroke positive group and only 4.7% lie in the stroke negative group.

#### _Statistical Significance_

The features below were tested and proven to have statistical significance in the determination of a patient’s stroke risk:
  * Work Type
  * Smoking Status
  * Marital Status
  * Hypertension
  * Heart Disease
  * Age
  * BMI
  * Average Glucose Levels

The only two features that did not show statistical significance were Gender and Residence Type. Since there is already research showing gender is an important factor in determination of stroke risk, it was not dropped from the dataset. A model was built with the Residence Type feature included as well as a model without it included -- overall, performance was better when the Residence Type feature was kept within the data.

# 4. Modeling 

A Random Forest Classifer was used the model our data. It was determined that keeping the Residence Type The following parameters were used for our model:
  * n_estimators = 2500
  * min_samples_split = 5
  * min_samples_leaf = 1 
  * max_features = 'auto'
  * max_depth = 30

The ROC/AUC Score for our model came out to 0.992

![Screen Shot 2021-07-19 at 5 11 47 PM](https://user-images.githubusercontent.com/79958096/126244583-f919d6af-817c-436f-88e8-03c0afb62352.png)

The Confusion Matrix Results for our model were: 
  * True Negative: 1449
  * False Positive: 26
  * False Negative: 80
  * True Positive: 1362 

![Screen Shot 2021-07-19 at 5 11 39 PM](https://user-images.githubusercontent.com/79958096/126244658-5c893bf7-c1ff-4bf1-a6bd-8bca8e0dd2bb.png)


# 5. Future Work 
Since all of this data is generally already collected from most patients that are seen by a doctor, it could become a model that is integrated in a normal chart processing system that can alert a doctor about a patient’s risk level. The idea is to work on preventative care instead of risking fatality or post disease treatment.

