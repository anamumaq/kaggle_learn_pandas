# Resumen Pandas

# Creating, Reading and Writing

## ****Getting started****

- Para iniciar con pandas se debe llamar a la librería de pandas
    
    ```python
    import pandas as pd
    ```
    

## ****Creating data****

### Creando dataframe

El dataframe es una tabla de valores 

- Genera un index desde cero por default
    
    ```python
    pd.DataFrame({'columna_1':[1,2,3], 'columna_2':['a','b','c']})
    ```
    
    | index | columna_1 | columna_2 |
    | --- | --- | --- |
    | 0 | 1 | a |
    | 1 | 2 | b |
    | 2 | 3 | c |
- Puedo definir el nombre de mis index
    
    ```python
    pd.DataFrame(
        {'columna_1':[1,2,3], 'columna_2':['a','b','c']},
        # index=range(3,6) con una lista de range
        index=['a1','a2','a3']
        )
    ```
    
    | index | columna_1 | columna_2 |
    | --- | --- | --- |
    | a1 | 1 | a |
    | a2 | 2 | b |
    | a3 | 3 | c |
- Es necesario que sea del mismo tamaño o genera error
    
    ```python
    pd.DataFrame({'columna_1':[1,2,3,4], 'columna_2':['a','b','c']})
    ```
    
    ![Untitled](Resumen%20Pandas%20ffb107c541174d61b958b75b7c3427a7/Untitled.png)
    

### Creando series

Si el dataframe es como una tabla de valores, las series son una secuencia de valores de datos, es una lista de valores.

- Generando una serie desde una lista con un index por default
    
    ```python
    pd.Series([1,2,3,4,5,6,7,8,9,10])
    pd.Series(range(4))
    ```
    
    > 0    0
    1    1
    2    2
    3    3
    dtype: int64
    > 
- Una serie con un index definido
    
    ```python
    pd.Series(range(1,4), index=['primero', 'segundo', 'tercero'])
    ```
    
    > primero    1
    segundo    2
    tercero    3
    dtype: int64
    > 
- Una serie definiendo el nombre
    
    ```python
    pd.Series(range(1,4),
              index=['primero', 'segundo', 'tercero'],
              name='lista')
    ```
    
    > primero    1
    segundo    2
    tercero    3
    Name: lista, dtype: int64
    > 

## Reading data files

### Lectura y escritura

- El archivo mas común de leer es el .csv, este podemos almacenarlo en una variable llamada df
    
    ```python
    df = pd.read_csv('/content/sample_data/california_housing_test.csv')
    ```
    
- Otro archivo común puede ser los. xlsx
    
    ```python
    df = pd.read_excel('/content/sample_data/california_housing.xlsx',
    										sheet_name='Hoja 2')
    ```
    
- Podria definir la columna index para el dataframe
    
    ```python
    df_0 = pd.read_csv('/content/sample_data/california_housing_test.csv',
                     index_col=0 # la columna 0 sea la columna indice
                     )
    ```
    
- Asi como leo un dataframe tambien puedo guardarlo
    
    ```python
    df.to_csv('nuevo_archivo.csv') 
    ```
    

### Conociendo el dataframe

- Puedo consultar el tamano del dataframe para darme una idea de como esta estructurado, numero de filas y columnas
    
    ```python
    df.shape
    ```
    
    > (3000, 9)
    > 
- Tambien puedo hacer otras consultas de las primeras filas, ultimas filas e incluso una muestra del dataframe
    
    ```python
    # las primeras 5 filas
    df.head()
    
    # las ultimas 5 filas
    df.tail()
    
    # una fila random
    df.sample(5)
    ```
    

# Indexing, Selecting & Assigning

## Indexing

- Puedo acceder a las columnas de mi dataframe de la siguiente manera
    
    ```python
    df.total_bedrooms
    df['total_bedrooms']
    ```
    
    > 0        661.0
    1        310.0
    2        507.0
    3         15.0
    4        244.0
    ... 2995     642.0
    2996    1082.0
    2997     201.0
    2998      14.0
    2999     263.0
    Name: total_bedrooms, Length: 3000, dtype: float64
    > 
- Acceder a una fila especifica de la columna
    
    ```python
    df['total_bedrooms'][0]
    ```
    
    > 661.0
    > 
