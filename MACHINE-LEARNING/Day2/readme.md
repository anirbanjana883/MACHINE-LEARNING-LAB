# =====================================
# 📘 LINEAR REGRESSION EXPLAINED LINE BY LINE
# =====================================

import numpy as np                     # Import numpy for mathematical operations and array handling
import matplotlib.pyplot as plt         # Import matplotlib for plotting and visualizing data


def coeff(x, y):                        # Define a function to calculate regression coefficients (slope & intercept)
    n = np.size(x)                      # Get total number of data points in x
    mx = np.mean(x)                     # Calculate mean (average) of x values
    my = np.mean(y)                     # Calculate mean (average) of y values

    # Calculate covariance of x and y (numerator part for slope)
    ss_xy = np.sum(x * y) - n * mx * my

    # Calculate variance of x (denominator part for slope)
    ss_xx = np.sum(x * x) - n * mx * mx

    b1 = ss_xy / ss_xx                  # Compute slope (b1) using formula: b1 = cov(x, y) / var(x)
    b0 = my - (b1 * mx)                 # Compute intercept (b0) using formula: b0 = mean(y) - b1 * mean(x)
    return (b0, b1)                     # Return both coefficients as a tuple (b0, b1)


def lr_plot(p, q, b):                   # Define a function to plot regression line with data points
    plt.scatter(p, q, color='r', marker='s', s=50)   # Plot the original data points as red squares
    y_out = b[0] + b[1] * p             # Calculate predicted y values using regression line equation: y = b0 + b1*x
    plt.plot(p, y_out, color='g')       # Plot the regression line in green
    plt.xlabel("x axis")                # Label x-axis
    plt.ylabel("y axis")                # Label y-axis
    plt.title("Linear Regression Plot") # Add a title for clarity
    plt.show()                          # Display the plot on screen


def main():                             # Define the main function (entry point)
    # Create sample data arrays for x (independent variable) and y (dependent variable)
    x = np.array([0,1,2,3,4,5,6,7,8,9])
    y = np.array([1,3,2,5,7,8,8,9,10,12])

    b = coeff(x, y)                     # Call coeff() to calculate intercept (b0) and slope (b1)
    print("b0 = {} and b1 = {}".format(b[0], b[1]))   # Print the coefficients

    lr_plot(x, y, b)                    # Call lr_plot() to visualize data points and regression line



    # =====================================
# ⚡ SIGMOID CURVE EXPLAINED LINE BY LINE
# =====================================

import numpy as np                      # Import numpy for numerical computations
import matplotlib.pyplot as plt         # Import matplotlib for plotting the curve

# Create an array of 100 evenly spaced values from -10 to 10
x = np.linspace(-10, 10, 100)

# Apply sigmoid formula: σ(x) = 1 / (1 + e^(-x))
z = 1 / (1 + np.exp(-x))

plt.plot(x, z, color='b')               # Plot the sigmoid curve in blue
plt.title("Sigmoid Function")           # Add a title to the plot
plt.xlabel("x values")                  # Label x-axis
plt.ylabel("σ(x) values")               # Label y-axis
plt.grid(True)                          # Add grid lines for better readability
plt.show()                              # Display the sigmoid curve



if __name__ == "__main__":              # This ensures code runs only if file is executed directly (not imported)
    main()                              # Call main() to execute the regression process
