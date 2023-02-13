![Banner_Visualización&Storytelling.png](Banner_Visualización&Storytelling.png)

## Dashboard 2: visualización y documentación para narrar a un equipo de trabajo
### Modelar los datos 

En el notebook, se realizarán los siguientes pasos de modelado: 

1. Extraer la base de datos “Ask A Manager Salary Survey 2021” de AskAManager.org (https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792)  

2. Limpiar los campos de “Country” y “City” para homogenizar los nombres de los lugares. 

3. Crear 2 campos nuevos: “salario_anual” y “compensaciones” convirtiendo sueldos y compensaciones a Pesos Colombianos basados en la tasa de cambio del día que hacen el ejercicio. 

4. Crear un campo adicional sumando salario anual y compensaciones en pesos colombianos.  

### Librerías a importar

A continuación, se muestran las librerias a importar para poder implementar los procedimientos de este notebook:


```python
import pandas as pd
from dataprep.clean import clean_country
import warnings
from fuzzywuzzy import process, fuzz
import numpy as np
```

### 1. Importar la base de datos

Se emplea la libreria de pandas para importar el archivo de datos a la sesión de trabajo.


```python
df = pd.read_csv("Ask A Manager Salary Survey 2021 (Responses) - Form Responses 1.csv", thousands=',')
```


```python
#Tamaño del dataset
print(f"Número de observaciones en la base de datos: {df.shape[0]}")
print(f"Número de columnas en la base de datos: {df.shape[1]}")
```

    Número de observaciones en la base de datos: 27936
    Número de columnas en la base de datos: 18
    

#### Renombrar las columnas del dataset


```python
# Old column names
old_col_names = df.columns.values

# New column names
new_col_names = ['timestamp', 'age_range','industry','job_title','additional_context_job','annual_salary','additional_monetary_compensation','currency','other_currency','additional_context_income','country','state_US','city','years_work_experience','years_work_experience_field','level_education','gender','race']

# Create a dictionary mapping old column names to new column names
col_name_map = {old: new for old, new in zip(old_col_names, new_col_names)}

# Use the rename method to update the column names
df.rename(columns=col_name_map, inplace=True)

# Verify that the columns have been renamed
print(df.columns)
```

    Index(['timestamp', 'age_range', 'industry', 'job_title',
           'additional_context_job', 'annual_salary',
           'additional_monetary_compensation', 'currency', 'other_currency',
           'additional_context_income', 'country', 'state_US', 'city',
           'years_work_experience', 'years_work_experience_field',
           'level_education', 'gender', 'race'],
          dtype='object')
    

### 2. Limpieza de los campos geográficos 

A continuación, se realiza la limpieza de los campos de “Country” y “City” para homogenizar los nombres de los lugares.

Primero, se realiza la limpieza del campo **country**. Se tiene en cuenta la función *clean_country* del paquete *dataprep* para la estandarización del campo mencionado pues la función limpia una columna que contiene nombres de países y/o códigos de país ISO 3166, y los normaliza en el formato deseado. Sin embargo, hay nombres de paises que no son resultos por la función pues tienen errores de escritura. De esta manera, se realiza una limpieza manual usando un diccionario con solo los textos faltantes. 


```python
country_dict = {'UK': 'U.K.', 'Scotland ': 'U.K.', 'England': 'U.K.','ENGLAND': 'U.K.', 'England ': 'U.K.', 'Scotland': 'U.K.', 'Uk': 'U.K.', 'England/UK': 'U.K.',
                'U.S>': 'USA', 'ISA': 'USA', 'United State': 'USA', 'America': 'USA', 'United State of America': 'USA', 'United Statws': 'USA', 'U.S': 'USA',
                'Unites States': 'USA', 'U. S. ': 'USA', 'United Sates': 'USA', 'Uniited States': 'USA', 'United Sates of America': 'USA',  'Unted States': 'USA',
                'United Stattes': 'USA', 'United Statea': 'USA', 'United Statea': 'USA', 'Unites States': 'USA', 'United Statees': 'USA', 'Uniyed states': 'USA', 
                'Uniyes States': 'USA', 'U.A.': 'USA', 'U. S.': 'USA', ' US of A': 'USA', 'United Kindom': 'U.K.', 'United Status': 'USA', 'Uniteed States': 'USA',
                'United Stares': 'USA', 'United Stares': 'USA', 'Unites states ': 'USA', 'The US': 'USA', 'UnitedStates': 'USA', 'United statew': 'USA',
                'United Statues': 'USA', 'United Statues': 'USA', 'Untied States': 'USA',  'Unitied States': 'USA', ' United Sttes': 'USA',
                'united stated': 'USA', ' Uniter Statez': 'USA', 'U. S ': 'USA', 'United Stateds': 'USA', 'Unitef Stated': 'USA',
                'United Stares ': 'USA', 'USaa': 'USA', 'america': 'USA', 'United Statss': 'USA', 'United  States': 'USA','United Stated	': 'USA','Northern Ireland	': "Ireland"}

df['country'] = df['country'].map(country_dict).fillna(df['country'])

```


