---
title: 'practise'
date: 2026-06-01
draft:  true
featured: false  
description: "networks"
thumbnail: "/posts/exam/images/.png"
featureImage: "/posts/exam/images/.png" 
shareImage: "/posts/exam/images/.png"
author: "Angel Vyas"
tags:
    - general
categories:     
    - general
---


### program 5 -  Random Forest Classification – Weather and Iris Dataset
```python

import pandas as pd import numpy as np
import matplotlib.pyplot as plt import seaborn as sns
from sklearn.model_selection import train_test_split from sklearn.ensemble import RandomForestClassifier from sklearn.preprocessing import LabelEncoder
from sklearn.tree import plot_tree
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
# Dataset
data = pd.DataFrame({
'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rain', 'Rain', 'Rain', 'Overcast',
'Sunny', 'Sunny', 'Rain', 'Sunny', 'Overcast', 'Overcast', 'Rain'],
'Temp': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool',
'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 'Hot', 'Mild'],
'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal',
'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'High'],
'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong',
'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Strong'],
'PlayTennis': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes',
'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})
# Encoding
le = LabelEncoder()
for column in data.columns:
data[column] = le.fit_transform(data[column])

# Splitting data
X = data.drop('PlayTennis', axis=1) y = data['PlayTennis']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=24)

# Random Forest model
rf = RandomForestClassifier(n_estimators=10, random_state=24) rf.fit(X_train, y_train)

# Prediction
y_pred = rf.predict(X_test)

# Evaluation
print("Accuracy:", accuracy_score(y_test, y_pred)) 
plt.show()
# Visualizing one tree plt.figure(figsize=(6,8))
plot_tree(rf.estimators_[0], filled=True, feature_names=X.columns, class_names=["No", "Yes"])
plt.title("Decision Tree from Random Forest") plt.show()


# Random Forest Classification – Iris Dataset


from sklearn.datasets import load_iris iris = load_iris()
X = pd.DataFrame(iris.data, columns=iris.feature_names)
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

rf_iris = RandomForestClassifier(n_estimators=10, random_state=42) rf_iris.fit(X_train, y_train)
y_pred = rf_iris.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred)) print("Classification Report:\n", classification_report(y_test, y_pred))
# Feature Importance plt.figure(figsize=(6,5))
sns.barplot(x=rf_iris.feature_importances_, y=iris.feature_names) plt.title("Feature Importances - Iris Dataset")
plt.show()
# Visualizing one tree plt.figure(figsize=(10,6))
plot_tree(rf_iris.estimators_[0], filled=True, feature_names=iris.feature_names, class_names=iris.target_names)
plt.title("Decision Tree from Random Forest - Iris") plt.show()
```

### program 6 - KNN
```python
import numpy as np import pandas as pd
import matplotlib.pyplot as plt
from sklearn.preprocessing import LabelEncoder from sklearn.neighbors import KNeighborsClassifier

# Step 1: Create the dataset data = 
{
"Name": ["Ajay", "Mark", "Sara", "Zaira", "Sachin", "Rahul", "Pooja", "Smith", "Laxmi", "Michael"],
"Age": [32, 40, 16, 34, 34, 40, 20, 15, 55, 15],
"Gender": ["M", "M", "F", "F", "M", "M", "F", "M", "F", "M"],
"Sport": ["Football", "Neither", "Cricket", "Cricket", "Neither", "Cricket", "Neither", "Cricket", "Football", "Football"]
}
df = pd.DataFrame(data)
# Step 2: Encode categorical data label_encoder = LabelEncoder()
df["Gender"] = label_encoder.fit_transform(df["Gender"]) # M -> 0, F -> 1 df["Sport"] = label_encoder.fit_transform(df["Sport"])

# Step 3: Prepare features and target X = df[["Age", "Gender"]]
y = df["Sport"]

# Step 4: Define test data (Angelina)
new_data = np.array([[5, 1]]) # Age = 5, Gender = F (1)

# Step 5: Train and predict with KNN
knn = KNeighborsClassifier(n_neighbors=3, metric='euclidean') knn.fit(X, y)
predicted_sport = knn.predict(new_data)

# Decode sport back to original label
predicted_sport_label = label_encoder.inverse_transform(predicted_sport)[0] print(f"Predicted Sport for Angelina: {predicted_sport_label}")

# Step 6: Visualization plt.figure(figsize=(8, 6)) colors = ['red', 'blue', 'green'] labels = df["Sport"].unique()
for sport, color in zip(labels, colors):
plt.scatter(df[df["Sport"] == sport]["Age"], df[df["Sport"] == sport]["Gender"], label=sport, color=color)
plt.scatter(new_data[0][0], new_data[0][1], color='black', marker='x', s=100, label='Angelina')
plt.xlabel("Age") plt.ylabel("Gender")
plt.title("KNN Classification of Sport based on Age and Gender") plt.legend()
plt.grid(True) plt.show()
```

### PROGRAM 7 - LINEAR REGRESSION USING MSE
```python

import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split from sklearn.linear_model import LinearRegression from sklearn.metrics import mean_squared_error
# Generate synthetic data np.random.seed(42)
X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)

# Split the dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Create and train the model model = LinearRegression() model.fit(X_train, y_train)

# Make predictions
y_pred = model.predict(X_test)
# Evaluate the model
mse = mean_squared_error(y_test, y_pred) print(f"Mean Squared Error: {mse}") print(f"Intercept: {model.intercept_[0]}") print(f"Coefficient: {model.coef_[0][0]}")

# Plot results
plt.scatter(X_test, y_test, color='blue', label='Actual Data') plt.plot(X_test, y_pred, color='red', linewidth=2, label='Regression Line') plt.xlabel("X")
plt.ylabel("y") plt.legend()
plt.title("Linear Regression Model") plt.show()
```

