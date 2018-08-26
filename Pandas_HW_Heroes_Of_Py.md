
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# File to Load (Remember to Change These)
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)
purchase_data




```




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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Yalae81</td>
      <td>22</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>3.61</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Itheria73</td>
      <td>36</td>
      <td>Male</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>2.18</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Iskjaskst81</td>
      <td>20</td>
      <td>Male</td>
      <td>162</td>
      <td>Abyssal Shard</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Undjask33</td>
      <td>22</td>
      <td>Male</td>
      <td>21</td>
      <td>Souleater</td>
      <td>1.10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Chanosian48</td>
      <td>35</td>
      <td>Other / Non-Disclosed</td>
      <td>136</td>
      <td>Ghastly Adamantite Protector</td>
      <td>3.58</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Inguron55</td>
      <td>23</td>
      <td>Male</td>
      <td>95</td>
      <td>Singed Onyx Warscythe</td>
      <td>4.74</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Haisrisuir60</td>
      <td>23</td>
      <td>Male</td>
      <td>162</td>
      <td>Abyssal Shard</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Saelaephos52</td>
      <td>21</td>
      <td>Male</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>4.18</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Assjaskan73</td>
      <td>22</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>1.70</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Saesrideu94</td>
      <td>35</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>4.86</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Lisassa64</td>
      <td>21</td>
      <td>Female</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>2.89</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Lisirra25</td>
      <td>20</td>
      <td>Male</td>
      <td>40</td>
      <td>Second Chance</td>
      <td>2.52</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Zontibe81</td>
      <td>21</td>
      <td>Male</td>
      <td>161</td>
      <td>Devine</td>
      <td>1.76</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Reunasu60</td>
      <td>22</td>
      <td>Female</td>
      <td>82</td>
      <td>Nirvana</td>
      <td>4.90</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Chamalo71</td>
      <td>30</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>4.64</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Iathenudil29</td>
      <td>20</td>
      <td>Male</td>
      <td>57</td>
      <td>Despair, Favor of Due Diligence</td>
      <td>4.60</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Phiarithdeu40</td>
      <td>20</td>
      <td>Male</td>
      <td>168</td>
      <td>Sun Strike, Jaws of Twisted Visions</td>
      <td>1.48</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Siarithria38</td>
      <td>38</td>
      <td>Other / Non-Disclosed</td>
      <td>24</td>
      <td>Warped Fetish</td>
      <td>3.81</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Eyrian71</td>
      <td>40</td>
      <td>Male</td>
      <td>151</td>
      <td>Severance</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Siala43</td>
      <td>30</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Lisirra87</td>
      <td>29</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>4.23</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Lirtossa84</td>
      <td>11</td>
      <td>Male</td>
      <td>71</td>
      <td>Demise</td>
      <td>1.61</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Eusri44</td>
      <td>7</td>
      <td>Male</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>3.09</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Aela59</td>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>4.32</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Tyida79</td>
      <td>24</td>
      <td>Male</td>
      <td>37</td>
      <td>Shadow Strike, Glory of Ending Hope</td>
      <td>3.16</td>
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
    </tr>
    <tr>
      <th>750</th>
      <td>750</td>
      <td>Iljask75</td>
      <td>22</td>
      <td>Male</td>
      <td>167</td>
      <td>Malice, Legacy of the Queen</td>
      <td>3.61</td>
    </tr>
    <tr>
      <th>751</th>
      <td>751</td>
      <td>Lisjaskan36</td>
      <td>11</td>
      <td>Male</td>
      <td>180</td>
      <td>Stormcaller</td>
      <td>3.36</td>
    </tr>
    <tr>
      <th>752</th>
      <td>752</td>
      <td>Mindjasksya61</td>
      <td>17</td>
      <td>Male</td>
      <td>112</td>
      <td>Worldbreaker</td>
      <td>2.60</td>
    </tr>
    <tr>
      <th>753</th>
      <td>753</td>
      <td>Frichirranya75</td>
      <td>36</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>4.23</td>
    </tr>
    <tr>
      <th>754</th>
      <td>754</td>
      <td>Pheosurllorin41</td>
      <td>23</td>
      <td>Female</td>
      <td>79</td>
      <td>Alpha, Oath of Zeal</td>
      <td>4.05</td>
    </tr>
    <tr>
      <th>755</th>
      <td>755</td>
      <td>Raesty92</td>
      <td>12</td>
      <td>Male</td>
      <td>76</td>
      <td>Haunted Bronzed Bludgeon</td>
      <td>3.15</td>
    </tr>
    <tr>
      <th>756</th>
      <td>756</td>
      <td>Ilast79</td>
      <td>20</td>
      <td>Male</td>
      <td>73</td>
      <td>Ritual Mace</td>
      <td>2.05</td>
    </tr>
    <tr>
      <th>757</th>
      <td>757</td>
      <td>Eratiel90</td>
      <td>18</td>
      <td>Male</td>
      <td>57</td>
      <td>Despair, Favor of Due Diligence</td>
      <td>4.60</td>
    </tr>
    <tr>
      <th>758</th>
      <td>758</td>
      <td>Iral74</td>
      <td>21</td>
      <td>Male</td>
      <td>182</td>
      <td>Toothpick</td>
      <td>4.03</td>
    </tr>
    <tr>
      <th>759</th>
      <td>759</td>
      <td>Tyaelorap29</td>
      <td>25</td>
      <td>Male</td>
      <td>72</td>
      <td>Winter's Bite</td>
      <td>3.77</td>
    </tr>
    <tr>
      <th>760</th>
      <td>760</td>
      <td>Aithelis62</td>
      <td>21</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>2.38</td>
    </tr>
    <tr>
      <th>761</th>
      <td>761</td>
      <td>Assim27</td>
      <td>45</td>
      <td>Male</td>
      <td>17</td>
      <td>Lazarus, Terror of the Earth</td>
      <td>1.70</td>
    </tr>
    <tr>
      <th>762</th>
      <td>762</td>
      <td>Asur53</td>
      <td>26</td>
      <td>Male</td>
      <td>110</td>
      <td>Suspension</td>
      <td>1.44</td>
    </tr>
    <tr>
      <th>763</th>
      <td>763</td>
      <td>Lassilsala30</td>
      <td>21</td>
      <td>Male</td>
      <td>85</td>
      <td>Malificent Bag</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>764</th>
      <td>764</td>
      <td>Saedaiphos46</td>
      <td>18</td>
      <td>Male</td>
      <td>113</td>
      <td>Solitude's Reaver</td>
      <td>4.07</td>
    </tr>
    <tr>
      <th>765</th>
      <td>765</td>
      <td>Irith83</td>
      <td>18</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>2.07</td>
    </tr>
    <tr>
      <th>766</th>
      <td>766</td>
      <td>Aelastirin39</td>
      <td>23</td>
      <td>Male</td>
      <td>58</td>
      <td>Freak's Bite, Favor of Holy Might</td>
      <td>4.14</td>
    </tr>
    <tr>
      <th>767</th>
      <td>767</td>
      <td>Ilmol66</td>
      <td>8</td>
      <td>Female</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>768</th>
      <td>768</td>
      <td>Assassasta79</td>
      <td>38</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>769</th>
      <td>769</td>
      <td>Ilosian36</td>
      <td>15</td>
      <td>Male</td>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>4.58</td>
    </tr>
    <tr>
      <th>770</th>
      <td>770</td>
      <td>Lirtosia63</td>
      <td>34</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>1.02</td>
    </tr>
    <tr>
      <th>771</th>
      <td>771</td>
      <td>Iskossasda43</td>
      <td>16</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>4.35</td>
    </tr>
    <tr>
      <th>772</th>
      <td>772</td>
      <td>Asur53</td>
      <td>26</td>
      <td>Male</td>
      <td>136</td>
      <td>Ghastly Adamantite Protector</td>
      <td>3.58</td>
    </tr>
    <tr>
      <th>773</th>
      <td>773</td>
      <td>Hala31</td>
      <td>21</td>
      <td>Male</td>
      <td>19</td>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>1.02</td>
    </tr>
    <tr>
      <th>774</th>
      <td>774</td>
      <td>Jiskjask80</td>
      <td>11</td>
      <td>Male</td>
      <td>101</td>
      <td>Final Critic</td>
      <td>4.19</td>
    </tr>
    <tr>
      <th>775</th>
      <td>775</td>
      <td>Aethedru70</td>
      <td>21</td>
      <td>Female</td>
      <td>60</td>
      <td>Wolf</td>
      <td>3.54</td>
    </tr>
    <tr>
      <th>776</th>
      <td>776</td>
      <td>Iral74</td>
      <td>21</td>
      <td>Male</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.63</td>
    </tr>
    <tr>
      <th>777</th>
      <td>777</td>
      <td>Yathecal72</td>
      <td>20</td>
      <td>Male</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>3.46</td>
    </tr>
    <tr>
      <th>778</th>
      <td>778</td>
      <td>Sisur91</td>
      <td>7</td>
      <td>Male</td>
      <td>101</td>
      <td>Final Critic</td>
      <td>4.19</td>
    </tr>
    <tr>
      <th>779</th>
      <td>779</td>
      <td>Ennrian78</td>
      <td>24</td>
      <td>Male</td>
      <td>50</td>
      <td>Dawn</td>
      <td>4.60</td>
    </tr>
  </tbody>
</table>
<p>780 rows × 7 columns</p>
</div>



## Player Count

* Display the total number of players



```python
number = purchase_data["Purchase ID"].count()
number
```




    780




```python
pd.DataFrame({"Player Count":[number]})

```




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
      <th>Player Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>780</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
unique_items = len(purchase_data["Item ID"].unique())
average_price = purchase_data["Price"].mean()
average_price
```




    3.050987179487176




```python
pd.DataFrame({"Number Of Unique Items":[unique_items],"Average Price":[average_price]})

```




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
      <th>Number Of Unique Items</th>
      <th>Average Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>3.050987</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
pd.DataFrame({"Total Count":[male_players],"Total Count":[female_players],"Total Count"[other/_non-disclosed],
              "Percentage of Players":[male_players],[female_players],[other/_non-disclosed]})
                                                                                                             
```


      File "<ipython-input-25-92569239fbb7>", line 1
        pd.DataFrame({"Total Count":[male_players],"Total Count":[female_players],"Total Count"[other/_non-disclosed],
                                                                                                                     ^
    SyntaxError: invalid syntax
    



## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$4.47</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$1,967.64</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$4.56</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python

```




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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$3.76</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$4.12</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$4.76</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$3.19</td>
    </tr>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>19</th>
      <th>Pursuit, Cudgel of Necromancy</th>
      <td>8</td>
      <td>$1.02</td>
      <td>$8.16</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>8</td>
      <td>$4.88</td>
      <td>$39.04</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>


