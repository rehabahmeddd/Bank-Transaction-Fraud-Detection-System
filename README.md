# Bank Transaction Fraud Detection System

This project goes through a complete fraud detection process for bank transactions. It starts with raw transaction records and gradually turns them into information that can be used to identify suspicious activity.

## What the project does

The project first creates a Spark session so that the transaction data can be processed at a large scale. It then loads the transaction records and examines the information connected to each transfer, including the transaction type, amount, sender, receiver, and the balances before and after the transaction.

The data is cleaned before it is used. Missing balance values are handled, and the transaction fields are prepared for analysis. The project then creates additional features that can reveal unusual behavior, such as:

- Whether the receiver is a merchant
- Whether the sender's balance changes consistently with the transaction amount
- Whether the destination balance changes as expected
- Whether the sender and receiver represent the same account
- Whether a destination account also appears as an origin account in other transactions

The project also looks at the transactions as a network. Accounts are treated as points in a graph, while transfers between accounts are treated as connections. This makes it possible to study how accounts interact and to look for suspicious relationships or unusual transaction patterns. The graph is also visualized, including views focused on fraudulent transactions.

After the data has been prepared, the project converts the selected transaction information into machine-learning features. Text-based values such as the transaction type are transformed into numerical representations, and the different numerical features are assembled into a format that the models can process.

Because fraudulent transactions are much less common than normal transactions, the project takes the class imbalance into account. It creates a labeled training set containing examples of both fraudulent and non-fraudulent transactions, keeps a separate test set, and rebalances the remaining training data. Class weights are also used so that the models do not simply favor the much larger normal-transaction class.

The notebook trains and compares several classification models, including:

- Logistic regression
- Random forest
- Gradient-boosted trees

Each model is tested on transactions it did not train on. The project checks how many fraudulent transactions were correctly detected, how many normal transactions were incorrectly flagged, and how many fraudulent transactions were missed. It uses these results to calculate measures such as precision, recall, F1-score, and area under the ROC curve.

The prediction threshold is then adjusted to study the trade-off between catching more fraud and producing more false alarms. This is important because a fraud detection system may need to prioritize finding as many fraudulent transactions as possible, even if that means reviewing some additional legitimate transactions.

## How the models are evaluated

The models are evaluated on a separate test set rather than only on the transactions used during training. The project looks at:

- **True positives:** fraudulent transactions detected correctly
- **False positives:** normal transactions incorrectly flagged as fraud
- **True negatives:** normal transactions correctly identified
- **False negatives:** fraudulent transactions that were missed

These values are used to measure accuracy, precision, recall, F1-score, and the area under the precision-recall curve. Precision shows how reliable the fraud alerts are, while recall shows how much of the actual fraud the system manages to find. Recall is especially important here because a missed fraudulent transaction can be more serious than an extra transaction being sent for review.

The notebook evaluates the models at different prediction thresholds and compares their results. This shows how the system behaves when the priority changes from reducing false alarms to detecting as much fraud as possible.

Finally, the project compares the models, examines feature importance, and creates visualizations to show which transaction characteristics contribute most to the predictions. Overall, the notebook demonstrates the full path from transaction data, through cleaning and feature engineering, to graph analysis, model training, evaluation, and interpretation.

## What the results show

The output of the notebook provides a practical comparison between the different models and their ability to detect fraudulent transactions. It also shows the effect of balancing the training data and changing the classification threshold. The feature-importance analysis gives an indication of which transaction patterns are most useful for separating suspicious activity from normal behavior.

The project is intended as an analysis and modeling demonstration. Its predictions should not be treated as final decisions on their own: a real fraud detection system would need more historical validation, continuous monitoring, investigation workflows, and human review of flagged transactions.
