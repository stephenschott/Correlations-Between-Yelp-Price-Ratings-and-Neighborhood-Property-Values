Predicting Neighborhood Affluence with Yelp Ratings
Problem Statement
Is there any correlation between Yelp Restauraunt price ratings and neighborhood affluence in Seattle.
Data Gathering
We gathered our housing and rental values/rates from the Zillow Home Value Index (ZHVI) and Zillow Rent Index (ZRI), which were publicly available. We obtained income, median rent, and population statistics by neighborhood from city-data.com, which maintains a database of statistics on US cities through both city and private data sources. This information required web scraping, as an API was not available. Finally, we gathered yelp restaurant price ratings from Yelp.com utilizing their API.
Methods
In order to take as local an approach as possible, we attempted to correlate Yelp restaurant pricing with Seattle neighborhoods, which are significantly smaller areas than zip code or the city as a whole. We were able to find median home values, median rental rates, and median income for each neighborhood. After obtaining our Yelp data, we created a dataframe that contained nearly 1,000 random points throughout the city with their latitude and longitude, and then the proportion of restaurants with 1, 2, 3, and 4 price-point ratings by Yelp within both a half mile radius and a mile radius. We then looked for correlations with neighborhood data.
To attempt to get better scores, we attempted a second method which included using points randomly generated throughout the city, and running the Yelp API on the latitude and longitude of those points. The hope here is to get more restaurants, since we initially only got 960 out of roughly 3350 for the city. We then looked at both the number and proportion of restaurants with 1, 2, 3, and 4 price-point ratings by Yelp within a .5 and 1 mile radius. We did get more restaurants by doing this, and our scores improved somewhat.
Modeling
We ran models with the input being proportion of Yelp restaurant 1, 2, 3, and 4 price-points within a half-mile and a mile radius. The inputs were run three times, once against neighborhood median home values, once against neighborhood median rental rates, and finally against neighborhood median income. For median home values and median rental rates, we utililzed Linear Regression, Adaboost, LASSO, KNN, and Decision Tree models. For the median income of neighborhoods we utilized the same models plus Ridge and Bagged Decision Tree models.
Results
Ultimately, most of the models were overfit, and severely overfit in some cases. There were some instances that returned r squared scores in the upper 40s and low 50s percentage that weren't overfit, however this range is still not a super high rate for correlating Yelp price ratings to neighborhood affluence.
Conclusion
We were not able to find significant correlations between neighborhood affluence and Yelp restaurant price ratings. We cannot rule out that there are correlations, however. This is primarily because Yelp's API only allowed us to obtain about 40% of the restauarants in the city, well below what one would need for accurate results in this project. Additionally, to get more accurate results it would be beneficial to get every property value and its latitude and longitude for the city, so that when utilizing a random point's radius you can get an accurate median home value, whereas we had to utilize the next best thing which was neighborhood median home value.
Data Sources:
Housing and Rental value/rate data was gathered from Zillow. Datasets on the Zillow Home Value Index (ZHVI) and Zillow Rent Index (ZRI) were publicly available and downloaded directly from: https://www.zillow.com/research/data/
Income, median rent, and population statistics by neighborhood were gathered from city-data.com, which maintains a database of statistics on US cities through both city and private data sources. In the absence of an API/downloadable option, data was scraped from: http://www.city-data.com/nbmaps/neigh-Seattle-Washington.html#N11
Data Dictionary
Feature	Type	Dataset	Description
index	int	df	numbered index of the rows
latitude	float	df	the latitude of the point
longitude	float	df	the longitude of the point
neighborhood	object	df	the neighborhood in which the point sits
.5mi 1 dollar	float	df	percentage of 1 tier price rating within .5 mile radius of point
1.0mi 1 dollar	float	df	percentage of 1 tier price rating within 1 mile radius of point
0.5mi 2 dollar	float	df	percentage of 2 tier price rating within .5 mile radius of point
1.0mi 2 dollar	float	df	percentage of 2 tier price rating within 1 mile radius of point
0.5mi 3 dollar	float	df	percentage of 3 tier price rating within .5 mile radius of point
1.0mi 3 dollar	float	df	percentage of 3 tier price rating within 1 mile radius of point
0.5mi 4 dollar	float	df	percentage of 4 tier price rating within .5 mile radius of point
1.0mi 4 dollar	float	df	percentage of 4 tier price rating within 1 mile radius of point
median income	int	df	median income of neighborhood in which the point sits
median rent	int	df	median rent cost of neighborhood in which the point sits
median home value	int	df	median home value of neighborhood in which the point sits
Unnamed: 0	int	df2	old index
Unnamed: 0.1	int	df2	old index
Unnamed: 0.1.1	float	df2	longitude of the point
Unnamed: 1	float	df2	latitude of the point
1	int	df2	count of 1 price point restaurants in the 1 mile radius of the point
2	int	df2	count of 2 price point restaurants in the 1 mile radius of the point
3	int	df2	count of 3 price point restaurants in the 1 mile radius of the point
4	int	df2	count of 4 price point restaurants in the 1 mile radius of the point
GEN_ALIAS	obj	df2	neighborhood that the point falls in
1p	float	df2	proportion of 1 price point restuarants in the 1 mile radius of the point
2p	float	df2	proportion of 2 price point restuarants in the 1 mile radius of the point
3p	float	df2	proportion of 3 price point restuarants in the 1 mile radius of the point
4p	float	df2	proportion of 4 price point restuarants in the 1 mile radius of the point
MEDIAN_GROSS_RENT	int	df2	median gross rent of the neighborhood in which the point lies
HU_VALUE_MEDIAN_DOLLARS	int	df2	median home value of the neighborhood in which the point lies
MEDIAN_HH_INC_PAST_12MO_DOLLAR	int	df2	median household income of the neighborhood in which the point lies
median_rent	obj	seattle_rent	median rent price for neighborhood
median_home_value	int	seattle_rent	median home value for neighborhood
median_income	int	seattle_rent	median income for neighborhood
1 dollar	int	seattle_rent	proportion of 1 price point restuarants in the neighborhood
2 dollar	float	seattle_rent	proportion of 2 price point restuarants in the neighborhood
3 dollar	float	seattle_rent	proportion of 3 price point restuarants in the neighborhood
4 dollar	float	seattle_rent	proportion of 4 price point restuarants in the neighborhood
