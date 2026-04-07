# Retail-Affinity-Analytics-Engine
# Retail Affinity Analytics & Recommendation Engine

**Author:** Karla Acevedo  
**Course:** MSIN0312 Programming for Analytics  

## Executive Summary
This repository contains the codebase and methodology for a comprehensive study into retail transaction data. The project utilizes cross-category affinity analysis at both the department and commodity levels to identify unexpected cross-selling opportunities. Additionally, it evaluates the causal impact of promotions and physical co-displaying on high-affinity pairs. Finally, K-means clustering was applied to segment households, and a recommendation algorithm was designed and tested to maximize online retail sales.

## Methodology & Technical Approach

### 1. Data Processing & Basket Formation
* Processed `transaction_data.csv` by grouping purchase receipt lines by basket ID, retaining data on household, day of sale, quantity, and combined sales value.
* Applied noise-reduction filtering by excluding baskets with fewer than 3 items or a total sales value under $10.
* Merged transaction records with product datasets to categorize items by department and commodity levels.
* Iterated through meaningful baskets to generate all unique product ID combinations, setting a lower frequency limit of 20 to isolate persistent affinities.

### 2. Affinity Metrics
Calculated three core metrics to establish item relationships:
* **Support:** The percentage of baskets containing a specific product pair[cite: 4].
* **Confidence:** The probability of purchasing the second product in a pair given the first was purchased.
* **Lift:** How much more likely the second product is to be purchased relative to its baseline probability.
* *Note: Outlier lifts were eliminated to prevent distortion, and an Anchor Score was calculated combining breadth, volume, and affinity strength.*

### 3. Promotional Impact & Causal Inference
* Integrated `causal_data.csv` to flag transactions where products were actively promoted via display or mailer.
* **Halo Effect:** Calculated incremental partner revenue per basket, revealing that promoting anchor commodities drives incremental revenue in their highest affinity partner commodities.
* **Co-Display Lift:** Proven hypothesis that physically displaying high-affinity categories together (e.g., fresh produce pairings) increases combined purchase probability.

### 4. Customer Segmentation (K-Means Clustering)
Applied a K-means clustering algorithm grouped by household to categorize purchase behaviors. Features used included average basket size, total spend, average basket value, average department diversity, and weekly trip frequency.
* **Cluster 0 (Weekly Stock-Up):** High frequency, moderate basket size, high total spend.
* **Cluster 1 (Occasional Light):** Infrequent shoppers, smallest baskets, lowest value.
* **Cluster 2 (Moderate Regulars):** Medium frequency, broad department diversity, moderate spend.
* **Cluster 3 (Big Basket):** Low frequency, largest baskets, highest spend per trip.

### 5. Recommendation Engine Prototype
* Developed a predictive algorithm logic to maximize online sales by recommending items based on a user's current basket composition.
* The algorithm retrieves high-affinity commodity partners and calculates an affinity score (Confidence × Lift) to rank recommendations.
* **Performance:** Tested using a "hidden item" hit-rate logic, successfully matching customer preference with a 6.2% hit rate when the top 6 recommendations were displayed.

## Key Business Recommendations
* **Cross-Merchandising:** Promoting baked bread drives significant incremental meat purchases ($0.15-0.35 per basket); prioritize bread promotions during barbecue season.
* **Display Optimization:** Tropical fruit and pears/tomatoes/berries pairings benefit strongly from physical proximity; place them together in produce displays.
* **Targeted Bundling:** Bundle frozen items with fresh produce for the "Occasional Light" segment targeting "quick meal" messaging. Promote bulk nutrition bundles with health-oriented anchor promotions for the "Big Basket" segment.

## Data Privacy Note
*Note: The raw datasets (`transaction_data.csv` and `causal_data.csv`) contain proprietary retail information and have been excluded from this public repository.*
