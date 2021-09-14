# Data-Analysis-Farmers
This is an anlysis on data colleted on 4800 farmers 


## Installation
Use the package manager pip to install numpy,pandas,matplotlib and seaborn
```bash
pip install pandas
pip install numpy
pip install matplotlib.py1p1lo1t
pip install seaborn
``` 
## Usage
```python 
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
```python

### Import data and convert to csv file

```farmer_data = pd.read_excel('Farmer Profile.xlsx')```python
C:\Users\EMMANUELLA\AppData\Roaming\Python\Python37\site-packages\ipykernel_launcher.py:1: FutureWarning: Inferring datetime64[ns] from data containing strings is deprecated and will be removed in a future version. To retain the old behavior explicitly pass Series(data, dtype={value.dtype})
  """Entry point for launching an IPython kernel.```python

```farmer_data.to_csv('Farmer Profile.csv')```python
In [4]:
### Read first 10 rows of data
```farmer_data.head()
Out[4]:
Unnamed: 0	_id	device_response_id	completion_rate	contact_id	contact_language_id	device_id	duration	end_location	end_timestamp	...	user_contact_id	user_id	validated_by	validated_on	Do you have a Mobile Money account?	q24477o	q24477oc	Do you herewith confirm that the information given in this report is correct and complete	q24478o	q24478oc
0	9858.0	60d990f8a74a6f4549af0f37	a7e12664d4c44ab8-1603877929402	81.08	NaN	NaN	1158.0	02:05:50	{'type': 'Point', 'coordinates': [0.0, 0.0]}	2020-10-28 11:44:39	...	0.0	746.0	Mary Serwaa Numafo	2020-11-04 11:31:12	NaN	NaN	NaN	NaN	NaN	NaN
1	23756.0	60d993dfa74a6f4549af7c42	85f81e782b65cbc6-1602237039201	89.19	NaN	NaN	1135.0	00:07:15	{'type': 'Point', 'coordinates': [0.0, 0.0]}	2020-10-09 09:57:54	...	0.0	481.0	NaN	NaT	NaN	NaN	NaN	NaN	NaN	NaN
2	19974.0	60d992dca74a6f4549af5e4f	1602690782.4212-421-11	13.51	NaN	NaN	1.0	00:00:00	{'type': 'Point', 'coordinates': [-1.38882, 5....	2020-10-14 15:53:02	...	0.0	346.0	NaN	NaT	NaN	NaN	NaN	NaN	NaN	NaN
3	39495.0	60e30a85a74a6f4549b19c42	c50eb0582bd7181e-1599470200528	86.49	NaN	NaN	705.0	00:05:50	{'type': 'Point', 'coordinates': [0.0, 0.0]}	2020-09-07 09:22:30	...	0.0	466.0	NaN	NaT	NaN	NaN	NaN	NaN	NaN	NaN
4	44825.0	60e30bb3a74a6f4549b1c5ed	50027e9898a0f83a-1597685872897	21.62	63078.0	121.0	817.0	00:00:00	{'type': 'Point', 'coordinates': [0.0, 0.0]}	2020-08-17 17:37:52	...	0.0	520.0	NaN	NaT	NaN	NaN	NaN	NaN	NaN	NaN
5 rows × 140 columns```python

#### Checking for null values
```farmer_data.isnull().sum().head()
Out[5]:
Unnamed: 0               0
_id                      0
device_response_id       0
completion_rate          0
contact_id            1442
dtype: int64
In [6]:
sns.heatmap(farmer_data.isnull(), yticklabels = False ,cbar = True , cmap = 'viridis')
Out[6]:![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Null_values.png)```python
<AxesSubplot:>

In [7]:
###  Cleaning data
```## Columns like sales_point_name had 75% of it cells null
farmer_data.drop(['sale_point_name','sale_point_id','device_response_id','q24478oc','q24477oc','end_location','end_timestamp','duration','flags','farmer_verification','publish_date','Location','Please record your evidence of consent. Eg. "I, Akosua Mansa agree that my information can be taken"','flag_summary','internal_response_id','flagged_responses','Do you herewith confirm that the information given in this report is correct and complete'], axis = 1, inplace = True)```python
In [8]:
## Cleaning more data
```farmer_data.drop(['q10288oc','q10289oc','q10290oc','Phone Number','q10292oc','Farmer Image','q10306oc','q10308oc','q10319o','q10310oc','q10294oc','q10305oc','q10311oc','q10394p','q11827pid','q18427','q18427o','q18427oc','q24478o','q24477o','Do you have a Mobile Money account?','validated_on','Name of bank','user_contact_id','updated_at','survey_id','submitted_on','start_timestamp','start_location','score','q22148t','remarks','q18430oc','q18430o','q18428','Do you have a bank account?','q18429oc','q18429o','Do you have children?','q18428pid','q10301oc','q18428p','q10284oc','q10319oc','Provide the phone number of a relative if you do not own a phone.','q12024oc','Please provide phone number linked to your Mobile Money account.','q10322oc','q10321oc','q10319o','q10318oc','q10314oc','Date of birth','National ID image (ID card image  or Upload Image)'] ,axis = 1, inplace =True)```python
In [9]:
### Drop first column
```farmer_data.drop( columns = farmer_data.columns[0] , axis =1 ,inplace = True)```python
In [10]:
```sns.set_style('whitegrid')``python
In [11]:
### filling numerical null values with mean values of columns
```mean_age = farmer_data['Age'].mean()
farmer_data['Age'].fillna(value = mean_age , inplace = True)
In [12]:
mean_annual_primary_crop = farmer_data['What is your annual primary crop  yield estimate (bags)?'].mean().round()
farmer_data['What is your annual primary crop  yield estimate (bags)?'].fillna(value = mean_annual_primary_crop, inplace = True)
In [13]:
mean_farm_size_primary_crop = farmer_data['What is the farm size of your primary crop in acres?'].mean().round()
farmer_data['What is the farm size of your primary crop in acres?'].fillna(value = mean_farm_size_primary_crop , inplace = True)
In [14]:
mean_total_farmsize =farmer_data['What is your total farm size? (in acres)'].mean().round()
farmer_data['What is your total farm size? (in acres)'].fillna(value = mean_total_farmsize , inplace = True)
In [15]:
mean_years_of_farming_experience = farmer_data['Years of farming experience?'].mean().round()
farmer_data['Years of farming experience?'].fillna(value = mean_years_of_farming_experience  , inplace =  True)
In [16]:
mean_number_of_children = farmer_data['Indicate Number of children'].mean().round()
farmer_data['Indicate Number of children'].fillna(value = mean_number_of_children , inplace = True)
In [17]:
mean_household_size = farmer_data['Household size'].mean().round()
farmer_data['Household size'].fillna(value = mean_household_size , inplace = True)
In [18]:
farmer_data['Household size'].isnull().sum()
Out[18]:
0
In [19]:
### Fill null categorical variables with mode (highest) values of respective columns
farmer_data.fillna(farmer_data.mode().iloc[0], inplace = True)
``` python
In [20]:
### Group  categorical variables by respective codes

```farmer_data['consent'] = farmer_data.groupby(['I consent to my personal data being recorded and processed for purposes to aid farmer insight and decision making','q10284o']).ngroup()

farmer_data['Gender1'] = farmer_data.groupby(['Gender','q10288o']).ngroup()

farmer_data['Mobile phone'] = farmer_data.groupby(['Do you own a mobile phone?','q10289o']).ngroup()

farmer_data['Feature phone'] = farmer_data.groupby(['Is it a feature phone (yam phone) or a smartphone?','q10290o']).ngroup()

farmer_data["Farmer's Language1"] = farmer_data.groupby(["Farmer's Language",'q10292o']).ngroup()

farmer_data['Primary crop grown (Highest income-generating crop1)'] = farmer_data.groupby(['Primary crop grown (Highest income-generating crop)','q10294o']).ngroup()

farmer_data['Marital Status1'] = farmer_data.groupby(['Marital Status','q10301o']).ngroup()

farmer_data['Educational level'] = farmer_data.groupby(['What is your highest level of education','q10305o']).ngroup()

farmer_data['Main source of income'] = farmer_data.groupby(['What is your main source of income?','q10306o']).ngroup()

farmer_data['Secondary source of income'] = farmer_data.groupby(['Secondary source of income?','q10308o']).ngroup()

farmer_data['Livestock'] = farmer_data.groupby(['Do you keep livestock?','q10310o']).ngroup()

farmer_data[' Which Livestock '] = farmer_data.groupby(['Which animal do your rear?','q10311o']).ngroup()

farmer_data[' Farm ownership '] = farmer_data.groupby(['Farm ownership status?','q10314o']).ngroup()

farmer_data[' Secondary crop? '] = farmer_data.groupby(['Do you grow a secondary crop?','q10318o']).ngroup()

farmer_data[' Secondary crop(s) grown1 '] = farmer_data.groupby(['Secondary crop(s) grown','q10319cs']).ngroup()

farmer_data[' Secondary crops mixed with the primary crop in one farm'] = farmer_data.groupby(['Are your secondary crops mixed with the primary crop in one farm?','q10321o']).ngroup()

farmer_data['Mobile network  primarily registered for Mobile Money '] = farmer_data.groupby(['Which mobile network have you primarily registered for Mobile Money?','q10322o']).ngroup()

farmer_data[' Belong to Farmer group'] = farmer_data.groupby(['Do you belong to a farmer group?','q12024o']).ngroup()

farmer_data['Name of Farmer group'] = farmer_data.groupby(['Name of Farmer Group/ Association/ Agribusiness','q11827p']).ngroup()```python
In [21]:
``farmer_data['Marital Status'].head()
Out[21]:
0    Single/Never married
1                 Widowed
2                 Married
3                 Married
4                 Married
Name: Marital Status, dtype: object```python
In [22]:
```farmer_data.isnull().sum().head(40)
Out[22]:
_id                                                                                                                  0
completion_rate                                                                                                      0
contact_id                                                                                                           0
contact_language_id                                                                                                  0
device_id                                                                                                            0
is_complete                                                                                                          0
is_flagged                                                                                                           0
is_validated                                                                                                         0
language_id                                                                                                          0
organisation_id                                                                                                      0
I consent to my personal data being recorded and processed for purposes to aid farmer insight and decision making    0
q10284o                                                                                                              0
q10287geo                                                                                                            0
Gender                                                                                                               0
q10288o                                                                                                              0
Do you own a mobile phone?                                                                                           0
q10289o                                                                                                              0
Is it a feature phone (yam phone) or a smartphone?                                                                   0
q10290o                                                                                                              0
Farmer's Language                                                                                                    0
q10292o                                                                                                              0
Primary crop grown (Highest income-generating crop)                                                                  0
q10294o                                                                                                              0
Farmer Code                                                                                                          0
Marital Status                                                                                                       0
q10301o                                                                                                              0
Household size                                                                                                       0
Indicate Number of children                                                                                          0
What is your highest level of education                                                                              0
q10305o                                                                                                              0
What is your main source of income?                                                                                  0
q10306o                                                                                                              0
Secondary source of income?                                                                                          0
q10308o                                                                                                              0
Do you keep livestock?                                                                                               0
q10310o                                                                                                              0
Which animal do your rear?                                                                                           0
q10311cs                                                                                                             0
q10311o                                                                                                              0
Years of farming experience?                                                                                         0
dtype: int64
```python
####  No null values!
```sns.heatmap(farmer_data.isnull(),cbar = True, yticklabels = False, cmap = 'viridis')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/No_null_values.png)
Out[23]:
<AxesSubplot:>

##  GRAPHS


#Checking the level of compltion  of questionnaires by respondents(Farmers) 
```sns.histplot( x = 'completion_rate' , data = farmer_data )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/completion_rate.png)

<AxesSubplot:xlabel='completion_rate', ylabel='Count'>

#In seaborn, the hue parameter determines which column in the data frame should be used for colour encoding

In [25]:
#Checking if data collected 11by enumerators were validated  the data given is
# The graph indicates over 3500 of the data provided has been validated
```sns.countplot(x = 'is_validated' , data = farmer_data ,palette='YlOrBr')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/is_validated.png)
<AxesSubplot:xlabel='is_validated', ylabel='count'>

In [26]:
# All   farmers gave their consent for data collection 
```sns.countplot( x= 'I consent to my personal data being recorded and processed for purposes to aid farmer insight and decision making', data = farmer_data , palette='deep')```
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/consent.png)
<AxesSubplot:xlabel='I consent to my personal data being recorded and processed for purposes to aid farmer insight and decision making', ylabel='count'>

In [27]:
#Indicates the maximum of data entered is not flagged
```sns.countplot(x = 'is_flagged' , data = farmer_data,palette='icefire' )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/flagged.png)
<AxesSubplot:xlabel='is_flagged', ylabel='count'>

In [28]:
### Distribution of Female and Male farmers.
#Female farmers are more than male farmers
```sns.countplot(x = 'Gender' , data = farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/gender.png)
<AxesSubplot:xlabel='Gender', ylabel='count'>

In [29]:
```sns.histplot(x = 'Age', kde = True ,data = farmer_data )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Age_kde.png)
<AxesSubplot:xlabel='Age', ylabel='Count'>

In [30]:
```sns.histplot(x = 'Age', hue = 'Gender' , kde = True ,data = farmer_data )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Age_Gender.png)
<AxesSubplot:xlabel='Age', ylabel='Count'>

In [31]:
```# over 2000 female farmers are married, a little to 2000 males are married , thera are more sinle male farmers than female farmers , 
sns.countplot(x ='Marital Status'  , data = farmer_data, palette = 'icefire').legend(bbox_to_anchor= (1.2,1))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/marital_status.png)
No handles with labels found to put in legend.
Out[31]:
<matplotlib.legend.Legend at 0x1337f410>

In [32]:
# over 2000 female farmers are married, a little to 2000 males are married , thera are more sinle male farmers than female farmers , 
```sns.countplot(x ='Gender' ,hue='Marital Status'  , data = farmer_data ).legend(bbox_to_anchor= (1.2,1))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/gender_marital_status.png)
Out[32]:
<matplotlib.legend.Legend at 0x132ed210>

In [33]:
 ```plt.figure(figsize = (10,4))
sns.histplot( farmer_data, x= 'Indicate Number of children' ,hue = 'Gender'  ,bins = 20 )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/children_given_gender.png)
Out[33]:
<AxesSubplot:xlabel='Indicate Number of children', ylabel='Count'>

In [34]:
```sns.histplot(farmer_data, x= 'Household size' ,hue = 'Gender')
plt.figure(figsize=(15,4))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/household_gender.png)
Out[34]:
<Figure size 1080x288 with 0 Axes>

<Figure size 1080x288 with 0 Axes>
In [35]:
```sns.countplot( x= 'What is your highest level of education', data = farmer_data ,palette= 'colorblind')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/highest level of education.png)
<AxesSubplot:xlabel='What is your highest level of education', ylabel='count'>

In [36]:
```sns.countplot( x= 'What is your highest level of education',hue = 'What is your main source of income?', data = farmer_data )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/highest_level_ofedu_main_source_of_income.png)
<AxesSubplot:xlabel='What is your highest level of education', ylabel='count'>

```plt.figure( figsize = (15,8))
sns.countplot(x= "Farmer's Language"  ,data = farmer_data , palette='rocket')
plt.legend()```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farmer's language.png)

In [37]:

```plt.figure( figsize = (15,8))

sns.countplot(x= "Farmer's Language"  , hue = 'Gender',data = farmer_data , palette='rocket')
plt.legend()```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farmer's_language_gender.png)

Out[37]:highest level of education
<matplotlib.legend.Legend at 0x132dde90>

In [38]:
sns.histplot(x='Years of farming experience?'  ,kde = True, data =farmer_data)
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Yeas of farming experience.png)

<AxesSubplot:xlabel='Years of farming experience?', ylabel='Count'>

In [39]:
```plt.figure(figsize = (10,4))
sns.lineplot(x='Age',y = 'Years of farming experience?',data = farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/age_years_of_farming experience.png)

<AxesSubplot:xlabel='Age', ylabel='Years of farming experience?'>

In [40]:
```plt.figure(figsize=(10,4))
sns.lineplot(x='Age' , y= 'Years of farming experience?' , hue='Gender',data = farmer_data).legend(bbox_to_anchor= (1.2,1))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Age_Years_of_farming_experience_Gender.png)

<matplotlib.legend.Legend at 0x155d7d90>

In [41]:
# Graph of years of experience and annual crop yield estimate(bag)
```plt.figure(figsize = (10,4))
sns.lineplot(x= 'Years of farming experience?',y= 'What is your annual primary crop  yield estimate (bags)?',data = farmer_data, palette = 'viridis')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/years_annual_bags.png)```

<AxesSubplot:xlabel='Years of farming experience?', ylabel='What is your annual primary crop  yield estimate (bags)?'>

In [42]:
plt.figure(figsize = (10,4))
```sns.lineplot(x = 'Years of farming experience?',y= 'Primary crop grown (Highest income-generating crop)',data = farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/primary_years _of farming experience.png)

<AxesSubplot:xlabel='Years of farming experience?', ylabel='Primary crop grown (Highest income-generating crop)'>

In [43]:
```sns.lineplot(x = 'Age' ,y= 'What is your annual primary crop  yield estimate (bags)?',hue='Gender' ,data = farmer_data )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/annual_crop_yield_gender.png)

<AxesSubplot:xlabel='Age', ylabel='What is your annual primary crop  yield estimate (bags)?'>

In [44]:
```plt.figure(figsize = (10,4))
sns.countplot(x='What is your main source of income?' , data =farmer_data ,palette = 'mako')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/main_soruce of income.png)

<AxesSubplot:xlabel='What is your main source of income?', ylabel='count'>

In [45]:
```plt.figure(figsize = (10,4))
sns.countplot(x='What is your main source of income?' ,hue = 'Gender', data =farmer_data ,palette = 'mako')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/mainsource_of_income_gender.png)

<AxesSubplot:xlabel='What is your main source of income?', ylabel='count'>

In [46]:
```plt.figure(figsize = (12,5))

sns.countplot(x='Secondary source of income?' , data =farmer_data , palette='rocket_r')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/secondary_source_of_income.png)

<AxesSubplot:xlabel='Secondary source of income?', ylabel='count'>

In [47]:
plt.figure(figsize = (12,5))

```sns.countplot(x='Secondary source of income?',hue = 'Gender' , data =farmer_data , palette='rocket_r')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/secondary_source_of_income_gender.png)

<AxesSubplot:xlabel='Secondary source of income?', ylabel='count'>

In [48]:
```sns.lineplot(x = 'Age' ,y= 'What is your annual primary crop  yield estimate (bags)?' ,data = farmer_data )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/age_annual_bag.png)

<AxesSubplot:xlabel='Age', ylabel='What is your annual primary crop  yield estimate (bags)?'>

In [49]:
```plt.figure(figsize = (15,8))
sns.countplot( x= 'Primary crop grown (Highest income-generating crop)' ,data = farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/maize_highestcrop_grown.png)

<AxesSubplot:xlabel='Primary crop grown (Highest income-generating crop)', ylabel='count'>

In [50]:
```plt.figure(figsize = (15,8))
sns.countplot( hue= 'Primary crop grown (Highest income-generating crop)',x = 'Gender',data = farmer_data).legend(bbox_to_anchor= (1.2,1))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/primary_generating cro_gender.png)

<matplotlib.legend.Legend at 0x1534caf0>

In [51]:
 ```sns.countplot(x='Do you keep livestock?' , data =farmer_data, palette = 'RdBu_r')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/keep_livestock.png)
 

<AxesSubplot:xlabel='Do you keep livestock?', ylabel='count'>

In [52]:
```sns.countplot(x='Do you keep livestock?' ,hue='Gender', data =farmer_data, palette = 'RdBu_r')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/keep_livestock_gender.png)

<AxesSubplot:xlabel='Do you keep livestock?', ylabel='count'>

In [53]:
1#Graph of secondary source of income and Keeping livestock
```plt.figure(figsize = (10,4))
sns.lineplot(y= 'Do you keep livestock?',x= 'Secondary source of income?',data = farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/livestock_secondaryof_income_source.png)

<AxesSubplot:xlabel='Secondary source of income?', ylabel='Do you keep livestock?'>

In [54]:
```sns.histplot(x='Years of farming experience?'  ,kde = True, data =farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farmownership_years_of_experience.png)


<AxesSubplot:xlabel='Years of farming experience?', ylabel='Count'>

In [55]:
```plt.figure(figsize = (10,6))
sns.barplot(x='Farm ownership status?',y = 'Years of farming experience?' ,hue = 'Gender', ci = False, data =farmer_data ,palette = 'crest_r')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farmownership_years_of_experience_gender.png)

<AxesSubplot:xlabel='Farm ownership status?', ylabel='Years of farming experience?'>

In [56]:
```plt.figure(figsize=(18,8))
sns.lineplot( data = farmer_data ,y= 'What is the farm size of your primary crop in acres?' ,x='Primary crop grown (Highest income-generating crop)' )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farm_sizeland_farm_sice_pcrop.png)

<AxesSubplot:xlabel='Primary crop grown (Highest income-generating crop)', ylabel='What is the farm size of your primary crop in acres?'>

In [57]:
```plt.figure(figsize=(18,8))
sns.set(font_scale = 0.8)
sns.lineplot( data = farmer_data ,y= 'What is the farm size of your primary crop in acres?' ,x='Primary crop grown (Highest income-generating crop)' ,hue= 'Gender' )```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farm_size_primarycrops_grown_acres_primary_(highest)_income generating.png)

<AxesSubplot:xlabel='Primary crop grown (Highest income-generating crop)', ylabel='What is the farm size of your primary crop in acres?'>

In [58]:
```sns.histplot(x='What is your annual primary crop  yield estimate (bags)?' , data =farmer_data, bins = 10)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/annual_crop_yield_estimate_bags.png)

<AxesSubplot:xlabel='What is your annual primary crop  yield estimate (bags)?', ylabel='Count'>

In [59]:
#Count number of each categorical value in a specified column
```#Maize is the highest secondary crop grown, followed by Groundnut and RIce,Soyabean,Chilli Pepper among others
farmer_data['Secondary crop(s) grown'].value_counts()
Out[59]:
Maize                                                                         1945
Groundnut                                                                      229
Rice                                                                           207
Soybean                                                                        121
Chilli Pepper                                                                  101
                                                                              ... 
Tomato, Vegetables, Chilli Pepper                                                1
Millet, Tomato, Onion, Vegetables                                                1
Beans, Maize, Millet, Tomato, Vegetables                                         1
Soybean, Rice, Maize, Millet, Beans, Onion, Vegetables, Cabbage, Groundnut       1
Beans, Cassava, Yam                                                              1
Name: Secondary crop(s) grown, Length: 674, dtype: int64```python
In [72]:

```#Number of Farmers in the various Farmer Group/ Association/ Agribusiness
farmer_data['Name of Farmer Group/ Association/ Agribusiness'].value_counts()
Out[72]:
Gubkatimali          2128
ms bonsu               37
gubkatimal             31
Kpammaga farmers       30
Suglo n bori buni      30
                     ... 
KANWURO VSLA            1
Nulanfo                 1
gub katimal             1
nigeen                  1
Mansumsim               1
Name: Name of Farmer Group/ Association/ Agribusiness, Length: 892, dtype: int64```python
In [60]:

```sns.countplot(x='Do you grow a secondary crop?' , data =farmer_data, palette='cubehelix')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/do_you-grow_secondary_crop.png)

<AxesSubplot:xlabel='Do you grow a secondary crop?', ylabel='count'>

In [61]:
```sns.countplot(x='Do you grow a secondary crop?' ,hue = 'Gender', data =farmer_data, palette='cubehelix')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Do_you_grow_secondary_plots_gender.png)

<AxesSubplot:xlabel='Do you grow a secondary crop?', ylabel='count'>

In [62]:
```farmer_data['What is the farm size of your secondary crop in acres?'].hist(bins = 10, figsize =(10,4))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farm_size_of_secondary_crop.png)

<AxesSubplot:>

In [63]:
```sns.countplot(x='Are your secondary crops mixed with the primary crop in one farm?' , data =farmer_data , palette = 'dark:salmon_r')```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Are_your secondary_crops mixed_with primary_crops.png)

<AxesSubplot:xlabel='Are your secondary crops mixed with the primary crop in one farm?', ylabel='count'>

In [64]:
```sns.lineplot( x = 'What is the farm size of your primary crop in acres?', y='What is the farm size of your secondary crop in acres?', data = farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/farm_size_pri_sec.png)

<AxesSubplot:xlabel='What is the farm size of your primary crop in acres?', ylabel='What is the farm size of your secondary crop in acres?'>

In [65]:
```sns.countplot(x='Do you belong to a farmer group?' , data =farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/Belong_to farmer_group.png)

<AxesSubplot:xlabel='Do you belong to a farmer group?', ylabel='count'>

In [69]:
```sns.countplot( x='Is it a feature phone (yam phone) or a smartphone?',hue = 'Gender',data = farmer_data).legend(bbox_to_anchor= (1.2,1))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/feature_yam.png)

<matplotlib.legend.Legend at 0x1cbeaa90>

In [66]:
```sns.countplot(x='Do you own a mobile phone?' ,hue = 'Which mobile network have you primarily registered for Mobile Money?', data =farmer_data).legend(bbox_to_anchor= (1.2,1))```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/mobile_phone_mtn.png)

<matplotlib.legend.Legend at 0x1bc8daf0>

In [67]:
```sns.countplot(x='Which mobile network have you primarily registered for Mobile Money?' , data =farmer_data)```python
![image](https://github.com/ellakumi/Data-Analysis-Farmers/blob/main/which_mobile_network.png)

<AxesSubplot:xlabel='Which mobile network have you primarily registered for Mobile Money?', ylabel='count'>
