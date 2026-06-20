# Association Rule Learning in Unsupervised Learning


Association Rule Learning is an Unsupervised Machine Learning technique used to discover relationships and patterns among items in large datasets.

Unlike supervised learning, association rule learning does not require labeled data. It identifies hidden patterns and correlations between items.

Example:

```text
Customers who buy Milk often buy Bread.
```

This relationship can be represented as:

```text
Milk → Bread
```

---

#  What is Association Rule Learning?

Association Rule Learning finds relationships between variables in a dataset.

It answers questions such as:

* What products are frequently purchased together?
* What medicines are commonly prescribed together?
* Which movies are often watched by the same users?

General Rule:

```text
A → B
```

Meaning:

If A occurs, B is likely to occur.

Example:

```text
Milk → Bread
```

---

#  Why Use Association Rule Learning?

Association Rule Learning helps organizations:

* Understand customer purchasing behavior
* Recommend products
* Increase sales
* Discover hidden relationships
* Improve decision-making

---

#  Key Terminologies

## Item

A single product or object.

Examples:

```text
Milk
Bread
Butter
```

## Itemset

A collection of items.

Examples:

```text
{Milk}
{Milk, Bread}
{Milk, Bread, Butter}
```

## Transaction

A set of items purchased together.

Example:

```text
Milk, Bread, Butter
```

---

# Support

Support measures how frequently an itemset appears in the dataset.

## Formula

```text
Support(A) =
Number of transactions containing A
------------------------------------
Total number of transactions
```

## Example

Dataset:

```text
T1 = Milk, Bread
T2 = Milk, Butter
T3 = Milk, Bread
T4 = Bread, Butter
T5 = Milk, Bread
```

Milk appears in:

```text
T1
T2
T3
T5
```

Count = 4

Total transactions = 5

```text
Support(Milk) = 4/5 = 0.8
```

Support = 80%

---

# Confidence

Confidence measures how often B occurs when A occurs.

## Formula

```text
Confidence(A → B)

Support(A ∪ B)
--------------
Support(A)
```

## Example

Rule:

```text
Milk → Bread
```

Milk appears = 4

Milk and Bread together appear = 3

```text
Confidence = 3/4
```

Confidence = 75%

Interpretation:

75% of customers who buy Milk also buy Bread.

---

#  Lift

Lift measures the strength of the relationship.

## Formula

```text
Lift(A → B)

Confidence(A → B)
-----------------
Support(B)
```

## Interpretation

| Lift Value | Meaning               |
| ---------- | --------------------- |
| Lift > 1   | Positive relationship |
| Lift = 1   | No relationship       |
| Lift < 1   | Negative relationship |

---

#  Example Dataset

| Transaction | Items               |
| ----------- | ------------------- |
| T1          | Milk, Bread         |
| T2          | Milk, Diaper, Beer  |
| T3          | Milk, Bread, Diaper |
| T4          | Bread, Butter       |
| T5          | Milk, Bread, Butter |

---

# Association Rule Generation

From the frequent itemset:

```text
{Milk, Bread}
```

Possible rules:

```text
Milk → Bread
Bread → Milk
```

Calculate:

* Support
* Confidence
* Lift

Keep only strong rules.

Example:

```text
Milk → Bread
Support = 60%
Confidence = 75%
```

---

#  Apriori Algorithm

## What is Apriori?

Apriori is an Association Rule Learning algorithm used to find frequent itemsets.

It works based on the Apriori Principle:

> If an itemset is frequent, all of its subsets must also be frequent.

---

## Apriori Steps

### Step 1

Find frequent 1-itemsets.

```text
Milk
Bread
Butter
Diaper
```

### Step 2

Generate 2-itemsets.

```text
Milk, Bread
Milk, Butter
Bread, Butter
```

### Step 3

Remove itemsets with low support.

### Step 4

Generate 3-itemsets.

```text
Milk, Bread, Butter
Milk, Bread, Diaper
```

### Step 5

Repeat until no more frequent itemsets exist.

