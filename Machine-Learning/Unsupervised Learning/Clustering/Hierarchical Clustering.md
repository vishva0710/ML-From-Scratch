# Hierarchical Clustering in Machine Learning

## What is Hierarchical Clustering?

Hierarchical Clustering is an Unsupervised Machine Learning algorithm used to group similar data points into clusters by building a hierarchy of clusters.

Unlike K-Means Clustering, Hierarchical Clustering does not require specifying the number of clusters at the beginning.

The result is represented using a tree-like structure called a **Dendrogram**.

---

# Why Do We Need Hierarchical Clustering?

Hierarchical Clustering helps identify natural groupings in data when the number of clusters is unknown.

### Real-World Example

Suppose a school wants to group students based on:

* Marks
* Attendance
* Assignment Scores

The school does not know how many groups exist.

Hierarchical Clustering can automatically build groups and help identify:

* Top Performers
* Average Students
* Students Needing Improvement

---

# How Hierarchical Clustering Works

Consider the following dataset:

| Student | Marks |
| ------- | ----- |
| A       | 10    |
| B       | 12    |
| C       | 15    |
| D       | 80    |
| E       | 85    |

---

## Step 1: Treat Every Data Point as a Separate Cluster

Initially:

```text
[A] [B] [C] [D] [E]
```

Total Clusters = 5

---

## Step 2: Find the Closest Pair

Calculate distances:

| Pair | Distance |
| ---- | -------- |
| A-B  | 2        |
| A-C  | 5        |
| A-D  | 70       |
| A-E  | 75       |
| B-C  | 3        |
| B-D  | 68       |
| B-E  | 73       |
| C-D  | 65       |
| C-E  | 70       |
| D-E  | 5        |

Smallest Distance:

```text
A-B = 2
```

Merge:

```text
[AB] [C] [D] [E]
```

---

## Step 3: Find the Closest Pair Again

Using Single Linkage:

### AB-C

```text
A-C = 5
B-C = 3

Minimum = 3
```

### AB-D

```text
A-D = 70
B-D = 68

Minimum = 68
```

### AB-E

```text
A-E = 75
B-E = 73

Minimum = 73
```

Smallest Distance:

```text
AB-C = 3
```

Merge:

```text
[ABC] [D] [E]
```

---

## Step 4: Continue the Process

### ABC-D

```text
A-D = 70
B-D = 68
C-D = 65

Minimum = 65
```

### ABC-E

```text
A-E = 75
B-E = 73
C-E = 70

Minimum = 70
```

### D-E

```text
|80 - 85| = 5
```

Smallest Distance:

```text
D-E = 5
```

Merge:

```text
[ABC] [DE]
```

---

## Step 5: Final Merge

Calculate:

### ABC-DE

```text
A-D = 70
A-E = 75
B-D = 68
B-E = 73
C-D = 65
C-E = 70

Minimum = 65
```

Merge:

```text
[ABCDE]
```

Algorithm Stops.

---

# Dendrogram

The complete clustering process can be represented as:

```text
                 ABCDE
                 /   \
               ABC   DE
              / | \  / \
             A  B  C D  E
```

This tree structure is called a **Dendrogram**.

---

# What is a Dendrogram?

A Dendrogram is a tree-like diagram that shows how clusters are merged during Hierarchical Clustering.

It helps determine the optimal number of clusters.

### Example

If we cut the dendrogram here:

```text
                 ABCDE
                 /   \
        ---------     ---------
               ABC   DE
              / | \  / \
             A  B  C D  E
```

Result:

```text
Cluster 1 = {A, B, C}

Cluster 2 = {D, E}
```

Therefore:

```text
K = 2
```

---

# Types of Hierarchical Clustering

## 1. Agglomerative Clustering

Also known as the Bottom-Up approach.

### Process

```text
Individual Points
       ↓
Merge Closest Clusters
       ↓
Repeat
       ↓
One Final Cluster
```

Example:

```text
[A] [B] [C] [D] [E]
      ↓
[AB] [C] [D] [E]
      ↓
[ABC] [D] [E]
      ↓
[ABC] [DE]
      ↓
[ABCDE]
```

This is the most commonly used Hierarchical Clustering method.

---

## 2. Divisive Clustering

Also known as the Top-Down approach.

### Process

```text
[ABCDE]
      ↓
[ABC] [DE]
      ↓
[A] [B] [C] [D] [E]
```

Less commonly used in practice.

---

# Linkage Methods

Linkage methods determine how the distance between clusters is calculated.

---

## 1. Single Linkage

Uses the minimum distance between points.

### Formula

```text
Distance = Minimum Distance
```

Example:

```text
AB-C

A-C = 5
B-C = 3

Minimum = 3
```

---

## 2. Complete Linkage

Uses the maximum distance between points.

### Formula

```text
Distance = Maximum Distance
```

Example:

```text
AB-C

A-C = 5
B-C = 3

Maximum = 5
```

---

## 3. Average Linkage

Uses the average distance between points.

### Formula

```text
Distance = Average Distance
```

Example:

```text
AB-C

(5 + 3) / 2 = 4
```

---

## 4. Ward Linkage

The most commonly used linkage method.

It minimizes the variance within clusters and produces compact clusters.

Scikit-Learn uses Ward linkage by default.

---

# Real-World Applications

## Customer Segmentation

Group customers based on:

* Income
* Spending Habits
* Purchase History

---

## Student Performance Analysis

Group students based on:

* Marks
* Attendance
* Assignments

---

## Healthcare

Group patients with similar symptoms and medical histories.

---

## Document Clustering

Group similar articles, reports, or documents.

---

## Image Segmentation

Group similar pixels together for image analysis.

---

# Advantages

* No need to choose K initially
* Easy to visualize using dendrograms
* Works well for small datasets
* Reveals hierarchical relationships

---

# Limitations

* Computationally expensive
* Slow for large datasets
* Sensitive to noise and outliers
* Difficult to update when new data arrives

---

# Hierarchical Clustering vs K-Means

| Feature                | Hierarchical Clustering | K-Means |
| ---------------------- | ----------------------- | ------- |
| Need K Before Training | No                      | Yes     |
| Dendrogram Support     | Yes                     | No      |
| Speed                  | Slower                  | Faster  |
| Large Datasets         | Not Ideal               | Better  |
| Cluster Visualization  | Excellent               | Limited |

---

# Python Implementation

```python
from sklearn.cluster import AgglomerativeClustering

hc = AgglomerativeClustering(
    n_clusters=5,
    linkage='ward'
)

y_pred = hc.fit_predict(X)
```

Add cluster labels:

```python
df['Cluster'] = y_pred
```

---

# Summary

Hierarchical Clustering is an unsupervised learning algorithm that builds clusters step by step by merging or splitting data points.

### Key Concepts

* Hierarchical Clustering
* Dendrogram
* Agglomerative Clustering
* Divisive Clustering
* Single Linkage
* Complete Linkage
* Average Linkage
* Ward Linkage

### Workflow

```text
Each Point = Separate Cluster
            ↓
Find Closest Pair
            ↓
Merge Clusters
            ↓
Repeat Process
            ↓
Create Dendrogram
            ↓
Choose Number of Clusters
```

Hierarchical Clustering is widely used for customer segmentation, student analysis, healthcare analytics, document clustering, and image segmentation.
