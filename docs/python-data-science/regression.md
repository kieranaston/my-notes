# Regression

Regression is essentially finding the relationship between variables so that you can predict one thing using another.

## Linear regression

Here is an example of performing linear regression on advertising/sales data to find the relationship between advertising and sales.

```python
import statsmodels.formula.api as smf
# simple linear regression using statsmodels' formula API
lm_simple = smf.ols("sales ~ TV", data=Advertising).fit()
# ols is "ordinary least squares" which is the method used to estimate the coefficients
# sales ~ TV says we want to predict sales using TV
# returns a results object containing estimated coefficients, statistics, and other info about the fitted model
```

**Visualizing this result:**

```python
import seaborn as sns

plt.figure()
sns.scatterplot(data=Advertising, x="TV", y="sales", s=40, alpha=0.8)

# Build fitted line by sorting by TV and plotting predictions in order
tmp = Advertising[["TV", "sales"]].copy().sort_values("TV")
tmp["fitted"] = lm_simple.predict(tmp[["TV"]])
plt.plot(tmp["TV"], tmp["fitted"], color="blue", linewidth=2, label="Fitted line")
plt.title("Sales vs TV (Simple Linear Regression)")
plt.xlabel("TV advertising spend")
plt.ylabel("Sales")
plt.legend()
plt.tight_layout()
plt.show()

# Draw vertical residuals (linerange analogue) - these are the lines from actual point to predicted point
plt.figure()
sns.scatterplot(data=tmp, x="TV", y="sales", s=30, alpha=0.7, color="black")
plt.plot(tmp["TV"], tmp["fitted"], color="blue", linewidth=2, label="Fitted")
plt.vlines(x=tmp["TV"], ymin=tmp["fitted"], ymax=tmp["sales"], color="red", alpha=0.4, linewidth=1)
plt.title("Vertical Residuals: Observed vs Fitted")
plt.xlabel("TV advertising spend")
plt.ylabel("Sales")
plt.tight_layout()
plt.show()
```

## Multiple linear regression

Here we find the relationship between sales and TV, radio, newspaper. This is predicting one thing using multiple inputs. Essentially finding a plane (2 inputs) or hyperplane (3+ inputs) through higher-dimensional space.

```python
import statsmodels.formula.api as smf

# fitting multiple linear regression model
lm_multi = smf.ols("sales ~ TV + radio + newspaper", data=Advertising).fit()
# just like before we can summarize the model like so
print(lm_multi.summary())
```

## Logistic regression (credit card default)

While linear regression predicts a continuous number (like sales, temp.) logistic regression predicts a probability between 0 and 1 and is used for classification.

For example, linear regression could be used to predict someones income, while logistic regression could be used to predict whether they will buy a product.

The "default" column in our data denotes whether an individual defaulted or not. It is a binary value.

```python
from sklearn.model_selection import train_test_split
# getting train/test sets
train, test = train_test_split(Default, test_size=0.20, random_state)=42, stratify=Default["y"])
# puts 20% of the data in test set, 80% in train set
# random_state=42 sets the seed
# stratify=Default["y"] mimics the class ditribution from the original data into both the train and test sets
```

**Fitting the model:**

The following code fits the logistic regression model to predict credit card default.

```python
import statsmodels.formula.api as smf
import statsmodels.api as sm

non_features = ["y", "default"]
# those columns should not be considered since they are the columns describing the class
features = [c for c in train.columns if c not in non_features]
formula = "y ~ " + " + ".join(features)
# basically uses every feature to fit the model

# fits the model using statsmodels' GLM with Binomial family (logistic regression)
gln_binom = smf.glm(formula=formula, data=train, family=sm.families.Binomial()).fit()
```

Essentially automatically uses all available features to predict whether someone will default.

## Train/test evaluation & metrics

Can use `confusion_matrix` from `sklearn.metrics` to produce a confusion matrix showing true positives, false positives, true negatives, and false negatives.

**Core metrics:**

Accuracy = (True positives + True negatives) / all
Precision = True positivies / (True positivies + False positives)
Recall = True positivies / (True positives + False negatives)
Specificity = True negatives / (True negatives + False positives)

Should also examine f1 score and balanced accuracy: (Recall + Specificity) / 2

## Precision-recall curve

Useful for showing the trade-off between precision and recall for different thresholds. Higher recall typically comes at the cost of lower precision, and vice versa.

Ideally, we want to find a balance between the two that Minimizes false negatives and false positives, which corresponds to the upper right corner of the curve.

```python
from sklearn.metrics import precision_recall_curve

prec_curve, rec_curve, _ = precision_recall_curve(y_test_vec, proba_test)
plt.figure()
plt.plot(rec_curve, prec_curve)
plt.title("Precision–Recall Curve — Logistic Regression")
plt.xlabel("Recall")
plt.ylabel("Precision")
plt.tight_layout()
plt.show()
```

## K-nearest neighbours classification

K-nearest neighbours works by choosing a point and looking at the K-nearest neighbours to it in order to determine its class. If almost all the points near it are part of a given class that point it would predict that the point we are looking at is also a part of that class.

```python
# once you have chosen the features you want to consider, you can form train and test sets
Xtr = train[features_knn].copy()
ytr = train["y"].astype(int).to_numpy()
Xte = test[features_knn].copy()
yte = test["y"].astype(int).to_numpy()

# each feature is normalized since KNN uses a distance calculation
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier
from sklearn.pipeline import Pipeline

knn_clf = Pipeline([
    ("scaler", StandardScaler()),
    ("knn", KNeighborsClassifier(n_neighbors=5))
])
# StandardScaler() is a transformer that normalizes each feature to have mean 0 and standard deviation 1
# KNeighborsClassifier() is a KNN classifier set to use 5 neighbours

# the KNN classifier is then fit on training set and evaluated on the testing set
knn_clf.fit(Xtr, ytr)
proba_test_knn = knn_clf.predict_proba(Xte)[:, 1]
y_pred_knn = (proba_test_knn >= 0.5).astype(int)
```