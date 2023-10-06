### Will a Customer Accept the Coupon?

**Context**

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

**Overview**

The goal of this project is to use what you know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

**Data**

This data is from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50). 



### Data Description
Keep in mind that these values mentioned below are average values.

The attributes of this data set include:
1. User attributes
    -  Gender: male, female
    -  Age: below 21, 21 to 25, 26 to 30, etc.
    -  Marital Status: single, married partner, unmarried partner, or widowed
    -  Number of children: 0, 1, or more than 1
    -  Education: high school, bachelors degree, associates degree, or graduate degree
    -  Occupation: architecture & engineering, business & financial, etc.
    -  Annual income: less than \\$12500, \\$12500 - \\$24999, \\$25000 - \\$37499, etc.
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she buys takeaway food: 0, less than 1, 1 to 3, 4 to 8 or greater
    than 8
    -  Number of times that he/she goes to a coffee house: 0, less than 1, 1 to 3, 4 to 8 or
    greater than 8
    -  Number of times that he/she eats at a restaurant with average expense less than \\$20 per
    person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    

2. Contextual attributes
    - Driving destination: home, work, or no urgent destination
    - Location of user, coupon and destination: we provide a map to show the geographical
    location of the user, destination, and the venue, and we mark the distance between each
    two places with time of driving. The user can see whether the venue is in the same
    direction as the destination.
    - Weather: sunny, rainy, or snowy
    - Temperature: 30F, 55F, or 80F
    - Time: 10AM, 2PM, or 6PM
    - Passenger: alone, partner, kid(s), or friend(s)


3. Coupon attributes
    - time before it expires: 2 hours or one day

### Data Exploration and Analysis
This is an interesting data set showcasing different kind of coupons offered to drivers with different lifestyles. 
Started my analysis looking at the data set information first. Imported all the required libraries and used read_csv function in pandas to read the dataset into a dataframe. Looked for any missing data using Python isnull function.

<img width="240" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/846ec3a6-2f65-4616-9ec8-4ced04a4d318">



### Data Cleansing

1. Created a copy of the dataset and called it data_clean. There are 12684 rows of data in the original dataframe.

2. Columns Bar, CoffeeHouse, CarryAway, RestaurantLessthan20, Restaurant20to50 help us understand if a driver choses a coupon or not. If there isn't a value in any of these columns, we cannot effectively predict the driver's behavior. So, queried for the rows where information is missing in all these columns. There are a total of 42 rows with all these column values missing. Deleted the 42 rows from the dataset. Now there are 12642 rows of data.

3. Dropped the column 'car' as 12576 rows out of 12642 rows have null values

4. Cleaned up the data in 'age' column. Updated value '50plus' to 50 and 'below21' to 20. And converted integer column to a numeric column


<img width="247" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/019f34a1-a9a7-4230-b574-833da74420c2">

 
## Data Exploration Begins

Now with the clean dataset, started exploring the data patterns, behavior etc. to understand the acceptance rate of the coupons.
To begin with, looked at what proportion of the total observations chose to accept the coupon. It's a total of 56.61%

### Plotted a bar plot to see visualize the coupon column.

<img width="571" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/e25e7804-33b6-4ec0-a860-ff85e8f5ab8a">

### Also, plotted a distribution plot to observe the number of acceptances and rejectances for each coupon category 

<img width="563" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/73cc8387-2365-4cf4-b8d7-a3ea58358e9b">


### Plotted a histogram to visualize the temperature column

<img width="464" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/8acf9a24-1813-4b36-8c5b-883024dd4a1e">


### Created another histogram analyzing the coupon acceptance behavior with the temperature. Set bins = 5 to showcase the data a bit closer in the distribution

<img width="533" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/1b437d68-17e2-499f-965d-62281ce48e0c">


### Bar Coupons Investigation

To begin with created a new dataframe that contains only the bar coupon information using query function.
Calculated the proportion of the bar coupons that were accepted. It's observed that 40.94% of the bar coupons issued are accepted. Now started analyzing how various factord determine/impact the bar coupon acceptance rate.


### Bar coupon acceptance rate comparison based on drivers' bar visit frequency

1. Looked at various bar visit frequencies in the data
2. Created a dataframe subset with the information where the Bar coupon is accepted and grouped the data by Bar visit frequency
3. Visualized using a piechart the Percentage of total accepted bar coupons by drivers with varied Bar visit frequency
4. Calculated the total number of acceptances by drivers who visited bar 3 times or less in last two months
5. Calculated the total number of acceptances by drivers who visited bar 4 times or more in last two months
6. Compared the two values

<img width="588" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/87c9bcc3-7d7d-48d2-ae3c-3976b398fc6c">


### Observation: It's observed that drivers who visit bar 3 times or fewer are 3 times higher probable to accept the Bar coupons than those who visit the bar 4 times or more


### Bar coupon acceptance rate comparison based on drivers' over 25 years of age and bar visit frequency and 

