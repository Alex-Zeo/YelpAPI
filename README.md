# Data mining YelpAPI
Google Places is expensive! In the last project, the total cost was ~$2,000 in a week of testing and building.
Initially, it was assumed that place counts were free as stated in the API, but applying any filters (ie Restaurants) to the raw data resulted in unforeseen costs that weren't initially accounted for.

Free data mining options are available on Yelp & the pagination and rate limits are much friendlier for this project.
The limitations are somewhat different on Yelp API, where it's vital to track daily usage per API key instead.

**Module 1: API Keys** 
api_key: This is your Yelp API key, which is required for authentication when making requests to the Yelp API. If you have more than one you can list them here. 

![image](https://github.com/Alex-Zeo/YelpAPI/assets/6181715/d819013f-f31f-4224-9d91-258d02d19485)


**Module 2: Get Coordinates and Visually confirm results**
This script works in two steps. First, it fetches the geographical coordinates of a list of stadiums using the Yelp API and visualizes these locations on a map using the Folium library.
This map is then used to verify that the stadium coordinates generated by Yelp match our expected results:
![image](https://github.com/Alex-Zeo/YelpAPI/assets/6181715/fa8038cb-162b-423e-9541-d50c1f97e0d8)

![image](https://github.com/Alex-Zeo/YelpAPI/assets/6181715/092113cb-c195-4f33-bac9-b1b4e134b230)


**Module 3: Get Business details in the given Search radius**
This script fetches data about businesses in a given category from the Yelp API for the given list of search coordinates. In our case, this is 11 World Cup stadiums, and saves the information to Excel files.
It uses Python libraries: requests for making HTTP requests to the Yelp API and pandas for data manipulation and exporting the data to Excel format. Here's a breakdown of its components and functionality:

Initialization
The script expects two variables to be initialized beforehand:
coordinates: A dictionary with city names as keys and tuples of latitude and longitude as values. This variable defines the locations for which data will be fetched.
api_keys: A list of Yelp API keys. Multiple keys are provided to circumvent rate limits imposed by the Yelp API on individual keys.

![image](https://github.com/Alex-Zeo/YelpAPI/assets/6181715/d1364e82-12fb-42d5-8e43-20ee123a7101)


Categories Selection
categories: A string specifying the categories of businesses to fetch data for, with restaurants,food being the default value. This can be dynamically set to include different or additional categories.
The full list of available Yelp business categories to search: https://docs.developer.yelp.com/docs/resources-categories

Function: fetch_data
This function attempts to fetch business data from the Yelp API for a given latitude and longitude, with optional pagination support through the offset parameter.
It iterates through the provided api_keys, making a request with each until a successful response is received or all keys have been exhausted.

The request URL includes parameters for latitude, longitude, radius (set to 10,000 meters), categories, sorting by distance, limit (set to 50, the maximum allowed per request), and offset for pagination.
If the API returns a 429 status code (rate limited), the function tries the next API key.
On success, it returns the JSON response; if all keys fail, it returns None.

Data Collection Loop
The script iterates over each city in the coordinates dictionary.
It maintains a dictionary unique_businesses to store data about businesses, ensuring uniqueness by using business IDs as keys.
Using a while loop, it fetches data in batches of 50 (the maximum allowed) until no more data is available or an error occurs.
For each business fetched, it checks for uniqueness, extracts relevant information (e.g., name, categories, address, rating, etc.), and adds it to unique_businesses.
After fetching all data for a city, it converts unique_businesses into a pandas DataFrame.
Saving Data
The script dynamically generates an Excel file name based on the city and categories, then saves the DataFrame to this Excel file.
![image](https://github.com/Alex-Zeo/YelpAPI/assets/6181715/c55e2786-3aaa-4c41-a0e6-35c68cf4effd)

This process repeats for each city in coordinates, resulting in a separate Excel file for each city containing unique businesses related to the specified categories.
Error Handling and Notifications
The script prints messages to the console for various events, such as when moving to the next city, when an API key is rate-limited, when a unique business is added, and when data is saved to an Excel file.
This approach allows for efficiently collecting and organizing data on restaurants and food businesses from multiple cities using the Yelp API, making use of multiple API keys to handle rate limits and ensuring data uniqueness.
