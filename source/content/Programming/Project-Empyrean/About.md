---
title: About Project Empyrean
created: 02, Jan, 2025
modified:
  - 03, Jan, 2025
  - 02, Jan, 2025
---
## Summary

The goal of this project was to hook up to the [National Weather Service API](https://www.weather.gov/documentation/services-web-api) and fetch the `.json` files and process them into a non-technical-user friendly format. While the [weather.gov](https://www.weather.gov/) service already does an excellent job at providing this information, one of the requirements was to be able to provide this to a user (in the original design case: my mother) without requiring them to open a browser or use their phone. The goal was to create a service that would automatically format a markdown file and be ready for print (or otherwise reference) every morning.

# Versions

## v0.1

This all started off in an IPython notebook file, whose contents will be uploaded in the near future. The main personal goal was to hook up to the API and successfully download the information, as I had never attempted this before.

## v0.2-v0.3

These versions were mainly adjustments and improvements to the notebook file like plotting the data with [matplotlib](https://matplotlib.org/) and generating various forms of unformatted/formatted text.

## v0.4

After discovering the built-in gui library of `tkinter`, and realizing how expensive printing daily forecasts could become, the project shifted towards creating a desktop app to facilitate tracking multiple locations' forecast.

## v0.5

The current working version supports fetching and displaying forecasts and adding new locations during runtime. The big change was implementing and extending the [Tkinter Modern Themes](https://github.com/RobertJN64/TKinterModernThemes) package to give a little bit of life to the UI.

The main draw here was how TKMT tweaks the Treeview widget and simplifies displaying the data, if properly formatted and was crucial to getting a good UX for viewing a location's extended forecast.