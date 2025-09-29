# Bayesian Regression with Shrinkage Priors

This project explores **Bayesian Linear Regression** using **JAGS** on housing data (`homes_mapping_file.txt`). The study compares results between **uninformative Gaussian priors** and **Gaussian shrinkage priors**.

## 📊 Dataset

The dataset contains housing and environmental features. Selected variables include:

* **MeanAnnual.Temperature (x1)**
* **MeanAnnualPrecipitation (x2)**
* **Elevation (x3)**
* **Number of Bedrooms (y)** — transformed with `log()`

## 🧩 Methodology

1. **Preprocessing**:

   * Fixed categorical `NumberBedroooms` (converted `"6 or more"` → `6`).
   * Applied log transformation for normality.
   * Selected subset of predictors and target.

2. **Model Specification**:

   * **Likelihood**:
     [
     y_i \sim \mathcal{N}(\beta_0 + \beta_1 x_{1i} + \beta_2 x_{2i} + \beta_3 x_{3i}, \tau^{-1})
     ]
   * **Priors (Uninformative)**:
     [
     \beta_j \sim \mathcal{N}(0, 1000)
     ]
   * **Priors (Shrinkage)**:
     [
     \beta_j \sim \mathcal{N}(0, \tau_{\beta j}^{-1}), \quad \tau_{\beta j} \sim \text{Gamma}(0.1, 0.1)
     ]

3. **Inference**:

   * MCMC sampling using `rjags` and `coda`.
   * Convergence checked via traceplots.
   * Parameters estimated: (\beta_0, \beta_1, \beta_2, \beta_3, \sigma).

## 📈 Results & Interpretation

* **Uninformative Priors**:

  * All predictors ((x_1, x_2, x_3)) showed **weak positive effects** on the log of bedrooms.
  * Convergence was stable across chains.

* **Gaussian Shrinkage Priors**:

  * Coefficients shrunk closer to **zero**, especially those with weak evidence.
  * Plots were narrower, reflecting reduced variance.
  * Shrinkage reduced risk of **overfitting**.

## 🚀 How to Run

1. Clone this repository.
2. Place `homes_mapping_file.txt` in the working directory.
3. Run the `.Rmd` file in RStudio.
4. Required packages: `rjags`, `coda`.

---

📌 This project demonstrates how **shrinkage priors** improve robustness in Bayesian regression by penalizing weak predictors, a key tool in **Bayesian variable selection and regularization**.
