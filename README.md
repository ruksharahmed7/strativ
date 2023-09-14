# strativ

## Weather Forecasting API

### Data Collection

**Data Source**: [open-meteo.com](https://open-meteo.com/en/docs)

It is a free(for non-commercial use) and open-source weather API that provides access to weather data from multiple national weather providers. The API offers Historical weather data dating back to 1940. For the current project, the API will be used to gather historical weather(mean apparent temperature) data for Dhaka, Bangladesh.

The API is easy to use and can be integrated into any application or website.

*Why Mean Apparent Temperature?* 

Apparent temperature, also known as "feels like" temperature, is the temperature equivalent perceived by humans, caused by the combined effects of air temperature, relative humidity, sunlight, and wind speed. The measure is commonly applied to the perceived outdoor temperature. The apparent temperature is a useful tool for understanding how the weather will feel.

The apparent temperature can be higher or lower than the actual air temperature.

- On a hot, humid day, the apparent temperature can be 10-15 degrees Fahrenheit higher than the actual air temperature.
- On a cold, windy day, the apparent temperature can be 10-15 degrees Fahrenheit lower than the actual air temperature.
- On a sunny day, the apparent temperature can be 5-10 degrees Fahrenheit higher than the actual air temperature.


The apparent temperature is an important factor to consider when planning outdoor activities. If the apparent temperature is high, it is important to take precautions to stay cool, such as drinking plenty of fluids, wearing light-colored clothing, and taking breaks in the shade. 

Given its importance regarding planning outdoor activities and its calculation involving air temperature, humidity, wind speed, and sunlight, I chose this weather component for the forecasting project.

#### Downloading Data

Before downloading the data, you have to pick which weather components to download(mean apparent temperature), the time period of the historical data(1940 Jan to 2023 Sept), and the location(Dhaka) of the data. They have a variety of options to choose from to download the data. The easiest one is just to click on the *Download CSV* button to get the data directly in a CSV format.