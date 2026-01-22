# UCS654: Assignment 1 - Nonlinear PDF Parameter Estimation

**Title:** Learn Probability Density Functions using Roll-Number-Parameterized Non-Linear Model  
**Course:** UCS654 - Predictive Analytics  
**Student**: Ikansh Mahajan  
**Roll Number**: 102303754  

**Dataset:** India Air Quality Data (NO2 as feature)  
**Dataset Link:** [Kaggle - India Air Quality Data](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data)

## 📋 Overview

This assignment focuses on learning parameters of a probability density function (PDF) using a roll-number-parameterized non-linear transformation model. The goal is to estimate parameters λ, μ, and c for a target PDF structure using statistical estimation techniques and machine learning approaches.

## 🎯 Objectives

1. **Data Preprocessing**: Clean and prepare NO2 air quality data
2. **Non-linear Transformation**: Apply roll-number-parameterized transformation
3. **Parameter Estimation**: Learn PDF parameters using multiple techniques
4. **Model Comparison**: Compare different estimation approaches

## 📁 Project Structure

```
nonlinear-pdf-parameter-estimation/
├── assign1.ipynb              # Main Jupyter notebook implementation
├── requirements.txt           # Python dependencies
├── submission.json           # Generated submission file
├── submission.csv            # Alternative submission format
├── Assignment-1.pdf          # Assignment specification
├── README.md                 # This file
└── .venv/                    # Virtual environment
```

## 🛠️ Installation & Setup

### Prerequisites

- Python 3.12+
- Jupyter Notebook
- Git

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd nonlinear-pdf-parameter-estimation
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook assign1.ipynb
   ```

## 📊 Dataset

### Source
- **Name**: India Air Quality Data
- **Feature**: NO2 (Nitrogen Dioxide) concentrations
- **Size**: 419,509 records after cleaning

### Data Characteristics
- **Mean**: 25.81 μg/m³
- **Std Dev**: 18.50 μg/m³
- **Range**: 0 - 876 μg/m³
- **Missing Values**: 16,233 (3.73%) - dropped for analysis

### Data Distribution
The NO2 data exhibits:
- Right-skewed distribution
- Heavy tails (extreme pollution events)
- Floor effect at zero (sensor detection limit)
- Log-normal characteristics

## 🔬 Methodology

### Step 1: Data Preprocessing

1. **Load Data**: Import NO2 concentrations from Kaggle dataset
2. **Clean Data**: 
   - Remove null values (3.73% of data)
   - Validate no negative concentrations or infinities
3. **Explore Distribution**: 
   - Histogram analysis
   - Log-transformation for normality assessment
   - Q-Q plots for distribution analysis

### Step 2: Non-linear Transformation

Transform each value `x` into `z` using roll-number-parameterized function:

$$
z = T_r(x) = x + a_r * sin(b_r * x)
$$

Where:
- $a_r = 0.05 * (r\mod{7})$
- $b_r = 0.3 * (r\mod{5} + 1)$
- $r$ = University Roll Number

**Example Parameters (for roll number 102303754):**
- $a = 0.0$
- $b = 1.5$

### Step 3: Parameter Estimation

Target PDF structure:
$$
\hat{p}(z) = c \cdot e^{-\lambda(z-\mu)^2}
$$

#### Estimation Techniques:

1. **Maximum Likelihood Estimation (MLE)**
   - Analytical solution based on normal distribution properties
   - Parameters:
     - $\hat{\mu}$ = mean(z), $\hat{\sigma}^2$ = var(z), $\hat{\lambda} = \frac{1}{2\hat{\sigma}^2}$, $\hat{c}$ = $\sqrt{\frac{\hat{\lambda}}{\pi}}$

2. **Non-linear Curve Fitting**
   - Levenberg-Marquardt algorithm via `scipy.optimize.curve_fit`
   - Minimizes sum of squared residuals
   - Uses MLE results as initial guesses

## 📈 Results

### MLE Parameters:
- **Lambda (λ)**: 0.001460
- **Mu (μ)**: 25.809623
- **C (c)**: 0.021561

### Curve Fit Parameters:
- **Lambda (λ)**: 0.00349
- **Mu (μ)**: 19.90771
- **C (c)**: 0.03196

### Model Comparison:
- MLE provides baseline analytical solution
- Curve fitting offers improved fit to actual distribution
- Both methods capture the central tendency but differ in tail behavior

## 📤 Submission

### Required Parameters:
Submit the estimated parameters (λ, μ, c) through:

**Submission Link**: [Google Form](https://forms.gle/jYF3MDKozRnSCHvR8)

### Submission Files:
- `submission.json`: Automatically generated with parameters
- `submission.csv`: Alternative format

### Submission Format:
```json
{
  "rno": <your_roll_number>,
  "model_parameters": {
    "lambda": <estimated_lambda>,
    "mu": <estimated_mu>,
    "c": <estimated_c>
  }
}
```

## 🔧 Dependencies

### Core Libraries:
- **numpy**: Numerical computations
- **pandas**: Data manipulation
- **matplotlib**: Visualization
- **seaborn**: Statistical plotting
- **scipy**: Scientific computing and optimization

### Additional Tools:
- **kagglehub**: Dataset downloading
- **jupyter**: Notebook environment
- **tqdm**: Progress bars

## 📚 Key Concepts

### Probability Density Functions (PDF)
- Mathematical functions describing likelihood of continuous random variables
- Must integrate to 1 over entire domain
- Used for modeling continuous data distributions

### Maximum Likelihood Estimation (MLE)
- Statistical method for parameter estimation
- Maximizes likelihood function for observed data
- Provides analytical solutions for common distributions

### Non-linear Transformation
- Roll-number-parameterized sine wave modification
- Adds periodic component to original data
- Creates unique transformation per student

### Curve Fitting
- Non-linear optimization problem
- Levenberg-Marquardt algorithm
- Iterative parameter refinement

## 🎓 Learning Outcomes

Upon completion, student understands:

1. **Statistical Parameter Estimation**
   - MLE principles and applications
   - Analytical vs numerical solutions

2. **Data Distribution Analysis**
   - Histogram and Q-Q plot interpretation
   - Log-normal distribution characteristics

3. **Non-linear Modeling**
   - Transformation functions
   - Parameter optimization techniques

4. **Model Evaluation**
   - Visual comparison methods
   - Performance metrics

## 🐛 Troubleshooting

### Common Issues:

1. **Kaggle Dataset Download**
   ```bash
   # Ensure kagglehub is properly installed
   pip install kagglehub
   ```

2. **Memory Issues**
   - Use data sampling for large datasets
   - Clear unused variables

3. **Curve Fitting Convergence**
   - Provide good initial guesses
   - Check parameter bounds
   - Verify data preprocessing

4. **Virtual Environment**
   ```bash
   # If venv activation fails
   python -m venv .venv --clear
   ```

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

**Note**: This assignment is part of UCS654 Predictive Analytics course. Ensure you understand the theoretical concepts before implementing the code.