# Workflow Documentation

## Data Validation

In this step, we perform different sets of validation on the given set of training files.

### 1. Name Validation
- Validate the file names based on the schema file.
- Use a regex pattern as per the schema file for validation.
- Check the following in the file name:
  - **Date length**.
  - **Time length**.
- Files meeting all criteria are moved to the **Good_Data_Folder**, otherwise to the **Bad_Data_Folder**.

### 2. Number of Columns
- Validate the number of columns in the files.
- If the column count does not match the schema file, the file is moved to the **Bad_Data_Folder**.

### 3. Name of Columns
- Validate column names against the schema file.
- Files with mismatched column names are moved to the **Bad_Data_Folder**.

### 4. Datatype of Columns
- Validate the data types of columns during file insertion into the database.
- Files with incorrect data types are moved to the **Bad_Data_Folder**.

### 5. Null Values in Columns
- Check if any column in a file has all values as NULL or missing.
- Discard such files and move them to the **Bad_Data_Folder**.

---

## Data Insertion in Database

### 1. Database Creation and Connection
- Create a database with the specified name.
- If the database already exists, establish a connection to it.

### 2. Table Creation in Database
- Create a table named **Good_Data** in the database based on column names and data types in the schema file.
- If the table already exists, new files are inserted into the existing table.

### 3. Insertion of Files in the Table
- Insert all files from the **Good_Data_Folder** into the table.
- Files with invalid data types are not loaded and are moved to the **Bad_Data_Folder**.

---

## Model Training

### 1. Data Export from Database
- Export data from the database into a CSV file for model training.

### 2. Data Preprocessing
a) Check for null values in columns and impute them using a categorical imputer.  
b) Scale numeric values using a standard scaler.  
c) Check for correlation.

### 3. Clustering
- Use the **KMeans** algorithm to create clusters in the preprocessed data.
- Determine the optimal number of clusters using:
  - **Elbow plot**.
  - **KneeLocator** function for dynamic cluster selection.
- Train the KMeans model on preprocessed data and save it for future use.

### 4. Model Selection
- Identify the best model for each cluster using:
  - **Naïve Bayes**.
  - **XGBoost**.
- Use GridSearch to derive the best parameters for both algorithms.
- Calculate **AUC scores** and select the model with the highest score for each cluster.
- Save the selected models for use in prediction.
