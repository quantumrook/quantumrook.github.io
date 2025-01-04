---
title: Overview
created: 03, Jan, 2025
modified:
  - 04, Jan, 2025
  - 03, Jan, 2025
---
## Summary

This tutorial will show you how to create a simple python notebook that fetches your forecast from [weather.gov](https://www.weather.gov).

I'm using the Interactive Python Notebook for this, since it supports both code and markdown cells: which means you can add your own comments (in markdown) to better explain what's going on in the python cells. The same thing can be achieved with a pure python `.py` file, which I'll include in the Appendix, if IPython isn't to your taste.

# Goals

We want to be able to:

- Fetch the hourly forecast for our `location` for today
- Do some quick text formatting to make the output copy-paste-able as a markdown table
- Optionally create a temperature over time plot to visually see what the day is going to look like

## Example Output

> TODO: make sure this matches the tutorial

We use this to get all the data from the API:

```py
response = None

if is_reasonable_to_request_new_forecast() == True:
    points_url = f'https://api.weather.gov/points/{LATTITUDE},{LONGITUDE}'
    print(f'Getting data for {LATTITUDE,LONGITUDE}...\n')

    response = requests.get(url=points_url)

if response is None:
    #You're most likely attempting to retrieve forecast data while the currently loaded data set is still valid
    raise StopExecution

LAST_TIME_QUERIED = datetime.now()

if (response.status_code == HTML_ERROR_CODE) == True:

    print("Something went wrong with requesting data. Please verify the lattitude and longitude are correct before retrying.")
    print(f'\tService Error Message:\n\t\t{response.json()["detail"]}')
    raise StopExecution

if (response.status_code == HTML_OK_CODE) == True:
    points_data = response.json()

    forecast_urls = {
        "extended" : points_data["properties"]["forecast"],
        "hourly" : points_data["properties"]["forecastHourly"]
    }

    raw_forecast_data = {
        "extended" : { },
        "hourly" : { }
    }

  

    for forecast_type, forecast_url in forecast_urls.items():
        #Add delay to prevent requesting too quickly, otherwise Weather.gov will return invalid responses
        time_delay = 5
        print(f'\tWaiting {time_delay} seconds before sending request to avoid exceeding the request limit.')
        time.sleep(time_delay)

        #Request the forecast
        print(f'\t\tRequesting the {forecast_type} forecast...')
        raw_forecast_data[forecast_type] = requests.get(url=forecast_url)

        if is_good_response(raw_forecast_data[forecast_type], f'Verify that the grid coordinates for the specified lattitude and longitude {LATTITUDE,LONGITUDE} were retreived correctly.'):
            print(f'\tRequest "{forecast_type}" completed.\n')
        else:
            #We exit the loop if there is an issue to avoid sending another invalid request
            raise StopExecution
```

which gives this output for Portland, OR:

```
Last time queried:            2025-01-03 05:58
No current forecast data, request is reasonable.
Getting data for (45.5978, -122.6092)...

	Waiting 5 seconds before sending request to avoid exceeding the request limit.
		Requesting the extended forecast...
		Data recieved.
	Request "extended" completed.

	Waiting 5 seconds before sending request to avoid exceeding the request limit.
		Requesting the hourly forecast...
		Data recieved.
	Request "hourly" completed.
```

And this helper function to print the output as a markdown table:

```py
def print_forecast_as_markdown():

    for dates, times in dates_and_times.items():
        print(f'# {dates}\'s Forecast by the Hour:\n')
        print(f'| Time | ({DEGREE_SIGN}{temperature_unit}): Temperature, Wind Chill | Chance of Rain (%) | Forecast Comments |')
        print(f'| ---- | ---------------------------------------------- | ------------------ | ----------------- |')
        for t in times:
            rebuilt_date_time = f'{dates} {t}'
            temperature_and_windchill = f'{hourly_data[rebuilt_date_time].temperature}'
            if (hourly_data[rebuilt_date_time].wind_chill == 0) == False:
                temperature_and_windchill += f', {hourly_data[rebuilt_date_time].wind_chill}'
            forecast_comments = hourly_data[rebuilt_date_time].forecast_short
            if (hourly_data[rebuilt_date_time].forecast_detail == "") == False:
                forecast_comments += f'<br>{hourly_data[rebuilt_date_time].forecast_detail}'
            print(f'| {t} | {temperature_and_windchill} | {hourly_data[rebuilt_date_time].percent_precipitation} | {forecast_comments} |')
        print("\n")
```

And here's the Markdown Table:

```markdown
# 2025-01-03's Forecast by the Hour:

| Time | (°F): Temperature, Wind Chill | Chance of Rain (%) | Forecast Comments |
| ---- | ---------------------------------------------- | ------------------ | ----------------- |
| 05:00 | 44, 36 | 90 | Rain |
| 06:00 | 45, 37 | 92 | Rain |
| 07:00 | 45, 38 | 93 | Rain |
| 08:00 | 45, 38 | 89 | Rain |
| 09:00 | 47, 41 | 79 | Rain |
| 10:00 | 48, 42 | 56 | Rain Showers Likely |
| 11:00 | 48, 42 | 56 | Rain Showers Likely |
| 12:00 | 51 | 56 | Rain Showers Likely |
| 13:00 | 50, 45 | 54 | Chance Rain Showers |
| 14:00 | 50, 45 | 54 | Chance Rain Showers |
| 15:00 | 50, 45 | 54 | Chance Rain Showers |
| 16:00 | 49, 44 | 34 | Chance Rain Showers |
| 17:00 | 49, 44 | 29 | Chance Rain Showers |
| 18:00 | 47, 42 | 38 | Chance Rain Showers |
| 19:00 | 48, 42 | 32 | Chance Rain Showers |
| 20:00 | 47, 42 | 39 | Chance Rain Showers |
| 21:00 | 46, 40 | 53 | Chance Rain Showers |
| 22:00 | 46, 41 | 28 | Chance Rain Showers |
| 23:00 | 46, 41 | 32 | Chance Rain Showers |
```

### 2025-01-03's Forecast by the Hour:

| Time | (°F): Temperature, Wind Chill | Chance of Rain (%) | Forecast Comments |
| ---- | ---------------------------------------------- | ------------------ | ----------------- |
| 05:00 | 44, 36 | 90 | Rain |
| 06:00 | 45, 37 | 92 | Rain |
| 07:00 | 45, 38 | 93 | Rain |
| 08:00 | 45, 38 | 89 | Rain |
| 09:00 | 47, 41 | 79 | Rain |
| 10:00 | 48, 42 | 56 | Rain Showers Likely |
| 11:00 | 48, 42 | 56 | Rain Showers Likely |
| 12:00 | 51 | 56 | Rain Showers Likely |
| 13:00 | 50, 45 | 54 | Chance Rain Showers |
| 14:00 | 50, 45 | 54 | Chance Rain Showers |
| 15:00 | 50, 45 | 54 | Chance Rain Showers |
| 16:00 | 49, 44 | 34 | Chance Rain Showers |
| 17:00 | 49, 44 | 29 | Chance Rain Showers |
| 18:00 | 47, 42 | 38 | Chance Rain Showers |
| 19:00 | 48, 42 | 32 | Chance Rain Showers |
| 20:00 | 47, 42 | 39 | Chance Rain Showers |
| 21:00 | 46, 40 | 53 | Chance Rain Showers |
| 22:00 | 46, 41 | 28 | Chance Rain Showers |
| 23:00 | 46, 41 | 32 | Chance Rain Showers |

Let's get started!

[[Tutorials/Fetching your own Forecast (IPython)/1. Getting Set Up/index|1. Getting Set Up]]
