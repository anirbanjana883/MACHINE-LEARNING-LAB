🧩 1. Imports
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
import pandas as pd


You import:

matplotlib.pyplot → for plotting graphs.

numpy → for numerical operations.

seaborn → for easy statistical plotting (like regression plots).

pandas → for creating and managing tabular data (dataframes).

🧮 2. The coeff() Function — Calculate Regression Coefficients
def coeff(x, y):
    n = np.size(x)
    mx = np.mean(x)
    my = np.mean(y)
    ss_xy = np.sum(x * y) - n * mx * my
    ss_xx = np.sum(x * x) - n * mx * mx
    b1 = ss_xy / ss_xx
    b0 = my - b1 * mx
    return (b0, b1)

This function manually computes the coefficients b₀ (intercept) and b₁ (slope) using the least squares method (like simple linear regression).
<img width="1013" height="193" alt="image" src="https://github.com/user-attachments/assets/7b1972d4-fb85-499f-87dd-8c514c711f69" />

⚠️ Note:
This is linear regression, not true logistic regression — but we’ll later apply the sigmoid transformation to make it “logistic-like.”

📉 3. The lr_plot() Function — Plot Logistic Regression
def lr_plot(df, b):
    sns.regplot(x='age', y='insurance', data=df, logistic=True, marker='o', color='r')
    plt.xlabel("age")
    plt.ylabel("insurance")
    plt.title("graph")
    plt.show()


This uses seaborn.regplot() with the parameter logistic=True.

logistic=True → fits a logistic curve (sigmoid-shaped) rather than a straight line.

marker='o' → circular markers for the data points.

color='r' → red color for points and curve.

So, this shows how the probability of having insurance (y-axis) changes with age (x-axis).

🧠 4. The main() Function
def main():
    age = [22, 25, 47, 52, 46 ,56,55, 60, 62, 61, 18, 28, 27, 29]
    insurance = [0, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 0, 0, 0]

    df = pd.DataFrame({'age': age, 'insurance': insurance})

    x = df['age'].values.reshape(-1, 1)
    y = df['insurance'].values
    b = coeff(x, y)

    print("b0 & b1 values are:\n  b0 = {:.4f}\n  b1 = {:.4f}".format(b[0], b[1]))
    lr_plot(df, b)

Breakdown:

Creates two arrays:

age → independent variable (x)

insurance → dependent variable (y: 0 or 1)

Converts them into a pandas DataFrame df.

Calculates the linear regression coefficients using your custom coeff().

Prints them:

b0 = -39.4995
b1 = 0.9507


Passes the dataframe and coefficients to lr_plot() for visualization.

🧮 5. The Logistic Concept (what’s happening behind the scenes)

Even though you computed b0 and b1 linearly, logistic regression conceptually models:

<img width="857" height="100" alt="image" src="https://github.com/user-attachments/assets/b976ed06-0c09-4f51-8ec8-3a3c4008d0f0" />
That’s the sigmoid function, mapping any real number to a probability between 0 and 1.

Your Seaborn plot (logistic=True) automatically applies this transformation to show that S-shaped logistic curve.

⚠️ 6. The Warning Message
C:\Users\DELL\anaconda3\lib\site-packages\statsmodels\genmod\families\links.py:187: RuntimeWarning: overflow encountered in exp
  t = np.exp(-z)
  
This means that in the exponential calculation np.exp(-z), the value of z was too large (very positive or very negative).

  <img width="1053" height="476" alt="image" src="https://github.com/user-attachments/assets/c436491d-e386-4d75-bad3-3aad929de7dd" />


| Step        | Function                                                 | Purpose                           |
| ----------- | -------------------------------------------------------- | --------------------------------- |
| `coeff()`   | Computes regression coefficients manually                | Linear relationship setup         |
| `lr_plot()` | Plots logistic regression with seaborn                   | Visualize sigmoid fit             |
| `main()`    | Loads data, computes b₀, b₁, prints results, plots graph | Driver function                   |
| Output      | Logistic curve + coefficient values                      | Understanding logistic regression |

🖼️ 8. Example Output

Printed coefficients:

b0 = -39.4995
b1 = 0.9507


Plot:
Red data points (ages vs insurance status), with a blue S-shaped logistic curve showing probability of having insurance increasing with age.

