# ClusterAnalysisProject
TravelTide Rewards Program Analysis

## Project Overview

This repository, hosted at FichtnerLukas/ClusterAnalysisProject, contains the 1_traveltide_clustering_ipynb(1).py script for TravelTide's customer segmentation project. The analysis supports the marketing department’s rewards program by validating proposed perks (free hotel meal, free checked bag, no cancellation fees, exclusive discounts, one night free hotel with flight) and segmenting customers into distinct groups based on travel behavior and demographics to personalize email invitations for increased sign-ups.

## Objectives
- Validate the effectiveness of proposed rewards program perks.
- Segment customers into meaningful clusters to identify their preferred perks.
- Provide data-driven insights for personalized email campaigns to boost program enrollment.

## Dataset
The data is sourced from TravelTide’s PostgreSQL database, including:

- Flights: Flight bookings with base fare, discounts, and airport coordinates.
- Hotels: Hotel bookings with price per room night, nights, and discounts.
- Sessions: User session data, including page clicks, session duration, and booking details.
- Users: Demographic information, including age, gender, marital status, and home country.

## Methodology
1. Data Loading and Cleaning:
   
- Connected to a PostgreSQL database using SQLAlchemy.
- Filtered sessions post-January 4, 2023, for active users (>7 sessions).
- Merged datasets, handled missing values (e.g., filled zeros for discounts), and corrected negative nights by swapping check-in/check-out dates.
- Standardized country names (e.g., 'usa' → 'USA', 'canada' → 'Canada').

2. Feature Engineering:

- Flight Features: Calculated distance flown (geodesic), number of flights, and flight spend with discounts.
- Hotel Features: Computed hotel spend based on nights, rooms, and discounts.
- Trip Features: Derived trip duration and lead time to booking.
- User Features: Aggregated session duration, page clicks, and demographics (e.g., age, travel type: Family, Business, Leisure).

3. Exploratory Data Analysis (EDA):

- Visualized user demographics (home country, age by gender).
- Analyzed correlations between spending and travel distance.

4. Clustering:

- Standardized numeric features using StandardScaler.
- Applied PCA for 2D visualization.
- Used K-Means clustering (k=5, determined via silhouette scores and elbow method).
- Visualized clusters and summarized characteristics.

5. Post_clustering Analysis:

- Analyzed spending, trip duration, and discount usage by cluster.
- Identified outliers in distance flown and spending patterns by gender/marital status.

## Key Findings

Five customers segments were identified:
1. High-Spending, Long-Distance Frequent Flyers (15%): High spend ($13K+), long-haul flights (7,780 km). Likely to value exclusive discounts and no cancellation fees.
2. Mid-Tier, Multi-Trip Travelers (25%): Moderate spend ($4.3K), frequent trips. Prefer free hotel meals and one night free hotel with flight.
3. Budget-Conscious, Infrequent Travelers (30%): Low spend ($2.2K), short trips. Favor free checked bags.
4. Low-Engagement Occasional Travelers (20%): Minimal spend ($102), last-minute bookings. Prefer no cancellation fees.
5. Luxury Experience Seekers (10%): High hotel spend ($2.6K). Value one night free hotel with flight and exclusive discounts.

## Dependencies

- Python 3.8+
- Libraries: pandas, numpy, matplotlib, seaborn, sqlalchemy, geopy, sklearn
- PostgreSQL database access (credentials required)


# Setup Instructions

## Clone the repository:

git clone https://github.com/FichtnerLukas/ClusterAnalysisProject.git
cd ClusterAnalysisProject

## Install dependencies:

pip install -r requirements.txt


## Update database connection parameters in 1_traveltide_clustering_ipynb(1).py:

- username = 'your_username'
- password = 'your_password'
- host = 'your_host'
- port = 'your_port'
- database = 'your_database'

## Run the script:

python 1_traveltide_clustering_ipynb(1).py

## File Structure
- 1_traveltide_clustering_ipynb(1).py: Main script for data loading, cleaning, feature engineering, EDA, and clustering.
- README.md: This file, providing project documentation.
- requirements.txt: List of required Python libraries (create manually if needed).

## Outputs
- Cluster Assignments: Added as a cluster column in the final DataFrame.
- Visualizations: Inline plots (e.g., cluster scatter plots, boxplots of spending, histograms of discounts).
- CSV Export: Option to export the final DataFrame (final_df.csv) for Tableau or further analysis (commented out).


## Usage
The script generates a final DataFrame (final_df) with customer segments and features, enabling personalized marketing strategies. Use the cluster profiles to tailor email campaigns, emphasizing each segment’s preferred perk.

## Future Improvements
- Incorporate additional features (e.g., loyalty program interactions, seasonal trends).
- Test alternative clustering algorithms (e.g., DBSCAN, hierarchical clustering).
- Automate perk assignment using predictive modeling for real-time personalization.


