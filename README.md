# Bengaluru House Price Prediction

This project builds a machine learning model to predict house prices in Bengaluru, India, based on features like location, size (BHK), total square feet, and number of bathrooms.

![Bengaluru House](https://images.unsplash.com/photo-1596222774922-403f101153ec?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80)

---

## 📋 Table of Contents
* [Project Overview](#-project-overview)
* [Data Cleaning & Feature Engineering](#-data-cleaning--feature-engineering)
* [Model Building](#-model-building)
* [Technologies Used](#-technologies-used)
* [Setup & Installation](#-setup--installation)
* [How to Use](#-how-to-use)

---

## 📝 Project Overview

The primary goal of this project is to create a regression model that can accurately estimate the price of houses in Bengaluru. The model is trained on the "Bengaluru House Data" dataset, which includes various features of properties. The project involves extensive data cleaning, outlier removal, and feature engineering to prepare the data for modeling. Several models are evaluated, and the best-performing one is selected for the final predictions.

---

## 🧹 Data Cleaning & Feature Engineering

The initial dataset required several preprocessing steps to make it suitable for machine learning:

1.  **Handling Missing Values**: Rows with missing critical information (like `size` and `bath`) were dropped to ensure data quality.
2.  **Feature Engineering**:
    * A new integer column `bhk` was created by extracting the numerical part from the `size` column (e.g., '2 BHK' becomes 2).
    * The `total_sqft` column, which contained range values (e.g., '2100 - 2850'), was converted to a single numerical value by taking the average of the range.
3.  **Outlier Removal**:
    * **Dimensionality Reduction**: Locations with fewer than 10 data points were grouped into an 'other' category to reduce noise.
    * **Domain-based Outlier Removal**: Properties with a square feet per bedroom ratio of less than 300 were removed as they are considered anomalies.
    * **Statistical Outlier Removal**: Outliers in `price_per_sqft` were removed by filtering out data points that were beyond one standard deviation from the mean for each location. Properties where the number of bathrooms was greater than the number of bedrooms plus two were also removed.

---

## 🤖 Model Building

The project explored and evaluated three different regression models to find the best fit for the data:

1.  **Linear Regression**: The primary model used for the final predictions.
2.  **Lasso Regression**: Tested as an alternative.
3.  **Decision Tree Regressor**: Another model evaluated for performance.

A `GridSearchCV` was used to find the best parameters for each model. The results showed that **Linear Regression** provided the best score with an R-squared value of approximately **84.5%**.

| Model | Best Score | Best Parameters |
| :--- | :--- | :--- |
| **Linear Regression** | **0.845404** | **{'normalize': False}** |
| Lasso | 0.709613 | {'alpha': 1, 'selection': 'random'} |
| Decision Tree | 0.669810 | {'criterion': 'mse', 'splitter': 'random'} |


---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* Jupyter Notebook

---

## ⚙️ Setup & Installation

To run this project, you need to have Python and the required libraries installed.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/bengaluru-house-price-prediction.git](https://github.com/your-username/bengaluru-house-price-prediction.git)
    cd bengaluru-house-price-prediction
    ```

2.  **Install the required libraries:**
    ```bash
    pip install pandas numpy matplotlib scikit-learn jupyter
    ```
3.  **Download the dataset:**
    Make sure you have the `Bengaluru_House_Data.csv` file in the project directory.

4.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
    Then, open the `House_Price_Prediction_Model_Code.ipynb` file.

---

## 🚀 How to Use

You can run the Jupyter Notebook to see the entire data analysis and model building process. To predict the price of a house, you can use the `predict_price` function defined in the notebook.

**Function Definition:**
```python
def predict_price(location, sqft, bath, bhk):
    # Function body is in the notebook
```
# Predict the price of a 1000 sqft, 2 BHK, 2 bath apartment in '1st Phase JP Nagar'
predict_price('1st Phase JP Nagar', 1000, 2, 2)
# Expected Output: ~88.92 (Lakhs)

# Predict the price of a 1000 sqft, 2 BHK, 2 bath apartment in 'Indira Nagar'
predict_price('Indira Nagar', 1000, 2, 2)
# Expected Output: ~187.67 (Lakhs)
