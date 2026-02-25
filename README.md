# Hedonic-Real-Estate-Valuation-Model
This project estimates market values of residential properties using a hedonic pricing framework applied to transaction-level data from Douglas County, Colorado.

The objective is to simulate the information available to an investor in December 2012 and predict transaction prices for 191 properties using only historical data available at that time.

---

## Project Motivation

Real estate valuation requires decomposing a property's market value into the implicit prices of its characteristics (size, age, bedrooms, location, etc.). 

This project implements a hedonic regression approach to:

- Estimate the marginal contribution of observable property characteristics
- Incorporate geographic and time fixed effects
- Avoid in-sample overfitting through validation splitting
- Evaluate predictive accuracy against held-out transaction prices

The emphasis is on economic reasoning, careful data cleaning, and model transparency rather than purely black-box prediction.

---

## Data

The dataset consists of:

- ~210,000 arms-length transactions
- ~80,000 unique properties
- Transaction-level and property-level characteristics
- Historical sales from the mid-1980s through December 2012

### Training Data
Contains all transactions up to December 2012.  
For 191 homes sold in December 2012, transaction prices are removed (`Predict == 1`).

### Test Data
Contains the true transaction prices for those 191 homes.  
Used to evaluate out-of-sample prediction performance.

---

## Methodology

### 1. Data Cleaning
- Restriction to arms-length transactions
- Removal of extreme outliers
- Construction of relevant transformations (e.g., log price)
- Creation of time and geographic fixed effects

### 2. Model Specification

A hedonic pricing regression of the form:

\[
\log(P_{it}) = \beta X_{it} + \gamma_{location} + \delta_{time} + \varepsilon_{it}
\]

where:
- \(X_{it}\) includes structural characteristics
- Geographic fixed effects capture local price heterogeneity
- Time fixed effects capture market-wide appreciation

### 3. Validation Strategy

To avoid overfitting:
- A secondary validation sample (e.g., November 2012 or December 2011) was used
- Model complexity (especially geographic fixed effects) was selected based on predictive performance

### 4. Prediction

Predicted log prices were transformed back to levels using smearing correction to address retransformation bias.

---

## Results

Model performance is evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- Scatter plots of actual vs. predicted values
- Residual diagnostics

Prediction errors are analyzed to understand:

- Heterogeneity in valuation accuracy
- Potential omitted characteristics
- Limitations of purely observable hedonic models

---

## Key Takeaways

- Location fixed effects are crucial for accurate valuation.
- Overfitting can easily occur with overly granular geography.
- Log-linear models improve stability and interpretability.
- Even well-specified hedonic models struggle with idiosyncratic property features.

---

## Repository Structure
