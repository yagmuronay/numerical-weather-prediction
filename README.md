## Table of Contents

* [1) About Project](#about)
* [2) Requirements](#installation)
* [3) File Descriptions](#file)
* [4) Exploratory Data Analysis](#analysis)
* [5) Acknowledgements](#acknowledgements)

## 1) About Project <a class="anchor" id="about"></a>

Main purpose of this project is the bias correction of next-day maximum and minimum air temperatures forecast of the LDAPS model operated by the Korea Meteorological Administration over Seoul, South Koreaperform. It is also of interest to have an exploratory analysis to get some valuable insights from the dataset [Bias correction of numerical prediction model temperature forecast Data Set from UCI](https://archive.ics.uci.edu/ml/datasets/Bias+correction+of+numerical+prediction+model+temperature+forecast#) that has data from Seoul South Korea summer from 2013 to 2017.

Moreover, this projects attempts to recreate the findings from paper [Cho, D., Yoo, C., Im, J., & Cha, D. (2020). Comparative assessment of various machine learning-based bias correction methods for numerical weather prediction model forecasts of extreme air temperatures in urban areas. Earth and Space Science.](https://agupubs.onlinelibrary.wiley.com/doi/epdf/10.1029/2019EA000740). Authors aim machine learning based bias correction of air temperature forecasts of a numerical model. To achieve this, following three machine learning models, similar to as in paper, are implemented:

* an SVM regressor,
* a random forest,
* an ANN with two hidden layers

as well as an ensemble (MME) of these three machine learning models is evaluated.

This project adds up on the paper by creating another MME from top 3 models, searched with pycaret. In this second pipeline, polynomial and trigonometric features form existing ones are created and feature selection is conducted to imrove the model performance.

## 2) Requirements <a class="anchor" id="installation"></a>

All the dependencies are listed in requirements.txt. Install them: 

using pip
> 
pip install -r requirements.txt

or using Conda.
> 
> conda create --name <env_name> --file requirements.txt


## 3) File Descriptions <a class="anchor" id="file"></a>

* **explore\_data.py:** This Jupyter notebookis for exploratory analysis of the data. Missing values are also handled here and saved for later.

* **cho\_mme.ipynb:** Jupyter notebook that is based on paper below*. Three machine learning models (SVM regressor, RF, ANN) are implemented and an MME predicton of those is performed. 10% of data is splitted for holdout validation . Furthermore, 600 data points in the training set are reserved for validation and early stoppin during the training of ANN.

	You can only run this notebook to see a similar pipeline to the one mentioned in paper.

* **data:** Folder with the dataset
	* **raw/Bias\_correction\_ucl.csv:** Data from Seoul South Korea summer from 2013 to 2017
	* **no\_missing_values/Bias\_correction\_ucl\_without\_na.csv:** Missing value handled data set, hence there are no null entries. Date column is converted to two columns: month and day  (float). Missing date valeues after deleting entries with any missing values in columns Next_Tmax or Next_Tmin are dropped.
* **models:** Folder with the saved models

## 4) Exploratory Data Analysis <a class="anchor" id="analysis"></a>

* Both target variables, Next\_Tmax and Next\_Tmin, are highly correlated with each other.
* Furthermore, both target variables are in high correlation with:
	* LDAPS\_Tmax\_lapse,
	* LDAPS\_Tmin\_lapse,
	* Present\_Tmax and,
	* Present\_Tmin.

* There is a negative correlation between LDAPSCC variables and LDAPS\_Tmax\_lapse, because cloudy days tend to have a lower temperature.
	

* The humidy is in high correlation with clouds (see LDAPS\_RHmin, LDAPSCC1, 2, 3, and 4).
* There is some correlation between the LDAPS\_PPT variables: the next day is likely to rain if it rained the rain before.
* Similaryly, LDAPSCC variables are also correlated between themselves: the next day is likely to be cloudy if it was cloudy the day before.

Missing value counts in variables that are highly correlated with Next\_Tmax and/ or Next\_Tmin:

* Present_Tmax 70
* Present_Tmin 70
* LDAPS_RHmin 75
* LDAPS_RHmax 75
* LDAPS_Tmax_lapse 75
* LDAPS_Tmin_lapse 75


## 5) Acknowledgements <a class="anchor" id="acknowledgements"></a>
* Dataset: [Bias correction of numerical prediction model temperature forecast Data Set](https://archive.ics.uci.edu/ml/datasets/Bias+correction+of+numerical+prediction+model+temperature+forecast#)
* Paper: [Cho, D., Yoo, C., Im, J., & Cha, D. (2020). Comparative assessment of various machine learning-based bias correction methods for numerical weather prediction model forecasts of extreme air temperatures in urban areas. Earth and Space Science.](https://agupubs.onlinelibrary.wiley.com/doi/epdf/10.1029/2019EA000740) 
