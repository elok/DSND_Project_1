# Udacity Data Science Nanodegree - Project 1

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
* dsnd_project_1/DSND Project 1.ipynb
    * Jupyter notebook containing all the python code to read in above data and perform the analysis described below

## Summary of the results of the analysis 

The dataset was large -- I was only able to upload a subset of the data to GitHub. When iterating through the listings data, I could not simply read the whole csv file into a pandas dataframe. It was too large for memory. I found that the pandas read_csv function has an optional chunksize parameter which allows me to read the file in chunks of my choosing. This allowed me to work through the dataset in small subsets and save the results to a final dataframe.

The data was pretty clean. In terms of scrubbing and cleaning for missing fields, I didn't have much issues. For the calendar data set, I would filter out data where the date was blank. For the neighborhoods data set, I would remove entries  where the actual neighborhood is blank.

Pandas has a useful groupby function that allows you to aggregate data but when it comes to working with datetime objects it can become tricky. When I was looking for the most popular time of the time, I have a time series but I really only cared about the month. I could extract the month from the datetime into a new column and then groupby that new column but I found something better -- a class called Grouper. It allows the user to specify a groupby instruction for a target object. In my use case, I set the Grouper class to a monthly frequency and pandas will automatically extract the month and group by it.

**Popular Time of Year**

I first used the calendar data given by AirBnb but that was just listings, not actual rentals so it was pretty much useless as you can see in the following graph.

Then I decided to take a look at the listings summary data but it wasn't enough because it didn't tell you if it was rented or not. We will need a proxy data set - that's where the reviews data came in. I merged the listings summary with the reviews and that would tell me which apartments actually rented out. Grouping by the month will then tell us which month has the most rentals. The following graph shows you April is the most popular month with January a close second.

![Popular Time of Year](https://cdn-images-1.medium.com/max/800/1*7atUJt3RwTZan0E98h8U0A.png)

**Popular Neighborhood**

My next task is to see which neighborhood has the most rentals. I first read in the neighboorhoods data but it didn't contain any actual useful data so scrap that.

Then I went back to the listing summary data that was merged with the reviews data and noticed it contained all the neighborhoods. A simple group by neighborhood and count produces the following graph. Looks like Yau Tsim Mong is a very popular neighborhood.

![Popular Neighborhood](https://cdn-images-1.medium.com/max/800/1*Qw-IV4pz-w4q2piPpm8V0g.png)

**Most Expensive Listing**

Last, I wanted to know what the most expensive listing was in Hong Kong. I used the calendar data of all listings, removed any listing that didn't have any price, and sorted by price. It looked like all the most expensive listings had a price of $999. I'm not too sure how reliable the data is.

![Most Expensive Listing](https://cdn-images-1.medium.com/max/800/1*wPGdCC22hZXe8eho_hiU4A.png)
