---
format: html
title: Quarto Document
subtitle: Data Science!
author: Daniel Chen
toc: true
toc-deph: 3
code-overflow: scroll
code-line-numbers: true
execute:
  echo: true
keep-md: true
keep-ipynb: true
---


# Load

::: {.cell execution_count=1}
``` {.python .cell-code}
from palmerpenguins import load_penguins

penguins = load_penguins()
penguins.head()
```

::: {.cell-output .cell-output-display execution_count=1}

```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>species</th>
      <th>island</th>
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
      <th>sex</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>39.1</td>
      <td>18.7</td>
      <td>181.0</td>
      <td>3750.0</td>
      <td>male</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>39.5</td>
      <td>17.4</td>
      <td>186.0</td>
      <td>3800.0</td>
      <td>female</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>40.3</td>
      <td>18.0</td>
      <td>195.0</td>
      <td>3250.0</td>
      <td>female</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>36.7</td>
      <td>19.3</td>
      <td>193.0</td>
      <td>3450.0</td>
      <td>female</td>
      <td>2007</td>
    </tr>
  </tbody>
</table>
</div>
```

:::
:::


# EDA

::: {.cell execution_count=2}
``` {.python .cell-code}
import pandas as pd

penguins.describe()
```

::: {.cell-output .cell-output-display execution_count=2}

```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>342.000000</td>
      <td>342.000000</td>
      <td>342.000000</td>
      <td>342.000000</td>
      <td>344.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>43.921930</td>
      <td>17.151170</td>
      <td>200.915205</td>
      <td>4201.754386</td>
      <td>2008.029070</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.459584</td>
      <td>1.974793</td>
      <td>14.061714</td>
      <td>801.954536</td>
      <td>0.818356</td>
    </tr>
    <tr>
      <th>min</th>
      <td>32.100000</td>
      <td>13.100000</td>
      <td>172.000000</td>
      <td>2700.000000</td>
      <td>2007.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>39.225000</td>
      <td>15.600000</td>
      <td>190.000000</td>
      <td>3550.000000</td>
      <td>2007.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>44.450000</td>
      <td>17.300000</td>
      <td>197.000000</td>
      <td>4050.000000</td>
      <td>2008.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>48.500000</td>
      <td>18.700000</td>
      <td>213.000000</td>
      <td>4750.000000</td>
      <td>2009.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>59.600000</td>
      <td>21.500000</td>
      <td>231.000000</td>
      <td>6300.000000</td>
      <td>2009.000000</td>
    </tr>
  </tbody>
</table>
</div>
```

:::
:::


# Plot

::: {.cell execution_count=3}
``` {.python .cell-code}
from plotnine import ggplot, aes, geom_boxplot, theme_xkcd

(
  ggplot(
    data=penguins,
    mapping=aes(x="sex", y="body_mass_g", color="species")
  )
  + geom_boxplot()
  + theme_xkcd()
)
```

::: {.cell-output .cell-output-stderr}
```
/Users/danielchen/.pyenv/versions/ds/lib/python3.9/site-packages/plotnine/layer.py:334: PlotnineWarning: stat_boxplot : Removed 2 rows containing non-finite values.
```
:::

::: {.cell-output .cell-output-display}
![](01-quarto_files/figure-html/cell-4-output-2.png){}
:::

::: {.cell-output .cell-output-display execution_count=3}
```
<ggplot: (395165166)>
```
:::
:::


# Model

::: {.cell execution_count=4}
``` {.python .cell-code}
import statsmodels.formula.api as smf

penguins["sex_01"] = penguins.sex.replace({"male": 1, "female":0})
pen_no_na = penguins.dropna()

log_reg = smf.logit("sex_01 ~ body_mass_g", data=pen_no_na).fit()
log_reg.summary()
```

::: {.cell-output .cell-output-stdout}
```
Optimization terminated successfully.
         Current function value: 0.595563
         Iterations 5
```
:::

::: {.cell-output .cell-output-display execution_count=4}

```{=html}
<table class="simpletable">
<caption>Logit Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>        <td>sex_01</td>      <th>  No. Observations:  </th>  <td>   333</td>  
</tr>
<tr>
  <th>Model:</th>                 <td>Logit</td>      <th>  Df Residuals:      </th>  <td>   331</td>  
</tr>
<tr>
  <th>Method:</th>                 <td>MLE</td>       <th>  Df Model:          </th>  <td>     1</td>  
</tr>
<tr>
  <th>Date:</th>            <td>Wed, 09 Nov 2022</td> <th>  Pseudo R-squ.:     </th>  <td>0.1407</td>  
</tr>
<tr>
  <th>Time:</th>                <td>09:21:37</td>     <th>  Log-Likelihood:    </th> <td> -198.32</td> 
</tr>
<tr>
  <th>converged:</th>             <td>True</td>       <th>  LL-Null:           </th> <td> -230.80</td> 
</tr>
<tr>
  <th>Covariance Type:</th>     <td>nonrobust</td>    <th>  LLR p-value:       </th> <td>7.627e-16</td>
</tr>
</table>
<table class="simpletable">
<tr>
       <td></td>          <th>coef</th>     <th>std err</th>      <th>z</th>      <th>P>|z|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>Intercept</th>   <td>   -5.1625</td> <td>    0.724</td> <td>   -7.127</td> <td> 0.000</td> <td>   -6.582</td> <td>   -3.743</td>
</tr>
<tr>
  <th>body_mass_g</th> <td>    0.0012</td> <td>    0.000</td> <td>    7.177</td> <td> 0.000</td> <td>    0.001</td> <td>    0.002</td>
</tr>
</table>
```

:::
:::


