
## Predicting Bank Client's Financial Product subscription using Scikit Learn and XGBoost for imbalance dataset

This Code Pattern will focus on and guide you through how to use `xgboost`, `scikit learn` and `python` (in the Data Science Experience, or DSX) to predict Bank Client's subscription to financial product based off a [UCI reposository for Bank Marketing Data Set](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing).


Class imbalance is a common problem in data science, where number of positive samples are significantly less than number of negative samples. As data scientists, one would like to solve this problem to create classifier with good performance. XGBoost (Extreme Gradient Boosting Decision Tree) is very common tool for creating the Machine Learning Models for classification and regression. However, there are various tricks and techniques for creating good classification model using xgboost for imbalance data-set that it is non trivial and hence we have created this code pattern.

In this code pattern, 
We will illustrates the Machine Learning classification using the Extreme Gradient Boosted Tree. Gradient Boosted Tree, is usually a better choice compare to the logistic regression and other techniques. We will use the real life data set which is highly imbalance i.e the number of positive sample is much less than the number of negative samples.

We will walk the user to the the following conceptual steps


* Data Set Description.

* Exploratory Analysis to understand the data.

* Use various preprocessing to clean and prepare the data.

* Use naive XGBoost to run the classification.

    * Use cross validation to get the model.

    * Plot, precision recall curve and ROC curve.

* We will then tune it and use weighted positive samples to improve classification performance.

* We will also talk about the following advanced techniques.

    * Oversampling of majority class and Undersampling of minority class.

    * SMOTE algorithms.


![](doc/source/images/architecture.png)

## Flow

* Log into IBM's DSX service.

* Upload the data as a data asset into DSX.

* Start a notebook in DSX and input the data asset previously created.

* Follow following discussion and steps.

1. Introduction and Background.

2. Data Set Description.

3. Statement of Classification Problem.

4. Software and Tools(Xgboost and Scikit Learn).

5. Visual Data Exploration to understand data (Using seaborn and matplotlib).

6. Create Scikit learn ML Pipelines for Data Processing.

7. Model Training.

  7.1 What and Why of XGBoost.

  7.2 Discuss Metrics for Model Performance.

  7.3 First Attempt at Model Training and it's performance,evaluation and analysis.

  7.4 Strategy For Better Classifier for the Imbalance Data

  7.5 Second Attempt at Model Training using Weighted Samples and it's performance, evaluation and analysis.

  7.6 Third Attempt at Model Training using Weighted Samples and Feature Selection and it's performance analysis.

8. Inference Discussion (Generalization cwand Prediction)

9. Summary about what we learned about various techniques.

10. Pointers to Other Advanced Techniques like OverSampling, UnderSampling and SMOTE algorithms.

11. References for further reading.


## Included components

