# Question 1 – Used Car Dataset Analysis 

This project performs a complete data cleaning and transformation process on a used car dataset.  
The dataset includes information such as car name, location, manufacturing year, mileage, engine size, power, seats, fuel type, transmission, and price.  
The goal of this assignment is to properly clean the dataset, convert categorical data into numerical format, create meaningful new features, and perform essential data manipulation using Python.  
This README explains every step (a–e) in detail with clear reasoning, methodological justification, and step-by-step workflow so that the work is easy to follow and reproducible.

---

# (a) **Handling Missing Values – Detection, Imputation, and Justification**

In this step, we begin by reading the dataset and thoroughly checking for missing values across all columns.  
We use Python functions such as `df.isna().sum()` to count how many missing values are present in each attribute, allowing us to understand the data quality before processing it.  
Once the missing values are identified, we categorize the variables into **numeric** columns (such as Mileage, Engine, Power, Seats, New_Price, and Price) and **categorical** columns (such as Fuel_Type, Transmission, Owner_Type, and Location).  
For numeric columns, missing values are replaced using the **median** because the median is resistant to extreme values and provides a stable, central measurement of the feature.  
For categorical columns, missing values are replaced using the **mode**, which is the most frequently occurring category in that column, ensuring that we replace missing data with the most likely value.  
We choose **imputation instead of dropping rows** because dropping rows can lead to unnecessary information loss, especially when the dataset is not extremely large.  
By imputing values instead of removing data, we maintain the full dataset size and avoid biasing the analysis by removing potentially useful records.  
After imputation, we verify that there are no remaining missing values to ensure that downstream processing such as one-hot encoding or mathematical operations will run without errors.

---

# (b) **Removing Units and Converting Text Fields to Pure Numeric Values**

Several columns in the dataset contain numbers combined with units, such as `"18.6 kmpl"`, `"1197 CC"`, `"83 bhp"`, or `"10.9 Lakh"`.  
These unit-bearing values prevent Python from recognizing the columns as numeric, which will cause errors in calculations and transformations.  
To correct this, we use `str.extract()` with a regular expression that isolates the numeric part and discards any text, symbols, or units.  
For example, `"18.6 kmpl"` becomes `18.6`, `"1197 CC"` becomes `1197`, `"83 bhp"` becomes `83`, and `"10.9 Lakh"` becomes `10.9`.  
This transformation is crucial because numeric-only formatting is required for mathematical computations, correlation analysis, plotting, machine learning models, and feature engineering.  
Removing units ensures consistency across the dataset and prevents type-conversion problems that occur when numerical and text data are mixed in the same column.  
Each cleaned column is then converted into a `float` datatype to maintain numerical precision and compatibility with statistical operations.  
This process prepares the dataset for proper analysis by ensuring all numerical features are in clean, usable form.

---

# (c) **Converting Categorical Variables into One-Hot Encoded Numerical Columns**

In this step, we handle categorical features such as **Fuel_Type** and **Transmission**, which contain values like “Petrol”, “Diesel”, “Manual”, and “Automatic”.  
Machine learning algorithms, statistical models, and even some analytic functions cannot process string-based categories directly.  
To address this, we transform these categorical variables into new binary variables using **one-hot encoding** with the `pd.get_dummies()` function.  
One-hot encoding creates a separate column for each category and assigns a value of 1 if the observation belongs to that category and 0 otherwise.  
We use `drop_first=True` to avoid the “dummy variable trap,” meaning we drop one redundant category so that the encoded variables remain linearly independent.  
This transformation converts qualitative information into a numerical format while retaining the meaning of each category.  
As a result, the dataset becomes fully numeric, allowing us to use it for machine learning, regression analysis, or any mathematical modeling.  
This process also increases dataset flexibility by enabling filtering, grouping, and statistical comparisons based on encoded categories.

---

# (d) **Creating a New Feature Using Feature Engineering (Mutate Equivalent)**

Feature engineering enhances the dataset by creating new variables that add more analytical insight.  
In this question, we create a new feature called **Car_Age**, calculated by subtracting the manufacturing year of the vehicle from the current year.  
This is an important feature because the age of a car is strongly related to its price, condition, mileage, and overall depreciation rate.  
By adding this new feature, we provide the dataset with a more descriptive variable that captures how old the car actually is, which is more meaningful than year alone.  
Creating Car_Age allows deeper analysis such as exploring how car age affects pricing or how older and newer cars differ across other features.  
This new feature also helps improve statistical modeling since derived variables often capture relationships not directly visible in the raw dataset.  
The `mutate` equivalent in Python is applied by simply assigning a new column using vectorized subtraction.  
Overall, this step enriches the dataset and makes the analysis more informative and realistic.

---

