# Missing data

There are many ways to deal with missing values when dealing with a dataframe.

## Checking for missing values

`missing_values = custdata.isna().sum()`

## Reassigning missing values

Say you have data on employment status, with a number of NaN values. You could reassign those NaN values to "missing":

```python

custdata["is.employed.fixed"] = pd.Categorical(
    custdata["is.employed"].map({True: "employed", False: "not employed", np.nan: "missing"}),
    categories=["not employed", "employed", "missing"]
)
```

Creating a new column for the cleaned data is best so that we keep the original data intact. Making the data categorical type rather than plain strings will make working with it simpler and more efficient.

Now lets clean up the income column as well:

```python

custdata["income_fixed"] = np.where(
    custdata["is.employed"].isna() | (custdata["income"] < 0),
    np.nan,
    custdata["income"]
)
```

If the individual's employment status is missing', or if their income is negative, their income is set to NaN. Otherwise, the original income value is kept.

We can replace the missing income values with the overall mean income:

```python

custdata["income_fixed"] = custdata["income_fixed"].fillna(custdata["income_fixed"].mean())
```

We can also replace with mean income per state so that it is more accurate to the state the individual is in:

```python

custdata["income_fixed2"] = custdata.groupby("state.of.res")["income"]\
    .transform(lambda x: x.fillna(x.mean()))

```

This code groups data by state, then applies a function to each group that fills the NaN values with the mean of the group.

Lastly, we can also just replace missing income with 0:

`custdata["income_fixed3"] = custdata["income"].fillna(0)`

## Adding columns of useful data

Create a new table showing the average incomes by state:

```python

avg_income_by_state = custdata.groupby("state.of.res", as_index=False)["income"].mean(numeric_only=True)
avg_income_by_state.rename(columns={"income": "avg.income"}, inplace=True)
# as_index=False keeps the state as a column instead of an index, which makes a difference in how you can work with it
# mean(numeric_only=True) ensures that only numeric columns are considered for the mean calculation
```

Adding a column with standardized age (z-score):

`custdata["age.normalized"] = (custdata["age"] - custdata["age"].mean()) / custdata["age"].std()`

We calculate the z-score for the 'age' column by subtracting the mean and dividing by the standard deviation. This results in a new column 'age.normalized' that has a mean of 0 and a standard deviation of 1.

Normalizing income by state median:

Group the data by 'state.of.res' and normalize the income within each state. Show income relative to the median income of each state.

```python
custdata["income.nrml.by.state"] = custdata.groupby("state.of.res")["income"]\
    .transform(lambda x: x / x.median() * 100)
```

The transform function applies normalization to each group, while the lambda function divides each income value by the median income of its respective state and multiplies by 100.

## Sampling data for test and train sets (manual split)

For the test set we could randomly sample 10% of the rows, and use the rest for the training set:

```python
n_rows = custdata.shape[0]
test_idx = np.random.choice(n_rows, size=int(0.1 * n_rows), replace=False)
train_idx = np.setdiff1d(np.arange(n_rows), test_idx)

# create training and test sets using the indices we just got
train = custdata.iloc[train_idx]
test = custdata.iloc[test_idx]
```

Sampling using random uniform instead:

```python

custdata["sample"] = np.random.uniform(size=n_rows)
train_alt = custdata[custdata["sample"] >= 0.1]
test_alt = custdata[custdata["sample"] < 0.1]
```

We create a randonm sample column with uniform distribution. `np.random.uniform()` generates random floates between 0 and 1. We then split the data into training and test sets based on this sample.

You go through row by row and if the value for that row is greater than or equal 0.1 you put it in the train set and otherwise it goes in the test set. Since the values should follow a normal distribution this should result in about 10% of the values ending up in the test set. 