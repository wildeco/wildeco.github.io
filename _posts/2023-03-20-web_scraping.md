---
title: "Web scraping in R"
date: 2023-02-18T15:34:30-04:00
categories:
  - blog
tags:
  - webscraping
  - R
---

# Extract data from NSW Species Refugia website

Web scraping is the process of automatically extracting information from websites. It is an important technique because it allows users to gather data that might not be available through other means, and to analyze it in ways that would be difficult or impossible manually.

My problem was that I wanted to download species distribution models from the [NSW Climate Refugia Website](https://nswclimaterefugia.net/). However, the site offered an option to manually enter the names of ~ 400 species to download data. Heck, that's a real manual work. So I wrote a script to download the data for the ~400 species.  

The download path for the species in the website is structured as:
https://nswclimaterefugia.net/zip/genus_species.zip

So I need to create a vector of download links for all species

```ruby
#Load required packages
packages <- c("tidyverse", "stringi", "tabulizer)
lapply(packages, library, character.only = TRUE)
```

Get the names of all the species that is provided as a table in a report that's provided online, I use the tabulizer package to do that. Provide the link and the page number of the table. 

```r
#Report link
report_link <- "https://www.climatechange.environment.nsw.gov.au/sites/default/files/2021-06/Identifying%20climate%20refugia%20for%20key%20species%20in%20NSW.PDF" 

#Extract the table
rawtable <- extract_tables(report_link, pages = c(86:93))

#Clean the table
cleantable <- rawtable |>
  map(data.frame) |> 
  map_dfr(bind_rows)

#Get species names
species <- cleantable$X2 |> 
  stri_remove_empty() |> #Remove empty strings
  str_replace_all("[.]","") |> #Remove dots
  str_to_lower() |>
  str_replace_all("[ ]", "_") |> #Replace gaps with "_"
  str_c(".zip")  #The website has files with .zip extension

#Concanate species names website path to match the download path
species <- str_c("https://nswclimaterefugia.net/zip/", species)

#Specify the download path
save_path <- "./data/sdms" #Local directory to save file 

```
```r
#Write function to download files from each path
download_function <- function(x){
  download.file(x, file.path(save_path, basename(x)))
}
```
Finally run the function to get all the zips for all species

```r
#Run the function
purrr::walk(species, possibly(download_function, 
            print("Error: This species doesn't have data")))
```

However, some species could not be downloaded, check the warning and extract
the errors. 

There were two issues; 

1. one group of species had a name within the brackets (however the download portal didn't have such names)

* Solution1: Remove the name within the brackets

2. one group of species had names in two lines which were not captured from the table

* Solution2: Identify these two lines and merge them

```r
#Remove the species names within the brackets
group1 <- species[str_detect(species, "[()]")]
group1 <- group1 %>% str_replace_all("_.*_","_")
group1

#Some species had names in double lines fix them
group2 <- str_subset(species, "subsp.*.")
group2 <- str_subset(group2, "subsp.*_", negate = T)
group2 <- str_replace(group2, ".zip", "_")

#Manually get their names from the report and join them
manual_names <- c("fletcheri.zip","barbigerorum.zip", "juniperina.zip", "supplicans.zip")

#Join
group2 <- str_c(group2, manual_names)

#Merge both groups to download
group <- c(group1, group2)

group <- str_c("https://nswclimaterefugia.net/zip/", group)

purrr::walk(group, possibly(download_function, print("Error: This species doesn't have data")))


####Unzip only the required files (There are both thresholded and original SDMs)

zip_path <- dir("data/sdms/", full.names = T, pattern = ".zip$")

extract_threshold_sdms_only <- function(zip) {
  
  file_to_extract <- str_subset(unzip(zip, list = T)$Name, "_thr")
  
  threshold_sdm <- unzip(zip, files = file_to_extract, exdir = "data/sdms/unzipped/thresholded/")
}

extract_unthreshold_sdms_only <- function(zip) {
  
  file_to_extract <- str_subset(unzip(zip, list = T)$Name, "_2000\\.")
  
  threshold_sdm <- unzip(zip, files = file_to_extract, exdir = "data/sdms/unzipped/original/")
}

#Get the data for these groups
walk(zip_path, extract_threshold_sdms_only)
walk(zip_path, extract_unthreshold_sdms_only)
```