1. Looked at various age groups in the dataset
2. Plotted a violin chart to visualize the acceptance by varied age groups with different bar visit frequencies
3. Visualized using a piechart the Percentage of total accepted bar coupons by drivers with varied Bar visit frequency
4. Using query and shape functions calculated the individual acceptance ratios for the drivers of age group 25 or 
6. Compared the two values

<img width="579" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/104c8b2b-aae3-4e4f-8b0c-408c47ee59c6">
<img width="562" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/7b39ffe4-e8af-4450-aed5-e27c4adef3a5">


### Observation: 

It's observed that the acceptance rate of drivers who visit bar more than once a month and over 25 years of age is 3 times more than all others. So, there is no difference of acceptance rate from the above scenario

### Scenario: 
Wanted to compare the acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry, had to run multiple queries to arrive at the dataset required to calculate the acceptance rate.
    1. Queried for drivers who visit bar more than once a month. 
    2. Then queried to know how many drivers are taking passangers who are not kids
    3. Queried further to get a subset of drivers info whose occupation is not Farming Fishing and Forestry
    4. Then queried for those who accepted the coupon
Then calculated the acceptance rate between those who accepted and rest others

Used countplot function to plot and know various passangers
<img width="491" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/e1e8dd40-0760-4835-bab2-d0249135029f">


Used countplot to know various occupations of drivers

<img width="472" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/9b376cb7-71ac-4aee-847d-86294902536d">

### Observation: 
The acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry and others is  0.7132486388384754



### Scenario:
Further analysis is done to compare the acceptance rates between those drivers who:

- go to bars more than once a month, had passengers that were not a kid, and were not widowed *OR*
- go to bars more than once a month and are under the age of 30 *OR*
- go to cheap restaurants more than 4 times a month and income is less than 50K. 

### Observation -
Acceptance rate between the above drivers and the overall drivers for whom bar coupns issued is  1.2883211678832116. 


### Overall Observations - 

It's observed that drivers who visit bar 3 times or fewer are 3 times higher probable to accept the Bar coupons than those who visit the bar 4 times or more

It's observed that the acceptance rate of drivers who visit bar more than once a month and over 25 years of age is 3 times more than all others

The acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry is  0.7132486388384754


###  Hypothesis

Based on all the above observations, drivers who goto bar more than once a month, if they have passengers who are not kids, and are 21 or below age with less income have accepted the coupon fewer times than the drivers who go to a bar more than once a month and are over the age of 25

************************

### Recommendations and Next Steps:

With all the exploration and observations made so far, I would recommend to increase the issue of coupons to drivers who go to bar 3 or fewer times and are above 25 years of age. 

As a next step, I would like to further analyze the coupon acceptance behavior based on temperature. But there are only 3 categories of temperature data available 30,55,80. These are wide spread across. It will not help to predict the behavior accurately. So, I would like gather more data containing information with close temperatures

### Chosing to explore the Coffee House Coupons

Created a dataframe with drivers who received coffee house coupons and started exploration

Created a countplot to know frequency of visits of various drivers

<img width="420" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/f32dd9f7-ee97-4131-b3be-c134b2e20ba3">

Created a visualization using violin plot to see the distribution of drivers by the frequency of visits to the CoffeeHouse, and also visualize the groups who have higher coupon acceptances

<img width="561" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/faa604e9-8fbd-4992-bd5f-738565649097">

### CoffeHouse coupon acceptance rate comparison based on drivers' coffee house visit frequency

1. Created a dataframe subset with the information where the Coffee house coupon is accepted
3. Visualized using a piechart the Percentage of total accepted coffeehouse coupons by drivers with varied visit frequencies
4. Calculated the total number of acceptances by drivers who visited Coffeehouse 3 times or less in last two months
5. Calculated the total number of acceptances by drivers who visited Coffeehouse 4 times or more in last two months
6. Compared the two values

#### Observation: It's observed that drivers who visited Coffee House 3 times or fewer are 2 times higher probable to accept the Coffehouse coupons than those who visit the coffee house 4 times or more

Created a piechart to visualize percentage of total accepted Coffehouse coupons by drivers with varied coffehouse visit frequency


The acceptance rate between those who went to a CoffeeHouse 3 or fewer times a month to those who went more is 2.008417508417508

<img width="503" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/e62392c4-0b9b-4b92-9362-592ad00e929b">

#### Below visualization shows that higher the temperature, higher is the number of Coffee House coupons issued and also accepted

Created a visualization using displot function from Seaborn library to observe the acceptances of Coffeehouse coupons issued during different temperatures

<img width="406" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/0a497251-bbc4-462b-961e-d7be22ccb376">


#### Below pie chart shows that around 64% of the accepted CoffeeHouse coupons are by drivers driving in 80 degrees temperature

<img width="419" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/9c5a3e0a-ed69-459d-b885-9869c6493085">


#### Exploring acceptance ratios of CoffeeHouse coupons by the drivers that are -

1.Single/widowed/divorced 

