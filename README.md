# Waveform-Based Feature Analysis in Financial and Economic Times

**Authors:** Dharun Ramesh

## Introduction
### Objective
The goal of this analysis is to understand patterns and drivers in financial time series (e.g., stock prices) using waveform analysis. This approach leverages **conic sections** and **Fourier transforms** to extract deep insights from financial data.

### Key Concepts
* **Dispersion:** Similar to how white light is composed of component colors, the target (e.g., stock price) is viewed as a superposition of feature "frequencies."
* **Conic Sections:** Ellipses, Parabolas, and Hyperbolas are used to model the relationships between features and the target.
* **Waveforms:** These transform feature-target relationships into curves that capture trends, cyclicality, and anomalies.

---

## Waveform Equations & Selection
Waveforms are chosen based on the correlation coefficient ($r$) between a feature ($x$) and the target ($y$).

### 1. Ellipse Wave
* **Condition:** Used when $r > 0.1$ (Strong correlation).
* **Purpose:** Captures cyclical patterns.
* **Equation:**
    $$y = \mu_{y} + \sigma_{y} \sqrt{1 - \frac{(x - \mu_{x})^{2}}{\sigma_{x}^{2}}}$$

### 2. Parabola Wave
* **Condition:** Used when $r < 0.1$ (Weak correlation).
* **Purpose:** Captures trends without saturation.
* **Equation:**
    $$y = \mu_{y} + \frac{\sigma_{y}^{2}}{\sigma_{x}^{2}} (x - \mu_{x})^{2}$$

### 3. Hyperbola Wave
* **Condition:** Intermediate/specific correlations.
* **Purpose:** Captures growth or decay outside of the standard deviation.
* **Equation:**
    $$y = \mu_{y} + \sigma_{y} \sqrt{\frac{(x - \mu_{x})^{2}}{\sigma_{x}^{2}} - 1}$$
    *(Valid for $|x - \mu_{x}| \geq \sigma_{x}$)*

---

## Spectral Analysis (Fourier Transform)
Using Fast Fourier Transform (FFT), we identify underlying frequency patterns to distinguish noise from meaningful signals.

| Feature | Dominant Frequency | Observation |
| :--- | :--- | :--- |
| **Open Price** | High (~0.38) | Fast, repetitive movements; high short-term noise. |
| **GDP Growth** | Low (~0.17) | Slower, fundamental macro cycles; less structural noise. |

### Key Spectral Metrics:
* **Drift Score:** Indicates regime changes or long-term shifts.
* **Harmonic Count:** Higher counts imply more interacting cyclical forces (common in price data).
* **High-frequency Fraction:** Measures the "jumpiness" or volatility of the variable.

---

## Machine Learning Integration
The waveform transforms are used as enhanced features in machine learning models to improve prediction accuracy (RMSE).

### Model Performance Comparison:
* **Linear Regression**
* **Random Forest**
* **AdaBoost**
* **LightGBM**
* **XGBoost** (Often yields the lowest error in these time-series applications).

---

## Key Takeaways
1.  **Nonlinear Dependency:** Waveform analysis captures cyclical dependencies that standard linear models miss.
2.  **Frequency Insights:** Fourier Transforms help distinguish between macro-driven cycles and short-term market sentiment.
3.  **Interpretability:** Provides a mathematical reason ("the why") behind feature-driven predictions.
4.  **Improved Accuracy:** Integration with ML models (like XGBoost) enhances feature representation and reduces RMSE.
