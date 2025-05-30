# Fuzzy System Definition: Protein Intake (BMI Input)

This document outlines the fuzzy logic system components designed to estimate daily **Protein** intake based on BMI, Body Fat percentage, Gender, and Age. It includes comprehensive rule sets for both Mamdani and Sugeno inference methods.

**Dataset:** `fuzzy_macros_dataset_bmi.csv`
**Inputs:** BMI (kg/m²), BodyFat (%), Sex (M/F), Age (years)
**Output:** Protein_g (grams)

## 1. Fuzzy Variables and Membership Functions (MFs)

Triangular (trimf) and Trapezoidal (trapmf) MFs are used.

### 1.1. Input: BMI (kg/m²)
*   **Universe:** [15, 50]
*   **Terms:** Underweight, Normal, Overweight, Obese
*   **MFs:**
    *   `Underweight`: trapmf(BMI, [15, 15, 17, 18.5])
    *   `Normal`: trimf(BMI, [17, 21.75, 25])
    *   `Overweight`: trimf(BMI, [25, 27.5, 30])
    *   `Obese`: trapmf(BMI, [30, 35, 50, 50])

### 1.2. Input: BodyFat % (Men)
*   **Universe:** [2, 60] %
*   **Terms:** Lean_M, Normal_M, High_M
*   **MFs:**
    *   `Lean_M`: trapmf(BodyFat, [2, 2, 8, 14])
    *   `Normal_M`: trimf(BodyFat, [10, 18, 25])
    *   `High_M`: trapmf(BodyFat, [20, 30, 60, 60])

### 1.3. Input: BodyFat % (Women)
*   **Universe:** [10, 60] %
*   **Terms:** Lean_F, Normal_F, High_F
*   **MFs:**
    *   `Lean_F`: trapmf(BodyFat, [10, 10, 18, 24])
    *   `Normal_F`: trimf(BodyFat, [20, 28, 35])
    *   `High_F`: trapmf(BodyFat, [30, 40, 60, 60])

### 1.4. Input: Age (years)
*   **Universe:** [18, 80] years
*   **Terms:** Young, Middle, Senior
*   **MFs:**
    *   `Young`: trapmf(Age, [18, 18, 25, 40])
    *   `Middle`: trimf(Age, [30, 45, 60])
    *   `Senior`: trapmf(Age, [50, 65, 80, 80])

### 1.5. Output: Protein Intake (g)
*   **Universe:** [50, 200] g (Adjust based on dataset min/max if needed)
*   **Terms:** Low, Medium, High
*   **MFs (Mamdani):**
    *   `Low`: trapmf(Protein, [50, 50, 75, 100])
    *   `Medium`: trimf(Protein, [80, 125, 160])
    *   `High`: trapmf(Protein, [140, 170, 200, 200])
*   **Sugeno Constants:**
    *   `Protein_Low` = 80
    *   `Protein_Medium` = 125
    *   `Protein_High` = 170

## 2. Comprehensive Fuzzy Rules

Inputs considered: BMI (4 levels), BodyFat (3 levels/gender), Age (3 levels).
Total Rules = 4 * 3 * 3 * 2 (genders) = 72.

### 2.1. Mamdani System
*   **Operators:** AND (min), OR (max), Implication (min), Aggregation (max)
*   **Defuzzification:** Centroid
*   **Rules:**
    1. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein is Medium)
    2. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein is Medium)
    3. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein is Low)
    4. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein is Low)
    5. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein is Low)
    6. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein is Low)
    7. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein is Low)
    8. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein is Low)
    9. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein is Low)
    10. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein is High)
    11. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein is High)
    12. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein is Low)
    13. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein is High)
    14. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein is Medium)
    15. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein is Low)
    16. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein is Low)
    17. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein is Low)
    18. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein is Low)
    19. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein is High)
    20. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein is High)
    21. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein is Low)
    22. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein is High)
    23. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein is High)
    24. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein is Low)
    25. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein is Low)
    26. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein is Low)
    27. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein is Low)
    28. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein is Medium)
    29. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein is Low)
    30. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein is Low)
    31. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein is Medium)
    32. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein is Low)
    33. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein is Low)
    34. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein is Low)
    35. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein is Low)
    36. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein is Low)
    37. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein is Medium)
    38. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein is Medium)
    39. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein is Low)
    40. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein is Low)
    41. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein is Low)
    42. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein is Low)
    43. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein is Low)
    44. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein is Low)
    45. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein is Low)
    46. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein is High)
    47. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein is High)
    48. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein is Low)
    49. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein is High)
    50. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein is Medium)
    51. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein is Low)
    52. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein is Low)
    53. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein is Low)
    54. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein is Low)
    55. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein is High)
    56. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein is High)
    57. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein is Low)
    58. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein is High)
    59. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein is High)
    60. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein is Low)
    61. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein is Low)
    62. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein is Low)
    63. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein is Low)
    64. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein is Medium)
    65. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein is Low)
    66. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein is Low)
    67. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein is Medium)
    68. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein is Low)
    69. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein is Low)
    70. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein is Low)
    71. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein is Low)
    72. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein is Low)

