# DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

## What is DBSCAN?

DBSCAN is an Unsupervised Machine Learning clustering algorithm that groups closely packed data points together and marks isolated points as noise (outliers).

Unlike K-Means Clustering, DBSCAN does not require specifying the number of clusters before training.

---

# Why Do We Need DBSCAN?

Consider the following data:

```text
Cluster A          Cluster B

● ● ● ●            ● ● ●
● ● ●              ● ● ●

                     x
```

K-Means will force the point `x` into a cluster.

DBSCAN identifies:

```text
x = Noise (Outlier)
```

This makes DBSCAN useful for anomaly and outlier detection.

---

# Key Parameters

DBSCAN uses two important parameters:

## 1. eps (ε)

The maximum distance between two points to be considered neighbors.

Example:

```text
eps = 2
```

Points within distance 2 are considered neighbors.

---

## 2. min_samples

Minimum number of neighboring points required to form a cluster.

Example:

```text
min_samples = 5
```

A point needs at least 5 neighbors to become a Core Point.

---

# Types of Points in DBSCAN

## 1. Core Point

A point that has at least `min_samples` neighbors within `eps`.

Example:

```text
● ● ●
● X ●
● ● ●
```

X has many nearby points.

Therefore:

```text
X = Core Point
```

Core Points can create and expand clusters.

---

## 2. Border Point

A point that does not have enough neighbors to become a Core Point but lies within the neighborhood of a Core Point.

Example:

```text
A ●

B ●   D ●──E ○

C ●
```

D is a Core Point.

E does not have enough neighbors to become a Core Point.

However, E is connected to D.

Therefore:

```text
E = Border Point
```

Border Points join existing clusters but cannot create new clusters.

---

## 3. Noise Point

A point that is not connected to any Core Point.

Example:

```text
● ● ●

          N
```

N has no nearby neighbors.

Therefore:

```text
N = Noise Point
```

Noise Points are assigned the label:

```text
-1
```

---

# Simple Step-by-Step Example

Dataset:

```text
A(1,1)
B(1,2)
C(2,1)

D(8,8)
E(8,9)
F(9,8)

G(20,20)
```

Parameters:

```text
eps = 2
min_samples = 3
```

---

## Step 1: Check Point A

Neighbors:

```text
A
B
C
```

Total neighbors:

```text
3
```

Since:

```text
3 >= min_samples
```

A becomes a Core Point.

Create:

```text
Cluster 1 = {A, B, C}
```

---

## Step 2: Check Point D

Neighbors:

```text
D
E
F
```

Total neighbors:

```text
3
```

D becomes a Core Point.

Create:

```text
Cluster 2 = {D, E, F}
```

---

## Step 3: Check Point G

Neighbors:

```text
Only G
```

Total neighbors:

```text
1
```

Since:

```text
1 < min_samples
```

G cannot form a cluster.

Therefore:

```text
G = Noise Point
```

---

# Final Result

```text
Cluster 1:
A B C

Cluster 2:
D E F

Noise:
G
```

Visualization:

```text
● ●
●


       ● ●
       ●


                  x
```

where:

```text
x = Noise
```

---

# DBSCAN Workflow

```text
1. Select eps and min_samples

2. Pick a point

3. Find neighboring points within eps

4. If neighbors >= min_samples
      → Core Point
      → Create Cluster

5. Expand cluster using connected Core Points

6. Add Border Points to the cluster

7. Points that do not belong to any cluster
      → Noise (-1)
```

---

# Advantages of DBSCAN

* No need to specify the number of clusters
* Detects outliers automatically
* Works well with irregular cluster shapes
* Can discover clusters of arbitrary shape

---

# Limitations of DBSCAN

* Choosing eps can be difficult
* Struggles with clusters of varying densities
* Performance decreases on very high-dimensional data

---

# Real-World Applications

## Fraud Detection

Detect unusual transactions.

Example:

```text
Normal Transactions → Cluster

Suspicious Transaction → Noise
```

---

## Network Security

Detect abnormal network activity.

Example:

```text
Normal Traffic → Cluster

Attack Traffic → Noise
```

---

## GPS and Location Analysis

Group nearby locations.

Examples:

* Restaurants
* Tourist Attractions
* Delivery Zones

---

## Customer Segmentation

Identify groups of customers with similar behavior and detect unusual customers.

---

## Anomaly Detection

Find abnormal records in datasets.

Examples:

* Banking
* Healthcare
* Cybersecurity

---

# Python Implementation

```python
from sklearn.cluster import DBSCAN

dbscan = DBSCAN(
    eps=0.5,
    min_samples=5
)

labels = dbscan.fit_predict(X_scaled)

print(labels)
```

Example Output:

```text
0 0 0 1 1 1 -1
```

Meaning:

```text
0  → Cluster 1
1  → Cluster 2
-1 → Noise Point
```

---

# DBSCAN vs K-Means vs Hierarchical Clustering

| Feature          | K-Means | Hierarchical | DBSCAN    |
| ---------------- | ------- | ------------ | --------- |
| Need K           | Yes     | No           | No        |
| Detect Outliers  | No      | No           | Yes       |
| Dendrogram       | No      | Yes          | No        |
| Irregular Shapes | Poor    | Medium       | Excellent |
| Speed            | Fast    | Slow         | Medium    |

---
