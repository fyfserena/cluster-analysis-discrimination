## Cluster analysis and Discriminant analysis on Sina -Weibo Influencers 

Our aim is to define different roles of social media influencers quantitatively by the help of multivariate analysis techniques.

Statistical methods such as cluster analysis and discriminant analysis are used to classify the Sina-Weibo data of influencer according to their popularity and activity.
The results are as follows: 1) by  hierarchical cluster method and k-means clustering method, the roles can be divided into four categories: "superstar", "influencer", "artist" and "actors"; 2) the correct rate of Fisher's linear discriminant function was 94.5%.

### Background

With the development of social networks, the entertainment industry, as the focus of public attention, also relies on this kind of new media to gradually become transparent, interactive and popular. In the era of "trending search" and "nationwide Weibo", not only actors and artists, entertainment bloggers, but also the official agents of studios have attracted wide attention in Sina-Weibo. Whether it is a nobody or a superstar, everyone is likely to become a trending center.

Therefore, the evaluation of a star's Sina-Weibo influencing ability depends not only on its popularity in the corresponding fields, but also on the how attractive their blogs are. Thus, analysis of a star's influencing ability helps us better position the star's "money absorbing ability" in the era of "fan economy".

### Introduction to sample data

Sina-Weibo is the website with the most complete collection of stars and the widest user group. We select 1747 pieces of data, including information about actors, artists, athletes, influencer, etc.

**Dependent variable**: 
Microblog account: text format, the name of the star microblog account. 

**Features:**

