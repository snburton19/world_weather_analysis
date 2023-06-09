# World Weather Analysis - Module 6 Challenge
<sub>Chapel Hill - Data Analytics Bootcamp</sub>

## Overview of Project
For Module 6, APIs were used in conjunction with Python and the Citipy, GeoViews, NumPy, and Pandas python libraries. Separated into three files, the aim in `weather_database.ipynb` was to create a database of random coordinates and find the nearest city along with its current weather. In `vacation_search.ipynb`, the temperature range was specified by the user (in this case between 20 and 65 degrees Fahrenheit), and the database was narrowed down to areas within that range. Those still in the database were tested to find the nearest hotel, which were then plotted on a map. In `vacation_itinerary.ipynb`, four cities within the same country were located, and a path was plotted to form a vacation itinerary for the proposed trip.

## Results
* Weather Database
  * Using NumPy's `random.uniform` function, 2,000 latitudes and longitudes were randomly generated and zipped together before forming a list to create sets of coordinates. Citipy used these coordinates to determine the nearest city using the [nearest_city] function. The current set of coordinates led to a list of 767 cities.
  * Using an API, the program connected to OpenWeatherMap and searched each city, gathering the maximum temperature, humidity, cloud levels, wind speed, country, and weather description. Of the cities tested, only 703 had weather data available at the time.
  * After reordering the columns and confirming their data types, the dataframe was exported to `WeatherPy_Database.csv`.

![Weather database dataframe](/images/weather_database_df.png)

* Vacation Search
  * After importing the weather database CSV, the user was prompted for the minimum and maximum temperatures they would like for their vacation. A minimum of 20 and a maximum of 65 were requested.
  * Using the temperature range, the maximum temperature of each city was tested for eligibility, and those within the limits were added to a new dataframe. Any rows with missing values were then dropped.
  * Using an API, the program connected to Geoapify and searched for the nearest hotel for each city in the created dataframe, adding any found hotel names to a new column. Those without a hotel found were dropped, and the dataframe was exported to `WeatherPy_vacation.csv`.
  * The dataframe was used to plot the hotels on a worldwide map to allow easier visualization of hotel locations.

![Vacation search plot](/images/vacation_search_plot.png)

* Vacation Itinerary
  * Using the previous step's CSV and map plot, four cities that fit the weather requirements were found and linked as vacation stops in an itinerary dataframe. Using this, a waypoints database was created to store the longitude and latitudes of the cities in the itinerary.
  * Using an API, the program connected to Geoapify and used it to calculate a route between the cities. The results were stored in a JSON file before being stored in a `legs` variable, translated to lists of longitude and latitude, and pushed to a dataframe.
  * The route was visualized using GeoViews and superimposed on top of a map of the cities, forming a complete map of the vacation itinerary.

![Vacation itinerary plot](/images/vacation_itinerary_plot.png)


## Summary
Although the premise of using randomly-generated coordinates to create a vacation itinerary is fun, there should be conditions in place. The given route created for this project is a total of more than 18 hours of driving, and does not contain a city with an international airport. A better way of conducting this experiment could be to find coordinates where the nearest city has an international airport, or taking all international airports that fit the weather requirements of the user and generating coordinates within a certain distance of those airports.
