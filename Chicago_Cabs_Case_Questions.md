
----------
# Cab Consulting
_______

## Author Information
Jessen Hobson, Ph.D. </br>
Associate Professor of Accountancy </br> 
R.C. Evans Data Analytics Fellow </br>
University of Illinois at Urbana-Champaign

## Learning Objectives
* Retrieve data via API
* Store and access data via Pandas and CSV
* Clean data in Pandas
* Descriptive analytics: 
    * grouping data
    * visualization via box plots, scatter plots, histograms, and heat maps
* Predictive analytics using regression
* Story telling from a business analytics point of view

## Case Background
Yellow Cab Chicago has hired your small accounting and consulting firm to help them shave costs and increase revenues. Like many traditional cab companies, Yellow Cab is feeling significant pressure from ride-hailing companies like Lyft and Uber. You are a recent graduate and new to the firm and are excited to learn you will have role in this engagement. Your excitement quickly turns to apprehension, however, when the partner pulls you into her office.

"Thanks for meeting with me," she says. "This new engagement is really important to the firm, and I am happy you are on board. I heard that you have some data analytics skills. I would like you to see if you there is any data out there that might help us learn more about the situation Yellow Cab is in and if there are any interesting revenue opportunities out there that we have not thought of. You know, what is Yellow cab facing and were should they be focusing their efforts?"

You are a little overwhelmed, but after a quick internet search you find out that the city of Chicago puts a bunch of data out there about cab trips. This is just what you need!
 
-------

## Load Relevant Packages and Dependencies

-------

Set up the environment, load packages and dependencies.


```python
# database tool
import pandas as pd 
import numpy as np 
# for use with API to get data
from sodapy import Socrata 
# to show graphs inline
%matplotlib inline 
# disable an unneeded warning
pd.options.mode.chained_assignment = None  # default='warn'
```

To set home directory. Replace `C:\...` with your own home directory (where you want your files to be stored)


```python
%cd C:\Users\jlhobson\Documents\Data Analytics General\Cases
```

## Load Data and Save Data
Load through data.cityofchicago.org using their API. An application token was not needed for 2,000,000 observations. E.g., https://digital.cityofchicago.org/index.php/chicago-taxi-data-released/

------

Retrieve Data


```python
# Unauthenticated client only works with public data sets. Note 'None'
# in place of application token, and no username or password:
client = Socrata("data.cityofchicago.org", None)

# returned as JSON from API / converted to Python list of
# dictionaries by sodapy.
# to get a subset of 2,000,000
results = client.get("wrvz-psew", limit=2000000)

# Convert to pandas DataFrame
df = pd.DataFrame.from_records(results)
```

Save data as a CSV file so that you can save and return to your work without having to use an application token in the API.


```python
# ORIGINAL FILE
file = 'cab_data.csv' 
```


```python
# Export file for later use
df.to_csv(file, index=False)
```


```python
# Load data for use
df = pd.read_csv(file)
```

## 0. Look at the Data
--------

Question: take a look at 10 random rows of the DataFrame to get a sense of what you have downloaded.

## 1. Clean Data
--------

### 1.1 Eliminate bad data

Question:

#### 1.1.1 Delete trips with no cost, since these are mistakes or uninteresting cases

Question:

#### 1.1.2 Delete trips with NaN mileage and NaN seconds.

Question:

#### 1.1.2 Delete trips with no mileage but starting and stopping in a different community, since these are likely mistakes.
#### 1.1.3 Delete trips with no seconds but starting and stopping in a different community, since these are likely mistakes.

### 1.2 Fix datetime

Question:

#### 1.2.1 Create a new column that converts `trip_start_timestamp` and `trip_end_timestamp` to a datetime object

Questions;

#### 1.2.2 Create four new columns - for the year, month, day, and hour, respectively (use the start of the trip, since that is something the taxi driver can control)

### 1.3 Deal with outliers

Question:

The main focus in outliers is getting `trip_total` right, since you are trying to understand how Yellow Cab can make money. `trip_seconds` and `trip_duration` also have outliers, which you should look at, but we will focus on `trip_total` and `tips`.

First, draw box plots of those four variables to see how significant the outlier situation is and then describe what you see in a few sentences.

Your description of what you see: </br>

Question: <br>
Next, draw two scatter plots to see how cost and miles and cost and seconds relate to each other.

Question: <br>
These plots indicate that most very high cost trips are probably errors or uninteresting since they have took very few seconds and went very few miles. For example, it does not seem plausible that a $8,000 cab fare took went about 0 miles and took about 0 seconds. 

Let's correct this by eliminating rows with unusually high dollars per second (i.e., trip with unreasonably low seconds but high payment).

Question: <br>
Next, rerun the two scatterplots from above to visually inspect whether this worked. 

Your description of whether this worked: <br>


## 2. Descriptive Analytics - explore the data
----------

### 2.1 Histograms

Question: Next, explore the data using descriptive analytics. First graph in a bar graph / histogram five analyses--the number of trips by year, by month, by day of the month, by day of the week, and by hour of the day. 

### 2.2 Using total cost and tips as a dependent measure

#### 2.2.1 Costs and tips by pick-up community area

Question: Graph on a histogram the top 20 community areas to pick up in if you want to maximize total cost and tips. Thus, two graphs are required. Can you draw any useful conclusions from this analysis?

Can you draw any useful conclusions from this analysis?: </br>


#### 2.2.2 Costs and tips by hour of the day and day of week

Question: Graph on a histogram the mean cost of the trip and tips by hour of the day and by day of the week. Thus, four graphs are required. Can you draw any useful conclusions from this analysis?

Can you draw any useful conclusions from this analysis?: </br>


#### 2.2.3 Costs and tips by means of payment

Question: Graph on a histogram mean total cost and tips by type of payment. Thus, two graphs are required. Can you draw any useful conclusions from this analysis?

Can you draw any useful conclusions from this analysis?: </br>


### 2.3 Visualization

#### 2.3.1 Visualizing tips and total bill by location

Question: Next, explore some of the geographical characteristics of the data. Graph the data based upon latitude and longitude. Use the pick-up location, since this is something the driver can control. Use built in features of a Python package (e.g., pyplot from matplotlib) to also see the total bill and the tip amount on this graph. (Hint: outliers will skew the graph, look at trips under $50.) What conclusions can be drawn from this analysis?

What conclusions can be drawn from this analysis? </br>


## 3. Predictive Analytics - Regression
----------

### 3.1 Two Basic Regressions

Question: Next, use regression to examine the factors that are predictive of the total bill and tips. What does this analysis tell you?

What does this analysis tell you? </br>


### 3.2 Tell a story

Question: Finally, use descriptive and predictive analytics, as has been modeled above, to make recommendations to your supervisor for the Yellow Cab Company client.

#### Recommendation 1: 