- Acceder a todas las columnas de la primera fila
    
    ```python
    df.iloc[0]
    ```
    
    > longitude               -122.0500
    latitude                  37.3700
    housing_median_age        27.0000
    total_rooms             3885.0000
    total_bedrooms           661.0000
    population              1537.0000
    households               606.0000
    median_income              6.6085
    median_house_value    344700.0000
    Name: 0, dtype: float64
    > 
- Accediendo a todas las filas de la columna 0
    
    ```python
    df.iloc[:, 0]
    ```
    
    > 0      -122.05
    1      -118.30
    2      -117.81
    3      -118.36
    4      -119.67
    …2995   -119.86
    2996   -118.14
    2997   -119.70
    2998   -117.12
    2999   -119.63
    Name: longitude, Length: 3000, dtype: float64
    > 
- Tres primera filas de la columna cero
    
    ```python
    df.iloc[:3, 0]
    df.iloc[[0,1,2], 0]
    ```
    
    > 0   -122.05
    1   -118.30
    2   -117.81
    Name: longitude, dtype: float64
    > 
- Tres ultimas filas de la columna cero
    
    ```python
    df.iloc[-3:, 0]
    ```
    
    > 2997   -119.70
    2998   -117.12
    2999   -119.63
    Name: longitude, dtype: float64
    > 
- Tambien puedo usar la fila y el nombre de la columna con **loc**
    
    ```python
    df.loc[0, 'total_bedrooms']
    df['total_bedrooms'][0] #lo mismo
    ```
    
    > 661.0
    > 
- Seleccionar varias filas de algunas columnas y las puedo limitar con head()
    
    ```python
    df.loc[:, ['total_bedrooms', 'total_rooms']].head()
    ```
    
    | index | total_bedrooms | total_rooms |
    | --- | --- | --- |
    | 0 | 661.0 | 3885.0 |
    | 1 | 310.0 | 1510.0 |
    | 2 | 507.0 | 3589.0 |
    | 3 | 15.0 | 67.0 |
    | 4 | 244.0 | 1241.0 |
- Puedo redefinir el index del dataframe
    
    ```python
    df.set_index('longitude')
    ```
    

## Filtrando

- Aplicando filtro con loc, filtra solo los bedrooms con valor igual a 661
    
    ```python
    df.loc[df['total_bedrooms']==661]
    ```
    
- Generando una filtro con dos condicionales
    
    ```python
    df.loc[(df['total_bedrooms']<=700) & #and
           (df['total_bedrooms']>=300)]
    
    df.loc[(df['total_bedrooms']==700) | # or
           (df['total_bedrooms']==300)]
    ```
    
- Filtro simple como prefiero hacerlo (mayor orden y simpleza)
    
    ```python
    df.query('total_bedrooms == 661')
    ```
    
- Filtro con valores de una lista
    
    ```python
    df.loc[df['total_rooms'].isin([100,200,300,400,500,600])]
    ```
    
- Entrar valores nulos o vacios dentro del dataframe
    
    ```python
    # Encontrando valores nulos
    df.loc[df['total_bedrooms'].isnull()]
    # Encontrando valores NO nulos
    df.loc[df['total_bedrooms'].notnull()]
    ```
    

## Asignando

- Creando una nueva columna
    
    ```python
    # agregabdo una nueva olumna con un nuevo valor
    df['nueva_columna'] = 'valores nuevos'
    df.head()
    ```
    
- Creando una nueva columna como un índice invertido
    
    ```python
    df['indice_2'] = range(len(df),0,-1)
    df.head()
    ```
    

# Summary Functions and Maps

## Funciones resumen

- Resumen estadistico
    
    ```python
    df['total_rooms'].describe()
    ```
    
    > count     3000.000000
    mean      2599.578667
    std       2155.593332
    min          6.000000
    25%       1401.000000
    50%       2106.000000
    75%       3129.000000
    max      30450.000000
    Name: total_rooms, dtype: float64
    > 
- Valores promedio, media
    
    ```python
    df['total_rooms'].mean()
    df['total_rooms'].median()
    ```
    
- Valores únicos de una variable
    
    ```python
    df['total_rooms'].unique()
    ```
    
