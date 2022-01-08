# Shopify Data Science Internship Application

### Question 1

First, load the data and plot it.


```python
import pandas as pd
orders = pd.read_csv('2019 Winter Data Science Intern Challenge Data Set - Sheet1.csv')
orders["order_amount"].hist()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x114f37f28>




    
![png](Question%201_2_1.png)
    


After plotting the distribution of order_amount, I can see that there are a few orders that are much larger than the regular orders. These outliers made it so that the average is much larger than expected. Instead of using the average order value, it would be better to use the median order value so that these outliers don't skew our metric.


```python
print("The median order value is: ", orders["order_amount"].median())
```

    The median order value is:  284.0