2.Single/widowed/divorced driving in high temperatures

3a.Single/widowed/divorced, driving in higher temperatures and who visit coffee house less than 4 times a month

3b.Single/widowed/divorced, driving in higher temperatures and who visit coffee house more than 4 times a month


#### Observation: Below visualization shows that widowed drivers go once or less to the CoffeHouse in a month

<img width="604" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/ea69efc0-2fc4-404d-ab90-cfee0cfdc978">

<img width="597" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/ec37cfa3-f492-4193-9491-ce19dddee6f8">

#### Creating a new column CH and assigning numeric values to it based on the values in the CoffeeHouse column
#### Segregating the dataset in to three pieces 
 - drivers who have never been to CoffeeHouse get a value of 0 in CH column
 - drivers who have been to CoffeeHouse less than 4 times a month, get a value of 2 in CH column
 - drivers who have been to CoffeeHouse 4 or more times a month, get a value of 6 in CH column


#### Observation - Below barplot shows that the acceptance of CoffeeHouse coupons is maximum at 7 am when the venue is in the same direction as the driver's destination

<img width="417" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/a1cea04c-e422-4a57-a0aa-5b8773116310">


#### Observation: Below visualization clearly shows drivers are driving to an non-urgent place during the mornings betwen 10am and 2 pm.

<img width="525" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/d58d0517-b804-4b60-9c4c-c14103a60587">


#### Observation - From the above and below visualizations, it's clear that drivers when driving to a non-urgent place and in the morning time tend to accept CoffeeHouse coupons
Creating a new numeric column time_numeric and assigning time values as in 24 hour clock time_numeric column is assigned 7 for 7AM, 10 for 10AM, 14 for 2PM, 18 for 6PM and 22 for 10PM
Below plot shows the acceptance rate of CoffeeHouse coupons is greater when they are issued for the drivers 
driving between 10 am and 2 pm


<img width="394" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/72c157b0-f9f4-4953-bd98-67c7de0adaca">




Below code shows how the coupons' acceptance rate or % varies when the venue is in the same or opposite direction of the destination

Only 49.15% of the drivers accepted the Coffeehouse coupons when the venue is in the opposite direction of their destination

While 53.07% of the drivers accepted the Coffeehouse coupons when their venue is in the same direction as their destination

#### Above calculation shows that acceptance rate of the Coffeehouse coupons is higher when the venue is in the same direction as their destination

### Exploration with Time data: 

Below, we will explore and understand what's the best time for offering coupons so that the acceptance rate is high
#### Grouped the rows in the dataset using Groupby function and applied Sum() on the numeric values

<img width="413" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/c281fa89-52a1-4dc7-b647-82379468b4a1">



#### Observation:

Using python Groupby function, showcased that number of acceptances is quite high at 10 am and then at 6 pm irrespective of the direction in which the driver is driving.

Also plotted the same using a pie chart that as well confirms 10 am is the best time to offer a coupon to be accepted and the second best is 6 pm. 

<img width="457" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/0aa040fb-687f-473b-bf31-e7594503d500">


### Exploration with Temperature data



### Observation:

Grouping the drivers who are driving at different temperatures shows that when the temperature is 80, more number of driveres accepted the coffeehouse coupons. This makes sense as they might want to relax for few min in shade as it's pretty hot outside. 

Both the plotting in piechart and python grouping function show case the same result.

So, it's good to issue more CoffeeHouse coupons when it's hot.

<img width="441" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/b4158cb7-13f6-4c9d-9c8e-f279859a76de">


### Exploration with Passanger data

### Observation 

Below countplot shows that when the passangers are either Friends or kids or partners, the coupon acceptance rate is higher than when they are alone.

<img width="427" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/92092141-d0e8-495a-99d9-9be65b9df492">

<img width="488" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/ddf457cc-9609-4447-8ac1-d67e5057d76c">

#### Alone Passengers acceptance analysis when they are driving in hot temperatures

Used a countplot to see at what time of the day alone driving drivers accept the coupons when temperature is 80. 
This plot also clearly shows acceptance rate is highest at 10 am when compared to other times in the day.
It makes sense as many people would like to have a coffee early in the day to be active and get things done faster.


<img width="563" alt="Capture" src="https://github.com/jyothiknj/Test/assets/35855780/5696ada3-d823-451d-8b6f-88f274e60182">


### Recommendations

With all the observations made while analyzing the data for CoffeeHouse coupons, I highly recommend cutting down the issue of CoffeeHouse Coupons late in the night and increase the issue of coupons at all times before 2 pm. Also, the acceptance rate will be higher if the coupons are issued to the drivers when they are driving to no urgent destinations.
These two poins will highly increase the overall acceptance rate of the CoffeeHouse coupons.

### Next Steps

Most of the CoffeeHouse coupons are issued to drivers driving to a destination in an opposite direction of the venue. I would like to collect more data where CoffeeHouse coupons are issued to the driving driving in the same direction. This will definitely impact the acceptance rate of the coupons


