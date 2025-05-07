# Predicting Filming Locations: Thematic & Geospatial Influences in San Francisco 5/7/2025

Parth Rathi

This work was realized as part of the capstone project of the MS in Data Science at Pace University

Abstract: Filming locations are chosen based on a combination of script
requirements, budget, lighting, and iconography. Iconography in film—
the use of recurring visual symbols and motifs—shapes audience
perception and emotional engagement. This study explores the extent to
which genre, plot elements, and tourist traps influence filming location
choices in San Francisco by building a predictive clustering model.
Using Random Forest (RF) and XGBoost (XGB), we analyze factors
that contribute to location selection, including proximity to tourist
landmarks and genre-driven thematic significance. Results show that
XGB significantly outperforms RF, capturing nuanced location
characteristics more effectively.

Dataset: 
Source: San Francisco’s Open Data Portal (DataSF)
• Size: 2022 filming location records (movies & TV shows)
• Raw Features: Title, year, director, actors, location
• Feature Engineering: IMDb API scraping for missing metadata (ID,
ratings, genres, plot summary), Longitude/latitude verification due to
mismatches with described locations, Tourist proximity calculation
via geopy (min_distance_to_tourist_spot, is_tourist_spot), Location
clustering using DBSCAN and NearestNeighbors
• Final dataset: 1984 processed rows

The dataset is available here: [https://data.sfgov.org/Culture-and-Recreation/Film-Locations-in-San-Francisco/yitu-d5am/about_data]

Methodology: 
Predictive Modeling Approach:
• Built baseline location predictor using Random Forest (RF) and
XGBoost (XGB)
• RF ensures stability and interpretability, while XGB optimizes
accuracy and handles complexity
• Selected features: one-hot encoded genres, vectorized plot
summaries, normalized IMDb ratings, longitude, latitude, release
year, tourist proximity
• Target variable: location_cluster
Model Implementation:
RF:
• Grid Search for tuning (n_estimators, max_depth)
• Predictions via predict_proba()
XGB:
• Grid Search for tuning (learning_rate, max_depth, subsample)
• Trained with multi-class softmax objective

Results: 

<img width="549" alt="Screenshot 2025-05-07 at 10 52 21 AM" src="https://github.com/user-attachments/assets/a72f7e61-d391-40c2-8c5d-333f3be4b7a9" />

<img width="468" alt="Screenshot 2025-05-07 at 10 52 29 AM" src="https://github.com/user-attachments/assets/6090b9ff-6a0d-4c1d-a692-dc263e47803f" />

• XGB significantly outperforms RF (accuracy: 0.83 vs. 0.42)
• RF confidently distinguishes high-AUC clusters (AUC = 1.00), but
performance declines for sparse clusters (e.g., 3 vs. 16 points)
• XGB maintains high predictability (AUC = 0.99), demonstrating
superior performance across clusters
• Hyperparameter tuning improves XGB’s accuracy, with low learning
rate (0.01) and shallow depth (3)
• XGB effectively handles class imbalance (high TPR & low FPR),
making it more reliable for edge cases
• RF’s best-predicted clusters aren’t necessarily the most frequent filming
locations, suggesting location selection isn’t solely volume-driven
• Key predictors beyond location: Adventure genre and
min_distance_to_tourist_spot heavily influence clustering

Limitations: Lack of real data to draw specific conclusions & time to test other models.
