# Medical-Dataset-Cleaning

## Research Question

I suspect that patients with multiple pre-existing conditions are more susceptible to return to the hospital due to the complexity of their physical condition and their ability to be fully treated by hospitals. For this reason, I would like to answer the question: 

***“Are patients with more pre-existing medical conditions readmitted to the hospital more so than patients with fewer pre-existing medical conditions?”***

## Required Variables

|Variable|Description|Data Type|Example(s)|
|---|---|---|---|
|CaseOrder|Places the rows in their original order numerically|ordinal categorical|1, 2, 3|
|Customer_id|Represents each different customer using a unique ID|nominal categorical|C412403, Z919181|
|Interaction|Represents each different interaction for a customer using a unique ID|nominal categorical|8cd49b13-f45a-4b47-a2bd-173ffa932c2f
|UID|Another ID field for tracking customers|nominal categorical|3a83ddb66e2ae73798bdf1d705dc0932
|City|The city where the patient lives|nominal categorical|Eva, Marianna
|State|The state where the patient lives|nominal categorical|AL, FL, SD
|County|The county where the patient lives|nominal categorical|Morgan, Jackson
|Zip|The zip where the patient lives|nominal categorical|35621, 57110
|Lat|The latitudinal coordinates where the patient lives|nominal categorical|34.3496, 30.84513
|Lng|The longitudinal coordinates where the patient lives|nominal categorical|-86.72508, -96.63772
|Population|The number of people living in the zip code|quantitative, ratio, discrete (int64)|0, 2951, 13947
|Area|Description of the area where the patient lives|nominal categorical|rural, urban, suburban
|Timezone|The time zone for where the patient lives|nominal categorical|America/Chicago, America/New York
|Job|The patient’s job title|nominal categorical|Chief Executive Officer, Contractor, Police officer
|Children|How many children the patient has|quantitative, ratio, discrete|0, 1, 4
|Age|How old the patient is|quantitative, ratio, discrete|53, 78, 31
|Education|The highest level of education the patient has completed|ordinal categorical|GED, Regular High School Diploma
|Employment|Employment status of the patient|nominal categorical|Full Time, Retired, Student
|Income|Annual income of the patient|quantitative, ratio, continuous |86575.93, 24250.51
|Marital|Marital status of the patient |nominal categorical|Married, Divorced, Widowed
|Gender|Gender of the patient|nominal categorical |Male, Female, Prefer not to answer
|ReAdmis|Was the patient readmitted to the hospital a 2nd time?|Boolean|Yes, No
|VitD_levels|The patient’s vitamin-D levels|quantitative, interval, continuous |17.80233049, 19.96833731
|Doc_visits|Number of times the doctor visited the patient during their stay|quantitative, ratio, discrete |3, 5, 6
|Full_meals_eaten|Number of full meals the patient ate during their stay|quantitative, ratio, discrete |0, 1, 3
|VitD_supp|The number of times that vitamin-D was given to the patient|quantitative, ratio, discrete |0, 1, 2
|Soft_drink|Does the patient drink soda?|Boolean|Yes, No
|Initial_admin|How was the patient initially admitted?|nominal categorical|Emergency Admission, Elective Admission, Observation Admission
|HighBlood|Does the patient have high blood pressure?|Boolean|Yes, No
|Stroke|Has the patient ever had a stroke?|Boolean|Yes, No
|Complication_risk|What is the patient’s health risk for complications?|ordinal categorical|High, Medium, Low
|Overweight|Is the patient overweight?|Boolean|0, 1
|Arthritis|Does the patient have arthritis?|Boolean|Yes, No
|Diabetes|Does the patient have diabetes?|Boolean|Yes, No
|Hyperlipidemia|Does the patient have hyperlipidemia?|Boolean|Yes, No
|BackPain|Does the patient have chronic back pain?|Boolean|Yes, No
|Anxiety|Does the patient have anxiety?|Boolean|0, 1
|Allergic_rhinitis|Does the patient have allergies?|Boolean|Yes, No
|Reflux_esophagitis|Does the patient have reflux?|Boolean|Yes, No
|Asthma|Does the patient have asthma?|Boolean|Yes, No
|Services|Main service the patient received|nominal categorical|Blood Work, CT Scan, Intravenous 
|Initial_days|The number of days the patient stayed at the hospital|quantitative, ratio, continuous |10.58576971, 2.109411187
|TotalCharge|Average daily amount billed to the patient |quantitative, ratio, continuous |3191.048774, 4214.903546
|Additional_charges|Additional charges for extra medical services |quantitative, ratio, continuous|17939.40342, 17612.99812
|Item1|Patient survey: timely admission|ordinal categorical|1, 2, 8
|Item2|Patient survey: timely treatment|ordinal categorical|1, 2, 8
|Item3|Patient survey: timely visits|ordinal categorical|1, 2, 8
|Item4|Patient survey: reliability|ordinal categorical|1, 2, 8
|Item5|Patient survey: options|ordinal categorical|1, 2, 8
|Item6|Patient survey: hours of treatment|ordinal categorical|1, 2, 8
|Item7|Patient survey: courteous staff|ordinal categorical|1, 2, 8
|Item8|Patient survey: active listening from doctor|ordinal categorical|1, 2, 8

