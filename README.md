# HW-1_Dhanush: Understanding PCA with University Data

This Google Colab notebook explores the application of Principal Component Analysis (PCA) on a university dataset, critically demonstrating the impact of data scaling on the interpretability and validity of the PCA results.

## Overview

The primary goal of this notebook is to illustrate why data standardization is a crucial preprocessing step before performing PCA. It walks through applying PCA on raw, unscaled data and then repeats the process on standardized data, highlighting the vastly different and more meaningful insights derived from the latter.

## Key Features

*   **Data Loading & Inspection:** Reads and briefly inspects a university dataset.
*   **Data Preprocessing:** Cleans the dataset by removing categorical columns and handling missing values.
*   **PCA on Unscaled Data:** Demonstrates PCA on the raw numerical features, revealing how high-magnitude variables dominate the components.
*   **Detailed Interpretation (Unscaled PCA):** Provides a comprehensive analysis of the unscaled PCA results, explaining the bias introduced by differing scales.
*   **Data Standardization:** Applies `StandardScaler` to normalize the data.
*   **PCA on Scaled Data:** Performs PCA again on the standardized data, showcasing the balanced and insightful components.
*   **Comparative Analysis:** Offers a clear comparison of PCA results before and after normalization, emphasizing the benefits of scaling.

## Technologies and Libraries Used

*   **`pandas`**: For data manipulation and analysis.
*   **`sklearn.decomposition.PCA`**: For performing Principal Component Analysis.
*   **`sklearn.preprocessing.StandardScaler`**: For standardizing features (zero mean and unit variance).

## Analysis Workflow

The notebook follows a structured approach to demonstrate the PCA process:

1.  ### **Import Libraries**
    *   Essential libraries like `pandas`, `PCA`, and `StandardScaler` are imported.

2.  ### **Importing the Dataset**
    *   The `Universities.csv` dataset is loaded into a pandas DataFrame.
    *   Initial data inspection is performed using `.head()` and `.info()`.

3.  ### **Data Preprocessing**
    *   Categorical columns (object type) and rows with any null values are removed from the DataFrame to prepare it for numerical analysis.
    ```python
    uni_df = uni_df.select_dtypes(exclude = ['object']).dropna()
    ```

4.  ### **PCA with Regular (Unscaled) Data**
    *   PCA is applied directly to the preprocessed, unscaled `uni_df`.
    *   The principal components' loading weights are extracted and displayed.

5.  ### **In-Depth Interpretation and Recommendation (Unscaled PCA)**
    *   A detailed explanation is provided, showing that the first principal component (PC1) is heavily dominated by high-magnitude features like `in-state tuition` and `out-of-state tuition`.
    *   This section highlights how unscaled data leads to biased PCA results and strongly recommends data normalization.

6.  ### **Data Standardization**
    *   The `StandardScaler` is initialized and used to transform the `uni_df` data, ensuring all features have a mean of 0 and a standard deviation of 1.
    ```python
    scaler = StandardScaler()
    scaled_data = scaler.fit_transform(uni_df)
    ```

7.  ### **PCA with Scaled Data**
    *   PCA is performed again, this time on the `scaled_data`.
    *   The loading weights for the first five principal components are displayed.

8.  ### **Observations Before and After Normalization (PCA Analysis)**
    *   This section provides a clear, side-by-side comparison of the PCA results from unscaled and scaled data.
    *   It elaborates on how scaling allows PCA to reveal more meaningful and balanced underlying dimensions in the dataset.

## Key Insights and Results

*   **Unscaled PCA Bias:** When data is not scaled, PCA is heavily influenced by variables with larger numerical ranges. In this dataset, `in-state tuition` and `out-of-state tuition` disproportionately impacted PC1 due to their high values, masking the contributions of other important features.
*   **Crucial Role of Normalization:** Standardization (e.g., using `StandardScaler`) is essential before PCA. It ensures that all features contribute equally to the variance calculation, leading to unbiased and more accurate dimensionality reduction.
*   **Meaningful Components after Scaling:** After normalization, the principal components become much more interpretable, revealing distinct underlying patterns:
    *   **PC1:** Represents a blend of `financial investment`, `institutional cost`, and `academic quality`.
    *   **PC2:** Reflects `institutional size` and `selectivity` (e.g., number of applications, accepted, enrolled students).
    *   **PC3:** Captures `student financial burden` related to `book costs` and `personal expenses`.
    *   **PC4:** Indicates a potential trade-off between `student living costs` and `academic selectivity`.
    *   **PC5:** Further emphasizes `student expenditure`.

## How to Use/Run the Notebook

1.  **Open in Google Colab:**
    *   If you have the `.ipynb` file, upload it to your Google Drive.
    *   Open it with Google Colaboratory.
2.  **Dataset:** Ensure the `Universities.csv` file is accessible in your Colab environment. You might need to upload it to your session storage or mount your Google Drive if it's there.
    ```python
    # Example for uploading if needed:
    # from google.colab import files
    # uploaded = files.upload()
    # Then ensure the path in pd.read_csv matches.
    ```
3.  **Run Cells:** Execute each cell sequentially from top to bottom. You can do this by clicking the "Run" button on each cell or by selecting "Runtime" -> "Run all" from the Colab menu.
4.  **Observe Outputs:** Pay close attention to the `DataFrame` outputs and markdown explanations within the notebook to understand the analysis at each step.