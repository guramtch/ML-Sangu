# ML-Sangu
For midterm exam


def calculate_pearson_r(X, Y):
    """
    Calculates the Pearson correlation coefficient (r) between two lists of numbers.

    The calculation uses the raw score formula:
    r = [n * (sum(x*y)) - (sum(x) * sum(y))] /
        sqrt([n * sum(x^2) - (sum(x))^2] * [n * sum(y^2) - (sum(y))^2])
    
    Returns the coefficient 'r' and an error message (or None if successful).
    """
    
    # 1. Check for equal length and minimum data points
    n = len(X)
    if n != len(Y):
        return None, "Error: The lists must have the same number of elements."
    if n < 2:
        return None, "Error: At least two data points are required for correlation."

    # 2. Calculate the required sums using standard Python loops
    sum_x = 0
    sum_y = 0
    sum_x_sq = 0  # Sum of X squared (Σx²)
    sum_y_sq = 0  # Sum of Y squared (Σy²)
    sum_xy = 0    # Sum of (X * Y) (Σxy)

    for i in range(n):
        x_val = X[i]
        y_val = Y[i]

        sum_x += x_val
        sum_y += y_val
        sum_x_sq += x_val * x_val
        sum_y_sq += y_val * y_val
        sum_xy += x_val * y_val

    # 3. Calculate the Numerator
    # Numerator = n * sum(xy) - sum(x) * sum(y)
    numerator = (n * sum_xy) - (sum_x * sum_y)

    # 4. Calculate the Denominator components
    # Denom_X_Part = n * sum(x^2) - (sum(x))^2
    # Denom_Y_Part = n * sum(y^2) - (sum(y))^2
    denom_x_part = (n * sum_x_sq) - (sum_x * sum_x)
    denom_y_part = (n * sum_y_sq) - (sum_y * sum_y)

    # 5. Check for zero variance (division by zero)
    if denom_x_part <= 0 or denom_y_part <= 0:
        # If the variance is zero (all values in X or Y are identical), 
        # the correlation is undefined, but often reported as 0 or 1.
        # Given the data provided, this check is for robustness.
        if denom_x_part == 0 and denom_y_part == 0:
            return 1.0, "Note: Both variables have zero variance (all values are the same)."
        return 0.0, "Note: One of the variables has zero variance (all values are the same)."
        
    # Denominator = sqrt(Denom_X_Part * Denom_Y_Part)
    # Using ** 0.5 for square root, which is standard Python arithmetic
    denominator = (denom_x_part * denom_y_part) ** 0.5

    # 6. Calculate r
    pearson_r = numerator / denominator

    return pearson_r, None

# --- Data provided by the user (as standard Python lists) ---
X_data = [1, 3, 5, 7, -1, -3, -4, -5]
Y_data = [-2, -1, -3, -2, 1, -1, -4, 2] # Data derived from crossing points

# Execute the calculation
r, error = calculate_pearson_r(X_data, Y_data)

print("--- Pearson Correlation Coefficient Calculation (Pure Python) ---")
print(f"X Data: {X_data}")
print(f"Y Data: {Y_data}")

if error:
    print(error)
else:
    print(f"\nPearson Correlation Coefficient (r): {r:.4f}")

    # Interpret the result
    if r > 0.5:
        interpretation = "Strong positive linear correlation."
    elif r >= 0.2:
        interpretation = "Moderate positive linear correlation."
    elif r < -0.5:
        interpretation = "Strong negative linear correlation."
    elif r <= -0.2:
        interpretation = "Moderate negative linear correlation."
    else:
        interpretation = "Weak or no linear correlation."

    print(f"Interpretation: {interpretation}")

    # Re-calculating components for display purposes
    n = len(X_data)
    sum_x = sum(X_data)
    sum_y = sum(Y_data)
    sum_x_sq = sum(x*x for x in X_data)
    sum_y_sq = sum(y*y for y in Y_data)
    sum_xy = sum(X_data[i] * Y_data[i] for i in range(n))

    print("\n--- Manual Calculation Components (Pure Python) ---")
    print(f"n = {n}")
    print(f"Σx = {sum_x}")
    print(f"Σy = {sum_y}")
    print(f"Σx² = {sum_x_sq}")
    print(f"Σy² = {sum_y_sq}")
    print(f"Σxy = {sum_xy}")






    
