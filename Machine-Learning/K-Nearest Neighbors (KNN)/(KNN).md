# K-Nearest Neighbors (KNN) Algorithm

## What is KNN?

K-Nearest Neighbors (KNN) is a **Supervised Machine Learning Algorithm** used for:

- Classification
- Regression

Most commonly, KNN is used for **Classification**.

KNN predicts the class of a new data point by looking at the classes of its nearest neighbors.

---

# Why is KNN Called a Lazy Learning Algorithm?

Unlike Linear Regression or Logistic Regression, KNN does not learn any equation during training.

It simply stores:

```python
X_train
y_train
```

and performs calculations only when prediction is needed.

Therefore, KNN is called a **Lazy Learning Algorithm**.

---

# Training Phase

Suppose we have the following training data:

| Weight | Size | Fruit |
|----------|------|--------|
| 150 | 7 | Apple |
| 170 | 8 | Apple |
| 250 | 11 | Orange |

### X_train

```python
X_train = [
    [150, 7],
    [170, 8],
    [250, 11]
]
```

### y_train

```python
y_train = [
    "Apple",
    "Apple",
    "Orange"
]
```

### Model Training

```python
model.fit(X_train, y_train)
```

During training, KNN simply memorizes the dataset:

```text
(150,7) → Apple
(170,8) → Apple
(250,11) → Orange
```

No equation is created.

No gradient descent is used.

No weights are calculated.

---

# Prediction Phase

Suppose a new fruit arrives:

```python
x_test = [160, 7]
```

We do not know whether it is Apple or Orange.

KNN will compare this new point with every point in the training dataset.

---

# Step 1: Calculate Distance

KNN usually uses Euclidean Distance.

Formula:

\[
Distance = \sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}
\]

---

## Distance to First Training Point

Training Point:

```python
[150, 7]
```

Test Point:

```python
[160, 7]
```

Calculation:

\[
\sqrt{(160-150)^2 + (7-7)^2}
\]

\[
\sqrt{100 + 0}
\]

\[
10
\]

Store:

```text
Distance = 10
Class = Apple
```

---

## Distance to Second Training Point

Training Point:

```python
[170, 8]
```

Calculation:

\[
\sqrt{(160-170)^2 + (7-8)^2}
\]

\[
\sqrt{100 + 1}
\]

\[
10.05
\]

Store:

```text
Distance = 10.05
Class = Apple
```

---

## Distance to Third Training Point

Training Point:

```python
[250, 11]
```

Calculation:

\[
\sqrt{(160-250)^2 + (7-11)^2}
\]

\[
\sqrt{8100 + 16}
\]

\[
90.08
\]

Store:

```text
Distance = 90.08
Class = Orange
```

---

# Step 2: Create Distance Table

| Distance | Class |
|----------|--------|
| 10 | Apple |
| 10.05 | Apple |
| 90.08 | Orange |

---

# Step 3: Sort Distances

| Distance | Class |
|----------|--------|
| 10 | Apple |
| 10.05 | Apple |
| 90.08 | Orange |

Smallest distance means closest neighbor.

---

# Step 4: Choose K

Suppose:

```python
K = 3
```

Take the first 3 nearest neighbors:

```text
Apple
Apple
Orange
```

---

# Step 5: Majority Voting

Count each class:

```text
Apple  = 2
Orange = 1
```

Majority Class:

```text
Apple
```

Prediction:

```python
y_pred = "Apple"
```

---

# Complete KNN Workflow

```text
Training Data
      ↓
Store X_train and y_train
      ↓
Receive x_test
      ↓
Calculate distance to every training point
      ↓
Sort distances
      ↓
Select K nearest neighbors
      ↓
Majority voting
      ↓
Prediction
```

---

# What Does KNN Actually Know?

After training:

```python
X_train
y_train
```

KNN knows:

```text
(150,7) → Apple
(170,8) → Apple
(250,11) → Orange
```

When a new point arrives:

```python
x_test = [160,7]
```

KNN asks:

"Which stored points are closest to this new point?"

Then it uses their labels to vote.

---

# Difference Between Linear Regression and KNN

## Linear Regression

Learns an equation:

```text
y = wx + b
```

Model learns:

```text
w (weight)
b (bias)
```

Prediction uses the equation.

---

## KNN

Learns nothing.

Stores:

```python
X_train
y_train
```

Prediction process:

```text
Find nearest neighbors
↓
Vote
↓
Predict class
```

---

# Choosing K

### Small K

Example:

```python
K = 1
```

Advantages:

- Sensitive to local patterns

Disadvantages:

- Sensitive to noise

---

### Large K

Example:

```python
K = 50
```

Advantages:

- More stable

Disadvantages:

- May include far-away points

---

### Common Rule

\[
K = \sqrt{N}
\]

where:

```text
N = Number of samples
```

Example:

```text
N = 100

K = √100 = 10
```

Usually odd values are chosen:

```text
3, 5, 7, 9
```

to avoid ties.

---

# Importance of Feature Scaling

KNN uses distance calculations.

Example:

| Age | Salary |
|------|--------|
| 25 | 30000 |
| 30 | 80000 |

Salary dominates the distance because it has much larger values.

Therefore we scale features before using KNN.

Example:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
```

---

# KNN Implementation in Python

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score

data = load_iris()

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,
    random_state=42
)

model = KNeighborsClassifier(n_neighbors=5)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)

print("Accuracy:", accuracy_score(y_test, y_pred))
```

---

# Advantages

- Simple to understand
- Easy to implement
- No training time
- Works well on small datasets

---

# Disadvantages

- Slow on large datasets
- High memory usage
- Sensitive to noise
- Requires feature scaling

---

# Interview Questions

## Is KNN supervised or unsupervised?

Supervised Learning.

---

## Is KNN parametric or non-parametric?

Non-parametric.

---

## Why do we scale data before KNN?

Because KNN uses distance calculations and large-valued features can dominate the distance.

---

## Why are odd K values preferred?

To avoid ties.

Example:

```text
K = 4

Apple = 2
Orange = 2
```
Tie occurs.

---
# One-Line Definition

K-Nearest Neighbors (KNN) predicts the class of a new data point by finding the K closest training samples and assigning the majority class among them.