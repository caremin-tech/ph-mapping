# Philippines Mapping Project

## Workstream 1 -- Data Cleaning

### Summary: 
The goal of this workstream is to use a single source of truth (SSOT) file of province/city/barangay pairings to clean up another file -- also containing these three levels of geographic granularity -- matching as many occurences in the second (unclean) file as possible to SSOT file.

### Work Drivers:
- **Repo Setup and Environment Management:**
    - [ ] Create environment management files for repo:
        - [ ] Using conda throughout, I'll put together an env yaml file
    - [x] Create branching setup for the repo:
        - [x] Create a paul_dev branch to ensure we're working with best SDLC practices
- **Build Geo Label Matching Logic:**
    - [x] Import and manage file that screens out non-ICM regions -- `raw_data/non_icm_loc.csv`:
        - [x] Set Batangas and Bulacan to NOT be removed (done in Excel)
        - [x] Add First, Second, Third, and Fourth (districts of Manila) to file and set the them to be removed (done in Excel)
        - [x] Import file and drop all NaNs (so that now all provinces listed can be used as a negative screen)
    - [x] Create SSOT file:
        - [x] Import `raw_data/new_locations.csv` file (raw data taken from [this source here](https://gadm.org/download_country_v3.html)) and remove all rows that are in a province that is contained in the `raw_data/non_icm_loc.csv` file accompanied by the value: True (meaning it should be removed as it is not a part of the regions ICM serves)
        - [x] Save out the newly created SSOT file -- `processed_data/ssot_df.csv` -- for reference and future use
    - [ ] Clean up the *unclean* file --  `raw_data/original_locations.csv` -- and add new correct geo-mapping fields:
        - [x] As done with the SSOT file, remove all rows from the *unclean* file that are in a province contained in the `raw_data/non_icm_loc.csv` file accompanied by the value: True (meaning it should be removed as it is not a part of the regions ICM serves)
        - [ ] Create a new column -- `province_cleaned` -- to be appended to the *unclean* file, with the *correct* name for the province associated with each row:
            - [x] Create `province_mapping_df`, which will eventually serve as a mapping dictionnary of unclean to clean names, but will start by simply storing all unique province names in the *unclean* file
            - [x] Iterate over each unique province name in the *unclean* file, and check if the value in the `province` column matches a value contained in the `province` column of the SSOT file (accounting for capitalization differences)
            - [ ] After having done the automated matches possible, perform the manual matching necessary based on additional research:
                - [ ] Manually match "City of Isabela (Capital)", "Cotabato", and "Davao Occidental"
             - [ ] Use the `province_mapping_df` (and any other custom logic needed) to create the new `province_cleaned` column
        - [ ] Create a new column -- `city_cleaned` -- to be appended to `raw_data/original_locations.csv`, with the *correct* name for the city associated with each row:
            - [ ] Same subtasks as above, but more complicated matching logic is to be expected the more geographically granular you go
        - [ ] Create a new column -- `barangay_cleaned` -- to be appended to `raw_data/original_locations.csv`, with the *correct* name for the barangay associated with each row:
            - [ ] Same subtasks as above, but more complicated matching logic is to be expected the more geographically granular you go

### Additonal Notes / Exogenous Comments:
- The file `Region-Province-Names.pdf` (downloaded [from this link here](https://psa.gov.ph/classification/psgc/)) is the complete official list of the current names for geographies as of 12/31/2019 per the Official PSA (philippines statistical authority)
    - We need to follow these names as the official region/province names. Neither `original_locations.csv` or `new_locations.csv` may follow this naming schema, but it is the official philippines naming convention (SSOT)
- LUZON, VISAYAS, and MINDINAO are not official regions but actually just the 3 subsections of the Philippines (Top, Middle, Bottom in that order)
- We should focus on the Province-City-Barangay match; but Regions can help us subsection the data