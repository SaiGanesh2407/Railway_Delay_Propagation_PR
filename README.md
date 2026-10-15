![Amrita](https://github.com/user-attachments/assets/118097aa-96d2-4724-846c-88a21eb84bf2)

# Probabilistic Reasoning- 22AIE301

# Uncertainty-Aware Railway Delay Propagation

## Team C - 16
### Team Members

| Name | Roll No |
|-----|-----|
| K. Sai Ganesh | CB.SC.U4AIE24226 |
| P. Sathvik | CB.SC.U4AIE24240 |
| Ch. Uday | CB.SC.U4AIE24210 |
| G. Varshini | CB.SC.U4AIE24216 |

### Abstract
Railway delays are complex events that cannot be easily predicted or propagated due to their uncertain nature and dependencies with other train movements. In this research work, we introduce the Bayesian Network Uncertainty-Aware Railways Delay Propagation and Adaptive Mitigation Framework. Temporal, route, traffic proxy, and delay at departure probabilities are modeled using a connected Bayesian Network in order to predict the probabilities of delays as well as on-time. A propagation algorithm based on stations predicts possible relationships between consecutive movements through the same stations within two hours using the previously mentioned information. The Bayesian parameters and probabilistic inference methods were used in the solution, which obtained 83.60% of accuracy and 109,697 station-based movement pairs.

### Introduction
Railway delays are influenced by several uncertain factors, including time, route, traffic conditions, and departure delays. This project uses Bayesian Networks to estimate the probabilities of different delay categories and explore potential delay propagation between movements sharing a station.


### Problem Statement
Traditional delay estimates may not adequately represent uncertainty across different delay categories. The project aims to model dependencies among relevant factors and estimate the probabilities of on-time, minor, and major delays using probabilistic reasoning.


### Motivation
Understanding delay uncertainty can support better analysis of transportation disruptions. Bayesian Networks provide an interpretable way to represent dependencies, estimate delay probabilities, and investigate historical relationships between consecutive movements without assuming causation.

### Objectives
To develop a Bayesian Network-based framework to predict railway delay categories under uncertainty and analyze how delays may propagate between consecutive movements at the same station using historical data.


### Methodology

#### 1. Data Preprocessing and Delay Classification

Historical transportation records are cleaned, and relevant features are selected. Arrival delays are converted into three categories: ON_TIME ($\leq 5$ minutes), MINOR ($> 5$ and $\leq 15$ minutes), and MAJOR ($> 15$ minutes).

The non-negative arrival delay is calculated as:

$$
d_i^{+} = \max(0, d_i)
$$

Here, $d_i$ is the recorded arrival delay, and $d_i^{+}$ is its non-negative value used for classification.

#### 2. Bayesian Network Construction

A Bayesian Network (BN) is constructed using a predefined directed acyclic graph (DAG), where nodes represent delay-related variables and directed edges represent their dependencies. Conditional probability distributions are estimated using the Bayesian Dirichlet equivalent uniform (BDeu) method with an equivalent sample size of 10.

The joint probability distribution is factorized as:

$$
P(X_1, X_2, \ldots, X_n) = \prod_{i=1}^{n} P(X_i \mid Pa(X_i))
$$

Here, $Pa(X_i)$ represents the parent variables of $X_i$. This factorization allows the joint probability of the variables to be represented through local conditional probabilities.

#### 3. Probabilistic Inference and Delay Prediction

Variable Elimination is used to calculate the posterior probability of each delay category given the observed evidence, such as available operational and timing information.

The posterior probability is calculated as:

$$
P(C=c \mid E) = \frac{P(C=c, E)}{P(E)}
$$

The predicted category is selected using the maximum posterior probability:

$$
\hat{C} = \arg\max_{c \in \mathcal{C}} P(C=c \mid E)
$$

Here, $C$ denotes the delay category, $E$ denotes the observed evidence, and $\mathcal{C}$ represents the set of possible delay categories. The model therefore provides probabilities for ON_TIME, MINOR, and MAJOR delays.

#### 4. Delay Propagation Analysis

To investigate potential delay propagation, historical arrival events are matched with subsequent departure events at the same station, on the same calendar day, within a 120-minute window, excluding records with the same train number. The conditional probability of the next departure's delay category is calculated for each previous arrival category.

The conditional probability is calculated as:

$$
P(B=b \mid A=a) = \frac{N(A=a, B=b)}{N(A=a)}
$$

Here, $A$ is the previous arrival delay category, $B$ is the next candidate departure delay category, and $N$ represents the corresponding event counts. This analysis identifies historical associations between delay categories but does not establish causation or confirm that the movements are operationally connected.

#### 5. Model Evaluation

The model is evaluated using a stratified 80:20 train-test split, with performance metrics calculated on a sample of 500 test records. Accuracy, balanced accuracy, precision, recall, F1-score, and a confusion matrix are used to assess predictive performance.

Here, $K=3$ represents the three delay categories. Balanced accuracy is particularly useful for evaluating performance when the delay categories are unevenly distributed.
