# Spotify Music Analysis

## Project Overview

This project analyzes Spotify track data using exploratory data analysis, machine learning, and clustering. The goal is to understand patterns in Spotify audio features, predict track popularity, and group similar songs based on their audio characteristics.

## Project Goals

- Explore the structure of the Spotify dataset
- Analyze numerical and categorical audio features
- Identify patterns related to track popularity
- Build machine learning models to predict popularity
- Use clustering to group similar tracks based on audio features
- Interpret the results in a clear and meaningful way

## Dataset

The dataset contains Spotify track information, including song metadata, popularity scores, genre labels, and audio features.

Some of the main features include:

- `popularity`
- `duration_ms`
- `danceability`
- `energy`
- `loudness`
- `speechiness`
- `acousticness`
- `instrumentalness`
- `liveness`
- `valence`
- `tempo`
- `explicit`
- `track_genre`

## Tools and Libraries Used

- Python
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- VS Code
- Jupyter Notebook

## Project Structure

```text
Spotify/
│
├── dataset.csv
├── spotify_analysis.ipynb
├── README.md
├── requirements.txt
│
└── outputs/
    └── spotify_final_with_clusters.csv
```

## Exploratory Data Analysis

During exploratory data analysis, I examined the structure of the dataset, checked for missing values and duplicates, and analyzed both numerical and categorical features.

The EDA process included:

- Checking dataset shape, column names, and data types

- Removing missing values

- Removing fully duplicated rows

- Checking duplicated track IDs

- Analyzing the distribution of track popularity

- Exploring the number of tracks by genre

- Analyzing categorical features such as explicit content, key, mode, and time signature

- Visualizing numerical audio feature distributions

- Creating a correlation heatmap

The numerical feature distributions showed that some features, such as `speechiness`, `instrumentalness`, and `liveness`, were strongly right-skewed. The `duration_ms` feature also contained long-duration outliers, so I created a more interpretable duration feature in minutes.

The correlation heatmap showed that popularity had weak linear correlations with individual numerical audio features. This suggests that track popularity may depend on more complex relationships and external factors, not just one audio characteristic.

## Feature Engineering

I created a new feature called `duration_min` by converting track duration from milliseconds to minutes:

```python

df["duration_min"] = df["duration_ms"] / 60000

```

This made duration easier to interpret in visualizations, clustering, and machine learning.

## Machine Learning

The machine learning goal was to predict the numerical `popularity` score of a track. Since the target variable is numerical, this is a regression problem.

I compared two regression models:

1. Linear Regression

2. Random Forest Regressor

Linear Regression was used as a baseline model. Random Forest was used as a more flexible model that can capture non-linear relationships and interactions between features.

## Model Results

| Model | MAE | RMSE | R² Score |

|---|---:|---:|---:|

| Linear Regression | 14.23 | 19.39 | 0.25 |

| Random Forest | 10.46 | 15.54 | 0.52 |

The Random Forest model performed better than Linear Regression. It had a lower MAE and RMSE, meaning its predictions were closer to the actual popularity scores. It also had a higher R² score, explaining about 52% of the variation in track popularity.

## Feature Importance

After training the Random Forest model, I analyzed feature importance to understand which variables contributed most to the model's predictions.

The most important features included:

- acousticness

- duration

- loudness

- tempo

- valence

- speechiness

- danceability

- energy

- liveness

- instrumentalness

- selected genre categories

The feature importance results showed that the model used a combination of audio features and genre-related variables. No single feature completely dominated the predictions.

## Clustering

I used K-Means clustering to group tracks based on their numerical audio features. Clustering is an unsupervised learning method, meaning no target variable was used.

The clustering process included:

- Selecting numerical audio features

- Scaling features using `StandardScaler`

- Using the elbow method to choose the number of clusters

- Training a K-Means model

- Assigning cluster labels to tracks

- Analyzing average audio features by cluster

- Comparing average popularity by cluster

- Visualizing clusters using PCA

The elbow method suggested using 7 clusters.

The clusters represented different types of tracks, such as:

- calm acoustic/instrumental tracks

- energetic instrumental tracks

- loud energetic vocal tracks

- live-sounding tracks

- upbeat danceable tracks

- speech-heavy tracks

- mellow acoustic tracks

Popularity was not used to create the clusters. However, I compared average popularity by cluster afterward to see whether certain audio-based groups were associated with higher or lower popularity.

## Final Output

The final dataset with engineered features and cluster labels was saved as:

```text

outputs/spotify_final_with_clusters.csv

```

This final dataset includes the original Spotify track data along with additional columns such as:

- `duration_min`

- `cluster`

## Conclusion

This project demonstrates an end-to-end data science workflow using Spotify track data.

The project included:

- Data cleaning

- Exploratory data analysis

- Feature engineering

- Regression modeling

- Model comparison

- Feature importance analysis

- K-Means clustering

- PCA cluster visualization

The Random Forest model performed better than Linear Regression, suggesting that popularity is influenced by non-linear relationships between features. The clustering analysis also revealed meaningful groups of tracks based on audio characteristics.

Overall, this project shows how Spotify audio data can be used for exploration, prediction, and unsupervised grouping of similar songs.

## How to Run This Project

1. Clone or download this repository.

2. Install the required libraries:

```bash
pip install -r requirements.txt
```

3. Open the notebook:

```text
spotify_analysis.ipynb
```

4. Run the notebook cells from top to bottom.

5. The final processed dataset with cluster labels will be saved in:

```text
outputs/spotify_final_with_clusters.csv
```