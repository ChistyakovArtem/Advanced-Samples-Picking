# Advanced-Samples-Picking
Advanced Samples Picking - multipurpose heuristic for classification tasks

General idea

1) Suppose you need to train image classifier (for example image binary classifier: digit '0' or '1' (no other digits))
2) Your train data has 20% of '0' and 80% of '1' and you don't know anything about % of '0' in test.
3) Algorithm
   fit(train_X, train_y) -> predict(test_y) -> get probability distribution based on predictions (for example 30% of '0' and 70% of '1') ->
   -> modify picked samples to fit this distribution (the whole dataset has 20% of '0' and modified will have 30% of '0') -> fit(X_modif, y_modif) ...
   
4) Why we need it?
   If train and test are very dissimilar - we will get poor performace (for example if train has 10% of '0' but test has 90% of '0' -- linear regression (for image) will give us 11% accuracy)
   This is a way to fix this problem
   
5) What's wrong
   You can change probas here
   t_ = polish_data(get_loader(True, batch_size=one), batch_size=one, p=np.array([0.2, 0.8]))
   v_ = polish_data(get_loader(False, batch_size=one), batch_size=one, p=np.array([0.5, 0.5]))
   
   In some conditions my model with heuristic will diverge (accuracy decrease during training) (p=np.array([0.5, 0.5]) ... p=np.array([0.5, 0.5]) ).
   Basic model - 98%, with heuristic - 97%
   
6) Ideas to fix it
   Well, i invented it recently, give me time
   a) Learning rate (new = old + (new - old) * lr) -- if prev were 20% of zeros and now 30% we can make not 30% but 20 + (30 - 20) * lr
   b) idk
7) Some ideas how to improve performance
   a) Some momentum (if row (% of zeros in train) is 10; 15; 20; 25; 29; 29.8 --> 30) for better convergence
   b) idk
