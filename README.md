# Philippines Mappng Project

## Workstream 1 -- Data Cleaning

**Summary:** Goal here is to use a single source of truth (SSOT) file of region/province/city/barangay pairings to clean up another file -- also containing these four level of geographic granularity -- matching as many occurences in the second (unclean) file as possible to SSOT file.

**Next steps:**
- Create EDA notebook to explore the two primary files of interest:
    - `new_locations_only_icm.csv` --> SSOT file for all geos (limited to ICM network)
    - `original_locations.csv` --> ICM file with unclean names 
- Build logic that creates 4 new columns to add to the `original_locations.csv` file, each representing the "clean" label for the corresponding geography, based on matching the content in `original_locations.csv`as best as possible to `new_locations_only_icm.csv`
    - It appears at first glance as though there are many areas where text-based matching without additional context will be quite difficult, so I will do this via a jupyter notebook that goes one level of geographic granularity at a time, with the result of each section being the production of a 'cleaned' column variant. 
    - The acceptance criteria for this workstream is 4 new columns added, named:
        - region_cleaned
        - province_cleaned
        - city_cleaned
        - barangay_cleaned


**Open questions:**
