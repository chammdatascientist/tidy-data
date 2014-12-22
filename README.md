tidy-data
=========
#read training data
train_data <- read.table("X_train.txt")
#read test data
test_data <- read.table("X_test.txt")
#read test subject id for column bind
subj_test_id <- read.table("subject_test.txt")
#read test activity id for column bind
act_test_id <- read.table("y_test.txt")
#column bind test subjects, activity codes, test data
tog_test <- cbind(subj_test_id, act_test_id, test_data)
#read train subject id for column bind
subj_train_id <- read.table("subject_train.txt")
#read train activity id for column bind
act_train_id <- read.table("y_train.txt")
#column bind train subjects, activity codes, test data
tog_train <- cbind(subj_train_id, act_train_id, train_data)
#read column headings into string col vector
col_heads <- read.table("features.txt")
col_names <- as.character(col_heads$V2)
#demo_names <- c("subject", "activity")
#all_col_names <- cbind(demo_names,col_names)
#combine rows from test and training data
dat <- rbind(tog_test, tog_train)
#add column names to data 
colnames(dat) <- col_names
#install dplyr
library(dplyr)
#read data into data frame
dat_df <- data.frame(dat)
#load data into data frame tbl
dat_tbl <- tbl_df(dat_df)
#get variable with means
mean_vars <- select(dat_tbl, contains("mean"))
std_vars <- select(dat_tbl, contains("std"))
demo_vars <- select(dat_tbl, starts_with("subjects"))
demo_vars2 <- select(dat_tbl, starts_with("activ"))
sub_data <- cbind(demo_vars, demo_vars2, mean_vars, std_vars)
