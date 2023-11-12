# Ex-08-Data-Visualization-
# AIM
To Perform Data Visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
## STEP 1
Read the given Data

## STEP 2
Clean the Data Set using Data Cleaning Process

## STEP 3
Apply Feature generation and selection techniques to all the features of the data set

## STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
uploaded = files.upload()
df=pd.read_csv("SuperStore.csv",encoding='unicode_escape')
df
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/5896298f-696d-4b12-a4f0-80c9c56d477a)
```
df.isnull().sum()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/88ab4853-1610-4f52-acaf-cda47b80fbdb)
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/70e4092a-e39e-4abf-86b4-e4a82f99057f)

```
#detecting and removing outliers in current numeric data
plt.figure(figsize=(8,8))
plt.title("Data with outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/91189e71-f224-4e6b-abf6-2158ca519f5d)
```
plt.figure(figsize=(8,8))
cols = ['Sales','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/5b0612f9-4511-46d9-9f04-617258bbb40f)
## Which Segment has Highest sales?
```
sns.lineplot(x="Segment",y="Sales",data=df,marker='o')
plt.title("Segment vs Sales")
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/19bb0e5a-5262-4179-ab8b-692257020f74)
```
sns.barplot(x="Segment",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/afab2278-c292-4867-b21a-ac11d1e6c65a)
## Which City has Highest profit?
```
df.shape
df1 = df[(df.Profit >= 60)]
df1.shape
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/baf6145c-0952-41b1-8e10-f67c5e84684b)
```
plt.figure(figsize=(30,8))
states=df1.loc[:,["City","Profit"]]
states=states.groupby(by=["City"]).sum().sort_values(by="Profit")
sns.barplot(x=states.index,y="Profit",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("City")
plt.ylabel=("Profit")
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/94f50f0b-e894-43f6-927f-ff74bc1dbc5d)
## Which ship mode is profitable?
```
sns.barplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/08388592-b223-4c88-860b-369aa45e7240)
```
sns.lineplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/6f005b9a-9d99-41b0-bbb4-61c2fe7d1df3)
```
sns.violinplot(x="Profit",y="Ship Mode",data=df)
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/4170145e-d35c-4854-aaf8-5c793bf70920)
```
sns.pointplot(x=df["Profit"],y=df["Ship Mode"])
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/4407d9d9-5849-4dc0-982c-ae6478ca9971)
## Sales of the product based on region.
```
states=df.loc[:,["Region","Sales"]]
states=states.groupby(by=["Region"]).sum().sort_values(by="Sales")
sns.barplot(x=states.index,y="Sales",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("Region")
plt.ylabel=("Sales")
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/2c0014e2-ed99-4e7b-8eba-07a1ae54ba33)
```
df.groupby(['Region']).sum().plot(kind='pie', y='Sales',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/c2ccc1f4-d608-47c4-b5a7-10b151b2a798)
## Find the relation between sales and profit.
```
df["Sales"].corr(df["Profit"])
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/76eaaf31-a2da-45f8-bbea-9beebfb1eb02)
```
df_corr = df.copy()
df_corr = df_corr[["Sales","Profit"]]
df_corr.corr()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/3cc1c1a3-cbb0-44f5-bf05-fdea4f20b50f)
```
sns.pairplot(df_corr, kind="scatter")
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/8904b302-b75a-4c7f-a362-bc6d8e064be1)
## Heatmap
```
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/0a9eba2d-7711-4f07-a801-795ee2a9b042)
## Find the relation between sales and profit based on the following category.
## Segment
```
grouped_data = df.groupby('Segment')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/02fcef46-68f0-4a35-a38e-d0620195791a)
## City
```
grouped_data = df.groupby('City')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('City')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/ea631865-0641-4502-8449-43fb591853ec)
## States
```
grouped_data = df.groupby('State')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('State')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/9234dbd2-f536-497d-b1db-f11390e2ca7e)
## Segment and Ship Mode
```
grouped_data = df.groupby(['Segment', 'Ship Mode'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index='Segment', columns='Ship Mode', values=['Sales', 'Profit'])
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
pivot_data.plot(kind='bar', ax=ax)
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
plt.legend(title='Ship Mode')
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/3ef4a74d-8c40-48f1-a7f8-eabda167adb9)
## Segment, Ship mode and Region
```
grouped_data = df.groupby(['Segment', 'Ship Mode','Region'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index=['Segment', 'Ship Mode'], columns='Region', values=['Sales', 'Profit'])
sns.set_style("whitegrid")
sns.set_palette("Set1")
pivot_data.plot(kind='bar', stacked=True, figsize=(10, 5))
plt.xlabel('Segment-Ship Mode')
plt.ylabel('Value')
plt.legend(title='Region')
plt.show()
```
![image](https://github.com/Sathya-006/ODD2023-Datascience-Ex-08/assets/121661327/65ddd24a-d539-4462-af06-e4b046260338)

## RESULT:
Thus, Data Visualization is performed on the given dataset and save the data to a file.
