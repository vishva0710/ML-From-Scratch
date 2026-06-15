# K-Means Clustering in Machine Learning

## What is K-Means Clustering?

K-Means is one of the most popular Unsupervised Machine Learning algorithms used to group similar data points into clusters.

The algorithm divides the dataset into **K clusters**, where **K** is specified by the user before training.

The goal of K-Means is to ensure that data points within the same cluster are as similar as possible while data points in different clusters are as different as possible.

---

# Why Do We Need K-Means?

Many real-world datasets do not contain labels or categories. K-Means helps discover hidden groups in such data.

### Example

Suppose a shopping mall has customer information:

* Age
* Annual Income
* Spending Score

The mall does not know which customers are:

* High Spenders
* Medium Spenders
* Low Spenders

K-Means can automatically group customers into these categories.

---

# How K-Means Works

## Step 1: Choose K

Select the number of clusters.

Example:

```text
K = 2
```

This means we want the algorithm to create 2 clusters.

---

## Step 2: Select Initial Centroids

A centroid is the center point of a cluster.

Suppose K-Means randomly chooses:

```text
Centroid 1 = 15
Centroid 2 = 85
```

---

## Step 3: Calculate Distance

Dataset:

| Customer | Spending Score |
| -------- | -------------- |
| A        | 10             |
| B        | 15             |
| C        | 20             |
| D        | 80             |
| E        | 85             |
| F        | 90             |

Calculate the distance of each point from the centroids.

| Customer | Value | Distance to 15 | Distance to 85 |
| -------- | ----- | -------------- | -------------- |
| A        | 10    | 5              | 75             |
| B        | 15    | 0              | 70             |
| C        | 20    | 5              | 65             |
| D        | 80    | 65             | 5              |
| E        | 85    | 70             | 0              |
| F        | 90    | 75             | 5              |

---

## Step 4: Assign Data Points to the Nearest Centroid

### Cluster 1

```text
10
15
20
```

### Cluster 2

```text
80
85
90
```

---

## Step 5: Calculate New Centroids

### Cluster 1

Average:

```text
(10 + 15 + 20) / 3 = 15
```

### Cluster 2

Average:

```text
(80 + 85 + 90) / 3 = 85
```

New Centroids:

```text
15 and 85
```

---

## Step 6: Repeat

The algorithm repeats the process until centroids stop changing.

If the old and new centroids are the same, training stops.

---

# Final Clusters

### Cluster 1 (Low Spenders)

```text
10
15
20
```

### Cluster 2 (High Spenders)

```text
80
85
90
```

---

# Real-World Applications of K-Means

## 1. Customer Segmentation

Group customers based on:

* Income
* Spending Habits
* Purchase Frequency

Used for personalized marketing.

---

## 2. Student Performance Analysis

Group students based on:

* Marks
* Attendance
* Assignment Scores

Used to identify top performers and students needing support.

---

## 3. Healthcare

Group patients with similar symptoms or medical histories.

Used for disease pattern analysis.

---

## 4. E-Commerce

Group products with similar sales behavior.

Used for inventory management and recommendations.

---

## 5. Image Segmentation

Group similar pixels together.

Used in computer vision and image processing.

---

# Advantages of K-Means

* Easy to understand and implement
* Fast and efficient
* Works well on large datasets
* Widely used in industry
* Produces meaningful clusters

---

# Limitations of K-Means

* Must choose K beforehand
* Sensitive to outliers
* Different initial centroids can produce different results
* Assumes clusters are roughly spherical

---

# Choosing the Best Value of K

One of the biggest challenges in K-Means is deciding the optimal number of clusters.

Two commonly used methods are:

1. Elbow Method
2. Silhouette Score

---

# Elbow Method

The Elbow Method helps identify the best value of K by analyzing the relationship between:

* Number of Clusters (K)
* WCSS (Within Cluster Sum of Squares)

---

## What is WCSS?

WCSS measures the distance between data points and their cluster centroid.

* Lower WCSS indicates better clustering.
* Higher WCSS indicates poor clustering.

---

## Example

| K | WCSS |
| - | ---- |
| 1 | 1000 |
| 2 | 600  |
| 3 | 350  |
| 4 | 250  |
| 5 | 200  |
| 6 | 180  |

As K increases, WCSS decreases.

The point where the decrease becomes less significant is called the **Elbow Point**.

Example:

```text
Best K = 3
```

---

# Silhouette Score

The Silhouette Score measures how well a data point fits within its own cluster compared to other clusters.

The score ranges from:

```text
-1 to +1
```

---

## Interpretation

| Score     | Meaning              |
| --------- | -------------------- |
| +1        | Excellent Clustering |
| 0.7 - 0.9 | Very Good            |
| 0.5 - 0.7 | Good                 |
| Around 0  | Overlapping Clusters |
| Negative  | Poor Clustering      |

---

## Example

| K | Silhouette Score |
| - | ---------------- |
| 2 | 0.52             |
| 3 | 0.71             |
| 4 | 0.65             |
| 5 | 0.55             |

Highest Score:

```text
0.71
```

Therefore:

```text
Best K = 3
```

---

# Elbow Method vs Silhouette Score

| Feature            | Elbow Method | Silhouette Score         |
| ------------------ | ------------ | ------------------------ |
| Purpose            | Find Best K  | Evaluate Cluster Quality |
| Metric             | WCSS         | Silhouette Coefficient   |
| Output             | Elbow Point  | Score (-1 to +1)         |
| Easy to Understand | Yes          | Moderate                 |
| More Reliable      | No           | Usually Yes              |

---

# Best Practice

Data Scientists commonly follow this approach:

### Step 1

Use the Elbow Method to identify possible values of K.

### Step 2

Use the Silhouette Score to confirm the best K.

This combination often produces better clustering results.

---

# Summary

K-Means is one of the most widely used clustering algorithms in Machine Learning. It groups similar data points into clusters and is commonly used for customer segmentation, student analysis, healthcare, e-commerce, and image processing.

### Key Concepts

* K = Number of Clusters
* Centroid = Center of a Cluster
* WCSS = Measures Cluster Compactness
* Elbow Method = Helps Find Optimal K
* Silhouette Score = Evaluates Cluster Quality

Understanding K-Means, Elbow Method, and Silhouette Score is essential for mastering Unsupervised Learning and solving real-world clustering problems.
