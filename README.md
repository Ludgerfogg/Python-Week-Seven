# Python-Week-Seven
python- week 7 assignment


import pandas as pd

# Step 1: Load the dataset
# Replace 'iris.csv' with the path to your dataset if different.
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"  # Online dataset link
dataset = pd.read_csv(url)

# Step 2: Display the first few rows
print("First five rows of the dataset:")
print(dataset.head())

# Step 3: Explore the structure of the dataset
print("\nDataset Info:")
print(dataset.info())

print("\nSummary statistics:")
print(dataset.describe())

# Step 4: Check for missing values
print("\nMissing values in the dataset:")
print(dataset.isnull().sum())

# Step 5: Clean the dataset
if dataset.isnull().sum().sum() > 0:
    # Fill missing values (if any) with the mean of their respective column
    dataset.fillna(dataset.mean(), inplace=True)
    print("\nMissing values filled with column means.")
else:
    print("\nNo missing values detected. No cleaning required.")

# Display the dataset after cleaning
print("\nDataset after cleaning:")
print(dataset.head())



Task 2: Basic Data Analysis



import pandas as pd

# Load the dataset
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
dataset = pd.read_csv(url)

# Step 1: Compute basic statistics
print("Basic Statistics for Numerical Columns:")
print(dataset.describe())

# Step 2: Perform groupings and compute mean for each group
print("\nMean of numerical columns grouped by species:")
grouped_means = dataset.groupby('species').mean()
print(grouped_means)

# Step 3: Analyze patterns or interesting findings
print("\nFindings and Patterns:")
for column in grouped_means.columns:
    max_value = grouped_means[column].idxmax()
    print(f"The species with the highest average {column.replace('_', ' ')} is {max_value}.")


       sepal_length  sepal_width  petal_length  petal_width
count    150.000000   150.000000    150.000000   150.000000
mean       5.843333     3.057333      3.758000     1.199333
std        0.828066     0.435866      1.765298     0.762238
min        4.300000     2.000000      1.000000     0.100000
25%        5.100000     2.800000      1.600000     0.300000
50%        5.800000     3.000000      4.350000     1.300000
75%        6.400000     3.300000      5.100000     1.800000
max        7.900000     4.400000      6.900000     2.500000


The species with the highest average sepal length is virginica.
The species with the highest average sepal width is setosa.
The species with the highest average petal length is virginica.
The species with the highest average petal width is virginica.



Task 3: Data Visualization



import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the Iris dataset
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
dataset = pd.read_csv(url)

# Set a seaborn style for the plots
sns.set(style="whitegrid")

# 1. Line Chart: Trends over time (Example: Randomized cumulative sum for illustration)
# Generating a cumulative sum for a pseudo time-series
dataset['index'] = range(len(dataset))  # Simulate a time series
dataset['cumulative_petal_length'] = dataset['petal_length'].cumsum()

plt.figure(figsize=(8, 5))
plt.plot(dataset['index'], dataset['cumulative_petal_length'], label='Cumulative Petal Length', color='b')
plt.title('Cumulative Petal Length Over Time')
plt.xlabel('Index (simulated time)')
plt.ylabel('Cumulative Petal Length')
plt.legend()
plt.show()

# 2. Bar Chart: Average petal length per species
avg_petal_length = dataset.groupby('species')['petal_length'].mean()

plt.figure(figsize=(8, 5))
avg_petal_length.plot(kind='bar', color=['#FF9999', '#66B2FF', '#99FF99'])
plt.title('Average Petal Length by Species')
plt.xlabel('Species')
plt.ylabel('Average Petal Length')
plt.xticks(rotation=0)
plt.show()

# 3. Histogram: Distribution of petal length
plt.figure(figsize=(8, 5))
sns.histplot(dataset['petal_length'], bins=20, kde=True, color='purple')
plt.title('Distribution of Petal Length')
plt.xlabel('Petal Length')
plt.ylabel('Frequency')
plt.show()

# 4. Scatter Plot: Sepal length vs. Petal length
plt.figure(figsize=(8, 5))
sns.scatterplot(x='sepal_length', y='petal_length', hue='species', style='species', palette='deep', data=dataset)
plt.title('Sepal Length vs. Petal Length')
plt.xlabel('Sepal Length')
plt.ylabel('Petal Length')
plt.legend(title='Species')
plt.show()



Explanation of Visualizations:
Line Chart:

Simulates a trend over time using cumulative petal length as an example.
Uses a line plot to depict the "growth" over an index.
Bar Chart:

Displays the average petal length for each species.
Uses vibrant colors to differentiate species.
Histogram:

Shows the distribution of petal lengths across all species.
Includes a KDE (Kernel Density Estimate) line to visualize the density.
Scatter Plot:

Highlights the relationship between sepal length and petal length.
Differentiates species using colors and styles.
