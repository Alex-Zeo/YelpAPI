# Data mining YelpAPI
Google Places is expensive! In the last project, the total cost was ~$2,000 in a week of testing and building.
Initially, it was assumed that place counts were free as stated in the API, but applying any filters (ie Restaurants) to the raw data resulted in unforeseen costs that weren't initially accounted for.

Free data mining options are available on Yelp & the pagination and rate limits are much friendlier for this project.
The limitations are somewhat different on Yelp API, where it's vital to track daily usage per API key instead.

V1 Stadium coordinates generate a 9-tile grid for data pulls where the Stadium is the center point.
This data will be used to compare & validate Census restaurant data

![image](https://github.com/Alex-Zeo/YelpAPI/assets/6181715/16d74044-fa5f-4c95-bb32-c66876031e10)