- Contando valores en una variable y ordenándolos según su frecuencia de forma descendente
    
    ```python
    df['total_rooms'].value_counts().sort_values(ascending=False)
    ```
    

## Mapping

- Promedio de una variable. Hallando la diferencia de rooms menos rooms promedio
    
    ```python
    total_rooms_mean=df['total_rooms'].mean()
    
    df['total_rooms'].map(
        lambda d: d - total_rooms_mean)
    
    # otra forma sin map
    
    df['total_rooms']-df['total_rooms'].mean()
    ```
    

# Grouping and Sorting

- Agrupar y contar la frecuencia
    
    ```python
    df.groupby('housing_median_age')['housing_median_age'].count()
    ```
    
    > housing_median_age
    1.0       2
    2.0       6
    3.0      12
    4.0      28
    5.0      39
    6.0      25
    > 
- Agrupando con un multi index
    
    ```python
    df.groupby(by=['housing_median_age', 'total_rooms'], as_index=False)['median_income'].agg(['mean', 'min'])
    ```
    
    | housing\_median\_age | total\_rooms | mean | min |
    | --- | --- | --- | --- |
    | 1\.0 | 6\.0 | 1\.625 | 1\.625 |
    | 1\.0 | 83\.0 | 4\.875 | 4\.875 |
    | 2\.0 | 158\.0 | 2\.5625 | 2\.5625 |
    | 2\.0 | 200\.0 | 15\.0001 | 15\.0001 |
- Ordenando datos desde una columna
    
    ```python
    df.sort_values(by='housing_median_age', ascending=False)
    
    # ordenar desde el indice
    df.sort_index()
    ```
    

# Data Types and Missing Values

- Conocer el tipo de datos de todo el dataframe
    
    ```python
    df.dtypes
    
    # de una sola variable 
    df['longitude'].dtype
    ```
    
    > longitude             float64
    latitude              float64
    housing_median_age    float64
    indice_2                int64
    dtype: object
    > 
- Cambiar el tipo de una variable, de float a str
    
    ```python
    df['longitude'].astype('str')
    ```
    
- Encontrar los valores nulos (sin usar loc)
    
    ```python
    df[df['longitude'].isna()]
    ```
    
- Llenar los valores nulos, en este caso con la palabra ‘vacio’
    
    ```python
    df['longitude'].fillna('vacio')
    ```
    
- Reemplazar una valor con otro valor
    
    ```python
    df['total_bedrooms'].replace(300, 0)
    ```
    

# Renaming and Combining

## Renombrando

- Puedo renombrar columnas utilizando rename, cambiando total_rooms por total_cuartos
    
    ```python
    df.rename(columns={'total_rooms':'total_cuartos'})
    ```
    
- Tambien podria renombrar los index, poniendo como nombre zero al indice 0
    
    ```python
    df.rename(index={0:'zero', 1:'uno'})
    ```
    
- Tambien es util poder cambiar el nombre las filas y las columnas. Aqui cambio el nombre de las filas por **indices** y el nombre de las columnas por **parametros**
    
    ```python
    df.rename_axis('indices', axis='rows').rename_axis('parametros',  axis='columns')
    ```
    

## Combinando datasets

- Combinar datasets con el mismo nombre de columnas uno bajo el otro
    
    ```python
    df_1 = pd.DataFrame({'id':['a1','a2','a3','a4', 'a5'], 'sueldo':[1200, 1500, 2500, 2000, 2300]})
    df_2 = pd.DataFrame({'id':['a6','a7','a8','a9'], 'sueldo':[1200, 1500, 2500, 2000]})
    
    pd.concat([df_1, df_2])
    ```
    
- Otra forma de combinarlos es basados en un índice utilizando un join, aquí la combinación de datasets se hace como una al costado de otra
    
    ```python
    df_1 = pd.DataFrame({'id':['a1','a2','a3','a4', 'a5'], 'sueldo':[1200, 1500, 2500, 2000, 2300]})
    df_3 = pd.DataFrame({'id':['a1','a2','a3','a4'], 'edad':[23, 21, 25, 20]})
    
    df_1.join(df_3, lsuffix='_1',rsuffix='_3')
    ```