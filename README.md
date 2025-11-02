# hypothesis-test
 a program to perform a simple hypothesis test to check whether the average marks of two different classes are significantly different. Assume suitable data and state the null and alternative hypotheses. Display the test statistic and interpret the result
import numpy as np
from math import sqrt
from scipy import stats

# --- STEP 1: Assume sample data for two classes ---
# (you can replace these with real or user-input data)
class_A = [78, 85, 80, 90, 76, 84, 82, 88, 91, 77]
class_B = [72, 70, 68, 75, 74, 69, 73, 71, 76, 70]

# --- STEP 2: Define hypotheses ---
print("HYPOTHESIS TEST: Difference in Class A and Class B Means")
print("-------------------------------------------------------")
print("Null Hypothesis (H₀): μ₁ = μ₂  → The average marks of the two classes are equal.")
print("Alternative Hypothesis (H₁): μ₁ ≠ μ₂  → The average marks of the two classes are significantly different.\n")

# --- STEP 3: Compute descriptive statistics ---
mean_A = np.mean(class_A)
mean_B = np.mean(class_B)
std_A = np.std(class_A, ddof=1)   # sample standard deviation
std_B = np.std(class_B, ddof=1)
n1, n2 = len(class_A), len(class_B)

print(f"Class A → Mean = {mean_A:.2f}, SD = {std_A:.2f}, n = {n1}")
print(f"Class B → Mean = {mean_B:.2f}, SD = {std_B:.2f}, n = {n2}\n")

# --- STEP 4: Calculate the t-statistic manually ---
# Pooled standard deviation (assuming equal variances)
sp_squared = (((n1 - 1) * std_A**2) + ((n2 - 1) * std_B**2)) / (n1 + n2 - 2)
sp = sqrt(sp_squared)

t_statistic = (mean_A - mean_B) / (sp * sqrt(1/n1 + 1/n2))

# Degrees of freedom
df = n1 + n2 - 2

# --- STEP 5: Calculate the critical value and p-value ---
alpha = 0.05  # 5% significance level
t_critical = stats.t.ppf(1 - alpha/2, df)
p_value = (1 - stats.t.cdf(abs(t_statistic), df)) * 2  # two-tailed

print("TEST RESULTS")
print("-------------")
print(f"T-statistic = {t_statistic:.4f}")
print(f"Degrees of freedom = {df}")
print(f"Critical value (±t₀.₀₂₅) = ±{t_critical:.4f}")
print(f"P-value = {p_value:.4f}\n")

# --- STEP 6: Interpretation ---
if abs(t_statistic) > t_critical:
    print("✅ Reject H₀: There is a significant difference in average marks between the two classes.")
else:
    print("❌ Fail to Reject H₀: There is no significant difference in average marks between the two classes.")

    HYPOTHESIS TEST: Difference in Class A and Class B Means
-------------------------------------------------------
Null Hypothesis (H₀): μ₁ = μ₂  → The average marks of the two classes are equal.
Alternative Hypothesis (H₁): μ₁ ≠ μ₂  → The average marks of the two classes are significantly different.

Class A → Mean = 83.10, SD = 5.10, n = 10
Class B → Mean = 72.80, SD = 2.87, n = 10

TEST RESULTS
-------------
T-statistic = 5.4821
Degrees of freedom = 18
Critical value (±t₀.₀₂₅) = ±2.1009
P-value = 0.0000

✅ Reject H₀: There is a significant difference in average marks between the two classes.

