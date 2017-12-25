---
category: Statistics
---

# Bessel Correction or why to use n-1 instead of n as divisor for the variance
Statistics are always based on a sample drawn from a larger population. But the sample drawn may not be the best representative of the whole population so that a statistic, for instance the mean of the sample, may deviate from the population mean. This is ok as long as - on average - we are getting it right.
The expected value of the mean is indead the same as the population mean (see proof 1). But for the variance this is not the case! The expected value of the sample variance underestimates the population variance if the sample mean is used for the calculation (see proof 2).
The intuition is simple: The variance is defined as the average squared deviation from the mean. But the sample mean is by definition the point where the summed deviations are minimal (see proof 3). The deviations to the population mean therefore have to be equal or greater than the deviations to the sample mean. 


# Example: Estimating population mean and variance of a six-sided die

```python
import numpy as np
import matplotlib.pyplot as plt
```

## Compute the population mean and variance

```python
sides = np.array([1, 2, 3, 4, 5, 6])
mu_pop = np.sum(sides) / len(sides)
var_pop = np.sum((sides - mu_pop)**2) / len(sides)
std_pop = np.sqrt(var_pop)

print('mu_population = %.2f' % mu_pop)
print('var_population = %.2f' % var_pop)
print('std_population = %.2f' % std_pop)
```

    mu_population = 3.50
    var_population = 2.92
    std_population = 1.71


## Fix sample size (n) and draw lots of samples

```python
n = 100
nr_samples = 1000
sample_mat = np.zeros((nr_samples, n))
for i in range(nr_samples):
    sample_mat[i] = sides[np.random.randint(0, len(sides), n)]
```

## Compute the mean and variance for each sample with and without correction

```python
mu_sample = np.mean(sample_mat, 1)
var_sample = np.sum((sample_mat - np.repeat(np.array([mu_sample]).T, n, 1))**2, 1) / n
var_sample_corrected = np.sum((sample_mat - np.repeat(np.array([mu_sample]).T, n, 1))**2, 1) / n * (n / (n-1))
```

## Histogram of the means

```python
plt.figure()
plt.hist(mu_sample, bins=40)
plt.gca().axvline(np.mean(mu_sample), color='red', linewidth=2.0, label='mu_population')
plt.gca().axvline(mu_pop, linestyle='--', color='darkblue', linewidth=2.0, label='E[mu]_sample')
plt.xlabel('Mu Sample')
plt.ylabel('Count')
plt.legend()
plt.show()
print('mu_population = %.2f' % mu_pop)
print('E[mu]_sample = %.2f' % np.mean(mu_sample))
```

![png]({{ site.url }}{{ site.baseurl }}/images/Bessel-Correction/hist_means.png)


    mu_population = 3.50
    E[mu]_sample = 3.50


## Histogram of the variances

```python
plt.figure()
plt.hist(var_sample, bins=40, color='b', alpha=0.5)
plt.hist(var_sample_corrected, bins=40, color='orange', alpha=0.5)
plt.gca().axvline(var_pop, color='r', linewidth=2.0, label='var_population')
plt.gca().axvline(np.mean(var_sample_corrected), linestyle='--', color='darkorange', linewidth=2.0, 
                  label='E[var]_sample corrected')
plt.gca().axvline(np.mean(var_sample), linestyle='--', color='darkblue', linewidth=2.0, label='E[var]_sample')
plt.xlabel('Var Sample')
plt.ylabel('Count')
plt.legend()
plt.show()
print('var_population = %.2f' % var_pop)
print('E[var]_sample = %.2f' % np.mean(var_sample))
print('E[var]_sample corrected = %.2f' % np.mean(var_sample_corrected))
```


![png]({{ site.url }}{{ site.baseurl }}/images/Bessel-Correction/hist_variances.png)


    var_population = 2.92
    E[var]_sample = 2.89
    E[var]_sample corrected = 2.92


# Proofs
Sample: $$X_1, \dots X_n \overset{\text{i.i.d.}}{\sim} X$$ where $$E[X] = \mu, Var[X] = \sigma^2$$
We will use $$Var[X] = E[X^2] - E[X]^2$$.
Define the estimators
$$\begin{align}
	\hat{\mu} &= \frac1n \sum_{i=1}^n X_i \\
	\hat{\sigma}^2 &= \frac{1}{n} \sum_i^n{X_i^2} - \left(\frac{1}{n} \sum_i^n X_i \right)^2
\end{align}$$

## Proof 1: $$E[\hat{\mu}] = \mu$$
$$\begin{align}
	E[\hat\mu] = E\left[\frac1n \sum_{i=1}^n X_i\right] = \frac1n \sum_{i=1}^n E[X_i] = \frac{n}{n} E[X] = \mu 
\end{align}$$

## Proof 2: $$E[\hat{\sigma^2}] = \frac{n}{n-1} \sigma^2$$
$$\begin{align}
E[\hat{\sigma}^2] &= E\left[\frac{1}{n} \sum_i^n{X_i^2} - \left(\frac{1}{n} \sum_i^nX_i \right)^2\right] \\
&= \frac{1}{n} \sum_i^n E[X_i^2] - \frac{1}{n^2} E\left[\sum_i^nX_i \cdot \sum_j^nX_j\right] \\
&= \frac{1}{n} \sum_i^n E[X_i^2] - \frac{1}{n^2} E\Biggl[\underbrace{\sum_i^nX_i^2}_{dependent} \cdot \underbrace{\sum_{i \neq j}^nX_i X_j}_{independent}\Biggr] \\
&= \frac{1}{n} \sum_i^n E[X_i^2] - \frac{1}{n^2} \left( \sum_i^n E[X_i^2] + \sum_{i \neq j}^n E[X_i] E[X_j] \right)\\
&= \frac{n}{n} E[X^2] - \frac{1}{n^2} \left( n E[X^2] + (n^2 - n) E[X] E[X] \right) \\
&= \frac{n-1}{n} E[X^2] - \frac{n-1}{n} E[X]^2 \\
&= \frac{n-1}{n} (\sigma^2 + \mu^2) - \frac{n-1}{n} \mu^2 \\
&= \frac{n-1}{n} \sigma^2 \\
\sigma^2 &= \frac{n}{n-1} E[\hat{\sigma}^2]
\end{align}$$

## Proof 3: $$\mu = \frac{1}{n} \sum_i^n{X_i} \iff \min\limits_{\mu} \left(\frac{1}{n} \sum_i^n{(X_i - \mu)^2}\right)$$
$$\begin{align}
	\min\limits_{\mu} \left(\frac{1}{n} \sum_i^n{(X_i - \mu)^2}\right) & \\
	\frac{\delta}{\delta\mu} \left(\frac{1}{n} \sum_i^n{(X_i - \mu)^2}\right) &= 0 \\
	\frac{1}{n} \sum_i^n{2(X_i - \mu)\cdot -1} &= 0 \\
	-2\sum_i^n{X_i} + 2N\mu &= 0 \\
	\mu &= \frac{1}{n} \sum_i^n{X_i}
\end{align}$$
