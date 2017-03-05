### TOPICS:
- Introduction to concepts of popular classification algorithms
- Using scikit-learn
- What to ask when choosing an ML algorithm

### CHOOSING A CLASSIFICATION ALGORITHM
No algorithm is perfect for every scenario, you'll likely have to test a handful of them to find the best one. Efficency of the various algorithms depends on number of features/samples, noise, whether the classes are linearly separable or not

### STEPS FOR TRAINING AN ALGORITHM
- Selection of features
- Choosing a performance metric
- Choosing a classifier and an optimization algorithm
- Evaluating the performance
- Tuning the algorithm
`Numpy.unique(vector)` to return the different values inside the vector

Implementation of iris with sklearn [pdf page 75 - book page 50]
- Import datas and libraries
- Split datas into train and test using train_test_split
- Standardize features using StandardScaler
- Train perceptron
- Find accuracy using accuracy_score
- Plot decision boundary with matplotlib 

> Remember that the perceptron has the huge disadvantage that if the classes aren't linearly separable it never converges

Most classificators in sklearn support multiclass classification through One-vs-Rest method
### Logistic regression
In spite of his name logistic regression is a method for classification, it is based on the logarithm of the odds ratio: odds of the positive event (p) over the negative (1-p). Positive event just means the one we want to predict.
$$
logit(p) = \log{\frac{p}{(1-p)}}
$$
This way we transform values between 0 and 1 to values over the entire real numbers range.
We can use this number to express a relationship between feature values and the log-odds
$$
logit(p(y=1|x))=w_0x_0+w_1x_1+w_mx_m=\sum_{i=0}^{n}{w^Tx} 
$$
$p(y=1|x)$ is the probability of that sample belonging to the class 1, given features x
What we are actually interested in is given the features determining the probability of it being part of class 1, which is the inverse for of the logit function, also called logistic function or sigmoid function.
$$
\phi(z)=\frac{1}{1+e^{-z}}
$$
Where z is the net input (dot product of features and weights)

![sigmoid graph](https://i.imgur.com/hXFKiH6.png)

Above is the graph of the sigmoid. So the sigmoid takes an input in the real number range and gives an output in the [0,1] range
Schema of the logistic regression fitting

![schema of logistic regression](https://i.imgur.com/pmsKJDG.png)

The quantizer will simply check whether the sigmoid function's output is greater or equal to 0.5
The great thing about the sigmoid function is that it not only predicts the class, but also gives us the probability of it being in that class. This is why it's widely used in medicine.
After some math, we found out that the cost function J of the logistic regression is 
$$
J(w)=\sum_{i=1}^{n}{-log(\phi (z^{(i)}))-(1-y^{(i)}\log{(1-\phi (z^{(i)})})}
$$
Which plots to this for a single-sample instance. Remember that y is the correct class

![plot for single instance](https://i.imgur.com/q2pfPRu.png)

As you can see the cost approaches 0 if we correctly predict the class, but if the prediction is wrong it goes to infinity. This means that we penalize wrong predictions with an increasingly larger cost.
The logistic regression model works as the adaline, but with this different cost function.
With logistic regression model in sklearn we have an additional method called predict_proba that returns the probability of the element being part of any of the possible classes
### TACKLING OVERFITTING VIA REGULARIZATION
When your model is overfitting (performs well on the training set, but not on the test set), we say that it has high variance, which can be caused by having too many parameters and therefore too complex model
A model suffers of underfitting when it doesn't capture the complexity of the model

![underfitting and overfitting](https://i.imgur.com/Sj42YTq.png)

Variance is a measure of how much the model is sensitive to the randomness of the training data. (randomic error)
Bias is a measure of how far off the prediction are from the correct values. (systematic error)
To find a balance between bias and variance we can use regularization, that is a useful method to deal with collinearity (features that are highly correlated), filter out noise, prevent overfitting.
Regularization works by adding additional information to penalize extreme weights
A common form of regularization is the L2 regularization
$$
\frac{\lambda}{2}||w||^2=\frac{\lambda}{2}\sum_{j=1}^m{w^2_j}
$$
To apply the regularization we hav to add it in the cost function like so
$$
J(w)=C[\sum_{i=1}^{n}{(-\log{(\phi (z^{(i)})}) +(1-y^{(i)})) (-\log{(1-\phi (z^{(i)}))})}]+\frac{\lambda}{2}||w||^2
$$
A graph showing how weight coefficients and regularization are related: reducing the C coefficient(increasing regularization) we reduce the coefficients

![regularization graph](https://i.imgur.com/TmaLWdJ.png)

#### MAXIMUM MARGIN CLASSIFICATION WITH SUPPORT VECTOR MACHINES (SVM)
The Perceptron rule's goal was to minimize the missclassification, instead the SVM goal is to maximize margin, that is the distance between the decision boundary and the closest samples

![SVM margin](https://i.imgur.com/qWURMDo.png)

higher margin generally means less overfitting
To get an intuition for the margin maximization, let's take a closer look at those *positive* and *negative* hyperplanes that are parallel to the decision boundary, which can be expressed as follows:
$$
w_0+w^Tx_{pos}=1 \qquad (1) \\
w_0 + w^Tx_{neg}=-1\quad\:(2)
$$
If we subtract those two linear equations (1) and (2) from each other,we get:
$$
 \Rightarrow w^T(x_{pos}-x_{neg})=2
$$
We can **normalize this by the length of the vector *w***, which is defined as follows
$$
||w||=\sqrt{\sum_{j=1}^{m}{w^2_j}}
$$
So we arrive at the following equation:
$$
\frac{w^T(x_{pos}-x_{neg})}{||w||}=\frac{2}{||w||}
$$
The objective of SVN is to maximize the margin $\frac{2}{||w||}$. So written in equations
$$
w_0+w^T x{(i)}\ge1 \quad\text{if}\quad y^{(i)}=1 \\
w_0+w^Tx^{(i)}\lt-1 \quad\text{if}\quad y^{(i)}=-1
$$
Those equations are the constraints and simply mean that all the negative sample should fall on one side of the hyperplane and all the positive on the other
In practice it's easier minimizing the reciprocal term $\frac{1}{2}||w||^2$, that can be solved through quadratic programming (detailed discussion of this is beyond the scope of the book)
### DEALING WITH THE NONLINEARLY SEPARABLE CASE USING SLACK VARIABLES
In the non linearly separable case linear constraints need to be relaxed in order to allow for convergence. So it was introduced the slack variable $\xi$ 
We add it in the linear constraints
We can use the variable C to tune the bias-variance trade-off

![bias variance tradeoff](https://i.imgur.com/gKDN2Gp.png)

#### LOGISTIC REGRESSION VERSUS SVM
Logistic regression and SVM often yield to similar results, but logistic regression is easier to update (for example when working with streaming data), whereas SVM is less prone to errors
> for more optimized algorithms use liblinear and libsvm

### SOLVING NON-LINEAR PROBLEMS USING KERNEL SVM
SVM can be easily kernelized. The idea behind kernels is to create nonlinear combinations of the original features and project them onto higher dimensional space where they become linearly separable
One problem with this approach is that transforming the features into high dimensional ones is very computationally expensive.
{% method -%}
## Install {#install}

The first thing is to get the GitBook API client.

{% sample lang="python" -%}
```bash
$ npm install gitbook-api
```
{% endmethod %}
[pdf page 102]