- Following: continuous variable (unit: number), value range [04833], is the number of other people followed by a star. It can be used to reflect the microblog characteristics of the star.
- Number of Blog posted: continuous variable (unit: number), value range [2,193299], as of the date of data collection. The number of tweets that are still kept in time can be used to reflect the microblog activity of the star.
- Account rank: continuous variable (unit: rank LV), value range [2,46], according to the number of active days of users. It is confirmed that users with higher level can enjoy more privileges, which can be used to reflect the activity of the star's microblog.
- Followers: continuous variable (unit: person), value range [2239,90928261], which can be used to reflect stars how popular it is.
- Membership level: continuous variable, value range [1,6], member level of star registered microblog, need to recharge actively, can enjoy more privileges, to a certain extent, can reflect the influence of the star.
- Adoration value: continuous variable (unit: score), value range [22,5626047]. Fans need to sign in, or send flowers and gifts to the star to increase the adoration value. The value can reflect the popularity and influence of the star.
- Number of flowers received: continuous variable (unit: bundle), value range [11,2763629. Flowers and gifts need to be purchased, so this value can reflect the popularity and influence of the star.

### Data manipulation

**Cleaning**
1） Delete duplicate data: mark observations with the same posting name and delete duplicate information;
2） Dealing with missing values: We subjectively classify the data with missing values. For the stars that have many followers, the incomplete data is filled in manually. For the users with little influence, we delete their missing data.

**Feature engineering**
Firstly, we use **principal component analysis (PCA)** to do factor analysis on seven variables. The results are as follows:

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210317123344595.png" alt="image-20210317123344595" style="zoom:50%;" />

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210317123433524.png" alt="image-20210317123433524" style="zoom:50%;" />

The component matrix suggests that we extract two principal components, but their cumulative total variance of interpretation is only 63.486%. This can not reflect the important information of the original data, that is, the ability of each principal component to concentrate the original variable information is not significant different, so we do not choose the method of PCA for dimension reduction.

In addition, in order to verify the above conclusions and eliminate overlapping information, we conducted correlation analysis on these variables. The result shows that the correlation of most variables are less than 0.3, but there is a strong correlation between the "adoration value" and the "number of flowers received", with the Pearson correlation coefficient is as high as 0.998.

Since fans sending flowers to the stars is one of the ways to increase the star's "adoration value"), "number of flowers received" and the "adoration value" reflect the same information. Therefor, we delete the variable of "the number of flowers received".



### Cluster analysis

#### Hierarchical cluster method

In order to determine the details of within-group distance measurement and among-group distance measurement, we need to know more about the the sample data.

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210317144957920.png" alt="image-20210317144957920" style="zoom:50%;" />

Descriptive statistics show that each variable has great difference in value. In order to avoid the impact of magnitude difference on clustering results, we first use standardize variables, and model the cleaned data using inter-group-link clustering, with the square Euclidean distance as the measurement.

Now we see how the aggregation coefficient changing with the number of classifications. 

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210317150006705.png" alt="image-20210317150006705" style="zoom:50%;" />

When the number of categories is less than or equal to 3, the aggregation coefficient decreases rapidly with the increase of the number of categories; when the number of categories is greater than or equal to 4, the aggregation coefficient tends to zero gently. Therefore, the number classification should be 3 or 4.

Four groups of mean values were extracted for comparison:

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210317150420966.png" alt="image-20210317150420966" style="zoom:50%;" />

There is no significant difference between the four groups in the level of microblog and membership, and there are significant characteristics in other indicators.



#### k-means clustering

**Define k**

In the k-means clustering method, the determination of k value of the number of clusters depends on practical experience and the reference to the clustering results of the hierarchical clustering method. Thus we pick k = 4.

[k-means++: The Advantages of Careful Seeding](http://ilpubs.stanford.edu:8090/778/1/2006-13.pdf)

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318095538927.png" alt="image-20210318095538927" style="zoom:50%;" />

From the table above, it can be seen that the distance between the four centroids (seed points) is very large, and thus it is almost impossible to be in the same class, so the clustering results are relatively reliable.



**Final centroids** 

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318100222017.png" alt="image-20210318100222017" style="zoom:50%;" />

From the above "final cluster center" table, we can see that the four types of microblog user samples have their own characteristics in activity and popularity, which are consistent with our intuitive expectation.

**Analysis of Variance**

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318110130505.png" alt="image-20210318110130505" style="zoom:50%;" />

From the ANOVA table that the six variables selected have significant contributions to the classification, which indicates that previous variable selection process is scientific and the results are reliable.

In particular, compared with the hierarchical clustering results, the results obtained by k-means are quite different in the specific number of each class, but the characteristics and classification ideas of each class are almost the same. The conclusions of the two are similar and complementary to each other. The reliability of the two clustering results is supported by each other.



#### Discriminant analysis

After clustering Sina-Weibo influencer, we collect several trending influencer data, and try to identify the categories of these stars by discriminant analysis. (In order to eliminate the influence of dimension, we have standardized all the data here.)

**Decide prior probability**

In order to verify the feasibility of discriminant analysis and determine the prior probability, a discriminant analysis is carried out with the original data.

* **Using equal prior probability**

  <img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318114612435.png" alt="image-20210318114612435" style="zoom:50%;" />

The results show that 94.5% of the grouped cases are classified correctly, so we think that the method is feasible from the perspective of accuracy.

* **Using weighted prior probability**

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318114911183.png" alt="image-20210318114911183" style="zoom:50%;" />

Only 90.2% of the grouped cases are correctly classified by this method, so we choose equal priori probability for discrimination.

**Test for the equality of within-group means**

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318115612442.png" alt="image-20210318115612442" style="zoom:50%;" />

Since the centroids of all features in each group are significantly different, the discrimination analysis is meaningful.



**Fisher Canonical discriminant functions**

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318120016229.png" alt="image-20210318120016229" style="zoom:53%;" />

where $x_1$ is following, $x_2$ is fans, $x_3$ is number of posts, $x_4$ is account rank, $x_5$ is adoration value, and $x_6$ is membership level.      

**Description of discriminant functions**

<img src="C:\Users\fyfse\AppData\Roaming\Typora\typora-user-images\image-20210318140223255.png" alt="image-20210318140223255" style="zoom:50%;" />