library(tidyverse)
library(here)
library(stringr)

candy_2015 <- readxl::read_xlsx(here("raw_data/candy_ranking_data/boing-boing-candy-2015.xlsx"))
candy_2016 <- readxl::read_xlsx(here("raw_data/candy_ranking_data/boing-boing-candy-2016.xlsx"))
candy_2017 <- readxl::read_xlsx(here("raw_data/candy_ranking_data/boing-boing-candy-2017.xlsx"))
candy_2015 <- janitor::clean_names(candy_2015)
candy_2016 <- janitor::clean_names(candy_2016)
candy_2017 <- janitor::clean_names(candy_2017)

candy_2015 = add_column(candy_2015, year = 2015, country = NA , state = NA, gender = NA)
candy_2016 = add_column(candy_2016, year = 2016)
candy_2017 = add_column(candy_2017, year = 2017)
colnames(candy_2017) = str_remove_all(colnames(candy_2017), "q[0-9]*_")

candy_2015 = rename(candy_2015, age = how_old_are_you, going = are_you_going_actually_going_trick_or_treating_yourself)
candy_2016 = rename(candy_2016, age = how_old_are_you, going = are_you_going_actually_going_trick_or_treating_yourself, gender = your_gender, country = which_country_do_you_live_in, state = which_state_province_county_do_you_live_in)
candy_2017 = rename(candy_2017, state = state_province_county_etc, going = going_out)

common_cols = colnames(candy_2015)[colnames(candy_2015) %in% colnames(candy_2016)]
common_cols = colnames(candy_2017)[colnames(candy_2017) %in% common_cols]


irrellivant = c("cash_or_other_forms_of_legal_tender"
                ,"broken_glow_stick"
                ,"dental_paraphenalia"
                ,"creepy_religious_comics_chick_tracts"
                ,"hugs_actual_physical_hugs"
                ,"generic_brand_acetaminophen"
                ,"vicodin"
                ,"glow_sticks"
                ,"pencils"
                )

relevant = c("year", "age", "gender", "going", "country", "state")


wanted_cols = setdiff(common_cols, irrellivant)
wanted_cols = c(relevant, wanted_cols)

candy_2015 = select(candy_2015, wanted_cols)
candy_2016 = select(candy_2016, wanted_cols)
candy_2017 = select(candy_2017, wanted_cols)
merged_data = rbind(candy_2015, candy_2016, candy_2017)


#merged_data = mutate(merged_data, age = ifelse(age == "[0-9]+", age, NA))

tail(merged_data$age, 1000)

write.csv(merged_data, here("clean_data/candy_data_clean.csv"))