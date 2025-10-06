# Python data operations

## Basic vector operations

```python

a = np.array([2, 3, 4])

print("Vector a:", a)
print("Vector b:", b)
print("a + b:", a + b)
print("5 * a:", 5 * a)
print("a * b (elementwise):", a * b)
print("a @ b (dot product):", a @ b)
print("a ** 2 (elementwise square):", a ** 2)
print("a[0] (first element):", a[0])
# a[1:3] is a slice from index 1 to 2 (3 is excluded)
print("a[1:3] (slice from index 1 to 2):", a[1:3])
print("a[-1] (last element):", a[-1])
```

## Categorical data

```python
# Can use pandas to represent categorical data
cat_dtype = pd.CategoricalDtype(categories=["small", "medium", "large"], ordered=True)

# Wrap in series to retain categorixal type upon indexing
# Series is one-dimensional labeled array capable of holding any data type
sizes = pd.Series(["small", "medium", "large", "medium", "small"], dtype=cat_dtype)
# dtype is used to specify the data type of the Series. cat_dtype is used to specify the categorical data type

# Display categorical data
print("Sizes as ordered factors:\n", sizes)
print("Sizes categories:\n", sizes.cat.categories)
print("Sizes codes:\n", sizes.cat.codes)
```

## Matrices

```python
# Can use numpy arrays to represent matrices
M = np.arange(1, 13).reshape(3, 4)


print("Matrix M:\n", M)
print("Elementwise M * 2:\n", M * 2)
print("Transpose M.T:\n", M.T)
print("Sum of each column M.sum(axis=0):\n", M.sum(axis=0))
print("Sum of each row M.sum(axis=1):\n", M.sum(axis=1))
print("Mean of each column M.mean(axis=0):\n", M.mean(axis=0))
print("Mean of each row M.mean(axis=1):\n", M.mean(axis=1))
print("Standard deviation of each column M.std(axis=0):\n", M.std(axis=0))
print("Standard deviation of each row M.std(axis=1):\n", M.std(axis=1))
print("Maximum of each column M.max(axis=0):\n", M.max(axis=0))
print("Maximum of each row M.max(axis=1):\n", M.max(axis=1))
print("Minimum of each column M.min(axis=0):\n", M.min(axis=0))
print("Minimum of each row M.min(axis=1):\n", M.min(axis=1))
print("Elementwise square of M:\n", M ** 2)
print("Matrix multiplication M @ M.T:\n", M @ M.T)
```