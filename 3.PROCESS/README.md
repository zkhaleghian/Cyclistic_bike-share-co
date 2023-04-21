I use R and have added the ride_length and day_of_week columns to your dataset. 
The ride_length column is calculated by subtracting the started_at from the ended_at column and formatting the result into hours, minutes, and seconds. 
The day_of_week column is derived from the started_at column using the wday() function from the lubridate package to get the day of the week in label format.

```
# Load packages in R
library(readr)
library(tidyverse)
library(dplyr)
library(lubridate)
library(skimr)
library(janitor)

# import 12 .csv files and combine them
setwd("C:\\Users\\khale\\Documents\\GDA_capstone_1_cyclistic")
csv_files <- list.files(pattern = "*.csv")
cyc_data <- do.call(rbind, lapply(csv_files, read.csv))

# Write the combined data frame to a new CSV file
write.csv(cyc_data, file = "cyc_data.csv", row.names = FALSE)

# convert started_at and ended_at to POSIXct objects
cyc_data$started_at <- as.POSIXct(cyc_data$started_at, format = "%Y-%m-%d %H:%M:%S")
cyc_data$ended_at <- as.POSIXct(cyc_data$ended_at, format = "%Y-%m-%d %H:%M:%S")

# calculate ride_length as ended_at - started_at
cyc_data <- mutate(cyc_data, ride_length = ended_at - started_at)
# format ride_length to HH:MM:SS
cyc_data$ride_length <- sprintf("%02d:%02d:%02d", as.numeric(cyc_data$ride_length) %/% 3600,
                                (as.numeric(cyc_data$ride_length) %/% 60) %% 60,
                                as.numeric(cyc_data$ride_length) %% 60)

# calculate day of week from started_at
cyc_data$day_of_week <- wday(cyc_data$started_at, label = TRUE)

# Print the first few rows of the data
head(cyc_data)







```
