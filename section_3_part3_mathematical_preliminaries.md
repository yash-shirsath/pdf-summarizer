# Part III: Mathematical Preliminaries - Shannon's "A Mathematical Theory of Communication"

## Overview

Part III of Shannon's seminal work establishes the mathematical foundations necessary for extending information theory from discrete to continuous systems. This section focuses on function ensembles, continuous probability distributions, and entropy concepts that are essential for analyzing continuous communication channels.

## Section 18: Sets and Ensembles of Functions

### Fundamental Concepts

**Sets of Functions**
A set of functions is a class or collection of functions, typically of one variable (time). Sets can be specified either explicitly through mathematical representations or implicitly through defining properties.

**Examples of Function Sets:**
1. **Parametric functions**: $f_θ(t) = \sin(t + θ)$ where each value of θ determines a specific function
2. **Band-limited functions**: All functions containing no frequencies above W cycles per second
3. **Amplitude and band-limited functions**: Functions limited to both band W and amplitude A
4. **Speech signals**: The set of all English speech signals as functions of time

**Ensembles of Functions**
An ensemble extends a set of functions by adding a probability measure, allowing determination of the probability that functions possess certain properties. This transforms a mere collection into a statistical entity.

**Examples of Function Ensembles:**

1. **Discrete ensemble**: Finite set of functions $f_k(t)$ with probabilities $p_k$

2. **Parametric ensemble**: Functions of the form $f(α₁, α₂, ..., αₙ; t)$ with probability distribution $p(α₁, ..., αₙ)$

3. **Harmonic ensemble**: 
   $$f(a₁,...,aₙ,θ₁,...,θₙ;t) = \sum_{i=1}^n a_i\sin i(ωt+θ_i)$$
   with amplitudes $a_i$ normally distributed and phases $θ_i$ uniformly distributed

4. **White noise ensemble**:
   $$f(a_i, t) = \sum_{n=-∞}^{+∞} a_n \frac{\sin π(2Wt - n)}{π(2Wt - n)}$$
   with coefficients $a_i$ normal and independent with standard deviation $\sqrt{N}$

5. **Poisson impulse ensemble**: $\sum_{k=-∞}^∞ f(t+t_k)$ where $t_k$ follow a Poisson distribution

### Stationarity and Ergodicity

**Stationary Ensemble**: An ensemble where shifting all functions by any fixed time amount results in the same ensemble. The statistical properties are invariant under time translation.

**Ergodic Ensemble**: A stationary ensemble with no non-trivial stationary subsets (subsets with probability ≠ 0, 1 that remain invariant under time translations). In ergodic ensembles, each function is "typical" of the entire ensemble.

**Ergodic Property**: For ergodic ensembles, ensemble averages equal time averages with probability 1, meaning each function eventually exhibits all statistical behaviors of the ensemble with proper frequency.

### Operations on Ensembles

**Invariant Operators**: An operator T is invariant if shifting the input merely shifts the output:
$$g_α(t) = Tf_α(t) \implies g_α(t+t₁) = Tf_α(t+t₁)$$

