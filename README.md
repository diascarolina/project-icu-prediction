# COVID-19 - Clinical Data to Assess Diagnosis
[<img src="https://img.shields.io/badge/author-Carolina%20Dias-ff69b4?style=flat-square"/>](https://github.com/diascarolina) [![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=flat-square&logo=Jupyter)](https://jupyter.org/try) [![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg?style=flat-square)](https://github.com/diascarolina/project-icu-prediction/blob/main/LICENSE)

![]()

# Table of Contents

- [What **problem** do we have here? What can we do to **help**?](#intro)
- [Where did this **data** come from? What kind of **information** do we have in it?](#dat)
- [Methodology](#method)
- [Technologies Used](#tech)
- [Conclusion](#concl)
- [Acknowledgments](#ack)
- [References](#refs)
- [Contact](#contac)

<a name="intro"></a>
# What **problem** do we have here? What can we do to **help**?

The COVID-19 pandemic. Unfortunately we are all aware of it by now. We all know the sad and high number of deaths and the hopeful increasing number of vaccinated people (in some countries).

Seeing as the number of people infected by the virus keeps growing, we need more and more ways of better allocating these patients so as not to overwhelm our healthcare systems.

In this context, brazilian hospital Sírio-Libânes [published a dataset at Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) urging people to take action in predicting the need for ICU beds.

The tasks at hand are:

**Task 01:** Predict admission to the ICU of confirmed COVID-19 cases.

Based on the data available, is it feasible to predict which patients will need intensive care unit support?
The aim is to provide tertiary and quarternary hospitals with the most accurate answer, so ICU resources can be arranged or patient transfer can be scheduled.

**Task 02:** Predict NOT admission to the ICU of confirmed COVID-19 cases.

Based on the subsample of widely available data, is it feasible to predict which patients will need intensive care unit support?
The aim is to provide local and temporary hospitals a good enough answer, so frontline physicians can safely discharge and remotely follow up with these patients.

<a name="dat"></a>
# Where did we get this **data**? What kind of **information** do we have in it?

The data was taken directly from the [Kaggle problem](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) and uploaded to [Github](https://github.com/diascarolina/data-science-bootcamp/blob/main/data/Kaggle_Sirio_Libanes_ICU_Prediction.xlsx?raw=true) for easy access.

**From Kaggle:**

> The dataset contains **anonymized data** from Hospital Sírio-Libanês, São Paulo and Brasília. All data were anonymized following the best international practices and recommendations.

> Data has been cleaned and **scaled** by column according to MinMaxScaler to fit between -1 and 1.

_Disclaimer._ It is highly recommended that we apply a scaler to the data only **after** splitting between train and test data (_source:_ [Data Normalization Before or After Splitting a Data Set?](https://www.baeldung.com/cs/data-normalization-before-after-splitting-set)).  But since our data is already scaled, we won't go in too much detail in this aspect.

**From our dataset we have:**

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

> Beware **NOT to use the data when the target variable is present**, as it is unknown the order of the event (maybe the target event happened before the results were obtained). They were kept there so we can grow this dataset in other outcomes latter on.

**Examples obtained from Kaggle description:**

![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F1591620%2Fb1bc424df771a4d2d3b3088606d083e6%2FTimeline%20Example%20Best.png?generation=1594740856017996&alt=media)

![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F1591620%2F77ca2b4635bc4dd7800e1c777fed9de1%2FTimeline%20Example%20No.png?generation=1594740873237462&alt=media)



