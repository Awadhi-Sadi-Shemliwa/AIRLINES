# AIRLINES — Flight Delay Analysis

A portfolio project exploring which New York City departures are likely to leave 15 or more minutes late. The analysis covers flights scheduled from JFK, LaGuardia, and Newark in 2013, comparing schedule-time predictions with predictions using day-of-operations information.

## Project files

- [Analysis notebook](airlines_flight_delays_analysis.ipynb)
- [Interactive walkthrough](https://awadhi-sadi-shemliwa.github.io/AIRLINES/airlines_flight_delays_animation.html)
- [Project video: The List](https://awadhi-sadi-shemliwa.github.io/AIRLINES/airlines-the-list_hq.html)
- [MP4 video file](airlines-the-list_hq.mp4)
- [Original project notes](airlines_flight_delays_README.md)

## Headline result

The project reports a ROC AUC of about 0.67 using schedule-time features and 0.74 after adding day-of-operations features. Flagging the riskiest 10% of test flights catches about 29% of delays.

## Data and scope

The analysis uses the `nycflights13` package, which contains 2013 flight, weather, aircraft, and airline data. It is a historical, single-region analysis—not a live operational prediction service.

## Reproduction note

This repository includes the supplied notebook, HTML walkthrough, project video, and project notes. Reproducing the analysis may also require the project’s Python source, dependency list, and generated results and figures.
