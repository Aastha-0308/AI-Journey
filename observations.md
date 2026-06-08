# Anime Analysis

# Day 1 Findings

## Dataset Overview
- Loaded and explored the anime dataset using Pandas.
- Examined the available columns and identified key attributes such as score, members, genre, studio, source, and type.

## Genre Analysis
- Initially, Hentai appeared to be the most common genre.
- Further investigation revealed that the genre column contains multiple genres in a single row, making direct counting misleading.
- After splitting genre values, Comedy, Action, and Fantasy emerged among the most common genres.

## Popular Anime
- Analyzed anime with the highest member counts.
- Popular titles such as Attack on Titan and other well-known series appeared near the top of the rankings.
- Popularity rankings aligned with expectations from the anime community.

## Learning Outcomes
- Learned how to use:
  - `read_csv()`
  - `head()`
  - `value_counts()`
  - `sort_values()`
  - dictionaries
  - lambda functions
- Gained experience exploring a real-world dataset and validating results instead of accepting them blindly.



# Day 2 Findings

## Popularity vs Rating
- Created a scatter plot to analyze the relationship between anime popularity and ratings.
- Calculated a correlation coefficient of approximately 0.31 between members and score.
- Found a moderate positive relationship, suggesting that popular anime tend to have higher scores, but popularity alone does not determine quality.

## Members vs Favorites
- Calculated the correlation between members and favorites.
- Obtained a strong positive correlation of approximately 0.78.
- This suggests that anime with larger audiences generally accumulate more favorites.

## Studio Analysis
- Discovered that many anime are produced by multiple studios.
- Split studio names and used `explode()` to create separate entries for each studio.
- This allowed studio-level analysis using average scores.

## Sample Size Bias
- Initial studio rankings were dominated by studios with only one or two anime.
- Added anime counts for each studio and filtered out very small sample sizes.
- After filtering, rankings became more meaningful and highlighted established studios such as Bones, A-1 Pictures, and Studio Ghibli.

## Learning Outcomes
- Learned:
  - `groupby()`
  - `agg()`
  - `corr()`
  - `explode()`
  - scatter plots
  - data reshaping
- Understood that data often requires cleaning and restructuring before meaningful analysis can be performed.