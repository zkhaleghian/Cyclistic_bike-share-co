
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
```
