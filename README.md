# GetMyWeather API Documentation

## Introduction
The GetMyWeather API allows developers to embed microforecasts—i.e. a weather forecast for a specific location—into their websites. Calling the endpoint returns an HTML element. Developers can specify location, region size, and time. 

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
Returns weather forecast based on location, specificity (i.e. region size), and time. The forecast is returned as a div element. Latitude and longitude determine's the forecast's location. Specificity determines the size of the forecasted region—it represents the radius of a circle in meters, extending out from the original location. Time, measured in hours, determines how far into the future you wish to forecast. The larger the specifity or time parameters, the less accurate the forecast will be.   
### Example
![Visualizing GetWeather](example.png)

### Parameters
Parameters | Format
----------|-------------
Latitude | ISO 6709 (e.g. 50°40′46.461″N 95°48′26.533″W 123.45m)
Longitude |ISO 6709 (e.g. 50°03′46.461″S 125°48′26.533″E 978.90m)
Specificity | int
Time | double

### Using GetWeather Endpoint
Add the following code to request the GetWeather endpoint:
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

## Forecast return package
Parameter | Description
--------------|------------
temperature | Predicted in farenheit. 
windspeed | Predicted in miles per hour. 
chanceRain | Percent chance of rain. 
trust | The forecast's accuracy. Ranges from 1 (low trust) to 100 (highly trustworthy). Inputting large specificity or time parameters make predictions less trustworthy. If trust is between 0 and 10, the forecast is based on the region's historical average, as live weather readings would be too inaccurate. 

### Example of returned forecast package 
````javascript
<div class="forecast">
  <div class="temperature">78</div>
  <div class="windspeed">15</div>
  <div class="chanceRain">30</div>
  <div class="trust">80</div>
</div>
````

## Injecting result into your HTML page
The following code will display the result package:
````javascript
<div id="forecast"></div>
````

## Error messages
If the API server cannot fulfill your request, you will get one of the following errors:

Error Message | Debug
--------------|------------
Invalid Key   | Check that your code's API key matches the one you registered for at https://www.getmyweather.com.
Invalid parameter format | Check your input parameters conform to the appropriate format.
Parameter out of range | Check that your specifity parameter is no smaller than 10 meters, and no larger than 100,000 meters.
Server unavailable | Check your internet connection ([click here](https://www.speedtest.net/)). Alternatively, GetMyWeather's API might be down for maintenance, which you can confirm by going to the [website](https://www.getmyweather.com). 
