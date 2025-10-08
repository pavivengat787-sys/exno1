# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output



```python
import pandas as pd
df=pd.read_csv("SAMPLEIDS.csv")
df
```
<img width="999" height="701" alt="image" src="https://github.com/user-attachments/assets/29d2b753-83a9-451e-b418-42b7e8fe2b17" />

```python
df.shape
```
<img width="86" height="36" alt="image" src="https://github.com/user-attachments/assets/0c64a2fb-6229-48d1-8113-b3c21df02aa2" />

```python
df.describe()
```
<img width="925" height="352" alt="image" src="https://github.com/user-attachments/assets/d51ad3ff-980e-4afd-b5a3-36cd0d78b4d4" />

```python
df.info()
```
<img width="404" height="429" alt="image" src="https://github.com/user-attachments/assets/7a6bf7b1-4bcb-4d99-8c3d-010142d518d7" />

```python
df.head(5)
```
<img width="965" height="245" alt="image" src="https://github.com/user-attachments/assets/22d81327-7ad8-475b-af6e-a8fb632ef3d4" />

```python
df.tail(2)
```
<img width="974" height="124" alt="image" src="https://github.com/user-attachments/assets/698270b5-80d1-4319-a47f-2bd513401147" />

```python
df.dropna(how='any').shape
```
<img width="86" height="43" alt="image" src="https://github.com/user-attachments/assets/7afd3c23-e342-4fc5-acf0-c1d1062f5076" />

```python
df.isnull().sum()
```
<img width="174" height="560" alt="image" src="https://github.com/user-attachments/assets/10d26fb6-6a41-419d-a42e-5a69c04930e6" />

```python
mn=df.TOTAL.mean()
df.TOTAL.fillna(mn,inplace=True)
df
```
<img width="1280" height="620" alt="image" src="https://github.com/user-attachments/assets/d294611f-0cab-4a6c-b52a-385acbb253d8" />

```python
df.M1.dropna(inplace=True)
df
```
<img width="811" height="687" alt="image" src="https://github.com/user-attachments/assets/e6983b9c-8a5d-4fc5-96cd-a849411c9450" />

```python
df.isna().sum()
```
<img width="139" height="559" alt="image" src="https://github.com/user-attachments/assets/7d2b769a-f916-44f7-80d2-cc463ed5fafe" />

```python
df['M1'].fillna(method='ffill',inplace=True)
```
<img width="1280" height="157" alt="image" src="https://github.com/user-attachments/assets/a60a179b-0701-4694-a08a-8477702fbd04" />

```python
df.duplicated()
```
<img width="101" height="727" alt="image" src="https://github.com/user-attachments/assets/b29855d6-4311-4aca-947b-df57f4bb7cae" />

```python
df['DOB']
```
<img width="121" height="730" alt="image" src="https://github.com/user-attachments/assets/b2aff3a5-7a21-4047-83e3-96cc3375b3be" />

```python
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
<img width="505" height="504" alt="image" src="https://github.com/user-attachments/assets/22cf0346-8429-4b9e-adee-5f23b683cf3f" />

```python
import pandas as pd
import seaborn as sns
import numpy as np
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
<img width="70" height="468" alt="image" src="https://github.com/user-attachments/assets/ab1ea415-7422-4133-9da1-6109ffc924af" />

```python
**sns.boxplot(data=af)**
```
<img width="561" height="434" alt="image" src="https://github.com/user-attachments/assets/6c93dd09-6b32-4fd5-b28c-b4acfbb35e2c" />


```python
sns.scatterplot(data=af)
```
<img width="565" height="435" alt="image" src="https://github.com/user-attachments/assets/b312256b-3113-4ddf-ab65-b80d0b86b502" />

```python
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
<img width="111" height="119" alt="image" src="https://github.com/user-attachments/assets/13ffa760-b560-4ff0-843a-06db24730216" />

```python
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-q1
IQR
```
<img width="114" height="102" alt="image" src="https://github.com/user-attachments/assets/9fb86824-0296-474d-a151-93215406c333" />

```python
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound
```
<img width="117" height="112" alt="image" src="https://github.com/user-attachments/assets/11c7774c-643d-4673-97bc-950ccbc1cf14" />

```python
upper_bound
```
<img width="110" height="106" alt="image" src="https://github.com/user-attachments/assets/4b0c5613-ffe0-4747-9007-ca1fcce3b414" />

```python
outliers = [x for x in age if (x < lower_bound.iloc[0]) or (x > upper_bound.iloc[0])]
print("q1",q1)
print("q3",q3)
print("iqr",iqr)
print("lower bound",lower_bound)
print("upper bound",upper_bound)
print("outliers",outliers)
```
<img width="216" height="193" alt="image" src="https://github.com/user-attachments/assets/13aafa26-e6a9-4258-9a72-f466e9c02ef8" />

```python
af=af[((af>=lower_bound)&(af<=upper_bound))]
```
<img width="73" height="334" alt="image" src="https://github.com/user-attachments/assets/726462ae-9383-4a84-998a-3f48b10f0b08" />

```python
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
<img width="326" height="57" alt="image" src="https://github.com/user-attachments/assets/824f6c57-ed9b-4c48-aec5-456780dcfd1a" />

```python
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
    print('Outlier in dataset is:',outlier)
```
<img width="240" height="50" alt="image" src="https://github.com/user-attachments/assets/fb513648-d517-4d71-ac27-b0a6f82e5e86" />

```python
import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}

df=pd.DataFrame(data)
df
```
<img width="73" height="704" alt="image" src="https://github.com/user-attachments/assets/26e5fdfb-9c13-4a36-bf2e-6cf77693ce52" />

```python
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
<img width="87" height="57" alt="image" src="https://github.com/user-attachments/assets/96f21bd5-3cee-4aa0-977f-2a1155786aa8" />

```python
val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]


import numpy as np
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out

op=d_o(val)
op
```
<img width="72" height="28" alt="image" src="https://github.com/user-attachments/assets/d7d6b4ea-e48c-4543-83ae-4960309d1be0" />

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method