### 2.2. Sugeno System (Zero-Order)
*   **Operators:** AND (min), OR (max), Aggregation (Weighted Average)
*   **Rules:**
    1. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein = Protein_Medium)
    2. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein = Protein_Medium)
    3. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    4. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein = Protein_Low)
    5. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    6. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    7. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein = Protein_Low)
    8. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    9. IF (Sex is M) AND (BMI is Underweight) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    10. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein = Protein_High)
    11. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein = Protein_High)
    12. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    13. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein = Protein_High)
    14. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein = Protein_Medium)
    15. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    16. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein = Protein_Low)
    17. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    18. IF (Sex is M) AND (BMI is Normal) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    19. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein = Protein_High)
    20. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein = Protein_High)
    21. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    22. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein = Protein_High)
    23. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein = Protein_High)
    24. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    25. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein = Protein_Low)
    26. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    27. IF (Sex is M) AND (BMI is Overweight) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    28. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Lean_M) AND (Age is Young) THEN (Protein = Protein_Medium)
    29. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Lean_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    30. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Lean_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    31. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Normal_M) AND (Age is Young) THEN (Protein = Protein_Medium)
    32. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Normal_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    33. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is Normal_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    34. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is High_M) AND (Age is Young) THEN (Protein = Protein_Low)
    35. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is High_M) AND (Age is Middle) THEN (Protein = Protein_Low)
    36. IF (Sex is M) AND (BMI is Obese) AND (BodyFat is High_M) AND (Age is Senior) THEN (Protein = Protein_Low)
    37. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein = Protein_Medium)
    38. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein = Protein_Medium)
    39. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    40. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein = Protein_Low)
    41. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    42. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    43. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein = Protein_Low)
    44. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    45. IF (Sex is F) AND (BMI is Underweight) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    46. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein = Protein_High)
    47. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein = Protein_High)
    48. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    49. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein = Protein_High)
    50. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein = Protein_Medium)
    51. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    52. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein = Protein_Low)
    53. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    54. IF (Sex is F) AND (BMI is Normal) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    55. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein = Protein_High)
    56. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein = Protein_High)
    57. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    58. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein = Protein_High)
    59. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein = Protein_High)
    60. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    61. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein = Protein_Low)
    62. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    63. IF (Sex is F) AND (BMI is Overweight) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    64. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Lean_F) AND (Age is Young) THEN (Protein = Protein_Medium)
    65. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Lean_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    66. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Lean_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    67. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Normal_F) AND (Age is Young) THEN (Protein = Protein_Medium)
    68. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Normal_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    69. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is Normal_F) AND (Age is Senior) THEN (Protein = Protein_Low)
    70. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is High_F) AND (Age is Young) THEN (Protein = Protein_Low)
    71. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is High_F) AND (Age is Middle) THEN (Protein = Protein_Low)
    72. IF (Sex is F) AND (BMI is Obese) AND (BodyFat is High_F) AND (Age is Senior) THEN (Protein = Protein_Low)

---
*Note:* The rule outputs are based on general physiological principles and the assumed macro split. Fine-tuning these rules based on the specific dataset and desired model behavior is crucial for achieving high accuracy.
