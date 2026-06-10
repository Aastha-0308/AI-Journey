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


# Day 3 Findings - Source Material Analysis

## Source Distribution

The most common source categories in the dataset were:

* Unknown (4210 anime)
* Original (3368 anime)
* Manga (3120 anime)

This indicates that Original and Manga adaptations make up a significant portion of the dataset.

---

## Average Score by Source

Initial analysis showed that Light Novel adaptations had the highest average score among major source categories.

| Source      | Average Score |
| ----------- | ------------- |
| Light Novel | 6.80          |
| Manga       | 6.76          |
| Original    | 5.74          |

This suggested that anime adapted from Light Novels and Manga generally received higher ratings than Original anime.

---

## Importance of Sample Size

To avoid misleading results from categories with very few anime, only source categories with at least 100 anime were considered for comparison.

This reduced the impact of unusually high or low averages caused by small sample sizes.

---

## Data Quality Investigation

During analysis, several anime entries were found with:

* `score = 0`
* `scored_by = 0`

These entries were not poorly rated anime. Instead, they appeared to represent anime that had not received any ratings.

Example:

```text
score = 0
scored_by = 0
```

Because these entries were included in average calculations, they lowered the mean score of some source categories.

---

## Mean vs Median Comparison

The median score for several source categories was higher than the mean score.

Example:

| Source   | Mean | Median |
| -------- | ---- | ------ |
| Original | 5.74 | 5.97   |

This indicated that unusually low values (mainly score = 0 entries) were pulling averages downward.

---

## Recalculating After Cleaning

A cleaned dataset was created by removing entries with:

```python
score > 0
```

After recalculating averages:

| Source      | Cleaned Average Score |
| ----------- | --------------------- |
| Light Novel | 7.21                  |
| Manga       | 6.98                  |
| Original    | 5.90                  |

The averages increased and moved closer to their median values.

---

## Key Takeaways

* Light Novel adaptations achieved the highest average ratings among major source categories.
* Manga adaptations also performed strongly and consistently.
* Original anime showed lower average ratings despite having a large sample size.
* Entries with `score = 0` represented missing rating information rather than poor ratings.
* Mean values can be affected by missing or extreme values, making median an important metric for comparison.
* Data cleaning can significantly change analytical conclusions and should be performed before drawing final insights.



# Day 4 - Feature Investigation and Correlation Analysis

## Objective

Investigate which factors appear to be related to anime scores and identify potentially useful features for future machine learning models.

---

## Data Cleaning

Before analysis, anime entries with a score of `0` were removed.

Reason:

* A score of `0` often corresponded to `scored_by = 0`
* This indicated missing ratings rather than extremely low ratings
* Keeping these entries would distort averages and correlations

```python
df_clean = df[df["score"] > 0]
```

---

## Correlation with Anime Score

| Feature   | Correlation with Score |
| --------- | ---------------------- |
| Members   | 0.380                  |
| Scored By | 0.345                  |
| Favorites | 0.206                  |
| Episodes  | 0.092                  |

### Findings

* Member count showed the strongest relationship with score.
* Favorites had a weaker relationship than expected.
* Episode count showed almost no relationship with score.
* Popularity appears to matter more than episode length.

---

## Members vs Score

Correlation: **0.380**

### Observation

* Anime with low member counts had scores across the entire range.
* Highly popular anime were rarely poorly rated.
* Popularity does not guarantee a high score, but highly popular anime tend to avoid very low scores.

---

## Favorites vs Score

Correlation: **0.206**

### Observation

* A positive relationship exists, but it is relatively weak.
* Being heavily favorited does not automatically result in a high score.
* Favorites may capture emotional attachment rather than overall rating quality.

---

## Episodes vs Score

Correlation: **0.092**

### Observation

* Episode count showed almost no relationship with score.
* Both short and long anime can receive high or low ratings.
* Anime length alone is not a useful predictor of score.

---

## Type Analysis

Average scores by anime type:

| Type    | Average Score |
| ------- | ------------- |
| TV      | 6.777         |
| Special | 6.364         |
| OVA     | 6.252         |
| Movie   | 6.227         |
| ONA     | 5.557         |
| Music   | 5.177         |

### Findings

* TV anime achieved the highest average score.
* Music anime had the lowest average score.
* TV series appear to perform better overall than other release formats.

---

## Source Material Analysis

Average scores by source material:

Top sources:

| Source       | Average Score |
| ------------ | ------------- |
| Light Novel  | 7.210         |
| Manga        | 6.975         |
| Novel        | 6.843         |
| 4-koma Manga | 6.798         |

Lower-scoring sources:

| Source | Average Score |
| ------ | ------------- |
| Music  | 5.251         |
| Radio  | 5.489         |
| Other  | 5.750         |

### Findings

* Source material appears to influence scores more strongly than anime type.
* Adaptations from Light Novels, Manga, and Novels generally performed better.
* Music and Radio-based projects tended to receive lower scores.

---

## Correlation Matrix Analysis

Strongest correlations:

| Variables             | Correlation |
| --------------------- | ----------- |
| Members ↔ Scored By   | 0.987       |
| Favorites ↔ Scored By | 0.792       |
| Members ↔ Favorites   | 0.777       |

### Findings

* Members and Scored By are almost identical measures of popularity.
* Anime with larger audiences naturally receive more ratings.
* Members, Favorites, and Scored By form a "popularity cluster" of features.
* Episode count showed almost no relationship with any major variable.

---

## Conclusion

The strongest indicators related to anime scores were popularity-based features such as Members and Scored By.

Episode count contributed very little information and showed weak relationships with both score and popularity.

For future machine learning experiments, Members, Favorites, Scored By, Type, and Source appear to be promising features, while Episode Count may provide limited predictive value.
