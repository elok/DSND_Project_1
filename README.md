Udacity Data Science Nanodegree - Project 1

## Motivation
The AirBnb datasets are very interesting. For this project, I chose to work with the Hong Kong data. It's a large data set and there were some challenges I had to overcome.

## Libraries
* Pandas library was used strictly to manipulate the data.
* matplotlib was used to plot the bar charts.
* datetime was used to parse dates.

## Files
* data/listings_summary.csv
    * Summary information and metrics for listings in Hong Kong (good for visualisations).
* data/neighbourhoods.csv
    * Neighbourhood list for geo filter. Sourced from city or open source GIS files.
* data/calendar.csv
    * Detailed Calendar Data for listings in Hong Kong
    * This file was not uploaded due to size constraint
* data/listings.csv
    * Detailed Listings data for Hong Kong
    * This file was not uploaded due to size constraint
* data/reviews.csv
    * Detailed Review Data for listings in Hong Kong
    * This file was not uploaded due to size constraint

## Summary of the results of the analysis 

The dataset was large -- I was only able to upload a subset of the data to GitHub. When iterating through the listings data, I could not simply read the whole csv file into a pandas dataframe. It was too large for memory. I found that the pandas read_csv function has an optional chunksize parameter which allows me to read the file in chunks of my choosing. This allowed me to work through the dataset in small subsets and save the results to a final dataframe.

Pandas has a useful groupby function that allows you to aggregate data but when it comes to working with datetime objects it can become tricky. When I was looking for the most popular time of the time, I have a time series but I really only cared about the month. I could extract the month from the datetime into a new column and then groupby that new column but I found something better -- a class called Grouper. It allows the user to specify a groupby instruction for a target object. In my use case, I set the Grouper class to a monthly frequency and pandas will automatically extract the month and group by it.