* [IBM Data Science Experience](https://www.ibm.com/bs-en/marketplace/data-science-experience): Analyze data using RStudio, Jupyter, and Python in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.
* [Jupyter Notebook](http://jupyter.org/): An open source web application that allows you to create and share documents that contain live code, equations, visualizations, and explanatory text.

## Featured technologies

* [Data Science](https://medium.com/ibm-data-science-experience/): Systems and scientific methods to analyze structured and unstructured data in order to extract knowledge and insights.
* [Python](https://www.python.org/): Python is a programming language that lets you work more quickly and integrate your systems more effectively.
* [XGBoost](https://github.com/dmlc/xgboost): Extreme Gradient Boosting is decision tree based tools for creating ML model.
* [Scikit Learn](http://scikit-learn.org/stable/):  A Python library for providing efficient tools for data mining and machine learning.
* [Pandas](http://pandas.pydata.org/): A Python library providing high-performance, easy-to-use data structures.
* [Matplotlib](https://matplotlib.org/): A Python library integrating matplot for visualization.
* [SeaBorn](https://seaborn.pydata.org/): Another higher level Python library for visualization.


# Steps

This Code Pattern consists of following activities:

* [Run a Jupyter notebook in the IBM Data Science Experience.](#run-a-jupyter-notebook-in-the-ibm-data-science-experience)
* [Run end to end ML pipeline  Analyze and Predict the data](#analyze-and-predict-the-data).

## Run a Jupyter notebook in the IBM Data Science Experience

1. [Sign up for the Data Science Experience](#1-sign-up-for-the-data-science-experience)
2. [Create the notebook](https://github.com/IBM/ds_xgboost_clf_4_imbalance_data#2-create-the-notebook)
3. [Run the notebook](#3-run-the-notebook)
4. [Save and Share](#4-save-and-share)

### 1. Sign up for the Data Science Experience

Sign up for IBM's [Data Science Experience](https://datascience.ibm.com/). By signing up for the Data Science Experience, two services: ``DSX-Spark`` and ``DSX-ObjectStore`` will be created in your IBM Cloud account. If these services do not exist, or if you are already using them for some other application, you will need to create new instances.

To create these services:
* Login to your [IBM Cloud](http://bluemix.net) account.
* Create your Spark service by selecting the service type [Apache Spark](https://console.bluemix.net/catalog/services/apache-spark). If not already used, name your service ``DSX-Spark``. 
* Create your Object Storage service by selecting the service type [Cloud Object Storage](https://console.bluemix.net/catalog/infrastructure/object-storage-group). If not already used, name your service ``DSX-ObjectStorage``.

> Note: When creating your Object Storage service, select the ``Swift`` storage type in order to avoid having to pay an upgrade fee.

Take note of your service names as you will need to select them in the following steps.

![](doc/source/images/Screen%20Shot%202017-12-06%20at%202.22.06%20PM.png)

### 2. Create the notebook

> Note: if you would prefer to skip these steps and just follow along by viewing the completed Notebook, simply:
> * View the completed [notebook](https://github.com/aloknsingh/ds_xgboost_clf_4_imbalance_data/tree/master/notebooks/predict_bank_cd_subs_by_xgboost_clf_for_imbalance_dataset.ipynb) and its outputs, as is.
> * While viewing the notebook, you can optionally download it to store for future use.
> * When complete, continue this code pattern by jumping ahead to the [Analyze and Predict the Data](#analyze-and-predict-the-data) section.

If you want to create the project on your own, first you must create a new Project:
* From the [IBM Data Science Experience page](https://apsportal.ibm.com/analytics) either click the ``Get Started`` tab at the top or scroll down to ``Recently updated projects``.
* Click on ``New project`` under ``Recently updated projects``.
* Enter a ``Name`` and optional ``Description``. 
* For ``Spark Service``, select your Apache Spark service name.
* For ``Storage Type``, select the ``Object Storage (Swift API)`` option.
* For ``Target Object Storage Instance``, select your Object Storage service name.
* Click ``Create``.

Create the Notebook:
* Click on your project to open up the project details panel.
* Click ``add notebooks``.
* Click the tab for ``From URL`` and enter a ``Name`` and optional ``Description``.
* For ``Notebook URL`` enter: https://github.com/aloknsingh/ds_xgboost_clf_4_imbalance_data/tree/master/notebooks/predict_bank_cd_subs_by_xgboost_clf_for_imbalance_dataset.ipynb
* For ``Spark Service``, select your Apache Spark service name.
* Click ``Create Notebook``.

Upload the data as data assets:
* This project has 1 datasets. Upload these as data assets in your project. Do this by loading each dataset into the pop up section on the right hand side.
* Once complete, go into your notebook in the edit mode (click on the pencil icon next to your notebook on the dashboard). 
* Click on the ``1001`` data icon in the top right. The data files should show up. 
* Click on each and select ``Insert Pandas Data Frame``. Once you do that, a whole bunch of code will show up in your first cell. 
* Make sure your ``bank_loan.csv`` is saved as ``data_raw_all`` so that it is consistent with the original notebook. You may have to edit this because when your data is loaded into the notebook, it may be defined as a continuation of data frames, based on where I left off. This means your data may show up with ``bank_loan.csv`` as ``df_data_2``. Either adjust the data frame names to be in sync with mine (remove where I loaded data and rename your data frames or input your loading information into the original code) or edit the following code below accordingly. Do this to make sure the code will run!

 ![](doc/source/images/Screen%20Shot%202017-12-06%20at%202.29.41%20PM.png)

### 3. Run the notebook

When a notebook is executed, what is actually happening is that each code cell in
the notebook is executed, in order, from top to bottom.

Each code cell is selectable and is preceded by a tag in the left margin. The tag
format is `In [x]:`. Depending on the state of the notebook, the `x` can be:

* A blank, this indicates that the cell has never been executed.
* A number, this number represents the relative order this code step was executed.
* A `*`, this indicates that the cell is currently executing.

There are several ways to execute the code cells in your notebook:

* One cell at a time.
  * Select the cell, and then press the `Play` button in the toolbar.
* Batch mode, in sequential order.
  * From the `Cell` menu bar, there are several options available. For example, you
    can `Run All` cells in your notebook, or you can `Run All Below`, that will
    start executing from the first cell under the currently selected cell, and then
    continue executing all cells that follow.
* At a scheduled time.
  * Press the `Schedule` button located in the top right section of your notebook
    panel. Here you can schedule your notebook to be executed once at some future
    time, or repeatedly at your specified interval.
    
### 4. Save and Share

#### How to save your work:

Under the `File` menu, there are several ways to save your notebook:

* `Save` will simply save the current state of your notebook, without any version
  information.
* `Save Version` will save your current state of your notebook with a version tag
  that contains a date and time stamp. Up to 10 versions of your notebook can be
  saved, each one retrievable by selecting the `Revert To Version` menu item.

#### How to share your work:

You can share your notebook by selecting the ``Share`` button located in the top
right section of your notebook panel. The end result of this action will be a URL
link that will display a “read-only” version of your notebook. You have several
options to specify exactly what you want shared from your notebook:

* `Only text and output`: will remove all code cells from the notebook view.
* `All content excluding sensitive code cells`:  will remove any code cells
  that contain a *sensitive* tag. For example, `# @hidden_cell` is used to protect
  your dashDB credentials from being shared.
* `All content, including code`: displays the notebook as is.
* A variety of `download as` options are also available in the menu.

## Explore, Analyse and Predict Bank Client's CD subscription
 
1. Introduction and Background.

  Imbalance dataset where number of positive samples are lot more than negative samples are very common and we setup the premise of our whole code pattern here.

2. Data Set Description.

 Data set is from Purtugese Bank Marketing data, where bank's associate makes call to user to sell financial product i.e CD to bank's client. Data set contains 17 columns and is explained here.

3. Statement of Classification Problem.

 Before we start building our model, we should clearly defines, our object and high level problem statement.

4. Software and Tools(Xgboost and Scikit Learn).

 We will mostly use python based libraries i.e XGBoost, Scikit-learn, Matplotlib, SeaBorn, Pandas. In this section we will load and explain, each of the packages and it's sub packages.

5. Visual Data Exploration to understand data (Using seaborn and matplotlib).

 To get better insight into data, data scientists, usually perform data exploration, we will explore inputs for it's distribution, correlation and outliers

 We will also explore output and will note the class imbalance issues.

6. Create Scikit learn ML Pipelines for Data Processing.
  
 - Split data into train and test set.
 - Create ML pipeline for data preparation.
 In typical machine learning application, one would usually creates, ML pipeline, so that all the steps that are done on training data set, can be easily applied on the test set.

7. Model Training.

  Model Training is a iterative process and we will do several iteration to improve our model performance.

  7.1 What and Why of XGBoost.

   We will explain, why we choose XGBoost as our tool of choice.

  7.2 Discuss Metrics for Model Performance.

   We explain in detail various classification performance metrics like ROC curve, Precision-Recall curve, Confusion Matrix and our choice for this application.

  7.3 First Attempt at Model Training and it's performance,evaluation and analysis.

   We will build XGBoost model using cross validation and compare it's performance via various stats and visualization. We will note that, performance is not good for the positive class i.e recall is bad.

  7.4 Strategy For Better Classifier for the Imbalance Data

  To improve, recall, we will highlight a few tricks.

  7.5 Second Attempt at Model Training using Weighted Samples and it's performance, evaluation and analysis.

  Next, we will use one of the tricks of weighted samples to improve performance.

  7.6 Third Attempt at Model Training using Weighted Samples and Feature Selection and it's performance analysis.

  Lastly, we will build model with weighted samples and feature selection.

8. Inference Discussion (Generalization and Prediction)

 Now, our model is ready to used and we run it on held out data, to see it's performance on test data.

9. Summary about what we learned about various techniques.

10. Pointers to Other Advanced Techniques like OverSampling, UnderSampling and SMOTE algorithms.


Awesome job following along! Now go try and take this further or apply it to a different use case!

## Links

 - DSX:https://datascience.ibm.com/docs/content/analyze-data/creating-notebooks.html
 - Pandas:http://pandas.pydata.org/
 - Data:http://archive.ics.uci.edu/ml/datasets/Bank+Marketing
 - Scikit Learn:http://scikit-learn.org/stable/
 - XGBoost:https://github.com/dmlc/xgboost
 - Matplotlib:https://matplotlib.org/
 - SeaBorn:https://seaborn.pydata.org


# Learn more

* **Data Analytics Code Patterns**: Enjoyed this Code Pattern? Check out our other [Data Analytics Code Patterns](https://developer.ibm.com/code/technologies/data-science/)
* **AI and Data Code Pattern Playlist**: Bookmark our [playlist](https://www.youtube.com/playlist?list=PLzUbsvIyrNfknNewObx5N7uGZ5FKH0Fde) with all of our Code Pattern videos
* **Data Science Experience**: Master the art of data science with IBM's [Data Science Experience](https://datascience.ibm.com/)
* **Spark on IBM Cloud**: Need a Spark cluster? Create up to 30 Spark executors on IBM Cloud with our [Spark service](https://console.bluemix.net/catalog/services/apache-spark)

# License
[Apache 2.0](LICENSE)
