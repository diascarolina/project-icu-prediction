# Covid-19 - Clinical Data to Assess Diagnosis
[<img src="https://img.shields.io/badge/author-Carolina%20Dias-ff69b4?style=flat-square"/>](https://github.com/diascarolina) [![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg?style=flat-square)](https://github.com/diascarolina/project-icu-prediction/blob/main/LICENSE)

<p align="center">
  <img width="700" src="https://i.imgur.com/wxaTMWn.png">
</p>

# Table of Contents

1. [What **problem** do we have here? What can we do to **help**?](#intro)
2. [Where did this **data** come from? What kind of **information** do we have in it?](#dat)
3. [What **methodology** did we use for our analysis? What were the **steps taken**?](#method)
4. [Main Findings & Predictions](#find)
5. [What can we **conclude** from this project?](#conc)
6. [For Future Projects...](#fut)
7. [Technologies Used](#tech)
8. [Acknowledgments](#ack)
9. [References](#refs)
10. [Contact](#contac)

<a name="intro"></a>
# What **problem** do we have here? What can we do to **help**?

The COVID-19 pandemic. Unfortunately we are all aware of it by now. We all know the sad and high number of deaths and the hopeful increasing number of vaccinated people (in some countries).

Seeing as the number of people infected by the virus keeps growing, we need more and more ways of better allocating these patients so as not to overwhelm our healthcare systems.

In this context, brazilian hospital Sírio-Libânes [published a dataset at Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) urging people to take action in predicting the need for ICU beds.

The tasks at hand are:

🟢 **Task 01:** Predict admission to the ICU of confirmed COVID-19 cases.

Based on the data available, is it feasible to predict which patients will need intensive care unit support?
The aim is to provide tertiary and quarternary hospitals with the most accurate answer, so ICU resources can be arranged or patient transfer can be scheduled.

🟢 **Task 02:** Predict NOT admission to the ICU of confirmed COVID-19 cases.

Based on the subsample of widely available data, is it feasible to predict which patients will need intensive care unit support?
The aim is to provide local and temporary hospitals a good enough answer, so frontline physicians can safely discharge and remotely follow up with these patients.

<a name="dat"></a>
# Where did we get this **data**? What kind of **information** do we have in it?

The data was taken directly from the [Kaggle problem](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) and uploaded to [Github](https://github.com/diascarolina/data-science-bootcamp/blob/main/data/Kaggle_Sirio_Libanes_ICU_Prediction.xlsx?raw=true) for easy access.

**From Kaggle:**

> The dataset contains **anonymized data** from Hospital Sírio-Libanês, São Paulo and Brasília. All data were anonymized following the best international practices and recommendations.

> Data has been cleaned and **scaled** by column according to MinMaxScaler to fit between -1 and 1.

🟢 **From our dataset we have:**

1. Patient demographic information (03 columns)
2. Patient previous grouped diseases (09 columns)
3. Blood results (36 columns)
4. Vital signs (06 columns)

In total there are **54 features**, expanded when pertinent to the _mean, median, max, min, diff and relative diff_, where

- _diff = max - min_
- _relative diff = diff/median_

Furthermore, **our target variable is the ICU** column, in which we have **0** (zero) if that patient did not go to the ICU and **1** (one) if that corresponding patient did go to the ICU.

We also have a column called **Window**. What does this variable mean?

Again, from Kaggle:

> We were careful to include real life cenarios of window of events and available data. Data was obtain and grouped as follows:

- patient
    - patient encounter
    - aggregated by windows in chronological order


Window | Description
:---: | :---:
**0-2**	| From 0 to 2 hours of the admission
**2-4**	| From 2 to 4 hours of the admission
**4-6**	| From 4 to 6 hours of the admission
**6-12** | From 6 to 12 hours of the admission
**Above-12** | Above 12 hours from admission

<a name="method"></a>
# What **methodology** did we use for our analysis? What were the **steps taken**?

This project was divided into two main notebooks:

### 🟢 Part 1: Data Cleaning & Analysis

- [GitHub Link](https://github.com/diascarolina/project-icu-prediction/blob/main/notebooks/01_data_cleaning_and_analysis.ipynb) or [![](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1GbV_StVWhE5GUlYblbrWsJWzcRP_Dq7f?usp=sharing)
### 🟢 Part 2: Machine Learning

- [GitHub Link](https://github.com/diascarolina/project-icu-prediction/blob/main/notebooks/02_machine_learning_and_conclusion.ipynb) or [![](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1bLzbafHgRTXe2T4fFutOzRASrsSSs2or?usp=sharing)


For the first part we followed these **data cleaning** steps:

<p align="center">
  <img width="700" src="https://i.imgur.com/1AJyC0O.png">
</p>

Then we **analysed** the data as such:

<p align="center">
  <img width="700" src="https://i.imgur.com/MakbgMD.png">
</p>

Finally, for the **machine learning** part we followed:

<p align="center">
    <img width="700" src="https://i.imgur.com/BLDhdVY.png">
</p>

<a name="find"></a>
# Main Findings & Predictions

After our data cleaning process, we ended up with

- **352 rows**, one for each patient,
- **98** features and
- **1** target variable, our ```ICU``` column.

From the data analysis part, we've gathered some interesting information about the differences between patients that need to go to the ICU and those who did not. We've seen that age and gender play an important role that could be used in helping the prediction. For example, we can see here how the age group influences the need for ICU beds for patients:

<p align="center">
    <img width="700" src="https://i.imgur.com/7fCAglN.png">
</p>

From the machine learning modelling, we used the metric **F1-score**, that is a great way to balance precision and recall. We ended up with the following results from our modelling:

<p align="center">
    <img width="700" src="https://i.imgur.com/gJ2AqkY.png">
</p>

After taking a deeper look at the two best performing models, **LGBMClassifier** and **XGBoostClassifier**, we made our ICU prediction with the **LGBMClassifier** model. The final confusion matrix is:

<p align="center">
    <img width="400" src="https://i.imgur.com/635cX6H.png">
</p>

<a name="conc"></a>
# What can we **conclude** from this project?

From the cleaning part, we see that some data preparation was need in order to get an accurate sense of the data and to obtain the right kind information for analysis.

From the data analysis part, we can clearly see that many variables correlate with the need for a patient to go to the ICU. Age, gender, vital signs and blood results can be (anmd will be) very indicative and useful for our future machine learning modelling in predicting ICU admission.

COVID-19 has taken an enormous toll on healthcare systems all around the globe. Healthcare professionals are overworked and this raises the need for a helping hand. This can be achieved in the form of Machine Learning models used to predict the need for ICU beds for COVID-19 patients.

In this project we have seen that this is possible, but this tool can never be used alone (unless its predictions were right 100% of the time, but we're far from a model that achieves that). There needs to be a healthcare professional with better judgement than our models to assess the need for ICU admission.

<a name="fut"></a>
# For Future Projects...

For next projects, better hyperparameter tuning could lead to improved results and predictions.

This project could also be applied to other diseases, with the appropriate care and adaptations.

An interesting idea could be to implement a web app (for example, a Streamlit application) that receives the relevant information for a patient (or for a group of patients) and returns the prediction for the need of said patient to go to the ICU. It could also output a confidence value for that prediction, so healthcare professionals could take a closer look at patients in which the model could not predict very well.

<a name="tech"></a>
# Technologies Used

The notebooks were produced in [Google Colab](https://colab.research.google.com/) with the following libraries:
- Pandas 1.0.5
- Numpy 1.19.1
- Matplotlib 3.2.2
- Seaborn 0.11.1
- Sklearn 0.23.1
- LightGBM 2.3.1
- XGBoost 1.1.1
- Lazy Predict 0.2.9

<a name="ack"></a>
# Acknowledgments

This is the final project from [Alura](https://www.alura.com.br/)'s Data Science Bootcamp. Thanks for all the lessons to the instructors Thiago Gonçalves, Guilherme Silveira, Allan Spadini and last but not least, Karoline Penteado.

And thanks to my new friends who helped me all the way, Valquíria Alencar and Júnior Torres.

<a name="refs"></a>
# References

🟢 [Click here for the references used in this project.](https://github.com/diascarolina/project-icu-prediction/blob/main/docs/README.md)

<a name="contac"></a>
# Contacts

Any tips or suggestions? Feel free to contact me!

[<img src="https://img.shields.io/badge/carodias-0A66C2?style=flat-square&logo=linkedin&logoColor=white" />](https://www.linkedin.com/in/carodias/) [<img src="https://img.shields.io/badge/Gmail-EA4335?style=flat-square&logo=Gmail&logoColor=white" />](mailto:carolinadiasw@gmail.com)
