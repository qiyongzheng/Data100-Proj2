This is my solution for UCB [Data100](https://ds100.org) project2 Spam/Ham Classification. The notebook is original from [Spring 2022](https://github.com/DS-100/sp22). 

In this project, participants were asked to create their own classifier to distinguish spam emails from ham (non-spam) emails. They were only allowed to train logistic regression models. No decision trees, random forests, k-nearest-neighbors, neural nets, etc.

Since only logistic regression models were allowed, I focused on feature selection and **proposed a feature selection method using conditional probability**.

## Performance

Accuracy of the final model on the training data = 0.998  
4-fold cross-validation average accuracy on the training data = 0.977

## Approach

I focus only on finding words with ability to distinguish emails. Roughly speaking, we need to find words with high frequency of occurrence in spam emails. But a word with a high frequency of occurrence in spam emails may also have a high frequency of occurrence in ham emails, such as a stop word ("the", "a", "and", "in"). So frequency of occurrence is not an appropriate metric for our goal.

Note that our goal is to find "spam words" such that,  

&nbsp;&nbsp;&nbsp;&nbsp;If the word appears in an email, that email is likely to be spam, **while it is not likely to be ham**.

Using conditional probability, this means 

$$
P(spam \mid word) \rightarrow 1
$$

Since

$$
P(ham \mid word) = 1 - P(spam \mid word)
$$

Then

$$
P(ham \mid word) \rightarrow 0
$$

We can see that conditional probability is an appropriate metric of our goal.

Meanwhile, finding "ham words" will also be helpful. Therefore, we need to find words such that

$$
P(spam \mid word) \rightarrow 1
$$

or 

$$
P(ham \mid word) \rightarrow 1
$$

Let's define a word's "ability to distinguish emails" as 

$$
d = \max(P(spam \mid word), P(ham \mid word))
$$

To calculate the conditional probability, we use the formula

$$
P(A \mid B) = \frac{P(AB)}{P(B)}
$$

and estimate the probability with the frequency.
