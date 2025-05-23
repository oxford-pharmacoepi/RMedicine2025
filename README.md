## A framework for cohort building in R: the CohortConstructor package for data mapped to the OMOP Common Data Model
### R/Medicine 2025
### Edward Burn & Núria Mercadé-Besora, University of Oxofrd
##

This repository contains the contents for the Demo of the CohortConstructor R package at the [R/Medicine 2025](https://rconsortium.github.io/RMedicine_website/) online conference.

The Demo takes place the 9th of June at 10.00h (EDT) / 16.00h (CET).

If you are planning on attending the Demo and want to follow the examples along, please have the follwing packages and mock data download in your RStudio session. 
You can do so by following these instructions: 

1) Install or update the following required packages:

```{r}
install.packages("CDMConnector", "CodelistGenerator", "CohortConstructor", "CohortCharacteristics", "dplyr", "duckdb")
```

2) Set a folder where to download the Eunomia mock dataset, and download it.

```{r}
eunomia_folder <- "..." # for the user to input
Sys.setenv("EUNOMIA_DATA_FOLDER" = eunomia_folder)}
if (!dir.exists(Sys.getenv("EUNOMIA_DATA_FOLDER"))) {dir.create(Sys.getenv("EUNOMIA_DATA_FOLDER"))}
CDMConnector::downloadEunomiaData()  
```

3) Make sure you can connect to Eunomia with duckdb and create a CDM reference with CDMConnector

```{r}
# Load relevant packages
library(CDMConnector)
library(CodelistGenerator)
library(CohortConstructor)
library(CohortCharacteristics)
library(dplyr)

# Connect to the "database"
con <- DBI::dbConnect(duckdb::duckdb(), dbdir = eunomiaDir())

# Create CDM reference object
cdm <- cdmFromCon(
  con, 
  cdmSchema = "main", 
  writeSchema = "main",
  writePrefix = "my_study_"
)
```
