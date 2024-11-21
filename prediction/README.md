# Workflow Documentation

## Prediction Data Description

The client provides data in multiple batches of files located at a specified location. These files contain the **credit and payment records** of customers.

### Additional Files
Apart from the prediction data, a **schema file** is required from the client. The schema file contains relevant information about the files, such as:
- Name of the files.
- Length of the date value in the filename.
- Length of the time value in the filename.
- Number of columns.
- Name of the columns and their datatypes.

---

## Data Validation

In this step, various validations are performed on the prediction files.

### 1. Name Validation
- Validate the file names using a regex pattern derived from the schema file.
- Check the following:
  - **Length of date** in the filename.
  - **Length of time** in the filename.
- Files passing validation are moved to the **Good_Data_Folder**, and those failing are moved to the **Bad_Data_Folder**.

### 2. Number of Columns
- Validate the number of columns in the files.
- Files with mismatched column counts (compared to the schema file) are moved to the **Bad_Data_Folder**.

### 3. Name of Columns
- Validate that the column names match those in the schema file.
- Files with incorrect column names are moved to the **Bad_Data_Folder**.

### 4. Datatype of Columns
- Validate column datatypes based on the schema file.
- Files with incorrect datatypes are moved to the **Bad_Data_Folder**.

### 5. Null Values in Columns
- Check if any column has all values as NULL or missing.
- Such files are discarded and moved to the **Bad_Data_Folder**.

---

## Data Insertion in Database

### 1. Database Creation and Connection
- Create a database with the specified name.
- If the database already exists, establish a connection to it.

### 2. Table Creation in Database
- Create a table named **Good_Data** in the database.
- Use column names and datatypes from the schema file.
- If the table already exists, new files are inserted into the existing table.

### 3. Insertion of Files in the Table
- Insert all files from the **Good_Data_Folder** into the table.
- Files with invalid data types are not loaded into the table and are moved to the **Bad_Data_Folder**.

---

## Prediction

### 1. Data Export from Database
- Export data from the database into a CSV file for prediction.

### 2. Data Preprocessing
a) Check for null values in columns and impute them using a **categorical imputer**.  
b) Scale numeric values using a **standard scaler**.  
c) Check for **correlation**.

### 3. Clustering
- Load the **KMeans model** created during training.
- Predict clusters for the preprocessed prediction data.

### 4. Prediction
- Based on the predicted cluster number, load the respective model.
- Use the loaded model to predict data for that cluster.

### 5. Save Predictions
- Combine predictions from all clusters along with the **Wafer names**.
- Save the results in a CSV file at the specified location.
- Return the file location to the client.
