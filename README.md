
# Heart Disease Classification

In the United States, heart disease is the **leading cause** of death among men, women, and most racial and ethnic groups.<sup>1</sup> Although high blood pressure, high blood cholesterol, and smoking are well-known risk factors for heart disease<sup>2</sup>, predicting whether or not an individual will develop the disease or not is still a daunting task. Through the power of machine learning, predicting an individual's risk can become easier. This project uses `tensorflow` and `sklearn` to create a deep learning model to classify if an individual has heart disease. 

## About the Data
Dataset: https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset

Dataset shape: (1025, 14) i.e 1025 rows and 14 columns.

The [dataset](https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset) from 1988 compiles data from four databases and narrows down the original 76 attributes to a subset of just 14. Of the 14 attributes, 13 are predictive attributes and the final attribute, "Target" refers to the presence (value 1) or absence (value 0) of heart disease in the patient. 

Predictive attributes:

- Age
- Sex
- Chest Pain Type (values 1-4)
- Resting Blood Pressure
- Serum Cholesterol (in mg/dL)
- Fasting Blood Sugar (in mg/dL)
- Resting Electrocardiographic Results (values 0-2)
- Maximum Heart Rate
- Exercise Induced Angina
- Old Peak: ST depression induced by exercise relative to rest
- Slope of Peak Exercise ST Segment
- Number of Major Vessels Colored by Fluoroscopy (0-3)
- Thalassemia: reduced hemogolobin (0 = normal; 1 = fixed defect; 2 = reversable defect)

## Modules Used

```
Pandas
Tensorflow
Keras
Sqlalchemy
Sklearn
tensorflow_addons
```

## Steps Taken to Train the Model

1. Using postgresql, a database engine instance was created and further accessed by establishing a connection to the AWS hosted PostgreSQL server `heart-disease`. Using Select query , all rows were fetched and saved as a dataframe for further use. The same dataframe was also stored in a sqlite3 database table.

2. Training features included all of the predictive attributes: `age`, `sex`, `cp`, `trestbps`, `chol`, `fbs`, `restecg`, `thalach`,`exang`, `oldpeak`, `slope`, `ca`, and `thal`. The target values were the `target` column.

3. Based on different ranges, the `age`, `trestbps`, `chol`, and `thalach` columns have been modified and respective new columns were created. These columns were further modified using one hot encoding via `pandas.get_dummies`.

4. The preprocessed dataset was split into training and testing sets.

5. Training and testing sets were scaled using `sklearn.preprocessing.StandardScaler`.

6. Using `tensorflow.keras.models.Sequential`, a deep learning model was created with the metric "accuracy", loss function "binary_crossentropy," and optimizer "adam." Optimal hyperparameters were found in [optimizer.ipynb](optimizer.ipynb) after testing 60 randomly generated models.

The optimal hyperparameter values were as follows:

- 'activation': 'relu'
- 'first_units': 9
- 'num_layers': 5
- 'units_0': 17
- 'units_1': 9
- 'units_2': 17
- 'units_3': 9
- 'units_4': 13
- 'units_5': 5
- 'tuner/epochs': 20
- 'tuner/initial_epoch': 0
- 'tuner/bracket': 0
- 'tuner/round': 0

![Model Architecture](Resources/model_img.png)

7. The final model was created with the obtained hyperparameters and trained using the training dataset. The [model](Resources/Model/OptimizedModel.h5) was saved for future reference.

8. The trained model was evaluated on a testing dataset, and it gave 100% accuracy and R<sup>2</sup> value of 99.6%.

## How to Run 

Open and run the [heart_disease.ipynb](heart_disease.ipynb) file.

## Group Members

Dennis Chen, Sidney Bowe, Nancy Campos, and Scott Alexander

## References

1. Centers for Disease Control and Prevention, Naitonal Center for Health Statistics. [About Multiple Cause of Death, 1999-2020](https://wonder.cdc.gov/mcd-icd10.html)

2. Centers for Disease Control and Prevention, Naitonal Center for Health Statistics. [Know Your Risk for Heart Disease](https://www.cdc.gov/heartdisease/risk_factors.html)