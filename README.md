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

### Data Cleaning

At first when we open the [CSV file](https://github.com/ruksharahmed7/strativ/blob/main/Weather_Forecast/data/mean_apparent_temp_dhaka.csv), there are latitude, longitude info. we don't need. Also, there is a null value for 1940-01-01. We delete these unnecessary info. We mean apparent temperature for *1940-01-02 to 2023-09-07*(*30565* rows in total).

![screenshot of csv](https://github.com/ruksharahmed7/strativ/blob/main/images/1.png)

### Missing Data Analysis

The csv data being loaded in a pandas *df* variable, a quick check using *.info()* method ensures all temperature values are numeric and there are no missing values.

### Data Processing

- For training and testing, we keep the last 14 days of the data for testing.
- We normalize the temperature data using *MinMaxScaler* from *sklearn.preprocessing*.
- We use *Keras* library's TimeSeriesGenerator to generate data in sequences. The sequence length is 7 to account for weekly cycles. We can also choose 30 and 365 to account for monthly and yearly changes respectively.

### Model Building

- We build a simple model using 2 *LSTM* layers and 1 hidden *Dense* layer. We use *mean_absolute_error* as the loss function and *adam* as the optimizer. We got the idea of this model from [this code](https://github.com/bnsreenu/python_for_microscopists/blob/master/166b_COVID_forecasting_using_LSTM.py).

![model summary](https://github.com/ruksharahmed7/strativ/blob/main/images/model_summary.png)


- The model is trained for 50 epochs recording training and validation loss. From the graph below, we can see that the model's training and validation loss are decreasing and reach an approximate plateau.

![val loss](https://github.com/ruksharahmed7/strativ/blob/main/images/val_loss.png)

- From the image below, we can say the model at least fits the training data well.

![train fit](https://github.com/ruksharahmed7/strativ/blob/main/images/train_data.png)

- We can also see the model's prediction for the test data and its comparison with the actual test data. The green line is the predicted test data here.

![test data](https://github.com/ruksharahmed7/strativ/blob/main/images/test_data.png)

- The model and the scaling info is saved to be later used in FastAPI app.