## Plan to Assess Quality of Data

I will find duplicate values by using the duplicated() method. This method checks across all rows for complete duplicates. I will treat duplicate values by dropping the duplicated rows. I will find missing values by visualizing the data using the Missingno matrix. I will also get a sense for how much data is missing by using the isnull().sum function (and also isna() function). I will then treat missing values by dropping rows or columns that are sufficiently null or NA by assessing the randomness of the missing data (MCAR, MNAR, MAR). Rather than simply deleting all null or NA variables, I will look to see if it makes sense to impute the data by various means (backward/forward fill, univariate imputation, KNN, linear regression, etc.). 

I will visualize the data using histograms to assess how to impute the data correctly, and once the missing values are treated, I will look at the graph and statistics to ensure the treatment did not alter the data in a biased way. I will find outliers by visualizing the data graphically. I will use z-scores, boxplots, and histograms to locate the outliers. If the outlier is truly a factual error, then I will treat the outlier by imputation, retention, exclusion, or deletion. 

## Justification of Approach

To assess if there were duplicates, I used the Pandas duplicated function. This function returns a Boolean Series telling me if there are any duplicate rows in the dataset (Pandas, 2023). This is a good method for determining if there are duplicate rows as it checks for duplicated values across all variables. If all variables in a row are the same, then it will count this as “True” in the Boolean Series. You can then perform a sum function on the duplicated output to count the number of “True” and “False” values in the Series. 

To assess if there are missing values, I used the Pandas isnull/isna functions. Again, just like in the above process, using the sum function along with the isnull/isna functions will display how many values in each variable are null (or na). I then used the Missingno matrix to visualize the missingness of the data. Before treating the data, it’s important to know the randomness of the missing values. Therefore, I sorted each variable that had missing data separately in a different matrix so that I could see if there was any correlation to another column of missing data (Nehme, 2023). 

To assess if there are outliers, I used plots to visualize the outliers as this is an easy way to detect outliers in the data. I used matplotlib’s boxplot as well as Seaborn’s boxplot. Visually, the boxplot shows any values that fall outside of the inter-quartile range, and is easy to quickly decipher if there are outliers in the data (Waskom, 2012-2022).  

## Justification of Tools

For this assignment, I chose to use Python because of its ease of use. For me, it is much easier to read and has a better learning curve than R. There is a consistent syntax in Python that makes learning other packages straightforward (WGU, 2023).

The two most widely used packages in Python are NumPy and Pandas. NumPy uses arrays which store and retrieve information faster than just regular Python lists (NumPy, 2008-2022). Pandas allows data to be stored in a DataFrame and easily imports and exports a csv file which makes inputting and extracting data a breeze (DataFlair, 2023). I also imported Python’s statistics package so that I could use the median, mean, and mode functions when treating missing data and outliers. 

For visualizing the data, I chose several different libraries to import. First, I chose the Missingno package primarily for the matrix plot. This plot helps to visualize the missingness of each variable and can be sorted by a specific variable to show the randomness of the missingness compared to other variables. I also imported Matplotlib which has a wide array of plots you can use to visualize the data easily. I used the histogram plot often in my treatment for missing data as I can view the graph before and after treatment to confirm that the treatment method I used did not introduce a bias into the dataset. The histogram also helped me to see if the data was normally distributed, skewed, or some other distribution. Lastly, I used the boxplot graph to visualize outliers. The seaborn code is very easy to understand and displays a nice plot which easily helps me to identify outliers in the data. 

## Python Code