```python
# Ignore all warnings
warnings.filterwarnings("ignore")
df = clean_country(df, 'country', output_format= "name")
```


      0%|                                                                                            | 0/8 [00:00<…


    Country Cleaning Report:
    	15489 values cleaned (55.44%)
    	133 values unable to be parsed (0.48%), set to NaN
    Result contains 27803 (99.52%) values in the correct format and 133 null values (0.48%)
    

Cabe mencionar que el diccionario solo cuenta con los nombres de los paises que no son posibles de traducir por la función. Lo anterior, nos apoya en el proceso de limpieza pues no es necesario realizar una limpieza manual a muchos registros sino solo aquellos que la función no leyo. Hay de los registros originales de la base de datos solo un 0.48% (133 registros) no fueron estandarizados.

Finalemente, se crea una nueva variable **Country_clean** con los países estandarizados.


```python
df_clean = df
```

Ahora, se realiza la limpieza del campo **city**. Primero, se eliminar las filas que presenten ciudades en valores faltantes. Luego, se revisan y organizan las ciudades en una lista para aplicar la métrica de similitud de textos del paquete *fuzzywuzzy*.


```python
df_cities = df_clean["city"].tolist()
df_cities = [str(x) for x in df_cities]
```


```python
def remove_spaces(strings):
    return [string.strip() for string in strings]
city_no_spaces = remove_spaces(df_cities)
```


```python
def get_unique_values(lst):
    return list(set(lst))
unique_cities = get_unique_values(city_no_spaces)
sorted_unique_cities = sorted(unique_cities)
```


```python
len(sorted_unique_cities)
```




    4216




```python
score_sort = [(x,) + i
             for x in sorted_unique_cities
             for i in process.extract(x, sorted_unique_cities, scorer=fuzz.token_set_ratio)]
#Create a dataframe from the tuples
similarity_sort = pd.DataFrame(score_sort, columns=['city_sort','match_sort','score_sort'])
```

    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '-']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '--']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '---']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '-----']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '.']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '..']
    Applied processor reduces input query to empty string, all comparisons will have score 0. [Query: '/']
    


```python
similarity_sort['sorted_city_sort'] = np.minimum(similarity_sort['city_sort'], similarity_sort['match_sort'])
```


```python
high_score_sort = similarity_sort[(similarity_sort['score_sort'] >= 98) &
                (similarity_sort['city_sort'] !=  similarity_sort['match_sort']) &
                (similarity_sort['sorted_city_sort'] != similarity_sort['match_sort'])]
high_score_sort = high_score_sort.drop('sorted_city_sort',axis=1).copy()
```


```python
for index, row in df_clean.iterrows():
  c = high_score_sort[high_score_sort['match_sort'] == row['city']]
  if c.empty == False:
    df_clean.loc[index, 'city_clean'] = c.iloc[0]['city_sort']
  else:
    df_clean.loc[index, 'city_clean'] = row['city']
     
```


```python
# se reduce la cantidad de valores unicos de la columna City
len(df_clean['city_clean'].unique().tolist())
```




    3728



Aplicando la métrica de similitud de textos, logramos disminuir la cantidad de países únicos en aproximadamente 500. Finalmente, se crea un nuevo campo llamado *city_clean* donde estan las ciudades estandarizadas.

### 3. Crear campos nuevos: “salario_anual” y “compensaciones” 

Para crear los campos mencionados, se tuvo en cuenta la conversión de sueldos y compensaciones a Pesos Colombianos basados en la tasa de cambio del día 12/02/2023. 



```python
#Se revisan las divisas que aparecen
def get_unique_values_of_column(df, column_name):
    column = df[column_name].tolist()
    return list(set(column))
unique_currency = get_unique_values_of_column(df_clean,"currency")
unique_currency
```




    ['SEK',
     'CAD',
     'JPY',
     'Other',
     'CHF',
     'AUD/NZD',
     'USD',
     'HKD',
     'ZAR',
     'EUR',
     'GBP']




```python
# tipo de cambio obtenido el 12/02/2023 por https://www.xe.com/currencyconverter/
currency_dict = {'USD': 4803.71, 'AUD/NZD': 3020.89, 'GBP': 5782.32, 'CHF': 5187.04,'HKD': 611.47,'EUR': 5119.48,'SEK': 457.31, 'CAD': 3586.98, 'Other': 4803.71,  
                 'ZAR': 267.51,  'JPY': 36.40}
```


```python
# convertir a pesos colombianos
df_clean['salario_anual'] = df_clean.apply(lambda row: row['annual_salary']*currency_dict[row['currency']], axis=1)
df_clean['compensaciones'] = df_clean.apply(lambda row: row['additional_monetary_compensation']*currency_dict[row['currency']], axis=1)
```

### 4. Crear un campo adicional del salario total en pesos colombianos 

A continuación, se crea el campo adicional sumando salario anual y compensaciones en pesos colombianos.


```python
df_clean['ingreso_total'] = df_clean.apply(lambda row:  row['salario_anual'] + row['compensaciones'] if ~np.isnan(row['compensaciones']) else row['salario_anual'], axis=1)
```

### Guardar archivo con el modelamiento de los datos


```python
df_clean.to_excel("V&S_Encuestas_clean.xlsx", index=False, encoding="UTF-8")
```
