# **Problem Definition**

Our company's expansion and diversification plans include venturing into the aviation industry to own and operate airplanes for commercial and private enterprises. A key preliminary step for this consideration is risk assesment for different aircrafts to advise which aircrafts pose the lowest risk for the intended business endeavor. This projects seeks to assess risk potential from analysis of aviation accident data from 1962 to 2023. 

The primary objective of this exercise is to identify the lowest-risk aircraft for our company to purchase and operate. The following are some of the key considerations we expect to make:


*   Historical accident trends by aircraft type
*   Severity and frequency of accidents
*   Factors contributing to the accidents e.g. weather, pilot error or mechanical failures
*   Any correlations between operational risk and aircraft characteristics

# **Data Preprocessing**

This section prepare the provided aviation data for analysis. We intend to do the following:



*   Dataset Overview - Load and understand the data
*   Handling Missing Values using derived domain knowledge and imputation
*   Data Cleaning e.g. standardizing categorical values, deriving useful date data, removing duplicates etc

## **Dataset Overview**

It is imperative for us to understand the aviation dataset first i.e.:

*   The data structure e.g. available columns, data types and presence of missing values
*   Identify useful columns to focus on

Data Understanding will prescribe subsequent steps. Simple cleaning procedures e.g. capitalization will be done on the spot (immediately a need is observed) to ensure they are not forgotten. Complex cleaning procedures will be done in the **Data Cleaning** subsection

First, we initialize common libraries we project to utilize in this exercise:

*   pandas to create and manipulate dataframes
*   seaborn to facilitate any requisite visualizations within the notebook
*   numpy for mathematical calculations
*   etc

We then load the dataset and embark on a data understanding exercise.

### Data Understanding

Sampling a few columns to assess the various categorical data present will help us define how to clean the data, e.g.:

*   **Investigation.Type**: There are 71 different categories, but the only seemingly relevant categories here are 'Accident' and 'Incident'. The others seem like noise. Perusal of the 'noisy" data on excel showed that where the column "Event.Id" was blank, there was a noisy column in 'Investigation.Type'. Dropping rows with empty Event.ID may fix this
*   **Injury.Severity**: Where there are fatalities, the number of fatalies is appended on the string. This is unnecessary, since there's another column that details the number of fatalities. There is a need to clean this column to only have **Fatal**, **Serious**, **Minor**, **Non-Fatal**, **Incident** and **Unavailable**. There is missing data.
*   **Aircraft.damage**: The categorization of extent of damage seems okay as is i.e. 4 categories (**Destroyed**, **Substantial**, **Minor**, **Unknown**). There is no need for cleaning this column. There is missing data.
*   **Aircraft.Category**: The categorization of Aircrafts seems okay as is. But there is a need to combine '**Unknown**' and '**UNK**' such that they are the same category. There is missing data.
*   **Make**: Unstandardized capitalization is causing the same manufacturer to be split e.g. Cessna vs CESSNA. There is a need to regularize capitalization to prevent such an error. Also, there is noise intoduced by having entries such as 'Cessna Aircraft' vs 'Cessna Aircraft Co' vs 'Cessna Aircraft Co.'. As they are too many possibilities, we may need to ignore this for now (and revisit once we can make use of fuzzy logic to normalize similar/equivalent data). There is missing data/
*   **Model**: A bit of non-standardized capitalization introduces noise into the data. This will need to be corrected. There is missing data.
*   **Amateur.Built**: There are 2 categories: **Yes** and **No** as well ass missing data.
*   **Engine.Type**: The column seems clean, with Reciprocating Engine Aircrafts accounting for majority of the accidents/incidents. Entries with "UNK" should be substituted with "Unknown" to clean the data. There are missing values.
