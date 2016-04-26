---
layout: post
title:  "Notebook to Markdown conversion test"
date:   2016-03-30
categories:  Notebook to markdown test
---

The following is just a test page to convert an existing ipython notebook to markdown and then post it through Jekyll. The source ipython notebook is downloaded from [this link](https://github.com/agconti/kaggle-titanic/blob/master/Titanic.ipynb)


### Kaggle Competition | Titanic Machine Learning from Disaster

>The sinking of the RMS Titanic is one of the most infamous shipwrecks in history.  On April 15, 1912, during her maiden voyage, the Titanic sank after colliding with an iceberg, killing 1502 out of 2224 passengers and crew.  This sensational tragedy shocked the international community and led to better safety regulations for ships.

>One of the reasons that the shipwreck led to such loss of life was that there were not enough lifeboats for the passengers and crew.  Although there was some element of luck involved in surviving the sinking, some groups of people were more likely to survive than others, such as women, children, and the upper-class.

>In this contest, we ask you to complete the analysis of what sorts of people were likely to survive.  In particular, we ask you to apply the tools of machine learning to predict which passengers survived the tragedy.

>This Kaggle Getting Started Competition provides an ideal starting place for people who may not have a lot of experience in data science and machine learning."

From the competition [homepage](http://www.kaggle.com/c/titanic-gettingStarted).


### Goal for this Notebook:
Show a simple example of an analysis of the Titanic disaster in Python using a full complement of PyData utilities. This is aimed for those looking to get into the field or those who are already in the field and looking to see an example of an analysis done with Python.

#### This Notebook will show basic examples of: 
#### Data Handling
*   Importing Data with Pandas
*   Cleaning Data
*   Exploring Data through Visualizations with Matplotlib

#### Data Analysis
*    Supervised Machine learning Techniques:
    +   Logit Regression Model 
    +   Plotting results
    +   Support Vector Machine (SVM) using 3 kernels
    +   Basic Random Forest
    +   Plotting results

#### Valuation of the Analysis
*   K-folds cross validation to valuate results locally
*   Output the results from the IPython Notebook to Kaggle



#### Required Libraries:
* [NumPy](http://www.numpy.org/)
* [IPython](http://ipython.org/)
* [Pandas](http://pandas.pydata.org/)
* [SciKit-Learn](http://scikit-learn.org/stable/)
* [SciPy](http://www.scipy.org/)
* [StatsModels](http://statsmodels.sourceforge.net/)
* [Patsy](http://patsy.readthedocs.org/en/latest/)
* [Matplotlib](http://matplotlib.org/)

***To run this notebook interactively, get it from my Github [here](https://github.com/agconti/kaggle-titanic). The competition's website is located on [Kaggle.com](http://www.kaggle.com/c/titanic-gettingStarted).***


```python
import matplotlib.pyplot as plt
%matplotlib inline
import numpy as np
import pandas as pd
import statsmodels.api as sm
from statsmodels.nonparametric.kde import KDEUnivariate
from statsmodels.nonparametric import smoothers_lowess
from pandas import Series, DataFrame
from patsy import dmatrices
from sklearn import datasets, svm
from KaggleAux import predict as ka # see github.com/agconti/kaggleaux for more details
```

### Data Handling
#### Let's read our data in using pandas:


```python
df = pd.read_csv("data/train.csv") 
```

Show an overview of our data: 


```python
df 
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0  </th>
      <td>   1</td>
      <td> 0</td>
      <td> 3</td>
      <td>                           Braund, Mr. Owen Harris</td>
      <td>   male</td>
      <td> 22</td>
      <td> 1</td>
      <td> 0</td>
      <td>        A/5 21171</td>
      <td>   7.2500</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>1  </th>
      <td>   2</td>
      <td> 1</td>
      <td> 1</td>
      <td> Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td> female</td>
      <td> 38</td>
      <td> 1</td>
      <td> 0</td>
      <td>         PC 17599</td>
      <td>  71.2833</td>
      <td>         C85</td>
      <td> C</td>
    </tr>
    <tr>
      <th>2  </th>
      <td>   3</td>
      <td> 1</td>
      <td> 3</td>
      <td>                            Heikkinen, Miss. Laina</td>
      <td> female</td>
      <td> 26</td>
      <td> 0</td>
      <td> 0</td>
      <td> STON/O2. 3101282</td>
      <td>   7.9250</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>3  </th>
      <td>   4</td>
      <td> 1</td>
      <td> 1</td>
      <td>      Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td> female</td>
      <td> 35</td>
      <td> 1</td>
      <td> 0</td>
      <td>           113803</td>
      <td>  53.1000</td>
      <td>        C123</td>
      <td> S</td>
    </tr>
    <tr>
      <th>4  </th>
      <td>   5</td>
      <td> 0</td>
      <td> 3</td>
      <td>                          Allen, Mr. William Henry</td>
      <td>   male</td>
      <td> 35</td>
      <td> 0</td>
      <td> 0</td>
      <td>           373450</td>
      <td>   8.0500</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>5  </th>
      <td>   6</td>
      <td> 0</td>
      <td> 3</td>
      <td>                                  Moran, Mr. James</td>
      <td>   male</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           330877</td>
      <td>   8.4583</td>
      <td>         NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>6  </th>
      <td>   7</td>
      <td> 0</td>
      <td> 1</td>
      <td>                           McCarthy, Mr. Timothy J</td>
      <td>   male</td>
      <td> 54</td>
      <td> 0</td>
      <td> 0</td>
      <td>            17463</td>
      <td>  51.8625</td>
      <td>         E46</td>
      <td> S</td>
    </tr>
    <tr>
      <th>7  </th>
      <td>   8</td>
      <td> 0</td>
      <td> 3</td>
      <td>                    Palsson, Master. Gosta Leonard</td>
      <td>   male</td>
      <td>  2</td>
      <td> 3</td>
      <td> 1</td>
      <td>           349909</td>
      <td>  21.0750</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>8  </th>
      <td>   9</td>
      <td> 1</td>
      <td> 3</td>
      <td> Johnson, Mrs. Oscar W (Elisabeth Vilhelmina Berg)</td>
      <td> female</td>
      <td> 27</td>
      <td> 0</td>
      <td> 2</td>
      <td>           347742</td>
      <td>  11.1333</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>9  </th>
      <td>  10</td>
      <td> 1</td>
      <td> 2</td>
      <td>               Nasser, Mrs. Nicholas (Adele Achem)</td>
      <td> female</td>
      <td> 14</td>
      <td> 1</td>
      <td> 0</td>
      <td>           237736</td>
      <td>  30.0708</td>
      <td>         NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>10 </th>
      <td>  11</td>
      <td> 1</td>
      <td> 3</td>
      <td>                   Sandstrom, Miss. Marguerite Rut</td>
      <td> female</td>
      <td>  4</td>
      <td> 1</td>
      <td> 1</td>
      <td>          PP 9549</td>
      <td>  16.7000</td>
      <td>          G6</td>
      <td> S</td>
    </tr>
    <tr>
      <th>11 </th>
      <td>  12</td>
      <td> 1</td>
      <td> 1</td>
      <td>                          Bonnell, Miss. Elizabeth</td>
      <td> female</td>
      <td> 58</td>
      <td> 0</td>
      <td> 0</td>
      <td>           113783</td>
      <td>  26.5500</td>
      <td>        C103</td>
      <td> S</td>
    </tr>
    <tr>
      <th>12 </th>
      <td>  13</td>
      <td> 0</td>
      <td> 3</td>
      <td>                    Saundercock, Mr. William Henry</td>
      <td>   male</td>
      <td> 20</td>
      <td> 0</td>
      <td> 0</td>
      <td>        A/5. 2151</td>
      <td>   8.0500</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>13 </th>
      <td>  14</td>
      <td> 0</td>
      <td> 3</td>
      <td>                       Andersson, Mr. Anders Johan</td>
      <td>   male</td>
      <td> 39</td>
      <td> 1</td>
      <td> 5</td>
      <td>           347082</td>
      <td>  31.2750</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>14 </th>
      <td>  15</td>
      <td> 0</td>
      <td> 3</td>
      <td>              Vestrom, Miss. Hulda Amanda Adolfina</td>
      <td> female</td>
      <td> 14</td>
      <td> 0</td>
      <td> 0</td>
      <td>           350406</td>
      <td>   7.8542</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>15 </th>
      <td>  16</td>
      <td> 1</td>
      <td> 2</td>
      <td>                  Hewlett, Mrs. (Mary D Kingcome) </td>
      <td> female</td>
      <td> 55</td>
      <td> 0</td>
      <td> 0</td>
      <td>           248706</td>
      <td>  16.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>16 </th>
      <td>  17</td>
      <td> 0</td>
      <td> 3</td>
      <td>                              Rice, Master. Eugene</td>
      <td>   male</td>
      <td>  2</td>
      <td> 4</td>
      <td> 1</td>
      <td>           382652</td>
      <td>  29.1250</td>
      <td>         NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>17 </th>
      <td>  18</td>
      <td> 1</td>
      <td> 2</td>
      <td>                      Williams, Mr. Charles Eugene</td>
      <td>   male</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           244373</td>
      <td>  13.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>18 </th>
      <td>  19</td>
      <td> 0</td>
      <td> 3</td>
      <td> Vander Planke, Mrs. Julius (Emelia Maria Vande...</td>
      <td> female</td>
      <td> 31</td>
      <td> 1</td>
      <td> 0</td>
      <td>           345763</td>
      <td>  18.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>19 </th>
      <td>  20</td>
      <td> 1</td>
      <td> 3</td>
      <td>                           Masselmani, Mrs. Fatima</td>
      <td> female</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>             2649</td>
      <td>   7.2250</td>
      <td>         NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>20 </th>
      <td>  21</td>
      <td> 0</td>
      <td> 2</td>
      <td>                              Fynney, Mr. Joseph J</td>
      <td>   male</td>
      <td> 35</td>
      <td> 0</td>
      <td> 0</td>
      <td>           239865</td>
      <td>  26.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>21 </th>
      <td>  22</td>
      <td> 1</td>
      <td> 2</td>
      <td>                             Beesley, Mr. Lawrence</td>
      <td>   male</td>
      <td> 34</td>
      <td> 0</td>
      <td> 0</td>
      <td>           248698</td>
      <td>  13.0000</td>
      <td>         D56</td>
      <td> S</td>
    </tr>
    <tr>
      <th>22 </th>
      <td>  23</td>
      <td> 1</td>
      <td> 3</td>
      <td>                       McGowan, Miss. Anna "Annie"</td>
      <td> female</td>
      <td> 15</td>
      <td> 0</td>
      <td> 0</td>
      <td>           330923</td>
      <td>   8.0292</td>
      <td>         NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>23 </th>
      <td>  24</td>
      <td> 1</td>
      <td> 1</td>
      <td>                      Sloper, Mr. William Thompson</td>
      <td>   male</td>
      <td> 28</td>
      <td> 0</td>
      <td> 0</td>
      <td>           113788</td>
      <td>  35.5000</td>
      <td>          A6</td>
      <td> S</td>
    </tr>
    <tr>
      <th>24 </th>
      <td>  25</td>
      <td> 0</td>
      <td> 3</td>
      <td>                     Palsson, Miss. Torborg Danira</td>
      <td> female</td>
      <td>  8</td>
      <td> 3</td>
      <td> 1</td>
      <td>           349909</td>
      <td>  21.0750</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>25 </th>
      <td>  26</td>
      <td> 1</td>
      <td> 3</td>
      <td> Asplund, Mrs. Carl Oscar (Selma Augusta Emilia...</td>
      <td> female</td>
      <td> 38</td>
      <td> 1</td>
      <td> 5</td>
      <td>           347077</td>
      <td>  31.3875</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>26 </th>
      <td>  27</td>
      <td> 0</td>
      <td> 3</td>
      <td>                           Emir, Mr. Farred Chehab</td>
      <td>   male</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>             2631</td>
      <td>   7.2250</td>
      <td>         NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>27 </th>
      <td>  28</td>
      <td> 0</td>
      <td> 1</td>
      <td>                    Fortune, Mr. Charles Alexander</td>
      <td>   male</td>
      <td> 19</td>
      <td> 3</td>
      <td> 2</td>
      <td>            19950</td>
      <td> 263.0000</td>
      <td> C23 C25 C27</td>
      <td> S</td>
    </tr>
    <tr>
      <th>28 </th>
      <td>  29</td>
      <td> 1</td>
      <td> 3</td>
      <td>                     O'Dwyer, Miss. Ellen "Nellie"</td>
      <td> female</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           330959</td>
      <td>   7.8792</td>
      <td>         NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>29 </th>
      <td>  30</td>
      <td> 0</td>
      <td> 3</td>
      <td>                               Todoroff, Mr. Lalio</td>
      <td>   male</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           349216</td>
      <td>   7.8958</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>861</th>
      <td> 862</td>
      <td> 0</td>
      <td> 2</td>
      <td>                       Giles, Mr. Frederick Edward</td>
      <td>   male</td>
      <td> 21</td>
      <td> 1</td>
      <td> 0</td>
      <td>            28134</td>
      <td>  11.5000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>862</th>
      <td> 863</td>
      <td> 1</td>
      <td> 1</td>
      <td> Swift, Mrs. Frederick Joel (Margaret Welles Ba...</td>
      <td> female</td>
      <td> 48</td>
      <td> 0</td>
      <td> 0</td>
      <td>            17466</td>
      <td>  25.9292</td>
      <td>         D17</td>
      <td> S</td>
    </tr>
    <tr>
      <th>863</th>
      <td> 864</td>
      <td> 0</td>
      <td> 3</td>
      <td>                 Sage, Miss. Dorothy Edith "Dolly"</td>
      <td> female</td>
      <td>NaN</td>
      <td> 8</td>
      <td> 2</td>
      <td>         CA. 2343</td>
      <td>  69.5500</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>864</th>
      <td> 865</td>
      <td> 0</td>
      <td> 2</td>
      <td>                            Gill, Mr. John William</td>
      <td>   male</td>
      <td> 24</td>
      <td> 0</td>
      <td> 0</td>
      <td>           233866</td>
      <td>  13.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>865</th>
      <td> 866</td>
      <td> 1</td>
      <td> 2</td>
      <td>                          Bystrom, Mrs. (Karolina)</td>
      <td> female</td>
      <td> 42</td>
      <td> 0</td>
      <td> 0</td>
      <td>           236852</td>
      <td>  13.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>866</th>
      <td> 867</td>
      <td> 1</td>
      <td> 2</td>
      <td>                      Duran y More, Miss. Asuncion</td>
      <td> female</td>
      <td> 27</td>
      <td> 1</td>
      <td> 0</td>
      <td>    SC/PARIS 2149</td>
      <td>  13.8583</td>
      <td>         NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>867</th>
      <td> 868</td>
      <td> 0</td>
      <td> 1</td>
      <td>              Roebling, Mr. Washington Augustus II</td>
      <td>   male</td>
      <td> 31</td>
      <td> 0</td>
      <td> 0</td>
      <td>         PC 17590</td>
      <td>  50.4958</td>
      <td>         A24</td>
      <td> S</td>
    </tr>
    <tr>
      <th>868</th>
      <td> 869</td>
      <td> 0</td>
      <td> 3</td>
      <td>                       van Melkebeke, Mr. Philemon</td>
      <td>   male</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           345777</td>
      <td>   9.5000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>869</th>
      <td> 870</td>
      <td> 1</td>
      <td> 3</td>
      <td>                   Johnson, Master. Harold Theodor</td>
      <td>   male</td>
      <td>  4</td>
      <td> 1</td>
      <td> 1</td>
      <td>           347742</td>
      <td>  11.1333</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>870</th>
      <td> 871</td>
      <td> 0</td>
      <td> 3</td>
      <td>                                 Balkic, Mr. Cerin</td>
      <td>   male</td>
      <td> 26</td>
      <td> 0</td>
      <td> 0</td>
      <td>           349248</td>
      <td>   7.8958</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>871</th>
      <td> 872</td>
      <td> 1</td>
      <td> 1</td>
      <td>  Beckwith, Mrs. Richard Leonard (Sallie Monypeny)</td>
      <td> female</td>
      <td> 47</td>
      <td> 1</td>
      <td> 1</td>
      <td>            11751</td>
      <td>  52.5542</td>
      <td>         D35</td>
      <td> S</td>
    </tr>
    <tr>
      <th>872</th>
      <td> 873</td>
      <td> 0</td>
      <td> 1</td>
      <td>                          Carlsson, Mr. Frans Olof</td>
      <td>   male</td>
      <td> 33</td>
      <td> 0</td>
      <td> 0</td>
      <td>              695</td>
      <td>   5.0000</td>
      <td> B51 B53 B55</td>
      <td> S</td>
    </tr>
    <tr>
      <th>873</th>
      <td> 874</td>
      <td> 0</td>
      <td> 3</td>
      <td>                       Vander Cruyssen, Mr. Victor</td>
      <td>   male</td>
      <td> 47</td>
      <td> 0</td>
      <td> 0</td>
      <td>           345765</td>
      <td>   9.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>874</th>
      <td> 875</td>
      <td> 1</td>
      <td> 2</td>
      <td>             Abelson, Mrs. Samuel (Hannah Wizosky)</td>
      <td> female</td>
      <td> 28</td>
      <td> 1</td>
      <td> 0</td>
      <td>        P/PP 3381</td>
      <td>  24.0000</td>
      <td>         NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>875</th>
      <td> 876</td>
      <td> 1</td>
      <td> 3</td>
      <td>                  Najib, Miss. Adele Kiamie "Jane"</td>
      <td> female</td>
      <td> 15</td>
      <td> 0</td>
      <td> 0</td>
      <td>             2667</td>
      <td>   7.2250</td>
      <td>         NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>876</th>
      <td> 877</td>
      <td> 0</td>
      <td> 3</td>
      <td>                     Gustafsson, Mr. Alfred Ossian</td>
      <td>   male</td>
      <td> 20</td>
      <td> 0</td>
      <td> 0</td>
      <td>             7534</td>
      <td>   9.8458</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>877</th>
      <td> 878</td>
      <td> 0</td>
      <td> 3</td>
      <td>                              Petroff, Mr. Nedelio</td>
      <td>   male</td>
      <td> 19</td>
      <td> 0</td>
      <td> 0</td>
      <td>           349212</td>
      <td>   7.8958</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>878</th>
      <td> 879</td>
      <td> 0</td>
      <td> 3</td>
      <td>                                Laleff, Mr. Kristo</td>
      <td>   male</td>
      <td>NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           349217</td>
      <td>   7.8958</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>879</th>
      <td> 880</td>
      <td> 1</td>
      <td> 1</td>
      <td>     Potter, Mrs. Thomas Jr (Lily Alexenia Wilson)</td>
      <td> female</td>
      <td> 56</td>
      <td> 0</td>
      <td> 1</td>
      <td>            11767</td>
      <td>  83.1583</td>
      <td>         C50</td>
      <td> C</td>
    </tr>
    <tr>
      <th>880</th>
      <td> 881</td>
      <td> 1</td>
      <td> 2</td>
      <td>      Shelley, Mrs. William (Imanita Parrish Hall)</td>
      <td> female</td>
      <td> 25</td>
      <td> 0</td>
      <td> 1</td>
      <td>           230433</td>
      <td>  26.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>881</th>
      <td> 882</td>
      <td> 0</td>
      <td> 3</td>
      <td>                                Markun, Mr. Johann</td>
      <td>   male</td>
      <td> 33</td>
      <td> 0</td>
      <td> 0</td>
      <td>           349257</td>
      <td>   7.8958</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>882</th>
      <td> 883</td>
      <td> 0</td>
      <td> 3</td>
      <td>                      Dahlberg, Miss. Gerda Ulrika</td>
      <td> female</td>
      <td> 22</td>
      <td> 0</td>
      <td> 0</td>
      <td>             7552</td>
      <td>  10.5167</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>883</th>
      <td> 884</td>
      <td> 0</td>
      <td> 2</td>
      <td>                     Banfield, Mr. Frederick James</td>
      <td>   male</td>
      <td> 28</td>
      <td> 0</td>
      <td> 0</td>
      <td> C.A./SOTON 34068</td>
      <td>  10.5000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>884</th>
      <td> 885</td>
      <td> 0</td>
      <td> 3</td>
      <td>                            Sutehall, Mr. Henry Jr</td>
      <td>   male</td>
      <td> 25</td>
      <td> 0</td>
      <td> 0</td>
      <td>  SOTON/OQ 392076</td>
      <td>   7.0500</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>885</th>
      <td> 886</td>
      <td> 0</td>
      <td> 3</td>
      <td>              Rice, Mrs. William (Margaret Norton)</td>
      <td> female</td>
      <td> 39</td>
      <td> 0</td>
      <td> 5</td>
      <td>           382652</td>
      <td>  29.1250</td>
      <td>         NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>886</th>
      <td> 887</td>
      <td> 0</td>
      <td> 2</td>
      <td>                             Montvila, Rev. Juozas</td>
      <td>   male</td>
      <td> 27</td>
      <td> 0</td>
      <td> 0</td>
      <td>           211536</td>
      <td>  13.0000</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>887</th>
      <td> 888</td>
      <td> 1</td>
      <td> 1</td>
      <td>                      Graham, Miss. Margaret Edith</td>
      <td> female</td>
      <td> 19</td>
      <td> 0</td>
      <td> 0</td>
      <td>           112053</td>
      <td>  30.0000</td>
      <td>         B42</td>
      <td> S</td>
    </tr>
    <tr>
      <th>888</th>
      <td> 889</td>
      <td> 0</td>
      <td> 3</td>
      <td>          Johnston, Miss. Catherine Helen "Carrie"</td>
      <td> female</td>
      <td>NaN</td>
      <td> 1</td>
      <td> 2</td>
      <td>       W./C. 6607</td>
      <td>  23.4500</td>
      <td>         NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>889</th>
      <td> 890</td>
      <td> 1</td>
      <td> 1</td>
      <td>                             Behr, Mr. Karl Howell</td>
      <td>   male</td>
      <td> 26</td>
      <td> 0</td>
      <td> 0</td>
      <td>           111369</td>
      <td>  30.0000</td>
      <td>        C148</td>
      <td> C</td>
    </tr>
    <tr>
      <th>890</th>
      <td> 891</td>
      <td> 0</td>
      <td> 3</td>
      <td>                               Dooley, Mr. Patrick</td>
      <td>   male</td>
      <td> 32</td>
      <td> 0</td>
      <td> 0</td>
      <td>           370376</td>
      <td>   7.7500</td>
      <td>         NaN</td>
      <td> Q</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 12 columns</p>
</div>



### Let's take a look:

Above is a summary of our data contained in a `Pandas` `DataFrame`. Think of a `DataFrame` as a Python's super charged version of the workflow in an Excel table. As you can see the summary holds quite a bit of information. First, it lets us know we have 891 observations, or passengers, to analyze here:
    
    Int64Index: 891 entries, 0 to 890

Next it shows us all of the columns in `DataFrame`. Each column tells us something about each of our observations, like their `name`, `sex` or `age`. These colunms  are called a features of our dataset. You can think of the meaning of the words column and feature as interchangeable for this notebook. 

After each feature it lets us know how many values it contains. While most of our features have complete data on every observation, like the `survived` feature here: 

    survived    891  non-null values 

some are missing information, like the `age` feature: 

    age         714  non-null values 

These missing values are represented as `NaN`s.

### Take care of missing values:
The features `ticket` and `cabin` have many missing values and so can’t add much value to our analysis. To handle this we will drop them from the dataframe to preserve the integrity of our dataset.

To do that we'll use this line of code to drop the features entirely:

    df = df.drop(['ticket','cabin'], axis=1) 


While this line of code removes the `NaN` values from every remaining column / feature:
   
    df = df.dropna()
     
Now we have a clean and tidy dataset that is ready for analysis. Because `.dropna()` removes an observation from our data even if it only has 1 `NaN` in one of the features, it would have removed most of our dataset if we had not dropped the `ticket` and `cabin`  features first.




```python
df = df.drop(['Ticket','Cabin'], axis=1)
# Remove NaN values
df = df.dropna() 
```

For a detailed look at how to use pandas for data analysis, the best resource is Wes Mckinney's [book](http://shop.oreilly.com/product/0636920023784.do). Additional interactive tutorials that cover all of the basics can be found [here](https://bitbucket.org/hrojas/learn-pandas) (they're free).  If you still need to be convinced about the power of pandas check out this wirlwhind [look](http://wesmckinney.com/blog/?p=647) at all that pandas can do. 

### Let's take a Look at our data graphically:


```python
# specifies the parameters of our graphs
fig = plt.figure(figsize=(18,6), dpi=1600) 
alpha=alpha_scatterplot = 0.2 
alpha_bar_chart = 0.55

# lets us plot many diffrent shaped graphs together 
ax1 = plt.subplot2grid((2,3),(0,0))
# plots a bar graph of those who surived vs those who did not.               
df.Survived.value_counts().plot(kind='bar', alpha=alpha_bar_chart)
# this nicely sets the margins in matplotlib to deal with a recent bug 1.3.1
ax1.set_xlim(-1, 2)
# puts a title on our graph
plt.title("Distribution of Survival, (1 = Survived)")    

plt.subplot2grid((2,3),(0,1))
plt.scatter(df.Survived, df.Age, alpha=alpha_scatterplot)
# sets the y axis lable
plt.ylabel("Age")
# formats the grid line style of our graphs                          
plt.grid(b=True, which='major', axis='y')  
plt.title("Survival by Age,  (1 = Survived)")

ax3 = plt.subplot2grid((2,3),(0,2))
df.Pclass.value_counts().plot(kind="barh", alpha=alpha_bar_chart)
ax3.set_ylim(-1, len(df.Pclass.value_counts()))
plt.title("Class Distribution")

plt.subplot2grid((2,3),(1,0), colspan=2)
# plots a kernel density estimate of the subset of the 1st class passangers's age
df.Age[df.Pclass == 1].plot(kind='kde')    
df.Age[df.Pclass == 2].plot(kind='kde')
df.Age[df.Pclass == 3].plot(kind='kde')
 # plots an axis lable
plt.xlabel("Age")    
plt.title("Age Distribution within classes")
# sets our legend for our graph.
plt.legend(('1st Class', '2nd Class','3rd Class'),loc='best') 

ax5 = plt.subplot2grid((2,3),(1,2))
df.Embarked.value_counts().plot(kind='bar', alpha=alpha_bar_chart)
ax5.set_xlim(-1, len(df.Embarked.value_counts()))
# specifies the parameters of our graphs
plt.title("Passengers per boarding location")
```




    <matplotlib.text.Text at 0x119c1dd90>




![png](Titanic_files/Titanic_10_1.png)


### Exploratory Visualization:

The point of this competition is to predict if an individual will survive based on the features in the data like:
 
 * Traveling Class (called pclass in the data)
 * Sex 
 * Age
 * Fare Price

Let’s see if we can gain a better understanding of who survived and died. 


First let’s plot a bar graph of those who Survived Vs. Those who did not.



```python
plt.figure(figsize=(6,4))
fig, ax = plt.subplots()
df.Survived.value_counts().plot(kind='barh', color="blue", alpha=.65)
ax.set_ylim(-1, len(df.Survived.value_counts())) 
plt.title("Survival Breakdown (1 = Survived, 0 = Died)")
```




    <matplotlib.text.Text at 0x119a90fd0>




    <matplotlib.figure.Figure at 0x119931f10>



![png](Titanic_files/Titanic_12_2.png)


### Now let’s tease more structure out of the data,
### Let’s break the previous graph down by gender



```python
fig = plt.figure(figsize=(18,6))

#create a plot of two subsets, male and female, of the survived variable.
#After we do that we call value_counts() so it can be easily plotted as a bar graph. 
#'barh' is just a horizontal bar graph
df_male = df.Survived[df.Sex == 'male'].value_counts().sort_index()
df_female = df.Survived[df.Sex == 'female'].value_counts().sort_index()

ax1 = fig.add_subplot(121)
df_male.plot(kind='barh',label='Male', alpha=0.55)
df_female.plot(kind='barh', color='#FA2379',label='Female', alpha=0.55)
plt.title("Who Survived? with respect to Gender, (raw value counts) "); plt.legend(loc='best')
ax1.set_ylim(-1, 2) 

#adjust graph to display the proportions of survival by gender
ax2 = fig.add_subplot(122)
(df_male/float(df_male.sum())).plot(kind='barh',label='Male', alpha=0.55)  
(df_female/float(df_female.sum())).plot(kind='barh', color='#FA2379',label='Female', alpha=0.55)
plt.title("Who Survived proportionally? with respect to Gender"); plt.legend(loc='best')

ax2.set_ylim(-1, 2)
```




    (-1, 2)




![png](Titanic_files/Titanic_14_1.png)


Here it’s clear that although more men died and survived in raw value counts, females had a greater survival rate proportionally (~25%), than men (~20%)

#### Great! But let’s go down even further:
Can we capture more of the structure by using Pclass? Here we will bucket classes as lowest class or any of the high classes (classes 1 - 2). 3 is lowest class. Let’s break it down by Gender and what Class they were traveling in.



```python
fig = plt.figure(figsize=(18,4), dpi=1600)
alpha_level = 0.65

# building on the previous code, here we create an additional subset with in the gender subset 
# we created for the survived variable. I know, thats a lot of subsets. After we do that we call 
# value_counts() so it it can be easily plotted as a bar graph. this is repeated for each gender 
# class pair.
ax1=fig.add_subplot(141)
female_highclass = df.Survived[df.Sex == 'female'][df.Pclass != 3].value_counts()
female_highclass.plot(kind='bar', label='female, highclass', color='#FA2479', alpha=alpha_level)
ax1.set_xticklabels(["Survived", "Died"], rotation=0)
ax1.set_xlim(-1, len(female_highclass))
plt.title("Who Survived? with respect to Gender and Class"); plt.legend(loc='best')

ax2=fig.add_subplot(142, sharey=ax1)
female_lowclass = df.Survived[df.Sex == 'female'][df.Pclass == 3].value_counts()
female_lowclass.plot(kind='bar', label='female, low class', color='pink', alpha=alpha_level)
ax2.set_xticklabels(["Died","Survived"], rotation=0)
ax2.set_xlim(-1, len(female_lowclass))
plt.legend(loc='best')

ax3=fig.add_subplot(143, sharey=ax1)
male_lowclass = df.Survived[df.Sex == 'male'][df.Pclass == 3].value_counts()
male_lowclass.plot(kind='bar', label='male, low class',color='lightblue', alpha=alpha_level)
ax3.set_xticklabels(["Died","Survived"], rotation=0)
ax3.set_xlim(-1, len(male_lowclass))
plt.legend(loc='best')

ax4=fig.add_subplot(144, sharey=ax1)
male_highclass = df.Survived[df.Sex == 'male'][df.Pclass != 3].value_counts()
male_highclass.plot(kind='bar', label='male, highclass', alpha=alpha_level, color='steelblue')
ax4.set_xticklabels(["Died","Survived"], rotation=0)
ax4.set_xlim(-1, len(male_highclass))
plt.legend(loc='best')
```




    <matplotlib.legend.Legend at 0x10af39ed0>




![png](Titanic_files/Titanic_16_1.png)


Awesome! Now we have a lot more information on who survived and died in the tragedy. With this deeper understanding, we are better equipped to create better more insightful models. This is a typical process in interactive data analysis. First you start small and understand the most basic relationships and slowly increment the complexity of your analysis as you discover more and more about the data you’re working with. Below is the progression of process laid out together:


```python
fig = plt.figure(figsize=(18,12), dpi=1600)
a = 0.65
# Step 1
ax1 = fig.add_subplot(341)
df.Survived.value_counts().plot(kind='bar', color="blue", alpha=a)
ax1.set_xlim(-1, len(df.Survived.value_counts()))
plt.title("Step. 1")

# Step 2
ax2 = fig.add_subplot(345)
df.Survived[df.Sex == 'male'].value_counts().plot(kind='bar',label='Male')
df.Survived[df.Sex == 'female'].value_counts().plot(kind='bar', color='#FA2379',label='Female')
ax2.set_xlim(-1, 2)
plt.title("Step. 2 \nWho Survied? with respect to Gender."); plt.legend(loc='best')

ax3 = fig.add_subplot(346)
(df.Survived[df.Sex == 'male'].value_counts()/float(df.Sex[df.Sex == 'male'].size)).plot(kind='bar',label='Male')
(df.Survived[df.Sex == 'female'].value_counts()/float(df.Sex[df.Sex == 'female'].size)).plot(kind='bar', color='#FA2379',label='Female')
ax3.set_xlim(-1,2)
plt.title("Who Survied proportionally?"); plt.legend(loc='best')


# Step 3
ax4 = fig.add_subplot(349)
female_highclass = df.Survived[df.Sex == 'female'][df.Pclass != 3].value_counts()
female_highclass.plot(kind='bar', label='female highclass', color='#FA2479', alpha=a)
ax4.set_xticklabels(["Survived", "Died"], rotation=0)
ax4.set_xlim(-1, len(female_highclass))
plt.title("Who Survived? with respect to Gender and Class"); plt.legend(loc='best')

ax5 = fig.add_subplot(3,4,10, sharey=ax1)
female_lowclass = df.Survived[df.Sex == 'female'][df.Pclass == 3].value_counts()
female_lowclass.plot(kind='bar', label='female, low class', color='pink', alpha=a)
ax5.set_xticklabels(["Died","Survived"], rotation=0)
ax5.set_xlim(-1, len(female_lowclass))
plt.legend(loc='best')

ax6 = fig.add_subplot(3,4,11, sharey=ax1)
male_lowclass = df.Survived[df.Sex == 'male'][df.Pclass == 3].value_counts()
male_lowclass.plot(kind='bar', label='male, low class',color='lightblue', alpha=a)
ax6.set_xticklabels(["Died","Survived"], rotation=0)
ax6.set_xlim(-1, len(male_lowclass))
plt.legend(loc='best')

ax7 = fig.add_subplot(3,4,12, sharey=ax1)
male_highclass = df.Survived[df.Sex == 'male'][df.Pclass != 3].value_counts()
male_highclass.plot(kind='bar', label='male highclass', alpha=a, color='steelblue')
ax7.set_xticklabels(["Died","Survived"], rotation=0)
ax7.set_xlim(-1, len(male_highclass))
plt.legend(loc='best')
```




    <matplotlib.legend.Legend at 0x11bdf3ed0>




![png](Titanic_files/Titanic_18_1.png)


I've done my best to make the plotting code readable and intuitive, but if you’re looking for a more detailed look on how to start plotting in matplotlib, check out this beautiful notebook [here](http://nbviewer.ipython.org/github/jrjohansson/scientific-python-lectures/blob/master/Lecture-4-Matplotlib.ipynb). 

Now that we have a basic understanding of what we are trying to predict, let’s predict it.
## Supervised Machine Learning
#### Logistic Regression:

As explained by Wikipedia:
>In statistics, logistic regression or logit regression is a type of regression analysis used for predicting the outcome of a categorical dependent variable (a dependent variable that can take on a limited number of values, whose magnitudes are not meaningful but whose ordering of magnitudes may or may not be meaningful) based on one or more predictor variables. That is, it is used in estimating empirical values of the parameters in a qualitative response model. The probabilities describing the possible outcomes of a single trial are modeled, as a function of the explanatory (predictor) variables, using a logistic function. Frequently (and subsequently in this article) "logistic regression" is used to refer specifically to the problem in which the dependent variable is binary—that is, the number of available categories is two—and problems with more than two categories are referred to as multinomial logistic regression or, if the multiple categories are ordered, as ordered logistic regression.
Logistic regression measures the relationship between a categorical dependent variable and one or more independent variables, which are usually (but not necessarily) continuous, by using probability scores as the predicted values of the dependent variable.[1] As such it treats the same set of problems as does probit regression using similar techniques.

#### The skinny, as explained by yours truly:
Our competition wants us to predict a binary outcome. That is, it wants to know whether some will die, (represented as a 0), or survive, (represented as 1). A good place to start is to calculate the probability that an individual observation, or person, is likely to be a 0 or 1. That way we would know the chance that someone survives, and could start making somewhat informed perdictions. If we did, we'd get results like this:: 

![pred](https://raw.github.com/agconti/kaggle-titanic/master/images/calc_prob.png) 

(*Y axis is the probability that someone survives, X axis is the passenger’s number from 1 to 891.*)

While that information is useful it doesn’t let us know whether someone ended up alive or dead. It just lets us know the chance that they will survive or die. We still need to translate these probabilities into the binary decision we’re looking for. But how? We could arbitrarily say that our survival cutoff is anyone with a probability of survival over 50%. In fact, this tactic would actually perform pretty well for our data and would allow you to make decently accurate predictions. Graphically it would look something like this:

![predwline](https://raw.github.com/agconti/kaggle-titanic/master/images/calc_prob_wline.png)

If you’re a betting man like me, you don’t like to leave everything to chance. What are the odds that setting that cutoff at 50% works? Maybe 20% or 80% would work better. Clearly we need a more exact way to make that cutoff. What can save the day? In steps the **Logistic Regression**. 

A logistic regression follows the all steps we took above but mathematically calculates the cutoff, or decision boundary (as stats nerds call it), for you. This way it can figure out the best cut off to choose, perhaps 50% or 51.84%, that most accurately represents the training data.

The three cells below show the process of creating our Logitist regression model, training it on the data, and examining its performance. 

First, we define our formula for our Logit regression. In the next cell we create a regression friendly dataframe that sets up boolean values for the categorical variables in our formula and lets our regression model know the types of inputs we're giving it. The model is then instantiated and fitted before a summary of the model's performance is printed. In the last cell we graphically compare the predictions of our model to the actual values we are trying to predict, as well as the residual errors from our model to check for any structure we may have missed.


```python
# model formula
# here the ~ sign is an = sign, and the features of our dataset
# are written as a formula to predict survived. The C() lets our 
# regression know that those variables are categorical.
# Ref: http://patsy.readthedocs.org/en/latest/formulas.html
formula = 'Survived ~ C(Pclass) + C(Sex) + Age + SibSp  + C(Embarked)' 
# create a results dictionary to hold our regression results for easy analysis later        
results = {} 
```


```python
# create a regression friendly dataframe using patsy's dmatrices function
y,x = dmatrices(formula, data=df, return_type='dataframe')

# instantiate our model
model = sm.Logit(y,x)

# fit our model to the training data
res = model.fit()

# save the result for outputing predictions later
results['Logit'] = [res, formula]
res.summary()
```

    Optimization terminated successfully.
             Current function value: 0.444388
             Iterations 6
    




<table class="simpletable">
<caption>Logit Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>     <td>Survived</td>     <th>  No. Observations:  </th>  <td>   712</td>  
</tr>
<tr>
  <th>Model:</th>               <td>Logit</td>      <th>  Df Residuals:      </th>  <td>   704</td>  
</tr>
<tr>
  <th>Method:</th>               <td>MLE</td>       <th>  Df Model:          </th>  <td>     7</td>  
</tr>
<tr>
  <th>Date:</th>          <td>Sun, 20 Dec 2015</td> <th>  Pseudo R-squ.:     </th>  <td>0.3414</td>  
</tr>
<tr>
  <th>Time:</th>              <td>11:27:33</td>     <th>  Log-Likelihood:    </th> <td> -316.40</td> 
</tr>
<tr>
  <th>converged:</th>           <td>True</td>       <th>  LL-Null:           </th> <td> -480.45</td> 
</tr>
<tr>
  <th> </th>                      <td> </td>        <th>  LLR p-value:       </th> <td>5.992e-67</td>
</tr>
</table>
<table class="simpletable">
<tr>
          <td></td>            <th>coef</th>     <th>std err</th>      <th>z</th>      <th>P>|z|</th> <th>[95.0% Conf. Int.]</th> 
</tr>
<tr>
  <th>Intercept</th>        <td>    4.5423</td> <td>    0.474</td> <td>    9.583</td> <td> 0.000</td> <td>    3.613     5.471</td>
</tr>
<tr>
  <th>C(Pclass)[T.2]</th>   <td>   -1.2673</td> <td>    0.299</td> <td>   -4.245</td> <td> 0.000</td> <td>   -1.852    -0.682</td>
</tr>
<tr>
  <th>C(Pclass)[T.3]</th>   <td>   -2.4966</td> <td>    0.296</td> <td>   -8.422</td> <td> 0.000</td> <td>   -3.078    -1.916</td>
</tr>
<tr>
  <th>C(Sex)[T.male]</th>   <td>   -2.6239</td> <td>    0.218</td> <td>  -12.060</td> <td> 0.000</td> <td>   -3.050    -2.197</td>
</tr>
<tr>
  <th>C(Embarked)[T.Q]</th> <td>   -0.8351</td> <td>    0.597</td> <td>   -1.398</td> <td> 0.162</td> <td>   -2.006     0.335</td>
</tr>
<tr>
  <th>C(Embarked)[T.S]</th> <td>   -0.4254</td> <td>    0.271</td> <td>   -1.572</td> <td> 0.116</td> <td>   -0.956     0.105</td>
</tr>
<tr>
  <th>Age</th>              <td>   -0.0436</td> <td>    0.008</td> <td>   -5.264</td> <td> 0.000</td> <td>   -0.060    -0.027</td>
</tr>
<tr>
  <th>SibSp</th>            <td>   -0.3697</td> <td>    0.123</td> <td>   -3.004</td> <td> 0.003</td> <td>   -0.611    -0.129</td>
</tr>
</table>




```python
# Plot Predictions Vs Actual
plt.figure(figsize=(18,4));
plt.subplot(121, axisbg="#DBDBDB")
# generate predictions from our fitted model
ypred = res.predict(x)
plt.plot(x.index, ypred, 'bo', x.index, y, 'mo', alpha=.25);
plt.grid(color='white', linestyle='dashed')
plt.title('Logit predictions, Blue: \nFitted/predicted values: Red');

# Residuals
ax2 = plt.subplot(122, axisbg="#DBDBDB")
plt.plot(res.resid_dev, 'r-')
plt.grid(color='white', linestyle='dashed')
ax2.set_xlim(-1, len(res.resid_dev))
plt.title('Logit Residuals');
```


![png](Titanic_files/Titanic_22_0.png)


## So how well did this work?
Lets look at the predictions we generated graphically:


```python
fig = plt.figure(figsize=(18,9), dpi=1600)
a = .2

# Below are examples of more advanced plotting. 
# It it looks strange check out the tutorial above.
fig.add_subplot(221, axisbg="#DBDBDB")
kde_res = KDEUnivariate(res.predict())
kde_res.fit()
plt.plot(kde_res.support,kde_res.density)
plt.fill_between(kde_res.support,kde_res.density, alpha=a)
plt.title("Distribution of our Predictions")

fig.add_subplot(222, axisbg="#DBDBDB")
plt.scatter(res.predict(),x['C(Sex)[T.male]'] , alpha=a)
plt.grid(b=True, which='major', axis='x')
plt.xlabel("Predicted chance of survival")
plt.ylabel("Gender Bool")
plt.title("The Change of Survival Probability by Gender (1 = Male)")

fig.add_subplot(223, axisbg="#DBDBDB")
plt.scatter(res.predict(),x['C(Pclass)[T.3]'] , alpha=a)
plt.xlabel("Predicted chance of survival")
plt.ylabel("Class Bool")
plt.grid(b=True, which='major', axis='x')
plt.title("The Change of Survival Probability by Lower Class (1 = 3rd Class)")

fig.add_subplot(224, axisbg="#DBDBDB")
plt.scatter(res.predict(),x.Age , alpha=a)
plt.grid(True, linewidth=0.15)
plt.title("The Change of Survival Probability by Age")
plt.xlabel("Predicted chance of survival")
plt.ylabel("Age")
```




    <matplotlib.text.Text at 0x10dc26350>




![png](Titanic_files/Titanic_24_1.png)


### Now lets use our model to predict the test set values and then save the results so they can be outputed to Kaggle
### Read the test data


```python
test_data = pd.read_csv("data/test.csv")
```

### Examine our dataframe


```python
test_data
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PassengerId</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0  </th>
      <td>  892</td>
      <td> 3</td>
      <td>                                  Kelly, Mr. James</td>
      <td>   male</td>
      <td> 34.5</td>
      <td> 0</td>
      <td> 0</td>
      <td>             330911</td>
      <td>   7.8292</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>1  </th>
      <td>  893</td>
      <td> 3</td>
      <td>                  Wilkes, Mrs. James (Ellen Needs)</td>
      <td> female</td>
      <td> 47.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>             363272</td>
      <td>   7.0000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>2  </th>
      <td>  894</td>
      <td> 2</td>
      <td>                         Myles, Mr. Thomas Francis</td>
      <td>   male</td>
      <td> 62.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             240276</td>
      <td>   9.6875</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>3  </th>
      <td>  895</td>
      <td> 3</td>
      <td>                                  Wirz, Mr. Albert</td>
      <td>   male</td>
      <td> 27.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             315154</td>
      <td>   8.6625</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>4  </th>
      <td>  896</td>
      <td> 3</td>
      <td>      Hirvonen, Mrs. Alexander (Helga E Lindqvist)</td>
      <td> female</td>
      <td> 22.0</td>
      <td> 1</td>
      <td> 1</td>
      <td>            3101298</td>
      <td>  12.2875</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>5  </th>
      <td>  897</td>
      <td> 3</td>
      <td>                        Svensson, Mr. Johan Cervin</td>
      <td>   male</td>
      <td> 14.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>               7538</td>
      <td>   9.2250</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>6  </th>
      <td>  898</td>
      <td> 3</td>
      <td>                              Connolly, Miss. Kate</td>
      <td> female</td>
      <td> 30.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             330972</td>
      <td>   7.6292</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>7  </th>
      <td>  899</td>
      <td> 2</td>
      <td>                      Caldwell, Mr. Albert Francis</td>
      <td>   male</td>
      <td> 26.0</td>
      <td> 1</td>
      <td> 1</td>
      <td>             248738</td>
      <td>  29.0000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>8  </th>
      <td>  900</td>
      <td> 3</td>
      <td>         Abrahim, Mrs. Joseph (Sophie Halaut Easu)</td>
      <td> female</td>
      <td> 18.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>               2657</td>
      <td>   7.2292</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>9  </th>
      <td>  901</td>
      <td> 3</td>
      <td>                           Davies, Mr. John Samuel</td>
      <td>   male</td>
      <td> 21.0</td>
      <td> 2</td>
      <td> 0</td>
      <td>          A/4 48871</td>
      <td>  24.1500</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>10 </th>
      <td>  902</td>
      <td> 3</td>
      <td>                                  Ilieff, Mr. Ylio</td>
      <td>   male</td>
      <td>  NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>             349220</td>
      <td>   7.8958</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>11 </th>
      <td>  903</td>
      <td> 1</td>
      <td>                        Jones, Mr. Charles Cresson</td>
      <td>   male</td>
      <td> 46.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>                694</td>
      <td>  26.0000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>12 </th>
      <td>  904</td>
      <td> 1</td>
      <td>     Snyder, Mrs. John Pillsbury (Nelle Stevenson)</td>
      <td> female</td>
      <td> 23.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              21228</td>
      <td>  82.2667</td>
      <td>             B45</td>
      <td> S</td>
    </tr>
    <tr>
      <th>13 </th>
      <td>  905</td>
      <td> 2</td>
      <td>                              Howard, Mr. Benjamin</td>
      <td>   male</td>
      <td> 63.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              24065</td>
      <td>  26.0000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>14 </th>
      <td>  906</td>
      <td> 1</td>
      <td> Chaffee, Mrs. Herbert Fuller (Carrie Constance...</td>
      <td> female</td>
      <td> 47.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>        W.E.P. 5734</td>
      <td>  61.1750</td>
      <td>             E31</td>
      <td> S</td>
    </tr>
    <tr>
      <th>15 </th>
      <td>  907</td>
      <td> 2</td>
      <td>     del Carlo, Mrs. Sebastiano (Argenia Genovesi)</td>
      <td> female</td>
      <td> 24.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>      SC/PARIS 2167</td>
      <td>  27.7208</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>16 </th>
      <td>  908</td>
      <td> 2</td>
      <td>                                 Keane, Mr. Daniel</td>
      <td>   male</td>
      <td> 35.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             233734</td>
      <td>  12.3500</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>17 </th>
      <td>  909</td>
      <td> 3</td>
      <td>                                 Assaf, Mr. Gerios</td>
      <td>   male</td>
      <td> 21.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>               2692</td>
      <td>   7.2250</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>18 </th>
      <td>  910</td>
      <td> 3</td>
      <td>                      Ilmakangas, Miss. Ida Livija</td>
      <td> female</td>
      <td> 27.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>   STON/O2. 3101270</td>
      <td>   7.9250</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>19 </th>
      <td>  911</td>
      <td> 3</td>
      <td>             Assaf Khalil, Mrs. Mariana (Miriam")"</td>
      <td> female</td>
      <td> 45.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>               2696</td>
      <td>   7.2250</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>20 </th>
      <td>  912</td>
      <td> 1</td>
      <td>                            Rothschild, Mr. Martin</td>
      <td>   male</td>
      <td> 55.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>           PC 17603</td>
      <td>  59.4000</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>21 </th>
      <td>  913</td>
      <td> 3</td>
      <td>                         Olsen, Master. Artur Karl</td>
      <td>   male</td>
      <td>  9.0</td>
      <td> 0</td>
      <td> 1</td>
      <td>            C 17368</td>
      <td>   3.1708</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>22 </th>
      <td>  914</td>
      <td> 1</td>
      <td>              Flegenheim, Mrs. Alfred (Antoinette)</td>
      <td> female</td>
      <td>  NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>           PC 17598</td>
      <td>  31.6833</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>23 </th>
      <td>  915</td>
      <td> 1</td>
      <td>                   Williams, Mr. Richard Norris II</td>
      <td>   male</td>
      <td> 21.0</td>
      <td> 0</td>
      <td> 1</td>
      <td>           PC 17597</td>
      <td>  61.3792</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>24 </th>
      <td>  916</td>
      <td> 1</td>
      <td>   Ryerson, Mrs. Arthur Larned (Emily Maria Borie)</td>
      <td> female</td>
      <td> 48.0</td>
      <td> 1</td>
      <td> 3</td>
      <td>           PC 17608</td>
      <td> 262.3750</td>
      <td> B57 B59 B63 B66</td>
      <td> C</td>
    </tr>
    <tr>
      <th>25 </th>
      <td>  917</td>
      <td> 3</td>
      <td>                           Robins, Mr. Alexander A</td>
      <td>   male</td>
      <td> 50.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>          A/5. 3337</td>
      <td>  14.5000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>26 </th>
      <td>  918</td>
      <td> 1</td>
      <td>                      Ostby, Miss. Helene Ragnhild</td>
      <td> female</td>
      <td> 22.0</td>
      <td> 0</td>
      <td> 1</td>
      <td>             113509</td>
      <td>  61.9792</td>
      <td>             B36</td>
      <td> C</td>
    </tr>
    <tr>
      <th>27 </th>
      <td>  919</td>
      <td> 3</td>
      <td>                                 Daher, Mr. Shedid</td>
      <td>   male</td>
      <td> 22.5</td>
      <td> 0</td>
      <td> 0</td>
      <td>               2698</td>
      <td>   7.2250</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>28 </th>
      <td>  920</td>
      <td> 1</td>
      <td>                           Brady, Mr. John Bertram</td>
      <td>   male</td>
      <td> 41.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             113054</td>
      <td>  30.5000</td>
      <td>             A21</td>
      <td> S</td>
    </tr>
    <tr>
      <th>29 </th>
      <td>  921</td>
      <td> 3</td>
      <td>                                 Samaan, Mr. Elias</td>
      <td>   male</td>
      <td>  NaN</td>
      <td> 2</td>
      <td> 0</td>
      <td>               2662</td>
      <td>  21.6792</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>388</th>
      <td> 1280</td>
      <td> 3</td>
      <td>                              Canavan, Mr. Patrick</td>
      <td>   male</td>
      <td> 21.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             364858</td>
      <td>   7.7500</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>389</th>
      <td> 1281</td>
      <td> 3</td>
      <td>                       Palsson, Master. Paul Folke</td>
      <td>   male</td>
      <td>  6.0</td>
      <td> 3</td>
      <td> 1</td>
      <td>             349909</td>
      <td>  21.0750</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>390</th>
      <td> 1282</td>
      <td> 1</td>
      <td>                        Payne, Mr. Vivian Ponsonby</td>
      <td>   male</td>
      <td> 23.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>              12749</td>
      <td>  93.5000</td>
      <td>             B24</td>
      <td> S</td>
    </tr>
    <tr>
      <th>391</th>
      <td> 1283</td>
      <td> 1</td>
      <td>    Lines, Mrs. Ernest H (Elizabeth Lindsey James)</td>
      <td> female</td>
      <td> 51.0</td>
      <td> 0</td>
      <td> 1</td>
      <td>           PC 17592</td>
      <td>  39.4000</td>
      <td>             D28</td>
      <td> S</td>
    </tr>
    <tr>
      <th>392</th>
      <td> 1284</td>
      <td> 3</td>
      <td>                     Abbott, Master. Eugene Joseph</td>
      <td>   male</td>
      <td> 13.0</td>
      <td> 0</td>
      <td> 2</td>
      <td>          C.A. 2673</td>
      <td>  20.2500</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>393</th>
      <td> 1285</td>
      <td> 2</td>
      <td>                              Gilbert, Mr. William</td>
      <td>   male</td>
      <td> 47.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>         C.A. 30769</td>
      <td>  10.5000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>394</th>
      <td> 1286</td>
      <td> 3</td>
      <td>                          Kink-Heilmann, Mr. Anton</td>
      <td>   male</td>
      <td> 29.0</td>
      <td> 3</td>
      <td> 1</td>
      <td>             315153</td>
      <td>  22.0250</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>395</th>
      <td> 1287</td>
      <td> 1</td>
      <td>    Smith, Mrs. Lucien Philip (Mary Eloise Hughes)</td>
      <td> female</td>
      <td> 18.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              13695</td>
      <td>  60.0000</td>
      <td>             C31</td>
      <td> S</td>
    </tr>
    <tr>
      <th>396</th>
      <td> 1288</td>
      <td> 3</td>
      <td>                              Colbert, Mr. Patrick</td>
      <td>   male</td>
      <td> 24.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             371109</td>
      <td>   7.2500</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>397</th>
      <td> 1289</td>
      <td> 1</td>
      <td> Frolicher-Stehli, Mrs. Maxmillian (Margaretha ...</td>
      <td> female</td>
      <td> 48.0</td>
      <td> 1</td>
      <td> 1</td>
      <td>              13567</td>
      <td>  79.2000</td>
      <td>             B41</td>
      <td> C</td>
    </tr>
    <tr>
      <th>398</th>
      <td> 1290</td>
      <td> 3</td>
      <td>                    Larsson-Rondberg, Mr. Edvard A</td>
      <td>   male</td>
      <td> 22.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             347065</td>
      <td>   7.7750</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>399</th>
      <td> 1291</td>
      <td> 3</td>
      <td>                          Conlon, Mr. Thomas Henry</td>
      <td>   male</td>
      <td> 31.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>              21332</td>
      <td>   7.7333</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>400</th>
      <td> 1292</td>
      <td> 1</td>
      <td>                           Bonnell, Miss. Caroline</td>
      <td> female</td>
      <td> 30.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>              36928</td>
      <td> 164.8667</td>
      <td>              C7</td>
      <td> S</td>
    </tr>
    <tr>
      <th>401</th>
      <td> 1293</td>
      <td> 2</td>
      <td>                                   Gale, Mr. Harry</td>
      <td>   male</td>
      <td> 38.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              28664</td>
      <td>  21.0000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>402</th>
      <td> 1294</td>
      <td> 1</td>
      <td>                    Gibson, Miss. Dorothy Winifred</td>
      <td> female</td>
      <td> 22.0</td>
      <td> 0</td>
      <td> 1</td>
      <td>             112378</td>
      <td>  59.4000</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
    <tr>
      <th>403</th>
      <td> 1295</td>
      <td> 1</td>
      <td>                            Carrau, Mr. Jose Pedro</td>
      <td>   male</td>
      <td> 17.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             113059</td>
      <td>  47.1000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>404</th>
      <td> 1296</td>
      <td> 1</td>
      <td>                      Frauenthal, Mr. Isaac Gerald</td>
      <td>   male</td>
      <td> 43.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              17765</td>
      <td>  27.7208</td>
      <td>             D40</td>
      <td> C</td>
    </tr>
    <tr>
      <th>405</th>
      <td> 1297</td>
      <td> 2</td>
      <td>      Nourney, Mr. Alfred (Baron von Drachstedt")"</td>
      <td>   male</td>
      <td> 20.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>      SC/PARIS 2166</td>
      <td>  13.8625</td>
      <td>             D38</td>
      <td> C</td>
    </tr>
    <tr>
      <th>406</th>
      <td> 1298</td>
      <td> 2</td>
      <td>                         Ware, Mr. William Jeffery</td>
      <td>   male</td>
      <td> 23.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              28666</td>
      <td>  10.5000</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>407</th>
      <td> 1299</td>
      <td> 1</td>
      <td>                        Widener, Mr. George Dunton</td>
      <td>   male</td>
      <td> 50.0</td>
      <td> 1</td>
      <td> 1</td>
      <td>             113503</td>
      <td> 211.5000</td>
      <td>             C80</td>
      <td> C</td>
    </tr>
    <tr>
      <th>408</th>
      <td> 1300</td>
      <td> 3</td>
      <td>                   Riordan, Miss. Johanna Hannah""</td>
      <td> female</td>
      <td>  NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>             334915</td>
      <td>   7.7208</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>409</th>
      <td> 1301</td>
      <td> 3</td>
      <td>                         Peacock, Miss. Treasteall</td>
      <td> female</td>
      <td>  3.0</td>
      <td> 1</td>
      <td> 1</td>
      <td> SOTON/O.Q. 3101315</td>
      <td>  13.7750</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>410</th>
      <td> 1302</td>
      <td> 3</td>
      <td>                            Naughton, Miss. Hannah</td>
      <td> female</td>
      <td>  NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>             365237</td>
      <td>   7.7500</td>
      <td>             NaN</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>411</th>
      <td> 1303</td>
      <td> 1</td>
      <td>   Minahan, Mrs. William Edward (Lillian E Thorpe)</td>
      <td> female</td>
      <td> 37.0</td>
      <td> 1</td>
      <td> 0</td>
      <td>              19928</td>
      <td>  90.0000</td>
      <td>             C78</td>
      <td> Q</td>
    </tr>
    <tr>
      <th>412</th>
      <td> 1304</td>
      <td> 3</td>
      <td>                    Henriksson, Miss. Jenny Lovisa</td>
      <td> female</td>
      <td> 28.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>             347086</td>
      <td>   7.7750</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>413</th>
      <td> 1305</td>
      <td> 3</td>
      <td>                                Spector, Mr. Woolf</td>
      <td>   male</td>
      <td>  NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>          A.5. 3236</td>
      <td>   8.0500</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>414</th>
      <td> 1306</td>
      <td> 1</td>
      <td>                      Oliva y Ocana, Dona. Fermina</td>
      <td> female</td>
      <td> 39.0</td>
      <td> 0</td>
      <td> 0</td>
      <td>           PC 17758</td>
      <td> 108.9000</td>
      <td>            C105</td>
      <td> C</td>
    </tr>
    <tr>
      <th>415</th>
      <td> 1307</td>
      <td> 3</td>
      <td>                      Saether, Mr. Simon Sivertsen</td>
      <td>   male</td>
      <td> 38.5</td>
      <td> 0</td>
      <td> 0</td>
      <td> SOTON/O.Q. 3101262</td>
      <td>   7.2500</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>416</th>
      <td> 1308</td>
      <td> 3</td>
      <td>                               Ware, Mr. Frederick</td>
      <td>   male</td>
      <td>  NaN</td>
      <td> 0</td>
      <td> 0</td>
      <td>             359309</td>
      <td>   8.0500</td>
      <td>             NaN</td>
      <td> S</td>
    </tr>
    <tr>
      <th>417</th>
      <td> 1309</td>
      <td> 3</td>
      <td>                          Peter, Master. Michael J</td>
      <td>   male</td>
      <td>  NaN</td>
      <td> 1</td>
      <td> 1</td>
      <td>               2668</td>
      <td>  22.3583</td>
      <td>             NaN</td>
      <td> C</td>
    </tr>
  </tbody>
</table>
<p>418 rows × 11 columns</p>
</div>



### Add our independent variable to our test data. (It is usually left blank by Kaggle because it is the value you are trying to predict.)


```python
test_data['Survived'] = 1.23
```

Our binned results data:


```python
results 
```




    {'Logit': [<statsmodels.discrete.discrete_model.BinaryResultsWrapper at 0x10b1e8550>,
      'Survived ~ C(Pclass) + C(Sex) + Age + SibSp  + C(Embarked)']}




```python
# Use your model to make prediction on our test set. 
compared_resuts = ka.predict(test_data, results, 'Logit')
compared_resuts = Series(compared_resuts)  # convert our model to a series for easy output
```


```python
# output and submit to kaggle
compared_resuts.to_csv("data/output/logitregres.csv")
```

### Results as scored by Kaggle: RMSE = 0.77033  That result is pretty good. ECT ECT ECT


```python
# Create an acceptable formula for our machine learning algorithms
formula_ml = 'Survived ~ C(Pclass) + C(Sex) + Age + SibSp + Parch + C(Embarked)'
```

### Support Vector Machine (SVM)

*"So uhhh, what if a straight line just doesn’t cut it."*

**Wikipeda:**
>In machine learning, support vector machines (SVMs, also support vector networks[1]) are supervised learning models with associated learning algorithms that analyze data and recognize patterns, used for classification and regression analysis. The basic SVM takes a set of input data and predicts, for each given input, which of two possible classes forms the output, making it a non-probabilistic binary linear classifier. Given a set of training examples, each marked as belonging to one of two categories, an SVM training algorithm builds a model that assigns new examples into one category or the other. An SVM model is a representation of the examples as points in space, mapped so that the examples of the separate categories are divided by a clear gap that is as wide as possible. New examples are then mapped into that same space and predicted to belong to a category based on which side of the gap they fall on.
In addition to performing linear classification, SVMs can efficiently perform non-linear classification using what is called the kernel trick, implicitly mapping their inputs into high-dimensional feature spaces.

## From me
The logit model we just implemented was great in that it showed exactly where to draw our decision boundary or our 'survival cut off'.  But if you’re like me, you could have thought, "So uhhh, what if a straight line just doesn’t cut it". A linear line is okay, but can we do better? Perhaps a more complex decision boundary like a wave, circle, or maybe some sort of strange polygon would describe the variance observed in our sample better than a line.  Imagine if we were predicating survival based on age. It could be a linear decision boundary, meaning  each additional time you've gone around the sun you were 1 unit more or less likely to survive. But I think it could be easy to imagine some sort of curve, where a young healthy person would have the best chance of survival, and sadly the very old and very young a like: a poor chance. Now that’s a interesting question to answer. But our logit model can only evaluate a linear decision boundary. How do we get around this? With the usual answer to life the universe and everything;  $MATH$. 

**The answer:**
We could transform our logit equation from expressing a linear relationship like so:

$survived  = \beta_0 + \beta_1pclass + \beta_2sex + \beta_3age + \beta_4sibsp + \beta_5parch + \beta_6embarked$

Which we'll represent for convenience as: 
$y = x$
		

to a expressing a linear expression of a non-linear relationship: 
$\log(y) = \log(x)$

By doing this we're not breaking the rules. Logit models are *only* efficient at modeling linear relationships, so we're just giving it a linear relationship of a non-linear thing. 

An easy way to visualize this by looking at a graph an exponential relationship. Like the graph of $x^3$:

![x3](https://raw.github.com/agconti/kaggle-titanic/master/images/x3.png)

Here its obvious that this is not linear. If used it as an equation for our logit model, $y = x^3$; we would get bad results. But if we transformed it by taking the log  of our equation, $\log(y) = \log(x^3)$. We would get a graph like this:

![loglogx3](https://raw.github.com/agconti/kaggle-titanic/master/images/loglogx3.png)

That looks pretty linear to me. 

This process of transforming models so that they can be better expressed in a different mathematical plane is exactly what the Support Vector Machine does for us. The math behind how it does that is not trivial, so if your interested; put on your reading glasses and head over [here](http://dustwell.com/PastWork/IntroToSVM.pdf). Below is the process of implementing a SVM model and examining the results after the SVM transforms our equation into three different mathematical plains. The first is linear, and is similar to our logic model. Next is an exponential, polynomial, transformation and finally a blank transformation.



```python
# set plotting parameters
plt.figure(figsize=(8,6))

# create a regression friendly data frame
y, x = dmatrices(formula_ml, data=df, return_type='matrix')

# select which features we would like to analyze
# try chaning the selection here for diffrent output.
# Choose : [2,3] - pretty sweet DBs [3,1] --standard DBs [7,3] -very cool DBs,
# [3,6] -- very long complex dbs, could take over an hour to calculate! 
feature_1 = 2
feature_2 = 3

X = np.asarray(x)
X = X[:,[feature_1, feature_2]]  


y = np.asarray(y)
# needs to be 1 dimenstional so we flatten. it comes out of dmatirces with a shape. 
y = y.flatten()      

n_sample = len(X)

np.random.seed(0)
order = np.random.permutation(n_sample)

X = X[order]
y = y[order].astype(np.float)

# do a cross validation
nighty_precent_of_sample = int(.9 * n_sample)
X_train = X[:nighty_precent_of_sample]
y_train = y[:nighty_precent_of_sample]
X_test = X[nighty_precent_of_sample:]
y_test = y[nighty_precent_of_sample:]

# create a list of the types of kerneks we will use for your analysis
types_of_kernels = ['linear', 'rbf', 'poly']

# specify our color map for plotting the results
color_map = plt.cm.RdBu_r

# fit the model
for fig_num, kernel in enumerate(types_of_kernels):
    clf = svm.SVC(kernel=kernel, gamma=3)
    clf.fit(X_train, y_train)

    plt.figure(fig_num)
    plt.scatter(X[:, 0], X[:, 1], c=y, zorder=10, cmap=color_map)

    # circle out the test data
    plt.scatter(X_test[:, 0], X_test[:, 1], s=80, facecolors='none', zorder=10)
    
    plt.axis('tight')
    x_min = X[:, 0].min()
    x_max = X[:, 0].max()
    y_min = X[:, 1].min()
    y_max = X[:, 1].max()

    XX, YY = np.mgrid[x_min:x_max:200j, y_min:y_max:200j]
    Z = clf.decision_function(np.c_[XX.ravel(), YY.ravel()])

    # put the result into a color plot
    Z = Z.reshape(XX.shape)
    plt.pcolormesh(XX, YY, Z > 0, cmap=color_map)
    plt.contour(XX, YY, Z, colors=['k', 'k', 'k'], linestyles=['--', '-', '--'],
               levels=[-.5, 0, .5])

    plt.title(kernel)
    plt.show()
```


![png](Titanic_files/Titanic_38_0.png)



    <matplotlib.figure.Figure at 0x10d4820d0>



![png](Titanic_files/Titanic_38_2.png)



![png](Titanic_files/Titanic_38_3.png)


Any value in the blue survived while anyone in the read did not. Checkout the graph for the linear transformation. It created its decision boundary right on 50%! That guess from earlier turned out to be pretty good.  As you can see, the remaining decision boundaries are much more complex than our original linear decision boundary. These more complex boundaries may be able to capture more structure in the dataset, if that structure exists, and so might create a more powerful predictive model.

Pick a decision boundary that you like, adjust the code below, and submit the results to Kaggle to see how well it worked!


```python
# Here you can output which ever result you would like by changing the Kernel and clf.predict lines
# Change kernel here to poly, rbf or linear
# adjusting the gamma level also changes the degree to which the model is fitted
clf = svm.SVC(kernel='poly', gamma=3).fit(X_train, y_train)                                                            
y,x = dmatrices(formula_ml, data=test_data, return_type='dataframe')

# Change the interger values within x.ix[:,[6,3]].dropna() explore the relationships between other 
# features. the ints are column postions. ie. [6,3] 6th column and the third column are evaluated. 
res_svm = clf.predict(x.ix[:,[6,3]].dropna()) 

res_svm = DataFrame(res_svm,columns=['Survived'])
res_svm.to_csv("data/output/svm_poly_63_g10.csv") # saves the results for you, change the name as you please. 
```

### Random Forest

"Well, What if this line / decision boundary thing doesn’t work at all."

**Wikipedia, crystal clear as always:**
>Random forests are an ensemble learning method for classification (and regression) that operate by constructing a multitude of decision trees at training time and outputting the class that is the mode of the classes output by individual trees.

**Once again, the skinny and why it matters to you:**

There are always skeptics, and you just might be one about all the fancy lines we've created so far. Well for you, here’s another option; the Random Forest. This technique is a form of non-parametric modeling that does away with all those equations we created above, and uses raw computing power and a clever statistical observation to tease the structure out of the data. 

An anecdote to explain how this the forest works starts with the lowly gumball jar. We've all guess how many gumballs are in that jar at one time or another, and odds are not a single one of us guessed exactly right. Interestingly though, while each of our individual guesses for probably were wrong, the average of all of the guesses, if there were enough, usually comes out to be pretty close to the actual number of gumballs in the jar. Crazy, I know.  This idea is that clever statistical observation that lets random forests work.

**How do they work?** A random forest algorithm randomly generates many extremely simple models to explain the variance observed in random subsections of our data.  These models are like our gumball guesses. They are all awful individually. Really awful. But once they are averaged, they can be powerful predictive tools. The averaging step is the secret sauce. While the vast majority of those models were extremely poor; they were all as bad as each other on average. So when their predictions are averaged together, the bad ones average their effect on our model out to zero. The thing that remains, *if anything*, is one or a handful of those models have stumbled upon the true structure of the data.
The cell below shows the process of instantiating and fitting a random forest, generating predictions form the resulting model, and then scoring the results.


```python
# import the machine learning library that holds the randomforest
import sklearn.ensemble as ske

# Create the random forest model and fit the model to our training data
y, x = dmatrices(formula_ml, data=df, return_type='dataframe')
# RandomForestClassifier expects a 1 demensional NumPy array, so we convert
y = np.asarray(y).ravel()
#instantiate and fit our model
results_rf = ske.RandomForestClassifier(n_estimators=100).fit(x, y)

# Score the results
score = results_rf.score(x, y)
print "Mean accuracy of Random Forest Predictions on the data was: {0}".format(score)
```

    Mean accuracy of Random Forest Predictions on the data was: 0.945224719101
    

Our random forest performed only slightly better than a thumb wave, meaning that if you randomly assigned 1s and 0s by waving your thumb up and down you would do almost as well on average. It seems that this time our random forest did not stumble on the true structure of the data. 

These are just a few of the machine learning techniques that you can apply. Try a few for yourself and move up the leader board!

Ready to see more an example of a more advanced analysis? Check out these notebooks:

* [Kaggle Competition | Blue Book for Bulldozers Quantitative Model](http://nbviewer.ipython.org/github.com/agconti/AGC_BlueBook/master/BlueBook.ipynb#)
* [GOOG VS AAPL Correlation Arb](http://nbviewer.ipython.org/github.com/agconti/AGCTrading/master/GOOG%2520V.%2520AAPL%2520Correlation%2520Arb.ipynb)
* [US Dollar as a Vehicle Currency; an analysis through Italian Trade](https://github.com/agconti/US_Dollar_Vehicle_Currency)
        
#### Follow me on [github](https://github.com/agconti), and [twitter](https://twitter.com/agconti) for more books to come soon!

