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

We use this to get all the data from the API:

```py
from datetime import datetime
import time

import requests

#Optional:
# import matplotlib.pyplot as plt
# import numpy as np

latitude = 45.5958
longitude = -122.6092

points_url = f"https://api.weather.gov/points/{latitude},{longitude}"

response = requests.get(url=points_url)

print(response.status_code) #200 means everything worked
if response.status_code == 404:
    print("Something went wrong with requesting data. Please verify the latitude and longitude are correct before retrying.")
    print(f'\tService Error Message:\n\t\t{response.json()["detail"]}')

if response.status_code == 200:
    points_data = response.json()

forecast_urls = [
    points_data["properties"]["forecast"],
    points_data["properties"]["forecastHourly"]
]

forecast_response = [ ]

for request_url in forecast_urls:
    #Add delay to prevent requesting too quickly, otherwise Weather.gov will return invalid responses
    print(f'\tWaiting 2 seconds before sending request to avoid exceeding the request limit.')
    time.sleep(2)

    response = requests.get(url=request_url)

    if response.status_code == 200:
        print("\tRequest successful.")
        forecast_response.append(response.json())
    else:
        print("\tRequest failed.")
        print(f"Status code: {response.status_code}")
        break

hourly_data = forecast_response[1]
today = datetime.strftime(datetime.today(), "%Y-%m-%d")

print("## Today's Hourly Forecast")
print("| Time | Temperature (\N{DEGREE SIGN}F) | Chance of Rain (%)|")
print("| :--: | :---------: | :------------: |")

for period in hourly_data["properties"]["periods"]:
    period_date, period_time = period["startTime"].split("T")

    if period_date != today:
        break

    hour, minute, *extra = period_time.split(":")
    print(f"| {hour}:{minute} | {period["temperature"]} | {period["probabilityOfPrecipitation"]["value"]} |")
```

which gives this output for Portland, OR:

```
	Waiting 2 seconds before sending request to avoid exceeding the request limit.
	Request successful.
	Waiting 2 seconds before sending request to avoid exceeding the request limit.
	Request successful.
```

And here's the Markdown Table:

```markdown
### Today's Hourly Forecast
| Time | Temperature (°F) | Chance of Rain (%)|
| :--: | :---------: | :------------: |
| 11:00 | 47 | 62 |
| 12:00 | 48 | 82 |
| 13:00 | 48 | 89 |
| 14:00 | 49 | 93 |
| 15:00 | 50 | 97 |
| 16:00 | 49 | 99 |
| 17:00 | 49 | 94 |
| 18:00 | 49 | 80 |
| 19:00 | 49 | 69 |
| 20:00 | 49 | 61 |
| 21:00 | 49 | 56 |
| 22:00 | 49 | 56 |
| 23:00 | 49 | 51 |
```

### Today's Hourly Forecast

| Time | Temperature (°F) | Chance of Rain (%)|
| :--: | :---------: | :------------: |
| 11:00 | 47 | 62 |
| 12:00 | 48 | 82 |
| 13:00 | 48 | 89 |
| 14:00 | 49 | 93 |
| 15:00 | 50 | 97 |
| 16:00 | 49 | 99 |
| 17:00 | 49 | 94 |
| 18:00 | 49 | 80 |
| 19:00 | 49 | 69 |
| 20:00 | 49 | 61 |
| 21:00 | 49 | 56 |
| 22:00 | 49 | 56 |
| 23:00 | 49 | 51 |

Let's get started!

[[Tutorials/Fetching your own Forecast (IPython)/1. Getting Set Up/index|1. Getting Set Up]]