```python
#find duplicates
print(med_data.duplicated().value_counts())
print(med_data.duplicated('Customer_id', keep=False).value_counts())
print(med_data.duplicated('Interaction', keep=False).value_counts()) 
print(med_data.duplicated('UID', keep=False).value_counts())

#find missing values using msno matrix
msno.matrix(med_data, labels=True)

#find total number of missing values
med_data_nullity = med_data[['Children', 'Age', 'Income', 'Soft_drink',
                            'Overweight', 'Anxiety', 'Initial_days']].isnull()
print(med_data_nullity.sum())

#locate Income outliers 
plt.boxplot(med_data['Income'], vert=False)
plt.xlabel('Income')
plt.title('Income before treatment', fontsize=15, pad=10, color='blue')
plt.show()

#locate outliers = Population
plt.boxplot(med_data['Population'], vert=False)
plt.xlabel('Population')
plt.title('Population before treatment', fontsize=15, pad=10, color='blue')
plt.show()

#locate outliers = Children
plt.boxplot(med_data['Children'], vert=False)
plt.xlabel('Children')
plt.title('Children before treatment', fontsize=15, pad=10, color='blue')
plt.show()

#locate outliers = Age 
sns.boxplot(data=med_data[["Age"]], orient='h', color='green').set(title='Age showing no outliers')

#locate outliers = Initial_days
sns.boxplot(data=med_data[["Initial_days"]],
                          orient='h', color='green').set(title='Initial_days showing no outliers')

#locate outliers = TotalCharge
plt.boxplot(med_data['TotalCharge'], vert=False)
plt.xlabel('TotalCharge')
plt.title('TotalCharge before treatment', fontsize=15, pad=10, color='blue')
plt.show()

#locate outliers = Additional_charges
sns.boxplot(data=med_data[["Additional_charges"]],
                          orient='h', color='green').set(title='Additional_charges before treatment')

#locate outliers = VitD_levels
plt.boxplot(med_data['VitD_levels'], vert=False)
plt.xlabel('VitD_levels')
plt.title('VitD_levels before treatment', fontsize=15, pad=10, color='blue')
plt.show()
```

## Cleaning Findings

After checking for duplicates, I found none. I suspected there might be duplicates that weren’t appearing due to missing or invalid data, so I also queried for duplicates based solely off of the Customer_ID variable, the Interaction variable, and the UID variable. Still, no duplicates were found. 

When I checked for missing values, I found several different variables that were missing values. The variables and total missing values are as follows: 