### program 8 - naive bayes theorem 

```python

from sklearn.datasets import fetch_20newsgroups 
from sklearn.model_selection import train_test_split 
from sklearn.feature_extraction.text import CountVectorizer 
from sklearn.naive_bayes import MultinomialNB 
from sklearn.metrics import accuracy_score, classification_report 
 
# Load dataset 
categories = ['sci.space', 'rec.sport.baseball'] 
data = fetch_20newsgroups(subset='all', categories=categories, shuffle=True, 
random_state=42) 
 
# Split data 
X_train, X_test, y_train, y_test = train_test_split(data.data, data.target, test_size=0.3, 
random_state=42) 
 
# Convert text to numerical features 
vectorizer = CountVectorizer() 
X_train_counts = vectorizer.fit_transform(X_train) 
X_test_counts = vectorizer.transform(X_test) 
 
# Train Naïve Bayes model 
model = MultinomialNB() 
model.fit(X_train_counts, y_train) 
 
# Make predictions 
y_pred = model.predict(X_test_counts) 
 
# Evaluate 
accuracy = accuracy_score(y_test, y_pred) 
print(f"Accuracy: {accuracy:.2f}") 
print("\nClassification Report:") 
print(classification_report(y_test, y_pred, target_names=categories))
```

### program 9 - genetic algorithm in python.

```python 
import random 
 
# Objective function: f(x) = x^2 
def fitness(x): 
return x**2 
# Create initial population 
def generate_population(size, x_min, x_max): 
return [random.randint(x_min, x_max) for _ in range(size)] 
# Select parents: roulette wheel selection 
def select_parents(population): 
fitnesses = [fitness(ind) for ind in population] 
total_fit = sum(fitnesses) 
probs = [f / total_fit for f in fitnesses] 
parents = random.choices(population, weights=probs, k=2) 
return parents 
 
# Crossover: single-point 
def crossover(p1, p2): 
point = random.randint(1, 4) 
mask = (1 << point) - 1 
child1 = (p1 & mask) | (p2 & ~mask) 
child2 = (p2 & mask) | (p1 & ~mask) 
return child1, child2 
 
# Mutation: flip 1 bit 
def mutate(individual, mutation_rate=0.1): 
if random.random() < mutation_rate: 
bit = 1 << random.randint(0, 4) 
individual ^= bit 
return individual 
 
# GA driver 
def genetic_algorithm(generations=20, pop_size=6, x_min=0, x_max=31): 
population = generate_population(pop_size, x_min, x_max) 
print(f"Initial Population: {population}") 
 
for gen in range(generations): 
new_population = [] 
for _ in range(pop_size // 2): 
parent1, parent2 = select_parents(population) 
child1, child2 = crossover(parent1, parent2) 
new_population += [mutate(child1), mutate(child2)] 
population = new_population 
best = max(population, key=fitness) 
print(f"Generation {gen+1}: Best = {best}, Fitness = {fitness(best)}") 
return best 
# Run the GA 
best_solution = genetic_algorithm() 
print(f"\nBest solution found: x = {best_solution}, f(x) = {fitness(best_solution)}") 
```

### program 10 - finite word classification using back propagation algorithm 

```python

import numpy as np 
 
# Sigmoid activation and its derivative 
def sigmoid(x): 
return 1 / (1 + np.exp(-x)) 
def sigmoid_derivative(x): 
return x * (1 - x) 
# Training dataset: finite binary words and labels 
X = np.array([ 
[0, 0], 
[0, 1], 
[1, 0], 
[1, 1] 
]) 
# Labels (for example, classify based on parity) 
y = np.array([[0], [1], [1], [0]]) # XOR Problem 
 
# Seed for reproducibility 
np.random.seed(1) 
 
# Initialize weights randomly with mean 0 
input_layer_neurons = X.shape[1] 
hidden_layer_neurons = 4 
output_neurons = 1 
 
# Weights 
hidden_weights = 2 * np.random.random((input_layer_neurons, hidden_layer_neurons)) - 1 
output_weights = 2 * np.random.random((hidden_layer_neurons, output_neurons)) - 1 
 
# Learning rate 
lr = 0.5 
epochs = 10000 
 
# Training process 
for epoch in range(epochs): 
# Forward Propagation 
hidden_input = np.dot(X, hidden_weights) 
hidden_output = sigmoid(hidden_input) 
 
final_input = np.dot(hidden_output, output_weights) 
predicted_output = sigmoid(final_input) 
 
# Error calculation 
error = y - predicted_output 
if epoch % 1000 == 0: 
print(f"Epoch {epoch} Error: {np.mean(np.abs(error))}") 
 
# Backpropagation 
d_predicted_output = error * sigmoid_derivative(predicted_output) 
error_hidden_layer = d_predicted_output.dot(output_weights.T) 
d_hidden_layer = error_hidden_layer * sigmoid_derivative(hidden_output)
# Updating Weights 
output_weights += hidden_output.T.dot(d_predicted_output) * lr 
hidden_weights += X.T.dot(d_hidden_layer) * lr 
# Final output 
print("\nFinal Predicted Output:") 
print(np.round(predicted_output, 3))
```
