# Preventing Overfitting in Decision Trees
* Pruning (Limiting Tree Depth)
* Minimum Samples Split
* Cross-Validation

```python
from sklearn.ensemble import RandomForestClassifier

# Create a Random Forest classifier
rf_clf = RandomForestClassifier(n_estimators=100, max_depth=3, random_state=42)

# Train the classifier on the training data
rf_clf.fit(X_train, y_train)

# Make predictions on the testing data
y_pred_rf = rf_clf.predict(X_test)

# Evaluate the model
accuracy_rf = accuracy_score(y_test, y_pred_rf)
print(f"Random Forest Accuracy: {accuracy_rf}")
print(classification_report(y_test, y_pred_rf))
