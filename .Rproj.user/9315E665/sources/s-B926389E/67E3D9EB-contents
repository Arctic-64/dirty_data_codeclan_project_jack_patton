library(tidyverse)
library(here)
library(janitor)
library(stringr)

ship_ID <- readxl::read_xls(here("raw_data/seabirds.xls"), sheet = 1)
bird_ID <- readxl::read_xls(here("raw_data/seabirds.xls"), sheet = 2)

ship_ID <- janitor::clean_names(ship_ID)
bird_ID <- janitor::clean_names(bird_ID)

combined_data <- left_join(ship_ID, bird_ID, by = "record_id")

combined_data %>% 
  rowwise() %>%
  mutate(common_name = str_remove_all(species_common_name_taxon_age_sex_plumage_phase, paste(c("/D", "[A-Z][A-Z]+", "PR", "[0-9]"), collapse = "|")) %>%
           trimws()) -> combined_data

combined_data %>% 
  rowwise() %>%
  mutate(scientific_name = str_remove_all(species_scientific_name_taxon_age_sex_plumage_phase, paste(c("/D", "[A-Z][A-Z]+", "PR", "[0-9]"), collapse = "|")) %>%
           trimws()) -> combined_data

combined_data %>% 
  rowwise() %>%
  mutate(abbriviated_name = str_extract(species_abbreviation, "([A-Za-z]+)")) -> combined_data

combined_data <- select(combined_data, "common_name", "scientific_name", "abbriviated_name", "count", "nacc", "ocacc", "long", "lat")

write.csv(combined_data, here("clean_data/sea_birds_clean.csv"))