Most projects begin with data collection and exploratory data analysis (EDA), both of which can take up the bulk of a project. 

There's two ways to visualize data:
1. Univariate analysis. Analyze each feature independently, including range of the feature and whether outliers exist. Typically box plots and distribution plots. 
2. Bivariate analysis. Compare data between two features. Helps find correlation between features. Line plots, bar plots, and scatterplots. 
In box plots, data is represented at the 25th, 50th, and 75th quartiles. Maximum observations are present in the interquartile range. 

The most important statistics for data science are mean, median, mode, standard deviation, and Pearson correlation. Pearson correlation shows the change of one variable based on another, and can be positive, negative, or zero. Correlation is helpful in detecting label leakage. 

Data can be unbalanced, unreliable, or skewed. Skew is when the distribution of a feature has a mean that isn't equal to or near the median, and if the skewness is in the target variable, you can use the Synthetic Minority Oversampling Technique (SMOTE), undersampling, or oversampling. 

Outliers are easier to detect with plots and techniques such as:
- box plots
- z-score (Scaled value = (value − mean) / stddev)
- clipping
- interquartile range (IQR)

It's usually beneficial and recommended to have a schema for your data, including numerical vs categorical, allowed range, format, and distribution. 