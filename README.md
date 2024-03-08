# Epoca - Amazon-Trend-Prediction-from-TikTok-Hashtags

### Team Leader: Junjie Wu
### Team Members: Shiza Jamil, Romie Jean, Nick Albury
### Instructors: Dr. Jim Hoover, Taikgun Song
### Sponsor: Roberto Ortiz

## Business Objective
- To detect a relationship between TikTok trends and Amazon best-seller list and discover the time it takes for a trending product to end up on the Amazon best-seller list.
- The sponsor mentioned our team may need to combine the time-series data from both Amazon and TikTok to answer how soon a product that becomes popular on TikTok will have an effect on Amazon searches and/or sales.

## Project Objective
The team worked through Business Understanding, Data Understanding, Data Preperation, Modeling, Evaluation, and Deployment (CRISP-ML Framework)



## Data Preperation & Model History

### Version 1:
- Focus: 1000 hashtag vs. 1000 search term.
- Data Preperation: Merge multiple csv files into two `superfiles` to optimize the performance especially with huge datasets.
  - TikTok super parquet file with `800,000` observations
  - Amazon super parquet file with `800,000` observations
- Method: Testing feasibility for multiple Fuzzy Matching methods, Word2Vec, and Doc2Vec.

### Version 2:
- Focus: 1000 hashtag vs. 800,000 search term.
- Data Prepration: Drop duplicates by only keep the first date each `hashtag/search term` was collected in record and keep those columns models need for comparison.
  - TikTok dataset:
    - `Nsw_TikTok`: `hashtag`, `description`, `date_collected`, `nostopwords_description`.
  - Amazon dataset:
    - `Nsw_Amazon`: `Search Term`, `nostopwords_Search Term`, `Reporting Date`.
- Method: Sample output for Cosine Similarity and K-Nearest Neighbors.

### Version 3:
- Focus: 220,000 hashtags vs. 800,000 search term.
- Data Preparation for improve the data processing speed: 
  - Format changes for `Reporting Date` and `date_collected` to `%m/%d/%y`.
  - Remove numerical values like `00_12 ounce`and strange symbols like `⬜/emojis/ Arabic` in `hashtag descriptions`.
- Outcome: Final output for Cosine Similarity and K-Nearest Neighbors. The combined dataframe resulted in `226,523` observations.

![Model Evolution Graphic](https://github.com/JunjieWerg/Assets/blob/main/Model%20Evolution%20Graphic.png)

## Key Decision Making

Key decisions on important variables:
- Used `description` for TikTok instead of `Hashtag`.
- Used `search term` for Amazon instead of `Product Title`.
- Created `Delta Date` by subtracting `date_collected` from TikTok from the `reporting date` from Amazon.

## Visualizations

### Distribution of Word Counts in Descriptions

![Distribution of Word Counts in Descriptions](https://github.com/JunjieWerg/Assets/blob/main/Distribution%20of%20Word%20Counts.png)

### Distribution of Delta Dates

![Distribution of Delta Dates](https://github.com/JunjieWerg/Assets/blob/main/Distribution%20of%20Delta%20Dates.jpg)


## Y Variable Development

- The difference between the date a hashtag is trending on TikTok and the date the similar hashtag (category) is trending on Amazon.

![Y Variable Development](https://github.com/JunjieWerg/Assets/blob/main/Y%20Variable%20Development.png)


## Data Transformations

- One-hot encoding of the "Model" column.
- Min-max scaling of relevance scores.
- Calculation of time delta field.
- Calculation of accuracy percentages.

## Model Assessment Metrics

- Significance of hashtags/descriptions.
- Quality of matches for k-NN and Cosine Similarity.
- Correspondence to kitchen items category.
- Human assessment validations.
- Accuracy rates for different models.

## Final Model Justification
The team will work on this part on April 2024. We may try run the model again using without stop words datasets and figure out whether the accuracy of the model will improve or not.

## Future Directions

- Exploration of OpenAI word-embedding for fuzzy matching.