# (e) **Performing Select, Filter, Rename, Mutate, Arrange, and Summarize Operations**

This step focuses on performing essential data manipulation operations similar to R’s `dplyr` functions: `select()`, `filter()`, `rename()`, `mutate()`, `arrange()`, and `summarize()`.  
We begin with the **select** operation, where we choose a meaningful subset of columns such as Name, Year, Mileage, and Price to inspect specific information.  
Next, we apply **filter**, which extracts rows based on logical conditions, such as selecting cars with a price above a certain threshold or selecting only cars from a specific year.  
The **rename** operation is used to modify column names into more readable or standardized formats, helping improve clarity and consistency.  
We again use **mutate** to create additional computed fields such as price-per-kilometer, demonstrating how new variables can be derived from existing data.  
The **arrange** operation sorts the data either in ascending or descending order based on a specific variable like price or mileage, helping identify top or bottom records.  
Finally, the **summarize with group_by** operation allows us to compute aggregated statistics—such as average price by fuel type or by transmission—providing insights into how groups differ internally.  
These operations collectively demonstrate the essential tools needed for real-world data exploration, data wrangling, cleaning, and initial statistical analysis.  
They help convert raw data into a structured, readable, and meaningful format suitable for further modeling or visualization.


# Question 2 – Diabetes Dataset Analysis 

This project uses the `diabetes.csv` dataset, which contains 768 patient records with 8 attributes and one binary outcome variable.  
The dataset includes important health-related variables such as Glucose, BloodPressure, BMI, and Age, which help us understand diabetes risk.  
In this assignment, the entire dataset is considered the “population,” and we perform sampling and bootstrap procedures to study how samples behave compared to the population.  
The analysis is completed using Python inside a Jupyter Notebook, following the instructions carefully for parts (a), (b), and (c).  

---

## (a) Random Sample of 25 – Comparison of Glucose Mean and Maximum

In part (a), we begin by setting a random seed to make sure our results are reproducible every time the notebook is run.  
Next, we take a random sample of 25 observations from the full population of 768 patients, which represents a very small portion of the entire dataset.  
We then calculate the mean Glucose value for this sample and also find the highest Glucose value within the sample.  
After that, we compute the same two statistics (mean and maximum Glucose) for the entire population to serve as a reference.  
Comparing the sample and population statistics helps us understand whether a small sample can accurately reflect the characteristics of the full population.  
We expect some differences because samples are smaller and more variable, but the comparison shows how close or far the sample values can be.  
To make this comparison easier to understand, we create bar charts that visually show the differences between sample and population Glucose values.  
These charts allow us to clearly see whether the sample underestimates or overestimates the true population mean and maximum Glucose levels.

---

## (b) 98th Percentile of BMI – Sample vs Population Comparison

In part (b), we continue using the same sample of 25 observations taken in part (a), ensuring consistency across the assignment.  
We calculate the 98th percentile of BMI within that small sample, which helps us understand how extreme BMI values behave in limited data.  
Next, we compute the 98th percentile of BMI for the entire population, which gives a more stable estimate because it uses all 768 observations.  
Comparing these two percentiles allows us to observe how reliable or unstable a high-percentile statistic can be when calculated from a small sample.  
Because higher percentiles are sensitive to extreme values, the sample percentile may differ significantly from the population percentile.  
This difference helps demonstrate why larger samples often provide more accurate estimates, especially for tail-based statistics.  
To illustrate this comparison clearly, we produce a bar chart showing the sample 98th percentile and the population 98th percentile side by side.  
This visual comparison helps us quickly observe how well the sample approximates the population and highlights the influence of sample size on percentile calculations.

---

## (c) Bootstrap Analysis – 500 Samples of BloodPressure

In part (c), we conduct a bootstrap analysis to better understand how repeated sampling can estimate population characteristics.  
We generate 500 bootstrap samples, and each sample contains 150 observations drawn **with replacement** from the population.  
For every bootstrap sample, we calculate three key statistics for BloodPressure: the mean, the standard deviation, and the 98th percentile.  
After generating all 500 samples, we compute the average of all sample means, the average of all sample standard deviations, and the average of all 98th percentiles.  
These averaged values represent bootstrap-based estimates of the population parameters, allowing us to compare bootstrap estimates with the true population values.  
Bootstrap sampling mimics the idea of repeatedly collecting samples from a real population, which is especially useful when evaluating variability and estimation accuracy.  
We then compute the true population statistics for BloodPressure and compare them with the bootstrap averages to see how closely bootstrap results approximate the population.  
To visualize these comparisons, we create bar charts for mean, standard deviation, and 98th percentile, which clearly show the agreement or difference between bootstrap and population statistics.  
The results typically show that the bootstrap averages are very close to the population values, proving that bootstrap sampling is a reliable method for statistical estimation.