---

## Apriori Workflow

```text
Generate Candidates
↓
Calculate Support
↓
Prune
↓
Generate New Candidates
↓
Repeat
```

---

## Advantages of Apriori

* Easy to understand
* Easy to implement

## Disadvantages of Apriori

* Generates many candidate itemsets
* Slow for large datasets
* Multiple database scans required

---

# 11. FP-Growth Algorithm

## What is FP-Growth?

FP-Growth stands for Frequent Pattern Growth.

It is a faster alternative to Apriori.

Instead of generating candidate itemsets, it builds a compact structure called an FP-Tree.

---

## FP-Growth Workflow

```text
Build FP-Tree
↓
Compress Transactions
↓
Mine Frequent Patterns
```

---

## Example

Transactions:

```text
T1 = Milk, Bread
T2 = Milk, Bread, Diaper
T3 = Milk, Bread
T4 = Milk, Diaper
```

---

## Count Frequencies

```text
Milk = 4
Bread = 3
Diaper = 2
```

---

## Build FP-Tree

```text
Root
 |
Milk(4)
 | \
Bread(3) Diaper(1)
 |
Diaper(1)
```

---

## Why FP-Growth is Faster

Instead of generating:

```text
Milk, Bread
Milk, Diaper
Bread, Diaper
Milk, Bread, Diaper
```

FP-Growth stores common paths once and uses counts.

This reduces memory usage and computation time.

---

## Advantages of FP-Growth

* Faster than Apriori
* No candidate generation
* Fewer database scans
* Efficient for large datasets

## Disadvantages of FP-Growth

* More complex to understand
* FP-Tree construction can be difficult

---

# 12. Apriori vs FP-Growth

| Feature              | Apriori        | FP-Growth      |
| -------------------- | -------------- | -------------- |
| Candidate Generation | Yes            | No             |
| Database Scans       | Multiple       | Usually 2      |
| Speed                | Slow           | Fast           |
| Memory Usage         | High           | Low            |
| Large Datasets       | Less Efficient | More Efficient |
| Complexity           | Easy           | Moderate       |

---

#  Python Implementation

## Install Required Libraries

```bash
pip install pandas mlxtend
```

---

## Apriori

```python
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

frequent_itemsets = apriori(
    df,
    min_support=0.3,
    use_colnames=True
)

rules = association_rules(
    frequent_itemsets,
    metric="confidence",
    min_threshold=0.7
)

print(rules)
```

---

## FP-Growth

```python
from mlxtend.frequent_patterns import fpgrowth
from mlxtend.frequent_patterns import association_rules

frequent_patterns = fpgrowth(
    df,
    min_support=0.3,
    use_colnames=True
)

rules = association_rules(
    frequent_patterns,
    metric="confidence",
    min_threshold=0.7
)

print(rules)
```

---

# 14. Real-World Applications

## Market Basket Analysis

Example:

```text
Milk → Bread
```

---

## E-Commerce Recommendations

Example:

```text
Laptop → Mouse
```

---

## Healthcare

Example:

```text
Disease → Medicine
```

---

## Banking

Analyze customer spending patterns.

---

## Fraud Detection

Detect suspicious transaction combinations.

---

## Web Analytics

Analyze user navigation behavior.

---

# 15. Advantages and Disadvantages

## Advantages

* Finds hidden patterns
* Works without labels
* Useful for recommendation systems
* Easy to interpret

## Disadvantages

* Can generate many rules
* Not suitable for all datasets
* May produce irrelevant associations

---

# Conclusion

Association Rule Learning is a powerful Unsupervised Learning technique used to discover relationships between items in large datasets.

The two most popular algorithms are:

### Apriori

* Generates candidate itemsets
* Easy to understand
* Slower for large datasets

### FP-Growth

* Uses FP-Tree
* No candidate generation
* Faster and more efficient

Association Rule Learning is widely used in retail, healthcare, banking, recommendation systems, and fraud detection to uncover meaningful patterns and improve decision-making.
