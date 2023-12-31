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

