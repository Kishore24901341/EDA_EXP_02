# Exp - 2 Netflix Shows & Movies

## Aim

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

## Procedure / Algorithm

1)Load dataset (netflix_titles.csv).

2)Count movies vs TV shows.

3)Group by country → top contributors.

4)Create pivot table (release year vs type).

5)Visualize with bar & line charts.

## Program

### Load dataset directly from GitHub

```python 
import pandas as pd
import numpy as np

url="https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv"
df=pd.read_csv(url)
print("KISHORE V")
print("212224240077")

print("Shape:",df.shape)

print("Columns:",df.columns,"\n")

print("Types:",df['type'].value_counts(),"\n")
```

### Clean 'date_added' and extract year/month

```python
df['date_added']=df['date_added'].astype(str).str.strip()
df['date_added']=pd.to_datetime(df['date_added'],errors='coerce')
df['year_added']=df['date_added'].dt.year.astype('Int64')
df['month_added']=df['date_added'].dt.month_name()
print("KISHORE V")
print("212224240077")

df.head()
```
###  Movies vs TV Shows
```python
count_by_type = df.groupby('type')['title'].count()
print("KISHORE V")
print("212224240077")
print("Count by Type:\n", count_by_type, "\n")
```
###  Country vs Type Pivot Table
```python
pivot_country_type = df.pivot_table(
index='country',
columns='type',
values='title',
aggfunc='count',
fill_value=0
)
pivot_country_type['Total'] = pivot_country_type.sum(axis=1)
max_country = pivot_country_type['Total'].idxmax() 
max_count = pivot_country_type['Total'].max()
print("KISHORE V")
print("212224240077")
print("Pivot Table (Country vs Type):\n", pivot_country_type.head(), "\n")
print(f"Largest Overall: {max_country} with {max_count} titles\n")
```
### Top 5 Directors
```python
top_directors = df['director'].value_counts().head(5)
print("KISHORE V")
print("212224240077")
print("Top 5 Directors:\n", top_directors, "\n")
```

### Yearly Trend of Additions (Movies vs TV Shows)
```python
trend=df.groupby(['year_added','type']).size().unstack(fill_value=0)
print("KISHORE V")
print("212224240077")
print("Yearly Trend by Type\n")
print(trend.head())
```

### Expand Genres
``` python
df_genre = (df[['show_id','listed_in']]
.dropna()
.assign(listed_in=df['listed_in'].str.split(', '))
.explode('listed_in'))
df_expanded = df.merge(df_genre, on='show_id', how='left')
print("KISHORE V")
print("212224240077")
print("Columns after merge:\n", df_expanded.columns)
print("\nExpanded Genre Sample:\n",
df_expanded[['title','listed_in_y']].head())

top_genres = df_expanded['listed_in_y'].value_counts().head(5)
print("\nTop 5 Genres:\n", top_genres, "\n")
```
## Ouptut

### Load dataset directly from GitHub
<img width="629" height="147" alt="image" src="https://github.com/user-attachments/assets/1252fd31-27b5-4aca-a1a5-48399eb7183a" />



### Clean 'date_added' and extract year/month
<img width="918" height="472" alt="image" src="https://github.com/user-attachments/assets/d17dc9ed-36cf-494a-8307-6af713d17e99" />



###  Movies vs TV Shows
<img width="640" height="107" alt="image" src="https://github.com/user-attachments/assets/16a79902-a085-421b-a123-8726e59d1894" />



###  Country vs Type Pivot Table

<img width="690" height="197" alt="image" src="https://github.com/user-attachments/assets/8d702159-f30b-496f-903d-5968830f3c14" />




### Top 5 Directors

<img width="494" height="153" alt="image" src="https://github.com/user-attachments/assets/7ab67750-d5f0-4090-ab70-6eb127d0dadc" />



### Yearly Trend of Additions (Movies vs TV Shows)
<img width="400" height="171" alt="image" src="https://github.com/user-attachments/assets/6e194565-501c-4af1-9eeb-4bdc13b8acd9" />



### Expand Genres
<img width="947" height="544" alt="image" src="https://github.com/user-attachments/assets/39276e68-<img width="659" height="347" alt="image" src="https://github.com/user-attachments/assets/0f6f319c-913e-46db-b1e4-ffa1a01724c1" />




## Result 
Helps Netflix in content planning & investments.
