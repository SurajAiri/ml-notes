Here’s a list of popular metrics for regression models, along with explanations on when to use them and when to avoid them:

### 1. **Mean Absolute Error (MAE)**
   - **Formula**:  
     \[
     \text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|
     \]
   - **When to Use**: 
     - When you want a metric that is easy to understand and interpret.
     - When you prefer to treat all errors equally, regardless of whether they are small or large.
     - When your data has outliers but you don't want them to have a disproportionate effect on the model evaluation.
   - **When to Avoid**: 
     - If you care about penalizing larger errors more, as MAE treats all errors equally.

### 2. **Mean Squared Error (MSE)**
   - **Formula**:  
     \[
     \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
     \]
   - **When to Use**: 
     - When you want to penalize larger errors more heavily (since squaring the errors increases the impact of larger discrepancies).
     - When outliers are important in your analysis and you want to give them more weight.
     - Common for optimizing regression models during training (e.g., in linear regression).
   - **When to Avoid**: 
     - If outliers are not significant to your model, as MSE can be overly sensitive to them.

### 3. **Root Mean Squared Error (RMSE)**
   - **Formula**:  
     \[
     \text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
     \]
   - **When to Use**: 
     - When you want to interpret the error in the same units as the target variable (unlike MSE, which is in squared units).
     - When you need to penalize larger errors but prefer the error to be more interpretable than MSE.
   - **When to Avoid**: 
     - Similar to MSE, avoid if outliers should not have a disproportionate effect on your model.

### 4. **R-squared (R²)**
   - **Formula**:  
     \[
     R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}
     \]
   - **When to Use**: 
     - When you want to measure how well your model fits the data (explains variance).
     - When you want a percentage representation of the model's explanatory power.
     - It's useful for comparing models (higher R² means a better fit).
   - **When to Avoid**: 
     - If the model is overfitted, as R² can be artificially high.
     - For non-linear models, as R² might not be the best fit for evaluating the model’s performance.

### 5. **Adjusted R-squared**
   - **Formula**:  
     \[
     \text{Adjusted } R^2 = 1 - \left(\frac{1 - R^2}{{n - 1}} \times (n - p - 1)\right)
     \]
     where \(p\) is the number of predictors.
   - **When to Use**: 
     - When comparing models with different numbers of predictors.
     - If you want to avoid overestimating the goodness of fit (it adjusts for the number of predictors).
   - **When to Avoid**: 
     - If you have a simple model, as Adjusted R² can be less intuitive in such cases compared to R².

### 6. **Mean Absolute Percentage Error (MAPE)**
   - **Formula**:  
     \[
     \text{MAPE} = \frac{1}{n} \sum_{i=1}^{n} \left|\frac{y_i - \hat{y}_i}{y_i}\right| \times 100
     \]
   - **When to Use**: 
     - When you want to measure prediction accuracy as a percentage.
     - Ideal for problems where relative error matters (e.g., forecasting demand, sales).
   - **When to Avoid**: 
     - If the target values \(y_i\) can be zero or very close to zero, as it will cause large errors or undefined results.
     - If you have highly variable target values, as MAPE can be biased.

### 7. **Huber Loss**
   - **Formula**:  
     \[
     L_{\delta}(a) = \begin{cases} 
      \frac{1}{2} a^2 & \text{for } |a| \leq \delta \\
      \delta (|a| - \frac{1}{2} \delta) & \text{otherwise}
     \end{cases}
     \]
     where \(a = y_i - \hat{y}_i\) and \(\delta\) is a threshold.
   - **When to Use**: 
     - When you want a metric that is robust to outliers, combining the benefits of MSE (for small errors) and MAE (for large errors).
     - Often used in models where you want to minimize the influence of large errors without completely ignoring them.
   - **When to Avoid**: 
     - If you do not need to account for outliers and prefer simpler metrics like MSE or MAE.

### 8. **Log-Cosh Loss**
   - **Formula**:  
     \[
     \text{Log-Cosh Loss} = \frac{1}{n} \sum_{i=1}^{n} \log(\cosh(y_i - \hat{y}_i))
     \]
     where \(\cosh(x) = \frac{e^x + e^{-x}}{2}\).
   - **When to Use**: 
     - When you want a smooth loss function that behaves similarly to MSE for small errors and MAE for large errors.
     - Ideal when you want to avoid the extreme influence of large errors but still recognize them.
   - **When to Avoid**: 
     - If the computation time is a concern, as it involves more complex calculations than basic metrics like MSE or MAE.

---

### Summary:
- **Use MAE** when you want a straightforward metric and don't mind treating all errors equally.
- **Use MSE or RMSE** when penalizing large errors is important.
- **Use R²** when you need to measure model fit, but consider Adjusted R² when comparing models with different numbers of predictors.
- **Avoid MAPE** when the target variable has zero or near-zero values.
- **Use Huber Loss** or **Log-Cosh Loss** for models that need a balance between outlier sensitivity and error penalization.