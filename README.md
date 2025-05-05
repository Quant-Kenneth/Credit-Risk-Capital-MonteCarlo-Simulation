# Credit Risk Capital Estimation using Rating Transitions and Monte Carlo Simulation

## 1. Problem Statement: How Much Capital Should a Bank Hold Against Credit Risk?

Credit risk is the potential for a borrower to default or experience a downgrade in credit quality. For banks and financial institutions, failing to properly account for this risk can lead to significant losses and regulatory issues.

Under frameworks such as **Basel III** and **ICAAP**, institutions are required to calculate:
- **Expected Loss (EL)** – the average credit loss over a period
- **Unexpected Loss (UL)** – the potential deviation from the expected loss
- **Economic Capital** – the capital needed to absorb losses with a high confidence level (e.g., 99%)

The key question:
> **How much capital should the institution reserve to remain solvent under plausible worst-case scenarios?**

---

## 2. Methodology: Why This Approach?

We address the problem by modeling credit rating migrations as a **Markov process**, where each borrower's rating can change based on historical transition probabilities. This is a well-established method in credit risk modeling, aligning with industry practices and data availability.

Key components of our approach:
- **Transition Matrix** from Moody’s to capture rating dynamics
- **Default Probabilities (PD)** and **Recovery Rates** based on internal assumptions
- **Exposure at Default (EAD)** of $1 million per asset
- **Monte Carlo Simulation** with 1,000 iterations to capture portfolio loss variability

This combination allows us to:
- Simulate future credit rating paths
- Estimate portfolio loss distribution
- Calculate **Credit Value-at-Risk (VaR)** at 99% and 99.9% levels
- Determine the **capital buffer** required to absorb those losses

---

## 3. Solution: Simulation-Based Risk Quantification

### ➤ Input Ratings & Assumptions

| Rating | PD     | Recovery Rate |
|--------|--------|----------------|
| A      | 0.00   | 100%           |
| B      | 0.10   | 90%            |
| C      | 0.45   | 80%            |
| D      | 0.80   | 75%            |
| E      | 1.00   | 70%            |

Transition matrix used (simplified from Moody’s historical data):

| From \ To | A      | B      | C      | D      | E      |
|-----------|--------|--------|--------|--------|--------|
| A         | 0.923  | 0.076  | 0.001  | 0.000  | 0.000  |
| B         | 0.024  | 0.970  | 0.005  | 0.001  | 0.000  |
| C         | 0.001  | 0.004  | 0.929  | 0.063  | 0.003  |
| D         | 0.000  | 0.001  | 0.069  | 0.909  | 0.021  |
| E         | 0.000  | 0.000  | 0.027  | 0.054  | 0.919  |


---

### ➤ Simulation Results

#### 🔹 Per-Rating Risk Metrics (EAD = $1M)

| Rating | Expected Loss ($) | Unexpected Loss ($) | Economic Capital ($) |
|--------|-------------------|---------------------|-----------------------|
| A      | 850               | 3,870               | 9,017                 |
| B      | 10,350            | 8,389               | 19,547                |
| C      | 97,150            | 29,617              | 69,008                |
| D      | 194,320           | 32,384              | 75,455                |
| E      | 288,930           | 40,102              | 93,437                |

#### 🔹 Portfolio-Level Monte Carlo Simulation (1,000 Iterations)

- **Expected Loss (EL)**: $64.64M  
- **Credit VaR (99%)**: $66.16M  
- **Credit VaR (99.9%)**: $66.88M

#### 🔹 Capital Estimation Approaches

| Approach | Description | Capital Required ($) |
|----------|-------------|----------------------|
| 1        | VaR - EL (Economic Capital) | 1,518,260 |
| 2        | Full VaR Reserve (Regulatory View) | 66,160,200 |

---


## 4. Conclusion: Key Takeaways

- **Rating transitions** provide a realistic model of credit migration risk.
- **Lower-rated assets (C, D, E)** account for the majority of credit loss and volatility.
- Even though the **expected loss** is ~64M, institutions should hold **at least $1.5M in Economic Capital** for a 99% confidence level — or more depending on regulatory requirements.
- The framework is flexible for stress testing, sensitivity analysis, and adapting to real portfolio data.
- This approach demonstrates not only technical proficiency with modeling and simulation, but also awareness of **real-world regulatory implications**.

---

## 🔍 About This Project

This simulation was developed as part of a Quantitative Finance and Risk Modeling portfolio. The objective is to showcase strong skills in:
- **Probability theory & stochastic modeling**
- **Python for financial modeling**
- **Quantitative risk measurement techniques**
- **Clear and effective risk communication**

For questions or collaboration, feel free to connect.