```python
#total number of nulls
med_data_nullity = med_data[['Children', 'Age', 'Income', 'Soft_drink',
                            'Overweight', 'Anxiety', 'Initital_days']].isnull()
print(med_data_nullity.sum())
```
![IMG_1567](https://github.com/user-attachments/assets/a7b75f23-601b-4f46-8be1-27be49820a79)

When detecting outliers, I found the following variables had outliers: Income, Population, Children, TotalCharge, and VitD_levels. Income outliers begin at the upper whisker around $100,000. While it is not shown on the boxplot, I believe incomes less than $4,000 to be outliers due to the nature of that being incredibly low for annual income. The presence of such large income values causes the low-end outliers to not be present on the plot. 

Population outliers begin at the upper whisker around 35,000. While it is not shown on the boxplot, I believe population values less than 20 are also outliers. I verified these suspicions by googling population data based on Zip code. Children outliers begin at the upper whisker at values greater than 6. TotalCharge outliers begin at the upper whisker around 13,000. I found outliers in the VitD_levels variable to be on the lower end, but also the upper end. On the lower end, values less than 12 were considered outliers, whereas on the upper end, values greater than 26 were found to be outliers. 

## Justification of Mitigation Methods 

Because I found no duplicates, I did not drop any data because of duplication. For the missing values, I used various methods to treat each variable separately. 

![IMG_1568](https://github.com/user-attachments/assets/f9b35b77-ddb6-448f-9fa5-18fcde776485)

For the variables Soft_drink, Anxiety, and Overweight, I found these variables to be Boolean. To treat the missing data, I decided that the best treatment method was to impute the most common used value in each of these variables. I chose this because it was the most logical method given there are only 2 options to select: yes or no (or 1 or 0). 

![IMG_1569](https://github.com/user-attachments/assets/f6fdd29a-63ae-4db8-91dc-e45ab974c5a6)

For the Population variable, I chose to replace the missing values by imputing the median. Before doing so, I also decided to change all zero values as NaN. My interpretation of the data was that a zero in Population was actually a missing value. Using the median value made the most sense to me because I did not want to use the mean so as to distort the distribution of the data. 

![IMG_1570](https://github.com/user-attachments/assets/5d8efd2c-cb57-4ddb-ae16-d7068e2b9ca3)

For the Age variable, I went a different route and chose to use the K-Nearest Neighbor method of imputing missing values. Typically, this method is used for continuous variables, and Age is actually a discrete quantitative variable. However, I attempted to use univariate statistical imputation, and each time I did the distribution of the variable showed to be greatly distorted. When I used the KNN method to impute the missing values, the mean and the standard deviation were least impacted, which is why I decided to stick with this method. Lastly, using the KNN method left one missing value. So, in order to fully treat this last value, I simply chose to use forward fill imputation. While this would not have been ideal on a large scale in this dataset, imputing only 0.01% of the data in this way has a negligible impact. 

![IMG_1571](https://github.com/user-attachments/assets/d7477261-7dbf-42ad-ad26-f83b28cd0c2d)
    
For the Income variable, I found that the method used for Age also worked best: K-Nearest Neighbor. Looking over the data before and after imputation, KNN proved to be the best imputation technique as it did not alter the mean or standard deviation values much. 

![IMG_1572](https://github.com/user-attachments/assets/1f8ee0e3-5f79-4274-90e7-a4cd3d196acb)

For the Children variable, I chose to impute the missing values with the median. Using the mean wouldn’t make much sense for this variable as you can’t have 2.5 kids. Statistically speaking, the median value logically made the most sense to use for imputation. Though the graph changes slightly, the mean value before and after imputation is not altered much from 2.09 to 1.81, and the standard deviation moves from 2.15 to 1.91. 
          
![IMG_1573](https://github.com/user-attachments/assets/9b538f70-93f8-4d45-8d1e-140a822d4860)

Lastly, for the Initial_days variable, I used univariate statistical imputation by imputing the missing values with the mean. Given that this variable is a continuous quantitative variable, I felt it made perfectly logical sense to apply the mean rather than the median or mode. Though the plot changes visually, the mean value before and after imputation remains unchanged at 34.43. The standard deviation is only slightly altered from 26.28 to 24.86. 

![IMG_1574](https://github.com/user-attachments/assets/63c38808-f1c3-4aff-ab37-e884c70cfb71)

Next in the cleaning process, I looked at the outliers that were present in the Income, Population, Children, TotalCharge, and VitD_levels variables. For the Income variable outliers, I decided to use a few different means of treatment. First of all, given the output on the boxplot, the values on the upper whisker were very close to the whisker and were relatively compacted tightly together from $100,000 to $175,000. 

Therefore, when inputting the upper outliers, I decided to only impute values greater than $175,000 as I felt the rest of the values were most likely accurate. Therefore, I retained all outliers from $100,000 to $175,000, and imputed those values greater than $175,000 with the median. Secondly, despite the boxplot showing any values below the lower whisker, I do feel that any value lower than $4,000 should be considered an outlier as these values would be extremely low for any individual living in the United States. Therefore, I imputed values less than $4,000 with the median also. 

![IMG_1575](https://github.com/user-attachments/assets/914d7a2b-7cc4-48e3-8ecb-3d17994db4d5) 

For the Population variable outliers, as with Income, the boxplot showed tightly grouped values very close to the upper whisker. For this reason, I chose to only impute values greater than 100,000 as this is the point around where the plot started showing more dispersion. I also imputed values lower than 20 as I felt these values were outliers given the fact that I was able to verify in Google that these Zip codes were populated with much larger values than the data provided. Both sets of outliers were imputed using univariate statistical imputation by imputing the missing values with the median. 

![IMG_1576](https://github.com/user-attachments/assets/5553debf-c498-4419-bd71-421fa7358264)     

For the Children variable outliers, all values greater than 6 were considered outliers. However, these values could be possible. Due to this fact, I decided to exclude these outliers from the dataset, but not delete them entirely. I stored these outliers in a new Pandas DataFrame. After dropping these rows from the original dataset, I found that the new boxplot still showed outliers that were greater than 3. To treat these values, I again decided to exclude them by appending these values with the same outliers data frame from above. Once I updated the outliers DataFrame, I dropped all values greater than 3 from the original data set. 

![IMG_1577](https://github.com/user-attachments/assets/e4becc8a-f395-451f-bde8-ed0420befc35)

For the TotalCharge variable outliers, the boxplot showed tightly grouped data at the upper whisker. For this reason, I chose to only impute values greater than $21,000 as this is the point around where the plot started to show dispersion in the outliers. I decided to impute the values using univariate statistical imputation by imputing the missing values with the mean. 

![IMG_1578](https://github.com/user-attachments/assets/e52b09ee-38fd-4adf-9a30-9ea86a10defb)
      
For the Vit_D levels variable outliers, I decided to retain all lower end outliers and also any upper outliers lower than 40. This is because despite them being outliers, they are most likely valid values given they are patients in a hospital. However, typically any value greater than 40 would be considered abnormally high, so for that reason I decided to impute the mean value for any outlier greater than 40. 

![IMG_1579](https://github.com/user-attachments/assets/31699ddc-347b-4c27-a46d-7d6fc225f223)
     
## Mitigation Code

```python
#treat missing values
med_data['Soft_drink'] = med_data['Soft_drink'].fillna(med_data['Soft_drink'].mode()[0])
med_data['Anxiety'] = med_data['Anxiety'].fillna(med_data['Anxiety'].mode()[0])
med_data['Overweight'] = med_data['Overweight'].fillna(med_data['Overweight'].mode()[0])
med_data['Population'] = med_data['Population'].replace(0, np.nan)
med_data['Population'].fillna(med_data['Population'].median(), inplace=True)
med_data['Age'].interpolate(method='nearest', inplace=True)
med_data['Age'].interpolate(method='ffill', inplace=True)
med_data['Income'].interpolate(method='nearest', inplace=True)
med_data['Children'].fillna(med_data['Children'].median(), inplace=True)
med_data['Initial_days'].fillna(med_data['Initial_days'].mean(), inplace=True)

#treat outliers
med_data['Income'] = np.where(med_data['Income'] > 175000, np.nan, med_data['Income'])
med_data['Income'] = np.where(med_data['Income'] < 4000, np.nan, med_data['Income'])
med_data['Income'].fillna(med_data['Income'].median(), inplace=True)
med_data['Population'] = np.where(med_data['Population'] < 20, np.nan, med_data['Population'])
med_data['Population'] = np.where(med_data['Population'] > 100000, np.nan, med_data['Population'])
med_data['Population'].fillna(med_data['Population'].median(), inplace=True)
children_outliers = med_data[(med_data['Children'] > 6)]
med_data.drop(med_data[(med_data['Children'] > 6)].index, inplace=True)
children_outliers2 = med_data[(med_data['Children'] > 3)]
children_outliers = pd.concat([children_outliers, children_outliers2], axis='columns')
med_data.drop(med_data[(med_data['Children'] > 3)].index, inplace=True)
med_data['TotalCharge'] = np.where(med_data['TotalCharge'] > 21000, np.nan, med_data['TotalCharge'])
med_data['TotalCharge'].fillna(med_data['TotalCharge'].mean(), inplace=True)
med_data['VitD_levels'] = np.where(med_data['VitD_levels'] > 40, np.nan, med_data['VitD_levels'])
med_data['VitD_levels'].fillna(med_data['VitD_levels'].mean(), inplace=True)
```

## Limitations

There are no disadvantages to how I treated the duplicates because there were no duplicates in the dataset. To treat missing values and outliers, I used univariate statistical imputation, forward fill imputation, KNN, and exclusion. The limitations of univariate statistical imputation are that it could possibly alter the distribution of the data. By applying the median, mode, or mean, you could inherently distort statistical data such as the standard deviation or the mean (Chantal, 2019). 

Forward fill imputation, if used to fill large amounts of missing values could skew the distribution which could alter your statistical data. The limitations of K-Nearest Neighbor is that it doesn’t work very well with large datasets or with high dimensionality. It’s also “sensitive to noisy and missing data” (Soni, 2020).

Excluded data is limited in the sense that you may have excluded important information. Yes, the data is still there in a different data frame, but if you’re making analyses on the cleaned dataset, then you won’t have the excluded data in your analyses. Excluding data can also reduce your sample size, if you choose to exclude too many rows. 

## Impact of Limitations

A data analyst that worked with my now-cleaned data might experience a few impacts based on the limitations described above. Univariate Statistical Imputation and Forward Fill Imputation could have skewed the distribution of the dataset, which might have introduced a bias in the dataset that would cause a data analyst to potentially make assumptions that are wrong. In the cleaning of the data, I verified that the statistical data was only slightly altered so the impact here is minimal. 

However, I did choose to exclude all Children outliers greater than three. The impact here is that the data analyst won’t be able to make any conclusions on larger families. Since all families in this dataset are between zero and three, the analyst won’t have any data on the rows I excluded for families with more than three children. 

K-Nearest Neighbor Imputation might have been impacted by the high dimensionality of the dataset. KNN still chose the nearest value to impute, but due to the limitations in the dataset, this could have introduced a slight bias. The analyst may encounter biased data as a result.

## Principle Components 

The total number of principal components used in this analysis is seven. The variables selected in PCA are Lat, Lng, Income, VitD_levels, Initial_days, TotalCharge, and Additional_charge. I used only continuous quantitative variables in this analysis. 

```python
#fit PCA 
pca.fit(md_normalized)

#transform PCA
md_pca = pd.DataFrame(pca.transform(md_normalized), 
                      columns = ['PC1', 'PC2', 'PC3', 'PC4', 'PC5', 'PC6', 'PC7'])

#get PC loadings
loadings = pd.DataFrame(pca.components_.T, 
                        columns=['PC1', 'PC2', 'PC3', 'PC4', 'PC5', 'PC6', 'PC7'],
                        index=md.columns)
print(loadings)
```
![IMG_1580](https://github.com/user-attachments/assets/a3347162-0100-4bd6-8973-d163873b535d)

```python
#create covariance matrix
cov_matrix = np.dot(md_normalized.T, md_normalized)/md.shape[0]

#create eigenvalues
eigenvalues = [np.dot(eigenvector.T, np.dot(cov_matrix, eigenvector)) for eigenvector in pca.components_]

#plot eigenvalues
plt.plot(eigenvalues)
plt.xlabel('Number of Components')
plt.ylabel('Eigenvalue')
plt.title('Scree Plot', fontsize=20, pad=10, color='blue')
plt.axhline(y=1, color='red')
plt.axvline(x=3, color='green')
plt.show()
```
![IMG_1581](https://github.com/user-attachments/assets/cda297a5-0fc9-4183-b465-8ec1b975f07e)
  	
PC1, PC2, PC3, and PC4 should be retained by utilizing the Kaiser Rule. The Kaiser Rule recommends only keeping components that have an eigenvalue higher than 1.0. Given the scree plot of the eigenvalues in my PCA, you can see that the first four PC’s should be retained. 

## Benefits

There are many benefits to using PCA in general. High-dimensional datasets are problematic due to their complexity and size. Machine learning algorithms could fail or run very slowly with high-dimensional data. By using PCA, we can reduce the dimensionality which helps machine learning models to run faster and more efficiently(Bigabid, n.d.). You cannot visualize data in more than 3 dimensions, therefore, applying PCA to 3 dimensions or lower will allow you to visualize the data where you couldn’t have done so before. 

The benefits of my specific PCA are that by using PC1 you can see a strong correlation in Initial_days and TotalCharge. This makes sense in that patients who stayed at the hospital longer incurred higher charges. PC2 shows an indirectly strong correlation between latitude and longitude. This might lead the analyst to find correlations geographically in our medical data. PC3 shows there’s a strong negative correlation between Income and VitD_levels. PC4 shows a strong correlation between Income and Additional_charges. 

## Supporting Documentation
#### Sources of Third-Party Code

Pandas (2023, June 28). Retrieved August 17, 2023, from https://pandas.pydata.org/docs/reference/index.html

Waskom, M. (2012-2022). Seaborn Statistical Data Visualization. Retrieved August 17, 2023, from https://seaborn.pydata.org/index.html

Chantal D. Larose, Daniel T. Larose. Data Science Using Python and R. Wiley; 2019. 

Nehme, Adel (2023). Data Cleaning in Python. DataCamp. Retrieved August 17, 2023, from https://app.datacamp.com/learn/courses/cleaning-data-in-python

#### Sources

Tamboli, N. (2021, October 29). Effective Strategies for Handling Missing Values in Data Analysis (Updated 2023). Retrieved August 17, 2023, from  https://www.analyticsvidhya.com/blog/2021/10/handling-missing-value

Western Governors University (2023). R or Python. Retrieved August 17, 2023, from https://www.wgu.edu/online-it-degrees/programming-languages/r-or-python.html#_

DataFlair (2023). 6 Essential Advantages of Pandas Library – Why Python Pandas are Popular? Retrieved August 17, 2023, from https://data-flair.training/blogs/advantages-of-python-pandas/

Medium (2020, July 3). Advantages And Disadvantages of KNN. Retrieved August 19, 2023, from https://medium.com/@anuuz.soni/advantages-and-disadvantages-of-knn-ee06599b9336
