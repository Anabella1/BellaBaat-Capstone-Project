# BellaBeat Google Data Analytics Capstone Projec

## Table of Contents
- [About the Project](#about-the-project)
- [Ask Phase](#ask-phase)
- [Prepare Phase](#prepare-phase)
- [Limitations](#limitations)
- [Process Phase](#process-phase)
- [Analyse and Share Phase](#analyse-and-share-phase)
- [Act Phase](#act-phase)
- [Key Insights](#key-insights)
- [Recommendations](#recommendation)



## About the Project

This is a project for the Google Data Analytics Capstone Project, The Bellabeat dataset is download from Kaggle. I will be using the 6 stages (ASK, PREPARE, PROCESS, ANALYSE, SHARE and ACT ) of Data Analysis as learnt in the course. This project is intended to identify trends, make data driven decisions and give insights.

## Ask Phase
Business Task:
Identify trends and ascertain how consumers use the app and apply the insights gotten into Bellabeat Marketing Strategy

- What are some trends in smart device usage?
- How could these trends apply to Bellabeat customers?
- How could these trends help influence Bellabeat marketing strategy?

## Prepare Phase

- Source of Data
FitBit Fitness Tracker Data and stored in 11 CSV files. It is made available by Mobius. It is an open-source data. You can copy, modify, distribute and perform the work, even for commercial purposes, all without asking permission. The data is provided in a long format. Each distinct type of activity is recorded in a separate CSV file. Every user has a unique ID and different rows tracked by day and time.

### Limitations
We are not sure if the sample is representative of the population as a whole, the data was collected about 8 years ago in 2016, hence it may be somewhat outdated, the datasets are not original. They were collected by Amazon Mechanical Turk. he dataset does not contain any demographic information about the users.


## Process Phase
I choose to use R and EXcel for my analysis, R was chosen due to the amount of data I will be working with, some of the tables contain over 24,000 rows each,I also used R for its ability to create data visualization with ease. Excel was chosen because it is user friendly and easy to manipulate data on it.

 1. Tools used for Analysis
- Excel
  - Data Cleaning
  - Visualization
- R     - Data Cleaning
  - Visualization
  - Data Exploration
  - Data Analysis
  - Creating the Report

2. Data Cleaning
- Loading R package and setting up the enviroment - library(tidyverse)
- improting dataset with read.csv
-  using head(), tail(), and colnames() function to preview the data and return column names of each dataset.
-   Using n_unique() and nrows() to check the number of participant in the dataset and the number of rows in the dataset respectively.
-   Data cleaning and formating

  
3. Data Analysis
This sections includes the codes I wrote, I used R programming language and Excel for my analysis.


```R
library(tidyverse)
library(skimr)
library(janitor)
library(lubridate)
library(dplyr)
```

- Loading CSV 

```{r}
activity_daily <- read.csv("ActivityDaily.csv")
hourly_steps <- read.csv("hourlySteps_merged.csv")
hourly_calories <- read.csv("hourlyCalories_merged.csv")
hourly_intensities <- read.csv("hourlyIntensities_merged.csv")
```
![loading dataset](https://github.com/Anabella1/Capstone-Project/assets/119600515/83a0b555-2b15-4f0f-a65b-c592901e0892)



-  Previewing the dataset using head() to view the first 6 rows and tail() to view the last 6 rows
```{r}
head(activity_daily)
head(hourly_steps)
head(hourly_calories)
head(hourly_intensities)
tail(activity_daily)
tail(hourly_steps)
tail(hourly_calories)
tail(hourly_intensities)
```
![head and tail preview](https://github.com/Anabella1/Capstone-Project/assets/119600515/cbd9cd9c-b260-4929-b1d0-a72264c29f9f)



-  To return the name of the columnns on each data fram i will use colnames() function

```{r}
colnames(activity_daily)
colnames(hourly_steps)
colnames(hourly_calories)
colnames(hourly_intensities)
```
![columnnames](https://github.com/Anabella1/Capstone-Project/assets/119600515/4a0b60e6-75a4-416d-ab0d-0e85d81ae820)



-  To check for the number of participant in each datset using n_unique() function

```{r}
n_unique(activity_daily$Id)
n_unique(hourly_steps$Id)
n_unique(hourly_calories$Id)
n_unique(hourly_intensities$Id)

```

![unique ids](https://github.com/Anabella1/Capstone-Project/assets/119600515/ecf3db23-a323-4b67-90bf-10b9e6826a2c)



-  I will be using nrow() to check the number of observation each dataframe has

```{r}
nrow(activity_daily)
nrow(hourly_steps)
nrow(hourly_calories)
nrow(hourly_intensities)
```
![nrows](https://github.com/Anabella1/Capstone-Project/assets/119600515/d5c8d46a-23d6-48da-afa9-04144ccc634a)



## Analyse and Share Phase

-  Analysing quick summary statistics of the data frame to determine if they can help me in the Marketing Strategy of Bellabeat.

```{r}
activity_daily %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes) %>%
  summary()

```

![daily_activity Summary](https://github.com/Anabella1/Capstone-Project/assets/119600515/745374d7-8582-4483-b898-3615a2243be1)

### Explaining the summary
- The average steps taken is 6547 the recommended amount of steps to be taking per day is 10,000 steps, therefore, more steps should be taken for a healthy living.
- The average sedentary/inactive minute is 995.3(~16 hours) more steps should be taken and inactive minutes should be increased.
- 91 calories is burnt per hour.


##### Relationship between Steps Taken and Sedentary Minutes

```{r}
ggplot(data=activity_daily, aes(x=TotalSteps, y=SedentaryMinutes)) + geom_point() + geom_smooth(formula = y ~ x, method = "loess") + labs(title ="Total Steps vs. Sedentary Minutes")

```

![Total Steps Vs Sedentary minutes](https://github.com/Anabella1/Capstone-Project/assets/119600515/e1503434-1de2-479e-87fa-0f210567dd82)

- The lower the steps taken by customers the higher the sedentary minutes and the more steps taken the lower the sedentary minutes. When customers take more steps the hours of inactivity is bound to reduce.
-  Therefore, I recommend customers take more steps, experts have warned that sitting for long hours is unhealthy.



##### Relationship between Steps Taken and calories burnt

```{r}
ggplot(data=activity_daily, aes(x=TotalSteps, y=Calories)) + geom_point() + geom_smooth(formula = y ~ x, method = "loess") + labs(title ="Total Steps VS Calories")
```

![Total Steps vs Calories](https://github.com/Anabella1/Capstone-Project/assets/119600515/95249809-baad-4490-a9d2-f2524ba80bd9)

There is a positive corellation between steps taken and calories burnt. 



 ##### Very Active Minutes Vs Calories

```{r}
ggplot(data = activity_daily, aes(x = VeryActiveMinutes, y = Calories)) + 
  geom_point() +
 geom_smooth(formula = y ~ x, method = "loess") +
  labs(title = "Very Active Minutes VS Calories", 
       x = "Very Active Minutes", 
       y = "Calories") 
```

![Very Active Minutes vs Calories](https://github.com/Anabella1/Capstone-Project/assets/119600515/6fe03d7b-e35e-42c9-bdf0-1cafb5f2277c)



#####  Checking Steps taken daily by day of the Week
This is to know what week has the most active users.

```{r}
table1 <- activity_daily %>%
  group_by(Day_of_Week) %>%
  summarise(total_steps = mean(TotalSteps))
table1$weekdays <- ordered(table1$Day_of_Week, levels=c( "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))  
                                    
```


```{r}
table1 %>%
  ggplot(mapping=aes(x=weekdays, y=total_steps, fill=weekdays)) +
   geom_bar(position = "dodge",
           stat = "summary",
           fun = "mean") +
  geom_hline(yintercept = 7200) +
  labs(title = "Total Steps Per Weekdays")+
  theme(axis.text.x = element_text(angle = 45))+
  theme(text = element_text(size = 8))
  
```

![Total Steps Per Weekdays](https://github.com/Anabella1/Capstone-Project/assets/119600515/7136d2c0-732b-446d-bb90-b09b595cbc35)

- Wednesday has the highest average total steps taken in the week days while Tuesday has the lowest.


  
 ##### Hourly Intensities daily. 
The hourly intensity was run on excel, I splitted the time from date, then created a pivot table with time and total intensity, I summarised the value of the total intensity by Average and went ahead to create a pivot chart. From my findings from the chart revealed that:


![image](https://github.com/Anabella1/Capstone-Project/assets/119600515/2a94eead-4087-40a6-8907-d943d8048fe7)


##### Average Total Intensity vs. Time

![Image 10-05-2024 at 04 31](https://github.com/Anabella1/Capstone-Project/assets/119600515/86d573dd-fde0-43a8-8250-7a5a7a7edf00)

- People are more active between 6am and 7pm.
- 5pm - 7pm has the highest movement, it can be deduced that people are more active around that time, it can be said that when people are done with work for the day they take a walk instead of driving or taking taxi.



##### Daily hourly steps reloading and renaming from ActivityHour to date_time

```{r}
hourly_step <- read.csv("hourlyStepmergedd.csv")
  head(hourly_step)
```

![hourly step loading](https://github.com/Anabella1/Capstone-Project/assets/119600515/16438799-fd07-4471-ba3e-e948e62d7a75)

```{r}
hourly_steps<- hourly_step %>% 
  rename(date_time = ActivityHour) %>% 
  mutate(date_time = as.POSIXct(date_time, format ="%m/%d/%Y %I:%M:%S %p" , tz=Sys.timezone()))

```

- Hourly steps daily seperating date_time and making it into two columns (date and time)

```{r}
 hourly_steps <- hourly_steps %>%
  separate(date_time, into = c("date", "time"), sep= " ") %>%
  mutate(date = ymd(date)) 
```


- checking to see the data changed

```{r}
head(hourly_steps)
```
![datetime change](https://github.com/Anabella1/Capstone-Project/assets/119600515/12fbcd97-18e5-4eae-9f14-ea6927d2ac57)


###### Visualization of the hourly steps throughout the day.

```{r}
 hourly_steps %>%
  group_by(time) %>%
  summarize(average_steps = mean(StepTotal)) %>%
  ggplot() +
  geom_col(mapping = aes(x=time, y = average_steps, fill = average_steps)) + 
  labs(title = "Hourly Steps Per Day", x="Time", y="Avg_Steps") + 
  scale_fill_gradient(low = "#FF0000", high = "#00FF00")+
  theme(axis.text.x = element_text(angle = 90)) +
   theme(text = element_text(size = 8))
  
 
```

![Hourly Steps Per Day](https://github.com/Anabella1/Capstone-Project/assets/119600515/21995043-ebd9-447c-bdc7-c8f9daf89aeb)

- It shows that people are more active from 8am to 7pm, they were more steps between 12pm - 2pm and 5pm - 7pm respectively.
- the time more steps are recorded suggests that they have their lunch break (12pm-2pm) and close for the day (5pm-7pm) during those period assuming the respondents are working class.



## Act Phase

Bellabeat creates a high a high-tech manufacturer of health-focused products for women. 

- I carried out an analysis on the average number of steps per week day,   very active minutes vs calories burnt and     steps taken vs calories burned. 

- I also analysed the days which users are most active, the time of the day with the most activity users.


### Key insights

- Average users are not able to accomplish healthy.
  goals.
- Very active minute has positive relationship with calories.
- There is a positive orrelation between steps taken and calories burnt.
- Hourly steps increases during the day, e.g during working resumption time (8am-9pm) and during            closing hours (6pm-7pm).
- Sedentary minutes increases with a reduction in total steps.


### Recommendation 

- the CDC recommend that most adults aim for 10,000 steps per day. For most people, this is the equivalent of about 8 kilometers, or 5 miles. Daily notification should be sent to people to encourage them to take more steps. Daily reminders that compares yesterday and today's step depicting significant drop in their activities.
  
- If users want to lose weight, gain weight or maintain a specific weight, for instance, if a user want to lose weight fitbit tracker can suggest some ideas for low-calories food for such user, while adding the number of calories different food and portion contains.
  
- A reward system daily based on the level of activity on the app can ginger users to be consistent in walking because they find the reward satisfying.
  
- The online campaign images and messages should  portray the app as more than just a fitness activity app, but an inclusive app that caters to women of diverse background, color, and sizes. It should be seen as a guide that empowers women to strike a balance in their everyday life.




















