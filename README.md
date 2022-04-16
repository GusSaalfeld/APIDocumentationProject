# GetMyWeather API Documentation

## Introduction
The GetMyWeather API allows developers to embed microforecasts—i.e. a weather forecast for a specific location—into their websites. Calling the endpoint returns an HTML element. 

## Setting up the GetMyWeather API
In order to use GetMyWeather, you must first:
1. Register for an API key at https://www.getmyweather.com. API keys are free for testing and development. If you expect large traffic, you will have to pay for a commercial key. Costs depends on usage; learn more at our website.
2. The API runs off javascript. Make sure it is enabled on your browser. 

## Initializing GetWeather
````javascript
<script type="text/javascript">
var weatherForecast;
function init() {
weatherForecast =
new getWeather(document.getElementById('forecast')}
</script>
````

## Making a GetWeather request
Returns weather forecast based on location, specificity, and time. Forecast returned as a div element.
### Parameters
Parameters | Description
### Code
The following code requests the GetWeather endpoint:
````javascript
<script async defer
src="https://www.getmyweather.com/getWeather?
key=<YOUR_KEY>&
callback=init&
location=<LATITUDE>:<LONGITUDE>&
specificity=<SPECIFICITY>&
time=<TIME>">
</script>
````

### Sample Return Package
````javascript
<div class="forecast">
  <div class="temperature">78</div>
  <div class="windspeed">15</div>
  <div class="chanceRain">30</div>
  <div class="trust">80</div>
</div>
````

## Forecast return package
Parameter | Description
--------------|------------
temperature | Predicted temperature, measured in farenheit. 
windspeed | Predicted windspeed, measured in miles per hour.
chanceRain | Percent chance of rain.
trust | Represents the forecast's reliability. Ranges from 1 (low trust) to 100 (highly trustworthy). Inputting large specificity or time parameters make predictions less trustworthy. If trust is between 0 and 10, the forecast is based on the region's historical average, as live weather readings would be too inaccurate. 

## Injecting result into your HTML page
The following code will display the result package:
````javascript
<div id="forecast"></div>
````

## Error messages
If the API server cannot fulfill your request, you will get one of the following errors:

Error Message | Description
--------------|------------
Invalid Key   | Double-check that your code's API key matches the one you registered for at https://www.getmyweather.com.
Invalid parameter format | 
Parameter out of range |
Server unavailable | Check your internet connection ([click here](https://www.speedtest.net/)). Alternatively, GetMyWeather's API might be down for maintenance, which you can confirm by going to the [website](https://www.getmyweather.com). 
