# EPL Match Outcome Prediction

This project aims to predict English Premier League (EPL) football match outcomes (win, draw, or loss) and the number of goals scored by home and away teams using machine learning techniques based on historical match statistics.

## Table of Contents

- [Project Overview](#project-overview)
- [Data](#data)
- [Methodology](#methodology)
- [Modeling and Results](#modeling-and-results)
- [Conclusion](#conclusion)

## Project Overview

Football match outcome prediction, especially in a competitive league like the English Premier League (EPL), is a challenging and interesting topic in sports data analytics. This research focuses on building a predictive model using match statistics to forecast the final results of EPL matches. The project utilizes various machine learning algorithms to evaluate prediction performance.

## Data

The dataset used in this project includes historical match statistics from the EPL, spanning seasons from 2000/01 up to 2024/25 (with partial data for 2024/25).

Key features in the dataset include:
- `Season`: Football season (e.g., '2000/01').
- `MatchDate`: Date of the match.
- `HomeTeam` and `AwayTeam`: Participating teams.
- `FullTimeHomeGoals` and `FullTimeAwayGoals`: Goals scored by home and away teams at full-time.
- `FullTimeResult`: Full-time match result (Home Win, Away Win, Draw).
- `HalfTimeHomeGoals` and `HalfTimeAwayGoals`: Goals scored by home and away teams at half-time.
- `HalfTimeResult`: Half-time match result.
- Various other statistics such as `Shots`, `ShotsOnTarget`, `Corners`, `Fouls`, `YellowCards`, and `RedCards` for both home and away teams.

The dataset contains 9380 entries with 22 columns.

## Methodology

The methodology involves several steps to preprocess the data, engineer relevant features, and build predictive models.

### Data Pre-processing

The raw dataset is considered clean. The data is split into training data (seasons before 2024/25) and testing data (2024/25 season). Additional match schedules for the 2024/25 season are added to the test set, with target columns set to `None` for future predictions.

### Feature Engineering

To enhance the model's predictive capability, a comprehensive feature engineering process was undertaken:
-   **Date Feature Extraction**: Match dates are converted to datetime objects.
-   **Historical Team Statistics**: Calculation of mean and standard deviation for various historical team statistics, including goals scored/conceded (home and away), shots, and shots on target.
-   **Attack and Defense Differences**: Features like `AttackDiff` and `DefenseDiff` are created to capture the relative strength between competing teams.
-   **Aggregate Goal Features**: `HomeTeam_HighScoring` is added to indicate the percentage of home matches where a team scored more than two goals, identifying high-scoring tendencies.
-   **Dataset Formation**: Team statistics for home and away teams are merged into single rows per match. Additional features like performance in the last five matches, current league points, and home/away status are incorporated to enrich the context.
-   **Target Label Encoding**: The `FullTimeResult` is encoded into three classes: 0 for away win, 1 for a draw, and 2 for home win. The dataset is then separated into features (X) and labels (y) for model training.
-   Missing numerical features are imputed with zeros to maintain consistency.

### Outlier Analysis

Outlier analysis was performed on numerical features in the training data (excluding the 2024/25 season) to identify extreme values using the Interquartile Range (IQR) method. Features like `AwayRedCards` (8.31%), `FullTimeHomeGoals` (7.80%), and `HomeRedCards` (5.96%) show the highest percentages of outliers.

### Exploratory Data Analysis (EDA)

Visualizations were generated to understand the data distribution:
-   **Distribution of Full-Time and Half-Time Match Results**: Count plots show the frequency of Home (H), Draw (D), and Away (A) results at both full-time and half-time.
-   **Distribution of Full-Time Goals**: Histograms illustrate the distribution of `FullTimeHomeGoals` and `FullTimeAwayGoals`, showing that home teams generally score more goals.
-   **Goals by Match Result (Boxplots)**: Boxplots visualize the relationship between individual numerical features (e.g., goals, shots, fouls, cards) and the `FullTimeResult`.
-   **Average Goals per Match by Season**: A line plot tracks the average total goals scored per match across different seasons, indicating trends over time.

## Modeling and Results

Regression models were trained to predict `FullTimeHomeGoals` and `FullTimeAwayGoals`. The features used in the model include attributes related to match time, historical team performance statistics, and offensive/defensive strengths.

The Root Mean Squared Error (RMSE) was used to evaluate the performance of various regression algorithms for predicting Home Goals:

| Model                   | Algorithm Type              | RMSE        |
| :---------------------- | :-------------------------- | :---------- |
| Ridge Regression        | Linear Regularization       | 1.277554    |
| Linear Regression       | Linear                      | 1.277588    |
| Gradient Boosting       | Boosting (Gradient)         | 1.287697    |
| Neural Network          | Non-linear (Neural Network) | 1.296628    |
| Lasso Regression        | Linear Regularization (L1)  | 1.305619    |
| SVR                     | Non-linear (Kernel-based)   | 1.310591    |

## Conclusion

The experimental results indicate that certain machine learning algorithms can achieve relatively high prediction accuracy for EPL match outcomes. The effectiveness of the feature engineering process, particularly the use of historical team statistics, was a significant finding. These models have the potential to serve as decision-making tools within sports analytics.