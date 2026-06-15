# Unsupervised Learning in Machine Learning

## What is Unsupervised Learning?

Unsupervised Learning is a type of Machine Learning where the model learns patterns, structures, or relationships from data without any labeled target variable.

Unlike Supervised Learning, there is no correct output provided to the model. The algorithm explores the data and discovers hidden patterns on its own.

### Example

Suppose a shopping mall has customer data containing:

- Age
- Annual Income
- Spending Score

The mall does not know which customers belong to which category. An unsupervised learning algorithm can automatically group customers into different segments such as:

- High Income – High Spending
- High Income – Low Spending
- Low Income – High Spending
- Low Income – Low Spending

This process is called **Clustering**.

---

# Types of Unsupervised Learning

## 1. Clustering

Clustering is the process of grouping similar data points together.

### Real-World Applications

- Customer Segmentation
- Student Performance Analysis
- Document Classification
- Image Segmentation
- Social Network Analysis

### Popular Algorithms

- K-Means Clustering
- Hierarchical Clustering
- DBSCAN

---

## 2. Association Rule Learning

Association Rule Learning identifies relationships between items in a dataset.

### Real-World Applications

- Market Basket Analysis
- Product Recommendation Systems
- Cross-Selling Strategies
- Online Shopping Recommendations

### Example

Customers who buy:

- Bread
- Milk

may also buy:

- Butter

This relationship can help businesses improve product placement and recommendations.

### Popular Algorithms

- Apriori
- FP-Growth

---

## 3. Dimensionality Reduction

Dimensionality Reduction reduces the number of input features while preserving important information.

### Real-World Applications

- Data Visualization
- Faster Model Training
- Noise Reduction
- Feature Selection

### Popular Algorithms

- PCA (Principal Component Analysis)
- t-SNE

---

# Real-World Uses of Unsupervised Learning

## 1. Customer Segmentation

Grouping customers based on their behavior.

### Example

- High spenders
- Medium spenders
- Low spenders

**Algorithm:** K-Means

---

## 2. Recommendation Systems

Suggesting products, movies, or songs based on patterns.

### Example

- Amazon recommends products
- Netflix recommends movies

**Algorithms:** Apriori, FP-Growth

---

## 3. Fraud Detection

Finding unusual transactions or activities.

### Example

Detecting suspicious credit card transactions.

**Algorithm:** DBSCAN

---

## 4. Market Basket Analysis

Finding products that are frequently bought together.

### Example

- Bread + Milk
- Laptop + Mouse

**Algorithms:** Apriori, FP-Growth

---

## 5. Data Compression and Visualization

Reducing large datasets into fewer features.

### Example

- Compressing images
- Visualizing high-dimensional data

**Algorithm:** PCA

---

# Summary

Unsupervised Learning helps discover hidden patterns in unlabeled data. It is widely used for customer segmentation, recommendation systems, fraud detection, market basket analysis, and dimensionality reduction.

## Key Algorithms

| Algorithm  | Type                      | Common Use                      |
|------------|---------------------------|---------------------------------|
| K-Means    | Clustering                | Customer Segmentation           |
| Hierarchical Clustering                | Clustering | Student Grouping   |
| DBSCAN     | Clustering                | Fraud Detection                 |
| Apriori    | Association Rule Learning | Market Basket Analysis          |
| FP-Growth  | Association Rule Learning | Product Recommendations         |
| PCA        | Dimensionality Reduction  | Data Compression & Visualization|

## Conclusion

Unsupervised Learning is an important branch of Machine Learning that helps uncover hidden patterns and relationships in data without requiring labeled outputs. Understanding algorithms such as K-Means, DBSCAN, Apriori, FP-Growth, and PCA provides a strong foundation for solving real-world business and AI problems.