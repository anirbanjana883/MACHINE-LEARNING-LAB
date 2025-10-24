## 🧮 LINEAR REGRESSION

### 📂 Code
```python
import numpy as np
import matplotlib.pyplot as plt
👉 Imports libraries

numpy (as np) is used for mathematical and array operations.

matplotlib.pyplot (as plt) is used for plotting graphs.

python
Copy code
def coeff(x, y):
👉 Defines a function coeff() that will calculate the regression coefficients (slope and intercept).

python
Copy code
    n = np.size(x)
👉 Finds the number of data points in the array x and stores it in n.

python
Copy code
    mx = np.mean(x)
    my = np.mean(y)
👉 Calculates the mean (average) of both x and y.

python
Copy code
    ss_xy = np.sum(x * y) - n * mx * my  # covariance
👉 Calculates the numerator part of the slope formula (covariance of x and y):

cov
(
𝑥
,
𝑦
)
=
∑
(
𝑥
𝑦
)
−
𝑛
𝑥
ˉ
𝑦
ˉ
cov(x,y)=∑(xy)−n 
x
ˉ
  
y
ˉ
​
 
python
Copy code
    ss_xx = np.sum(x * x) - n * mx * mx  # variance
👉 Calculates the denominator part (variance of x):

var
(
𝑥
)
=
∑
(
𝑥
2
)
−
𝑛
𝑥
ˉ
2
var(x)=∑(x 
2
 )−n 
x
ˉ
  
2
 
python
Copy code
    b1 = (ss_xy / ss_xx)
👉 Computes the slope (b1) using the formula:

𝑏
1
=
cov
(
𝑥
,
𝑦
)
var
(
𝑥
)
b1= 
var(x)
cov(x,y)
​
 
python
Copy code
    b0 = my - (b1 * mx)
👉 Computes the intercept (b0) using:

𝑏
0
=
𝑦
ˉ
−
𝑏
1
𝑥
ˉ
b0= 
y
ˉ
​
 −b1 
x
ˉ
 
python
Copy code
    return (b0, b1)
👉 Returns both coefficients as a tuple — (intercept, slope).

python
Copy code
def lr_plot(p, q, b):
👉 Defines a function lr_plot() that will plot the data points and regression line.

python
Copy code
    plt.scatter(p, q, color='r', marker="s", s=50)
👉 Draws the data points on the graph as red squares (🔴) using a scatter plot.

color='r' → red

marker='s' → square

s=50 → size of marker

python
Copy code
    y_out = (b[0] + b[1] * p)
👉 Calculates the predicted y-values using the regression line equation:

𝑦
=
𝑏
0
+
𝑏
1
𝑥
y=b0+b1x
python
Copy code
    plt.plot(p, y_out, color='g')
👉 Draws the regression line (🟢 green line) based on predicted values.

python
Copy code
    plt.xlabel("x axis")
    plt.ylabel("y axis")
👉 Adds labels to the x-axis and y-axis for better readability.

python
Copy code
    plt.show()
👉 Displays the plot window with both data points and the regression line.

python
Copy code
def main():
👉 Defines the main() function that runs the full program.

python
Copy code
    x = np.array([0,1,2,3,4,5,6,7,8,9])
    y = np.array([1,3,2,5,7,8,8,9,10,12])
👉 Creates two NumPy arrays representing x (input) and y (output) data.

python
Copy code
    b = coeff(x, y)
👉 Calls the coeff() function to compute slope (b1) and intercept (b0), and stores them in b.

python
Copy code
    print("b0 = {} and b1 = {}".format(b[0], b[1]))
👉 Prints the calculated coefficients in a formatted way.

Example Output:

ini
Copy code
b0 = 1.2363636363636363 and b1 = 1.1696969696969697
python
Copy code
    lr_plot(x, y, b)
👉 Calls lr_plot() to display the scatter points and regression line.

python
Copy code
if __name__ == "__main__":
    main()
👉 This ensures the code inside main() runs only when the file is executed directly (not when imported).

📈 RESULT:
Prints coefficients

Displays graph with:

🔴 Red squares → data points

🟢 Green line → best-fit regression line

⚡ SIGMOID CURVE
📂 Code
python
Copy code
import numpy as np
import matplotlib.pyplot as plt
👉 Imports NumPy and Matplotlib again for numerical and plotting tasks.

python
Copy code
x = np.linspace(-10, 10, 100)
👉 Creates an array x with 100 evenly spaced values between -10 and 10.
This acts as our input range for the sigmoid function.

python
Copy code
z = (1 / (1 + np.exp(-x)))
👉 Applies the Sigmoid function:

𝜎
(
𝑥
)
=
1
1
+
𝑒
−
𝑥
σ(x)= 
1+e 
−x
 
1
​
 
Explanation:

np.exp(-x) → computes 
𝑒
−
𝑥
e 
−x
 

1 + np.exp(-x) → denominator of formula

Entire expression → gives values between 0 and 1

Large negative x → output ≈ 0

Large positive x → output ≈ 1

x = 0 → output = 0.5

python
Copy code
plt.plot(x, z)
👉 Plots the sigmoid curve (S-shaped curve) showing how input values map between 0 and 1.

python
Copy code
plt.show()
👉 Displays the final sigmoid graph on the screen.
