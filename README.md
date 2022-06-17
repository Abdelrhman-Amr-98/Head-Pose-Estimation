# Head-Pose-Estimation
---
This work is done with collaboration of my colleague and my friend: **Dina Zakaria**

## Description

---

This project was developed for angle/pose estimation **(pitch, yaw, roll)** using **68** landmarks from DLib with models trained on **AFLAW2000** Dataset

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/95924365-a9c0-4a0d-910f-64d36e44f17d/Untitled.png)

<aside>
💡 3D Reconstruction from 2D reference was performed.

</aside>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/828696f8-a9d3-4d03-a19f-6a08622ece0c/Untitled.png)

### Data Preprocessing
---

After reading the data 

1. Normalization of all the landmarks to one referenced landmark.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be00a9eb-75ce-4fd3-9ebb-643437e58ed0/Untitled.png)
    
    - Using the sparse representation of the normalized coordinates in this [paper](https://github.com/Abdelrhman-Amr-98/Head-Pose-Estimation/blob/main/Sources%20and%20References/%5B1%5D%20Sparse_Bayesian_Regression_for_Head_Pose_Estimation.pdf) outline **3.1**
    - Given that we have the nose landmark [**31**] performing as the CG feature of the face
        - We have used it instead of the approximation performed in the paper to estimate its position
        - Then we applied the normalization method using the nose as our CG.
2. Feature Selection
3. Using the Interquartile Rule to Find Outliers in both (**labels** and **landmarks**)
    - Calculate the interquartile range for the data. **Multiply the interquartile range (IQR) by 1.5**
     (a constant used to discern outliers). Add 1.5 x (IQR) to the third quartile. Any number greater than this is a suspected outlier.
4. Normalization of all selected features from [0, 1]

### Model 
---

1. Dividing data using `train_test_split` from `sklearn.model_selection`
    - Training: **60%**
    - Validation: **20%**
    - Testing: **20%**
2. **Histogram** plot of all training, validation and testing data to make sure they all follow a **gaussian distribution**.
3. **Training** using six models:
    - Linear Regression
    - Decision tree Regressor
    - Support vector Regression (SVR)
        - Grid Search
    - RandomForestRegressor
    - GradientBoostingRegressor
    - AdaBoostRegressor

### Model Performance and **Landmarks**
---

- **Pitch**: **12** landmarks were used
    - R2-score for testing data: **92.12% (SVR using Grid Search)**
- **Yaw: 5** landmarks were used
    - R2-score for testing data: **99.35% (Random Forest)**
- **Roll: 5** landmarks were used
    - R2-score for testing data: **93.28% (SVR using Grid Search)**

### Evaluation Metrices
---

- R2 Score
- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- Mean Absolute Percentage Error (MAPE)
- Explained Variance Score
- Max Error
- Median Absolute Error

### Video Trial
---
<a href="https://drive.google.com/file/d/1--1clYecOA_G6BgAU73B839oS9DkdIty/view?usp=sharing"><img src="(https://drive.google.com/file/d/1--1clYecOA_G6BgAU73B839oS9DkdIty/view?usp=sharing" style="width: 650px; max-width: 100%; height: auto" title="Click to enlarge picture" />


### [References](https://github.com/Abdelrhman-Amr-98/Head-Pose-Estimation/tree/main/Sources%20and%20References)

- Main paper:  [Sparse Bayesian Regression for Head Pose Estimation](https://github.com/Abdelrhman-Amr-98/Head-Pose-Estimation/blob/main/Sources%20and%20References/%5B1%5D%20Sparse_Bayesian_Regression_for_Head_Pose_Estimation.pdf)
