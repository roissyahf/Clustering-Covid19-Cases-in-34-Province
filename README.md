# Clustering Covid-19 2020 Cases in Indonesia
We aim to clustering 34 Province in Indonesia according to the Covid-19 2020 Cases using historical data set.
Our main goal of pushing this mini project is to showcase our learning progress also we hope to get feedback, advice, or critics from public.

# Problem Understanding
Clustering province based on the Monthly Covid-19 Cases will help the Indonesia central government to prioritize the funding of Covid-19.

# Data Understanding
- Data of Indonesia's Covid-19 2020 from 31 March 2020 to 31 December 2020.
- We obtained this data set from our mentor in ISE! Data Science Academy 2022 held by ITS. We can also obtained the data set from Kaggle independently.
- The data set has 37 columns and 9959 rows.
- There's no data dictionary available, however we can grouped each variable in 4 section:

| **Section** | **Variables** |
| --- | --- |
| **Time** | Date, Time Zone |
| **Geographical** | Location ISO Code, Location, Location Level, Continent, Country, Island, Province, Special Status, Longitude, Latitude, City or Regency, Total Cities, Total Regencies, Total Districts,  Total Urban Villages, Total Rural Villages, Area (km2) |
| **Region** | Population, Population Density |
| **Covid-19 Cases** | New Cases, New Deaths, New Recovered, New Active Cases, Total Cases, Total Deaths, Total Recovered, Total Active Cases, New Cases per Million, Total Cases per Million, New Deaths per Million, Total Deaths per Million, Case Fatality Rate, Case Recovered Rate, Growth Factor of New Cases, Growth Factor of New Deaths |

# Data Preparation
We use python packages like Pandas, NumPy, Seaborn, Matplotlib, Plotly, and Scikit-learn. 

# Data Cleansing
- There are 305 missing value in Province column, we need to drop it because there's no other way to impute Province.
- We detect outliers in 'Population Density', 'New Deaths', 'New Recovered', 'New Active Cases' but we didn't handle it because outliers is useful for creating its unique cluster. If we drop them, we will lose important insight.

# Exploratory Data Analysis
* What are 5 Province with the highest New Active Cases and 5 Provinces with the lowest New Active Cases?
Jawa Tengah, DKI Jakarta, Jawa Barat, Banten, and Jawa Timur are 5 provinces with the highest New Active Cases. Meanwhile Maluku Utara, Kalimantan Barat, Sulawesi Barat, Papua Barat, and Gorontalo are 5 province with the lowest New Active Cases.
* Show top 5 Province with the highest Case Fatality Rate and 5 Province with the lowest Case Fatality Rate?
Province with the highest Case Fatality Rate are Jawa Tengah, Jawa Timur, Bengkulu, Sumatera Selatan, and Nusa Tenggara Barat. While, province with the lowest Case Fatality Rate are Kalimantan Utara, Kalimantan Barat, Nusa Tenggara Timur, Papua, and Kepulauan Bangka Belitung.
* What are top 5 Province with the lowest New Recovered?
The conclusion obtained after sorting Province by lowest New Recovered is the number of New Recovered are higher than the number of New Death, even though the number of New Active Cases inreased.


# Data Manipulation
We decide to only use 'Province', 'New Deaths', 'New Recovered', 'New Active Cases', 'Case Fatality Rate', 'Case Recovered Rate' for modeling, thus we grouped clean data set by 'Province'.
After that, we aggregate 'New Deaths', 'New Recovered', 'New Active Cases', 'Case Fatality Rate', 'Case Recovered Rate' by its median, then we divide 'New Deaths', 'New Recovered', 'New Active Cases' with its Population to reduce variance.

# Modeling
We use KMeans Clustering, firstly we need to standarize features used, then fit and predict the scaled features.

# Evaluation
In this mini project, we use KElbowVisualizer to decide the optimal number of k, the answer is 4. After clusters formed, we calculate Silhouette Score and Davies Bouldin Score. We obtained these result using k=4:
| Silhouette Score | 0.601 |
| --- | --- |
| Davies Bouldin Score | 0.441 |

# Interpretation
We draw boxplot, and independent line chart to see the order of each cluster (Cluster 0, 1, 2, 3) in each variable ('New Deaths', 'New Recovered', 'New Active Cases'). Here's the result:

| **Cluster** | **Member** | **Characteristic** | **Zone** |
| --- | --- | --- | --- |
| **0** | Consist of 3 Provinces: Kalimantan Tengah, Kalimantan Utara, Papua | It has the highest New Active Cases compared to the rest 3 clusters. New Recovered and New Deaths in this cluster is in the third position. | It belongs to "Zone B" (comprises of provinces with the second active Covid-19 transmission) |
| **1** | Consist of 18 Provinces: Aceh, Banten, Bengkulu, Jambi, Jawa Barat, Kalimantan Barat, Kepulauan Bangka Belitung, Lampung, Maluku, Maluku Utara, Nusa Tenggara Barat, Nusa Tenggara Timur, Sulawesi Barat, Sulawesi Tengah, Sulawesi Selatan, Sulawesi Tenggara, Sumatera Selatan, Sumatera Utara | It has the lowest New Active Cases, New Recovered, New Deaths compared to another 3 clusters | It belongs to "Zone C" (comprises of provinces with the third active Covid-19 transmission) |
| **2** | Consist of 1 Province: DKI Jakarta | New Active Cases in this cluster is the second highest, moreover this cluster has the highest New Recovered, and New Deaths | It belongs to "Zone A" (comprises of provinces with the most active Covid-19 transmission) |
| **3** | Consist of 12 Provinces: Bali, Daerah Istimewa Yogyakarta, Gorontalo, Jawa Tengah, Jawa Timur, Kalimantan Selatan, Kalimantan Timur, Kepulauan Riau, Papua Barat, Riau, Sulawesi Utara, Sumatera Barat | New Active Cases of this cluster is in the third position, meanwhile New Recovered, and New Deaths are the second highest | It belongs to "Zone D" (comprises of provinces with the least active Covid-19 transmission) |

# Recommendation
Here is the priority of Province according to formed clusters (the amount of funding given should be considered according to its zone):
* Zone A, consist of DKI Jakarta
* Zone B, consist of Kalimantan Tengah, Kalimantan Utara, Papua
* Zone C, consist of Aceh, Banten, Bengkulu, Jambi, Jawa Barat, Kalimantan Barat, Kepulauan Bangka Belitung, Lampung, Maluku, Maluku Utara, Nusa Tenggara Barat, Nusa Tenggara Timur, Sulawesi Barat, Sulawesi Tengah, Sulawesi Selatan, Sulawesi Tenggara, Sumatera Selatan, Sumatera Utara
* Zone D, consist of Bali, Daerah Istimewa Yogyakarta, Gorontalo, Jawa Tengah, Jawa Timur, Kalimantan Selatan, Kalimantan Timur, Kepulauan Riau, Papua Barat, Riau, Sulawesi Utara, Sumatera Barat.

### Additional Work
Visit this [link](https://public.tableau.com/app/profile/roissyahfernanda/viz/ClusteringCovid-192020CasesinIndonesiasProvince/Dashboard) to view Dashboard Covid-19 2020 Cases in Indonesia's Province