**Key Properties**:
- If T is invariant and input is stationary → output is stationary
- If T is invariant and input is ergodic → output is ergodic
- Linear invariant operators naturally lead to Fourier analysis (Wiener's insight)

**Communication Theory Perspective**: Communication systems should be designed for ensembles of functions (e.g., speech ensembles) rather than individual functions or sine waves.

## Section 19: Band Limited Ensembles of Functions

### Sampling Theorem Foundation

**Theorem 13**: Any function $f(t)$ containing no frequencies above W cycles per second can be completely reconstructed from samples taken at intervals of $\frac{1}{2W}$ seconds:

$$f(t) = \sum_{n=-∞}^∞ X_n \frac{\sin π(2Wt - n)}{π(2Wt - n)}$$

where $X_n = f(\frac{n}{2W})$ are the sample values.

### Geometric Interpretation

**Function Space Representation**:
- Band-limited functions correspond to points in infinite-dimensional space
- Coordinates $X_n$ represent the expansion coefficients
- Functions limited to band W and duration T correspond to points in $2TW$-dimensional space

**Geometric Relationships**:
- Functions with total energy ≤ E correspond to points within a sphere of radius $r = \sqrt{2WE}$
- Function ensembles are represented by probability distributions $p(x₁,...,x_n)$ in this space
- For unlimited time functions, $2TW$ coordinates represent the function structure over interval T

### Statistical Structure

**Ensemble Representation**: Band-limited ensembles are characterized by probability distributions in the finite-dimensional coordinate space, providing a bridge between continuous function theory and finite-dimensional probability theory.

## Section 20: Entropy of a Continuous Distribution

### Definition and Basic Properties

**Continuous Entropy Definition**:
For a continuous distribution with density $p(x)$:
$$H = -\int_{-∞}^∞ p(x) \log p(x) dx$$

For n-dimensional distributions:
$$H = -\int···\int p(x₁,...,x_n) \log p(x₁,...,x_n) dx₁···dx_n$$

**Joint and Conditional Entropies**:
- Joint entropy: $H(x,y) = -\iint p(x,y) \log p(x,y) dx dy$
- Conditional entropies: $H_x(y) = -\iint p(x,y) \log \frac{p(x,y)}{p(x)} dx dy$

### Fundamental Properties

1. **Maximum Entropy**: For fixed volume v, entropy is maximized when $p(x)$ is uniform, giving $H(x) = \log v$

2. **Independence**: $H(x,y) ≤ H(x) + H(y)$ with equality iff x and y are independent

3. **Averaging Operations**: Generalized averaging increases entropy

4. **Decomposition**: $H(x,y) = H(x) + H_x(y) = H(y) + H_y(x)$

5. **Gaussian Maximum**: For fixed standard deviation σ, the Gaussian distribution maximizes entropy:
   $$p(x) = \frac{1}{\sqrt{2π}σ}e^{-x²/(2σ²)}$$

6. **Gaussian Entropy**: One-dimensional Gaussian with standard deviation σ has entropy:
   $$H(x) = \log \sqrt{2πe}σ$$

7. **Exponential Maximum**: For positive variables with fixed mean a:
   $$p(x) = \frac{1}{a}e^{-x/a}, \quad H = \log ea$$

### Coordinate System Dependence

**Critical Difference from Discrete Case**: Continuous entropy is **relative to the coordinate system**, unlike discrete entropy which measures absolute randomness.

**Coordinate Transformation**: Under transformation to coordinates $y₁...y_n$:
$$H(y) = H(x) - \int···\int p(x₁,...,x_n) \log J\left(\frac{x}{y}\right) dx₁...dx_n$$

where J is the Jacobian of the transformation.

**Linear Transformations**: For $y_j = \sum_i a_{ij} x_i$:
$$H(y) = H(x) + \log |a_{ij}|$$

**Information Theoretic Significance**: Although individual entropies depend on coordinates, **entropy differences** (crucial for information rates and channel capacities) are coordinate-independent.

### Entropy Rate for Function Ensembles

**Definition**: For band-limited ergodic ensembles:
$$H' = -\lim_{n→∞} \frac{1}{n} \int···\int p(x₁,...,x_n) \log p(x₁,...,x_n) dx₁...dx_n$$

**Entropy per Second**: $H = 2WH'$ where W is the bandwidth.

**White Noise**: For Gaussian white noise with power N:
- $H' = \log \sqrt{2πeN}$
- $H = W \log 2πeN$
- White noise has maximum entropy for given power

### Entropy Power

**Definition**: The power in white noise (limited to the same band) that has the same entropy:
$$N₁ = \frac{1}{2πe} \exp 2H'$$

**Geometric Interpretation**: Measures high-probability volume by the squared radius of an equivalent sphere.

**Fundamental Property**: Entropy power of any noise ≤ its actual power (since white noise maximizes entropy for given power).

## Section 22: Entropy Loss in Linear Filters

### Main Result

**Theorem 14**: When an ensemble with entropy $H₁$ per degree of freedom in band W passes through a filter with characteristic $Y(f)$, the output entropy becomes:

$$H₂ = H₁ + \frac{1}{W} \int_W \log |Y(f)|² df$$

### Mathematical Foundation

**Linear Transformation Perspective**: Filtering is essentially a coordinate transformation where frequency components are multiplied by the filter characteristic $Y(f)$.

**Jacobian Calculation**: For n sine and n cosine components:
$$J = \prod_{i=1}^n |Y(f_i)|²$$

In the continuous limit:
$$J = \exp\frac{1}{W}\int_W \log|Y(f)|²df$$

**Entropy Power Form**: If input entropy power is $N₁$, output entropy power is:
$$N₂ = N₁ \exp \frac{1}{W} \int_W \log |Y(f)|² df$$

### Practical Interpretation

**Geometric Mean Gain**: The entropy power is multiplied by the **geometric mean gain** of the filter over the band.

**Decibel Relationship**: If gain is measured in dB, the entropy power increases by the **arithmetic mean dB gain** over the bandwidth.

**Filter Examples**: Shannon provides a table showing various filter characteristics and their corresponding entropy power factors, including:
- Linear rolloff: $-8.69$ dB entropy power gain
- Quadratic rolloff: $-5.33$ dB entropy power gain  
- Square root rolloff: $-2.67$ dB entropy power gain

## Section 23: Entropy of a Sum of Two Ensembles

### Ensemble Addition

**Mathematical Framework**: When combining two ensembles $f_α(t)$ and $g_β(t)$ with density functions $p(x₁,...,x_n)$ and $q(x₁,...,x_n)$, the sum has density:

$$r(x₁,...,x_n) = \int···\int p(y₁,...,y_n)q(x₁-y₁,...,x_n-y_n)dy₁···dy_n$$

This **convolution operation** represents the mathematical addition of signals or noises.

### Fundamental Bounds

**Theorem 15**: For two ensembles with average powers $N₁$, $N₂$ and entropy powers $\overline{N₁}$, $\overline{N₂}$, the entropy power of their sum $\overline{N₃}$ satisfies:

$$\overline{N₁} + \overline{N₂} ≤ \overline{N₃} ≤ N₁ + N₂$$

### White Noise Absorption Property

**Special Case**: White Gaussian noise can "absorb" other signal ensembles with remarkable properties:

**Conditions**: When signal power is small compared to white noise power N, the resulting entropy power approximately equals the sum of noise power and signal power.

**Mathematical Analysis**:
1. White noise corresponds to spherical Gaussian distribution in function space
2. Signal ensemble has second moments $a_{ij}$ about its center of gravity
3. Coordinate rotation aligns with principal directions, giving diagonal form $b_{ii}$
4. Requirement: each $b_{ii} << N$

**Result**: Convolution produces approximately Gaussian distribution with entropy power:
$$\left[\prod(N+b_{ii})\right]^{1/n} ≈ N + \frac{1}{n}\sum b_{ii}$$

The first term represents noise power, the second represents signal power.

## Mathematical Foundations Summary

Part III establishes several crucial mathematical concepts:

1. **Function Ensembles**: Extends probability theory to continuous function spaces, providing the framework for continuous communication theory.

2. **Sampling and Dimensionality**: Shows that band-limited continuous functions can be treated as points in finite-dimensional spaces, bridging continuous and discrete theories.

3. **Continuous Entropy**: Extends Shannon entropy to continuous distributions while identifying key differences from discrete case (coordinate dependence).

4. **Linear Systems**: Demonstrates how linear filtering affects entropy through geometric mean gain, connecting information theory to classical filter theory.

5. **Signal Combination**: Provides bounds for entropy when combining signals, with special results for white noise systems.

These mathematical tools prepare the foundation for analyzing continuous communication channels, where signals and noise are continuous functions rather than discrete symbols. The transition from discrete to continuous information theory requires these sophisticated probability-theoretic and functional-analytic concepts, while preserving the essential information-theoretic insights of the discrete case.