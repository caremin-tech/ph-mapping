# Philippines Mapping Project

## Workstream 1 -- Data Cleaning

**Summary:** Goal here is to use a single source of truth (SSOT) file of region/province/city/barangay pairings to clean up another file -- also containing these four level of geographic granularity -- matching as many occurences in the second (unclean) file as possible to SSOT file.

**Next steps:**
- Create environment management files for repo:
    - Using conda throughout, I'll put together an env yaml file
- Create branching setup for the repo:
    - I'll create a paul_dev branch to ensure we're working with best SDLC practices
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
### COMMENTS BELOW ###
- Why does `the new_locations_only_icm.csv` file not have the id fields / lat / long fields that the `new_locations.csv` file does? Can I assume we can join that back later on down the line and for now I can just concern myself with using the `the new_locations_only_icm.csv` as my SSOT for cleaning up the `original_locations.csv` mappings? 
### this was because new_locations_only_icm was actually an old file I wasn't too familiar with new_locations I pulled last Friday from the gadm.org website and kept their ids and lat/long. See answer to your last question for next steps on this.
- Where exactly is the SSOT file from again?
    - I think I heard that it's from [gadm.org](gadm.org) but was wondering where exactly / when it was pulled?
    ### Correct (4/10/2020) -- https://gadm.org/download_country_v3.html
- Ran into a question/roadblock for region-name-tagging
    - Check out [the exploratory notebook here](https://github.com/caremin-tech/ph-mapping/blob/master/data_cleaning_workstream/data_cleaning_workbook.ipynb) and control+F for "Questions / Roadblocks" to see my notes and question. 
    ### I have added 2 new files to the repo: 
    ### 1. Official PSA (philippines statistical authority) Region-Province-Names.pdf (this is the complete official list of the current names as of 12/31/2019. WE need to follow these names as the official region/province names. Neither original_locations or new_locations may follow this naming schema but it is the official philippines naming convention (SSOT).
    ### 2. non_icm_loc.csv: Re: your first open question, let's use new_locations and just remove the provinces labeled TRUE in this file. They are the ones in the Luzon region (excluding Palawan which we want to keep) -- that will create a new_locations_icm_only.csv file. 
   
**Additional Notes**: 
- 1. LUZON, VISAYAS, MINDINAO are not official regions but actually just the 3 subsections of the Philippines (Top, Middle, Bottom in that order)
- 2. We should focus on the Province-City-Barangay match; but Regions can help us subsection the data. As you suggested in the Jupyter notebook manual effort will need to done to understand which provinces from the old/new fall under which region/ the new PSA names.

