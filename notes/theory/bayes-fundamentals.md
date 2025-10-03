# Theoretical Concepts

## Bayes' Theorem

### Mathematical Foundation
```
P(A|B) = P(B|A) × P(A) / P(B)
```

Where:
- P(A|B) = Posterior probability
- P(B|A) = Likelihood
- P(A) = Prior probability
- P(B) = Evidence

## Naive Bayes Assumption

The "naive" assumption states that features are conditionally independent given the class:

```
P(X|y) = P(x₁|y) × P(x₂|y) × ... × P(xₙ|y)
```

## Types of Naive Bayes Classifiers

### 1. Gaussian Naive Bayes
- **Use case**: Continuous features that follow normal distribution
- **Assumption**: Features are normally distributed
- **Formula**: Uses probability density function of normal distribution

### 2. Multinomial Naive Bayes
- **Use case**: Discrete count features (text classification, word counts)
- **Assumption**: Features represent counts or frequencies
- **Formula**: Uses multinomial distribution

### 3. Bernoulli Naive Bayes
- **Use case**: Binary/boolean features
- **Assumption**: Features are binary (0 or 1)
- **Formula**: Uses Bernoulli distribution

### 4. Complement Naive Bayes
- **Use case**: Text classification with imbalanced datasets
- **Advantage**: Better performance on imbalanced data
- **Formula**: Uses complement of each class

## Key Mathematical Concepts

### Laplace Smoothing (Additive Smoothing)
```
P(xᵢ|y) = (count(xᵢ, y) + α) / (count(y) + α × |V|)
```

Where:
- α = smoothing parameter (usually 1)
- |V| = size of vocabulary/feature space

### Log Probabilities
To avoid numerical underflow, use log probabilities:
```
log P(y|X) = log P(y) + Σ log P(xᵢ|y)
```

## Notes Section
*Add your theoretical insights and questions here*

---

### Questions to Explore
- [ ] When does the independence assumption break down?
- [ ] How does feature correlation affect performance?
- [ ] What are the computational complexity implications?
- [ ] How to handle zero probabilities?