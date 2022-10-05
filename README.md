# Clustering Covid-19 Cases in 34 Province
Clustering Indonesia's Province according to the Covid-19 Cases Using KMeans

## Mini Project Description
We aim to clustering 34 Province according to the Monthly Covid-19 Cases using historical data set.
Our main goal of pushing this mini project is to showcase our learning progress also we hope to get feedback, advice, or critics from public.

# Problem Understanding
Clustering province based on the Monthly Covid-19 Cases will help the Indonesia central government to prioritize the funding of Covid-19.

# Data Understanding
- Data of Indonesia's Covid-19 2020 from 31 March 2020 to 31 December 2020.
- We obtained this data set from our mentor in ISE! Data Science Academy 2022 held by ITS. We can also obtained the data set from Kaggle independently.
- The data set has 37 columns and 9959 rows.
- There's no data dictionary available. 

# Data Preparation
We use python packages like Pandas, NumPy, Seaborn, Matplotlib, Plotly, and Scikit-learn. 

# Data Cleansing
- There are 305 missing value in Province column, we need to drop it because there's no other way to impute Province.
- We detect outliers in 'Population Density', 'New Deaths', 'New Recovered', 'New Active Cases' but we didn't handle it because outliers will be grouped into its unique cluster. 
If we drop them, we will lose important insight.

# Exploratory Data Analysis
* What are 5 Province with the highest New Active Cases and 5 Provinces with the lowest New Active Cases?
* Show top 5 Province with the highest Case Fatality Rate and 5 Province with the lowest Case Fatality Rate?
* What are top 5 Province with the lowest New Recovered? 
* How's the trend of New Active Cases, New Recovered, New Deaths during 10 months?

# Data Manipulation
We decide to only use 'Province', 'New Deaths', 'New Recovered', 'New Active Cases', 'Case Fatality Rate', 'Case Recovered Rate' for modeling, thus we grouped clean data set by 'Province'.
After that, we aggregate 'New Deaths', 'New Recovered', 'New Active Cases', 'Case Fatality Rate', 'Case Recovered Rate' by its median, then we divide 'New Deaths', 'New Recovered', 'New Active Cases' with its Population to reduce variance.

# Modeling
We use KMeans Clustering, firstly we need to standarize features used, then fit and predict the scaled features.

# Evaluation
In this mini project, we use KElbowVisualizer to decide the optimal number of k, the answer is 4. After clusters formed, we calculate Silhouette Score and Davies Bouldin Score. We obtained these result using k=4: Silhouette Score=0.601, Davies Bouldin Score=0.441.

# Interpretation
We draw boxplot to see the order of each cluster (Cluster 0, 1, 2, 3) in each variable ('New Deaths', 'New Recovered', 'New Active Cases'). Here's the result:
1. **Cluster 0**
    * Consist of 3 Provinces: Kalimantan Tengah, Kalimantan Utara, Papua
    * It has the highest New Active Cases compared to the rest 3 clusters
    * New Recovered and New Deaths in this cluster is in the third position
    * It belongs to "Zone B" (comprises of provinces with the most active Covid-19 transmission)

2. **Cluster 1**
    * Consist of 18 Provinces: Aceh, Banten, Bengkulu, Jambi, Jawa Barat, Kalimantan Barat, Kepulauan Bangka Belitung, Lampung, Maluku, Maluku Utara, Nusa Tenggara Barat, Nusa Tenggara Timur, Sulawesi Barat, Sulawesi Tengah, Sulawesi Selatan, Sulawesi Tenggara, Sumatera Selatan, Sumatera Utara
    * It has the lowest New Active Cases, New Recovered, New Deaths compared to another 3 clusters
    * It belongs to "Zone C" (comprises of provinces with the third active Covid-19 transmission)

3. **Cluster 2**
    * Consist of 1 Province: DKI Jakarta
    * New Active Cases in this cluster is the second highest
    * While, this cluster has the highest New Recovered, and New Deaths
    * It belongs to "Zone A" (comprises of provinces with the most active Covid-19 transmission)

4. **Cluster 3**
    * Consist of 12 Provinces: Bali, Daerah Istimewa Yogyakarta, Gorontalo, Jawa Tengah, Jawa Timur, Kalimantan Selatan, Kalimantan Timur, Kepulauan Riau, Papua Barat, Riau, Sulawesi Utara, Sumatera Barat
    * New Active Cases of this cluster is in the third position
    * New Recovered, and New Deaths are the second highest 
    * It belongs to "Zone D" (comprises of provinces with the least active Covid-19 transmission)

# Recommendation
Here is the priority of Province according to formed clusters (the amount of funding given should be considered according to its zone):
* Zone A, consist of DKI Jakarta
* Zone B, consist of Kalimantan Tengah, Kalimantan Utara, Papua
* Zone C, consist of Aceh, Banten, Bengkulu, Jambi, Jawa Barat, Kalimantan Barat, Kepulauan Bangka Belitung, Lampung, Maluku, Maluku Utara, Nusa Tenggara Barat, Nusa Tenggara Timur, Sulawesi Barat, Sulawesi Tengah, Sulawesi Selatan, Sulawesi Tenggara, Sumatera Selatan, Sumatera Utara
* Zone D, consist of Bali, Daerah Istimewa Yogyakarta, Gorontalo, Jawa Tengah, Jawa Timur, Kalimantan Selatan, Kalimantan Timur, Kepulauan Riau, Papua Barat, Riau, Sulawesi Utara, Sumatera Barat.
