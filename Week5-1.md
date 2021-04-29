# Survey of evacuation shelters in Shibuya Ward

## Ⅰ. Introduction And Problem

Japan has so many earthquakes that it is called an earthquake powerhouse. In recent years, more earthquakes have occurred in Japan. On March 11, 2011, the worst earthquake called the Great East Japan Earthquake caused about 20,000 casualties. It is predicted that a huge earthquake directly under the capital will occur in Tokyo, the capital of Japan, in the near future.

If an earthquake occurs in the economic center of Japan, it will cause more damage than the Great East Japan Earthquake. Possible problems such as the collapse of a towering office building, the tsunami from Tokyo Bay, and the inundation of landfills can be easily imagined. Therefore, the ward must arrange and grasp the evacuation site area in case of an earthquake.

In this project, we will focus on Shibuya Ward, which is adjacent to various companies in Tokyo, and cluster evacuation shelters.
By doing so, the ward will be able to determine the optimal division, and in the event of an earthquake, it will be possible to guide the victims and distribute supplies smoothly.

## II. Dataset

The official website of Shibuya Ward publishes some open data that can be used for business. Fortunately, there is shelter data in it, so we will use it.

Looking at the data,

1. NO
2. prefecture name
3. city / ward / town / village name
4. name
5. name_kana
6. address
7. dialect
8. latitude
9. longitude
10. extension number
11. city / ward / town / village code
12. disaster type_flood
13. disaster type_cliff Collapse
14. landslides and landslides
15. disaster type_high tide
16. disaster type_earthquake
17. disaster type_tsunami
18. disaster type_large-scale fire
19. disaster type_inland flood
20. disaster type_volcanic phenomenon
21. area
22. location type
23. designated evacuation center There are columns for duplication with
24. target town councils / disaster associations
25. images
26. URLs
27. remarks

This time we will use the name, latitude and longitude.
Most of the other data were missing values and are not used.

## Ⅲ. Methodology

To get started, I created a datafrane of the name, latitude, and longitude of the shelter in Shibuya Ward.

Below is the head of dataframe which displays 5 of 118 shelters.

![dataframe](/result/dataframe.png)

<div style="text-align: center;">Figure 1: Shibuya Shelter Dataframe</div>
<br>

After accessing the exact latitude and longitude of Shibuya, Tokyo, Japan using the geocode library, I created a map using the Folium python library.
I set the shelter marker on the map and used geojson to draw the border of Shibuya.

![map](/result/map.png)
<div style="text-align: center;">Figure 2: Map of the Shelter of Shibuya</div>
<br>

Areas of shelter were clustered and divided into compartments using the Kmeans method.
After that, using the Folium API, we obtained a venue near the evacuation shelter and examined the relationship with the evacuation shelter.

## IV. Results and Discussion

From the clustering model, cluster labels were generated for each of the shelters, as shown in the head of the dataframe below.

![cluster_dataframe](/result/cluster_dataframe.png)
<div style="text-align: center;">Figure 3: Shelter with Cluster Labels</div>
<br>

We created a colored map of clustered shelters. The following is a clustered map.

![cluster_map](/result/cluster_map.png)
<div style="text-align: center;">Figure 4: Map of Shelter with Cluster Labels</div>
<br>

If you look at this map, you can see that it is classified into three categories from the top.
The bar graph below shows the number of shelters in each area.

![cluster_count](/result/Count_of_cluster.png)
<div style="text-align: center;">Figure 5: Count of cluster id</div>
<br>

The number of id 0 is the largest, and id 2 is the smallest.
We define this clustering label from 0 as north, center, and south.

Next, the venue with a radius of 500m from the evacuation center is acquired and displayed on the map.

![cluster_venue_map](/result/cluster_venue_map.png)
<div style="text-align: center;">Figure 6: Venure Map</div>
<br>

The venues were counted by category and graphed.

![Count_of_Venue_Category](/result/Count_of_Venue_Category.png)
<div style="text-align: center;">Figure 7: Count of Venue Category</div>
<br>

Most facilities are restaurants.
Shibuya is a business district, and many people eat with their colleagues at restaurants during breaks and on their way home.

In addition, shelters were counted for each clustering.

![Count_of_Venue_Category_By_Cluster_Ids](/result/Count_of_Venue_Category_By_Cluster_Ids.png)
<div style="text-align: center;">Figure 8: Count of Venue Category By Cluster Ids</div>
<br>

There are many cafes and Italian restaurants in the north.
Since there are many evacuation centers such as parks instead of schools, it is expected that the main area is tourism for young people.
It has the largest number of shelters, but because it is a park, it may be a temporary shelter or you may be forced to live outdoors.
Since various business people come and go, it can be expected that there will be many people, so it may be that many parks have been set up as shelters.

![North](/result/North.png)
<div style="text-align: center;">Figure 9: Map of the North</div>
<br>

Many different restaurants are lined up in the center.
There is also a large park called Yoyogi Park in the center, which is a base for people's lives.
Many young people come to Harajuku every day for clothes and trendy food.
There are many evacuation centers and schools, and relatively safe evacuation routes are secured.
However, each shelter is a little far away, and it is expected that it will be difficult to meet with the family in the event of confusion.
Since a relatively large number of people can evacuate to Yoyogi Park, it would be wise to evacuate to Yoyogi Park if you are near here.

![Central](/result/Central.png)
<div style="text-align: center;">Figure 10: Map of Central</div>
<br>

There are overwhelmingly many cafes in the south, and there are many evacuation centers and schools.
This is a residential area, and it is expected that a small group will come to evacuate.
Since the number of children and the elderly is expected to increase, it is better to set the priority of supply of supplies relatively high.
However, there is only one evacuation center for Hiroo, and the other evacuation centers are far away.
A shelter should be built in this place as soon as possible.

![South](/result/South.png)
<div style="text-align: center;">Figure 11: Map of South</div>
<br>

## V. Conclusion

In this project, we checked the status of evacuation shelters in Shibuya Ward and examined which places are suitable as evacuation shelters and which places have problems.

From the results of clustering, it is divided into north, central, and south, the north is a business district with many temporary shelters such as parks, and the center is expected to be flooded with young people such as Harajuku, so those who evacuated to a large park called Yoyogi Park Is relatively safe, the south is a residential area, and the number of children and the elderly is expected to increase due to the relatively large number of schools, so it was predicted that it would be better to prioritize the supply of supplies.