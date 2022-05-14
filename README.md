# Knime-WorldHappinessReport
Analyzing World Happiness Report by using Knime

Introduction:

	Happiness is the main purpose of life and people who decide or want to live in a country where they will be happy. Every person anticipates good life conditions from their country. Not only for themselves but also for their children. All of the countries are responsible to fulfill the main needs of their citizens and increase the conditions every passing day. If not, people try to change the city or migrate to other countries where they believe to be happy. Economic production, social support, life expectancy, freedom, absence of corruption, and generosity are the main factors of happiness. The World Happiness Report 2021 is a publication that includes these parameters and shows us the survey of global happiness [1].

Main:

Knime is a commonly used data mining tool. It is easy to use and preferred not only for personal usage but also by companies. We can visually create data flows, determine parameters, execute steps and inspect results without writing programming codes. In Knime, nodes are having different processes and by using these nodes we conduct the flow. These make Knime more usable. That’s why I use Knime for the analysis of this report [2]. 
Happiness is not a single case, it connects some parameters.  In my data mining process I used these parameters; Life Ladder, Log GDP per Capita, Social Support, Healthy Life Expectancy at Birth, Freedom to make life choices, Generosity, Perceptions of corruption, Positive and Negative effects.
There will be 2 different analyses; one is whole data from 2008 to 2020 and the data only includes 2020 parameters. We will visualize them and make a conclusion and prediction for the happiest countries in the world.

Data Mining:

For this analysis data set as “csv” file took from “kaggle.com” and was attained from Gallup company. Gallup is an American analytics and advisory company that makes polls about specific topics all around the world from 1980. The company collects the World Happiness report data from 2008 and this analysis includes the period between 2008 to 2020.

Phases:

For Modelling 4 parts were designed for the flow. They are data reading, data cleaning and filtering, data modeling, and visualization phases.


