# DATA 512 Assignment A2
Emily Yamauchi


## Introduction

### Objective

The goal of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries. For this assignment, you will combine a dataset of Wikipedia articles with a dataset of country populations, and use a machine learning service called ORES to estimate the quality of each article.

### Data Source

Data is collected from two separate sources  
- [Wikipedia politicians by country dataset](https://figshare.com/articles/Untitled_Item/5513449) from Figshare 
- [World population data by country](https://www.prb.org/international/indicator/population/table/) as published by the Population Reference Bureau

The data file for the politician dataset can be extracted by downloading and unzipping the file, which is called `page_data.csv`.  

The article quality score prediction is accessed from the machine learning system called ORES, which was originally an acronym for "Objective Revision Evaluation Service", but since renamed simply ORES.  
ORES is a machine learning tool that can provide estimates of Wikipedia article quality. The article quality estimates are, from best to worst:
1. FA - Featured article
2. GA - Good article
3. B - B-class article
4. C - C-class article
5. Start - Start-class article
6. Stub - Stub-class article

The ORES quality score is accessed through a REST API endpoint [documentation](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model).  


### Data Processing

The politician dataset include pages that are not articles, which have page names starting with `Template:`. These are discarded from the dataset.  
The population dataset include subregion data which are aggregates of the countries in that subregion (i.e. North Africa). These subregions are indicated by ALL CAPS in the `geography` field. These rows are discarded though the subregion category will be noted for later analysis.  

The politician and population dataset are merged by country name, and the combined dataset have the following schema:  

| Column      |
| ----------- |
| country |
| article_name |
| revision_id |
| article_quality_est. |
| population |


### Known Issues

The politician and population datasets are merged on country name rather than some ID key- this means that if the country names are not identical (i.e. Ivory Coast vs Cote d'Ivoire) the two will not merge.  
Some articles do not have prediction values, which are logged separately in a file called `no_scores.csv` in the `data_clean` folder.  

### Folder Structure

```
 data-512-a1
    ├── LICENSE
    ├── README.md
    ├── data_raw
    │   ├── country.zip
    │   └── export.csv
    ├── data_clean
    │   ├── no_scores.csv
    │   ├── politicians.csv
    │   ├── populations.csv
    │   ├── subregions.csv
    │   ├── wp_wpds_countries_no_match.csv
    │   └── wp_wpds_politicians_by_country.csv
    └── data-512-a2.ipynb
```