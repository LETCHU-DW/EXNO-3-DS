## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:

import pandas as pd 
d=pd.read_csv("encoding data.csv")
df=pd.DataFrame(d)
print(df)

<img width="422" height="248" alt="image" src="https://github.com/user-attachments/assets/52f65499-ed2e-407e-82f3-7a3db9507fae" />


df.isna()

<img width="369" height="365" alt="image" src="https://github.com/user-attachments/assets/d92da6bc-51f1-447b-aa7a-b11d030cda06" />


df

<img width="393" height="373" alt="image" src="https://github.com/user-attachments/assets/62ce5538-3693-4b60-9f6a-0db91ef56930" />


from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])

<img width="255" height="236" alt="image" src="https://github.com/user-attachments/assets/7e0d9108-3968-4f52-97e5-b0480832dc4f" />


df['bo2']=e1.fit_transform(df[["ord_2"]])
df

<img width="397" height="370" alt="image" src="https://github.com/user-attachments/assets/fbdb0b3a-19e3-4e1b-ba0f-f3ba6714a709" />


le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc

<img width="370" height="370" alt="image" src="https://github.com/user-attachments/assets/e4673b93-c4a1-4440-8f6d-67f360ff347b" />


from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse=False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[['nom_0']]))
enc

<img width="218" height="372" alt="image" src="https://github.com/user-attachments/assets/b9c34a1c-493a-423b-99a5-49123b03a20b" />


df2=pd.concat([df2,enc],axis=1)
df2

<img width="528" height="370" alt="image" src="https://github.com/user-attachments/assets/7a05af0d-b801-4aaa-8f6d-93f859a2baed" />


pd.get_dummies(df2,columns=["nom_0"])

<img width="788" height="374" alt="image" src="https://github.com/user-attachments/assets/5bddd590-b345-4722-bd34-00d8c03b7c9f" />


from category_encoders import BinaryEncoder
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv("data.csv")
df

<img width="563" height="382" alt="image" src="https://github.com/user-attachments/assets/c4f80c85-65d8-41af-a70e-0a81c4974747" />


be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb1=df.copy()
dfb

<img width="770" height="372" alt="image" src="https://github.com/user-attachments/assets/b2e841ec-ce41-4947-9e54-1cb26cd74725" />


from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc

<img width="610" height="384" alt="image" src="https://github.com/user-attachments/assets/b8fd4cf9-262d-4567-ba82-aee4c1e10356" />


import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv("data_to_transform.csv")
df

<img width="831" height="448" alt="image" src="https://github.com/user-attachments/assets/54102f26-c219-401b-aff1-fb472c2c6386" />


df.skew()

<img width="394" height="128" alt="image" src="https://github.com/user-attachments/assets/2deacda5-b615-4629-b5ec-3f3a03a4b43c" />


np.log(df["Highly Positive Skew"])

<img width="639" height="276" alt="image" src="https://github.com/user-attachments/assets/ed29a920-cd73-4605-8ea9-f68d5e1f94ca" />


np.reciprocal(df["Moderate Positive Skew"])

<img width="645" height="274" alt="image" src="https://github.com/user-attachments/assets/8e0e54af-adba-42bc-8a6a-0060c5933c3e" />


np.sqrt(df["Highly Positive Skew"])

<img width="630" height="277" alt="image" src="https://github.com/user-attachments/assets/7f6eb798-1f8b-4ef4-97b5-7d313f2b5c08" />


np.square(df["Highly Positive Skew"])

<img width="665" height="277" alt="image" src="https://github.com/user-attachments/assets/cdf4e384-152c-4e6e-b107-3acd68e3d30b" />


df["Highly Positive Skew_boxcox"],parameters=stats.boxcox(df["Highly Positive Skew"])
df

<img width="1060" height="449" alt="image" src="https://github.com/user-attachments/assets/32260aa1-c671-4989-9869-f240d340da78" />


df["Moderate Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Moderate Negative Skew"])
df

<img width="1253" height="466" alt="image" src="https://github.com/user-attachments/assets/8c4a36dc-fe2d-4fbd-8061-1b84a85af25a" />


df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
df

<img width="1249" height="472" alt="image" src="https://github.com/user-attachments/assets/899957a1-58ee-4424-b6d7-47bb2b16951e" />


from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal')
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
df

<img width="1247" height="486" alt="image" src="https://github.com/user-attachments/assets/ef326e6f-a2cd-44e7-8a02-d2f24e977750" />


import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()

<img width="819" height="547" alt="image" src="https://github.com/user-attachments/assets/6ce820dd-8342-47b7-82dc-bf28db173208" />


sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()

<img width="856" height="550" alt="image" src="https://github.com/user-attachments/assets/20c1bc0c-11fa-44c4-b87f-95adda79da83" />


from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()

<img width="886" height="553" alt="image" src="https://github.com/user-attachments/assets/cd37827d-36be-4e86-8d09-65904d5fc0cb" />


df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line='45')
plt.show()

<img width="810" height="546" alt="image" src="https://github.com/user-attachments/assets/fa56493e-50fe-47e1-bd56-a1b080f5e87d" />


sm.qqplot(df["Highly Negative Skew_1"],line='45')
plt.show()

<img width="850" height="537" alt="image" src="https://github.com/user-attachments/assets/cacc333d-f27a-4487-aa99-f0d2d5044af5" />


dt=pd.read_csv("titanic_dataset.csv")
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
dt["Age_1"]=qt.fit_transform(dt[["Age"]])
sm.qqplot(dt['Age'],line='45')
plt.show()

<img width="823" height="540" alt="image" src="https://github.com/user-attachments/assets/9e38dd07-0c2a-4b76-8c14-50bd1611905c" />

```
sm.qqplot(dt['Age_1'],line='45')
plt.show()
```
<img width="837" height="537" alt="image" src="https://github.com/user-attachments/assets/f8e3ffa6-464b-4dbe-ad5c-eeb9c65880ae" />

     
# RESULT:
     The above code is excuted successfully
       