![image](https://user-images.githubusercontent.com/81926522/168450121-dff5baa2-e07e-4916-8952-e5910288169d.png)


 
Data Reading:

Before reading the data first, I converted “csv” file to “xlm” file and investigated the content. There were some unknown values. On the internet, some values can be reachable and I searched all missing values and wrote the ones that I found. Then I checked that there were any unprepared values or wrong marks and then I fixed them on excel.

![image](https://user-images.githubusercontent.com/81926522/168450126-15752713-c176-4213-8ecb-4e9fb4ec505e.png)

 

	Next, convert the “xlm” file to “csv” and add it into the “File reader” nodes. Every node should be configured first. We can choose parameters and change settings with configure tab.

Data Preperation:

	We also call “Cleanin and Filtering Process” for this part. In the data preparation phase first, we can change column names on excel files but we can also use the “Column Rename” node for this. Then the filtering process is coming. There is comprehensive and also redundant data in the dataset. So, it is important to choose only the ones we will use. So we use “Row Filter” nodes and select the including and excluding rows.
Then, with “Reference Row Filter” we chose the data and reference table columns we want to use. If we need more filtering like selecting year period or country name, etc., we can use the “Row Filter” node again. We will analyze both the whole period and 2020 data, so I added a filter as “2020”.  Then I used a column filter for which columns would get into the process and which ones wouldn’t. I excluded the “Negative affect” column and include all the other columns as I examined.	
Lastly, I used the “Missing Value” node. We can erase, give the minimum, mean, maximum, or most frequent value for the missing ones on the data table. It is a very important part. Because some processes don’t work or can give wrong results if there are missing values on the data table. With this node, we finish our data cleaning and filtering phase.

Modeling:

	For determining the correlation between parameters I used the ”Linear Correlation” node and saw that the highest correlation is 0.8383 between Log GDP per Capita and Healthy Life Expectancy at Birth and 0.7855 between Life Ladder and Log GDP per Capita.  By using “Partitioning” Node for the first partition we used %80 relative value and %20 test value. Also, we selected linear sampling.
	For modeling I chose the “K-Means” clustering method. K-means places n number observations into k number clusters. Each cluster members have a relation with each other and take part with the nearest mean value. Imagine, there is a "k" number cluster center point (centroid) and try to make these points get near to the data but different from one another [3]. 
After that, assign each data point one by one to the closest centroid. Cluster center points and the cluster members are changing place during the process. At the end, the final shape of clusters comprises and prediction completes. At the “K-means” node, I selected 3 clusters.

  
![image](https://user-images.githubusercontent.com/81926522/168450132-a194ab73-aec5-492a-ac67-50ec586c9404.png) ![image](https://user-images.githubusercontent.com/81926522/168450136-c56e27e2-5833-4c54-947d-c6ea9e66eb5e.png)


These are the K-Means algorithm formula and Linear Correlation diagram. Clusters and labeled inputs were generated at the K-Means node. Also, I connected the “Cluster Assigner” node to assign parameters.

 ![image](https://user-images.githubusercontent.com/81926522/168450139-3e674203-efaa-4ceb-9416-80c0474134e1.png)


	“DBSCAN” is a density-based data clustering algorithm. It doesn’t require a number for clustering. It uses distance measure and groups the points together that are closed to each other [4].  DBSCAN determines the “noise” parameters. If the point is far and not reachable then it is a noise or outlier.

![image](https://user-images.githubusercontent.com/81926522/168450142-ee20ff7f-07e9-494f-bd70-afba64cafa39.png)
 

	When using DBSCAN I used “Cluster Assigner” and “Numeric Distance” nodes and connected them to the “DBSCAN” node. Then I passed to the visualization part.

Visualization:

	 “Color Manager” and “Shape Manager” nodes are used for determining the color and shape of the points in the clusters.  “Interactive Table” node shows each cluster member with their specific colors after the process.

![image](https://user-images.githubusercontent.com/81926522/168450147-71df5f9b-c79f-4ba6-83dd-3146ce8cde03.png)
 

	For visualization, the K-Means clusters “Scatter Plot” and “Scatter Matrix” nodes are used. The year column was filtered to “2020”. So, these nodes are showing 2020 values and predict with 2020 values. We can see 3 clusters separately and clearly.

 ![image](https://user-images.githubusercontent.com/81926522/168450154-cba77271-70e8-48fb-9c05-9736f9d6a29b.png)

 
	For DBSCAN, no filtering was used for the year parameter. So, all of the raw data was used in prediction. Also for visualizing the clusters Scatter Plot and Scatter Matrix nodes were used.

 ![image](https://user-images.githubusercontent.com/81926522/168450155-b18be30a-92e2-4aaf-8f22-50de5852c09a.png)

 
“Line Plot” node is also another visualization tool. By using this, we can visualize the data using lines [5].

 ![image](https://user-images.githubusercontent.com/81926522/168450157-a3d3ef2f-a23b-479d-96e2-dd5326abf2d1.png)


	ROC curve shows the performance of the classification model. In the figure, we can see the chosen lines make a curve, start from zero and reach 1 [6]. So, for our diagram, we see that it has good performance.

 ![image](https://user-images.githubusercontent.com/81926522/168450161-5ceddeb9-44c2-47f5-b2c3-d6a58a1fac3f.png)

 
Conclusion:

	After the visualization in the first cluster, there are; “Finland, Denmark, Switzerland, Iceland, Ireland, Netherland, Norway, Belgium, Singapore, France, Germany, Italy, Sweden, United Kingdom, Luxemburg, Malta, Netherland, New Zealand, Austria, South Korea, Japan, Canada, Australia, New Zealand, Croatia, Italy, Spain, and Israel. 
	In the middle cluster, there are; “USA, China, Saudi Arabia, Slovakia, Poland, UAE, Estonia, Russia, Lithuania, Argentina, Latvia, Bahrain, Lithuania, Serbia, Turkey, Greece, Uruguay, Brasil, Venezuela, Mexico, Colombia, Montenegro, Ukraine, South Cyprus, Bulgaria, Taiwan, Tajikistan, Kazakhstan, Ecuador, Albania, Macedonia, Dominican Republic, and Iran”. Turkey is in the middle of the second cluster and between 2008-2020 the points are close to each other. So we can say that Turkey has average happiness according to other countries in the world.
	In the last cluster, there are; “Mongolia, Kosova, Laos, Ghana, Ivory Coast, South Africa, Egypt, Ethiopia, Uganda, Iraq, Philipines, Cambodia, Namibia, Benin, Kenya, Myanmar, India, Tanzania, Zimbabwe”. 
	After the prediction, If we sort the top 10 happiest countries these are; “Finland, Denmark, Switzerland, Iceland, Ireland, Netherland, Norway, Sweden, Luxemburg, and Netherland”. We can easily see that all of them are located in North Europe. We can also say that the happiest continent is Europe and less happy one is Africa. The strongest factors are first healthy life expectancy, then life ladder, Log GDP per capita, and social support. Also, that is why many people try to migrate, live, work, and birt a child in these countries.
