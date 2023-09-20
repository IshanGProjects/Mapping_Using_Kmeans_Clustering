## Assigning Colorado Counties to Regions Using KMeans Clustering
![image](https://github.com/IshanGProjects/Mapping_Using_Kmeans_Clustering/assets/86436938/d5c8dec8-4cd0-4699-89fb-a6abe034b517)
![image](https://github.com/IshanGProjects/Mapping_Using_Kmeans_Clustering/assets/86436938/f7b1825b-29f7-46f4-8cb9-5c9ce14907b3)


### Introduction

The purpose of this code is to group the counties of Colorado into 9 distinct regions. Given that Colorado has more than 9 counties, we need a strategy to group multiple counties into a single region. We use the KMeans clustering algorithm to achieve this. 

### How it Works

1. **Data Retrieval**: 
    - We start by loading geographic data for all US counties from a given URL.
    - From this dataset, we filter out only the counties of Colorado using the state code `08`.

2. **Reprojection**:
    - The geographic data is originally in a latitude-longitude format, which isn't ideal for spatial distance calculations. Hence, we reproject (convert) this data to UTM Zone 13N (`EPSG:26913`), which is more suitable for Colorado.
    - This transformation ensures that the distance computations, which KMeans uses internally, are accurate.

3. **Centroid Calculation**:
    - For each county, we calculate the centroid, which is essentially the geographic center point of the county.
    - The centroids provide a single point representation for each county, simplifying our clustering task.

4. **KMeans Clustering**:
    - We feed the centroid coordinates of each county to the KMeans algorithm. 
    - KMeans will try to group the counties into 9 clusters (regions) such that the sum of the squared distances between the counties' centroids and the center of their respective clusters is minimized.
    - Each county is then assigned a `region_id` based on which of the 9 clusters it belongs to.
    


### Result

At the end of this process, each county in Colorado is assigned to one of 9 regions. The result is a table of counties with their associated `region_id`, which represents the region they belong to.

# Algorithm Explained


## 1. Initialization:
Choose **k** initial cluster centers. There are various methods to initialize these centers, but a common method is the "Forgy" method where **k** observations are chosen randomly from the dataset to serve as the initial centers.

$$ C^{(0)}_i \quad \text{for} \quad i = 1, \ldots, k $$

where $ C^{(0)}_i $ is the $ i^{th} $ initial cluster center.

## 2. Assignment:
Assign each observation to the nearest cluster center. Let $ x_j $ be the $ j^{th} $ observation, then the cluster $ r_j $ to which $ x_j $ is assigned is given by:

$$ r_j = \underset{i}{\text{argmin}} \ \| x_j - C^{(t)}_i \|^2 $$

where $ C^{(t)}_i $ is the $ i^{th} $ cluster center at iteration $ t $.

## 3. Update:
Recalculate cluster centers as the mean of all the observations assigned to each cluster.

$$ C^{(t+1)}_i = \frac{1}{|S_i|} \sum_{x_j \in S_i} x_j $$

where $ S_i $ is the set of all observations assigned to the $ i^{th} $ cluster.

## 4. Convergence:
Repeat the Assignment and Update steps until the cluster centers no longer change (or change very little) between iterations.

The primary objective of k-means clustering is to minimize the within-cluster sum of squares (WCSS):

$$ WCSS = \sum_{i=1}^{k} \sum_{x_j \in S_i} \| x_j - C_i \|^2 $$

The algorithm aims to find cluster centers $ C_i $ that minimize the WCSS.
