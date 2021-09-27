# Laboratorio  - Regresiones

## Objetivos

- Comprender el proceso asociado con la preparación de datos para una tarea de estimación.

- Construir un modelo capaz de estimar una variable objetivo continua a partir de una serie de variables observadas.

- Exportar el modelo de tal forma que pueda ser usado en ambiente de producción.

- Entender las diferentes estrategias que existen para cumplir las suposiciones de una regresión lineal.

- Extraer información útil para el negocio a partir de los coeficientes obtenidos en la regresión.


## Herramientas

- Librerías principales de Python para procesamiento y visualización de datos como: pandas, sklearn, seaborn, numpy y matplotlib.  
    Se recomienda usar la última distribución disponible de Anaconda Individual Edition, pueden encontrar el instalador en este [enlace](https://www.anaconda.com/products/individual). 

- Ambiente de desarrollo: JupyterLab en distribución de Anaconda.  

## Enunciado

### Descripción de negocio

AlpesGamesInsight es una empresa dedicada a la cobertura y análisis de diferentes competencias de video juegos profesionales. Uno de sus factores diferenciadores es el cálculo de un ranking de los diferentes jugadores por video juego. Este ranking sirve como referencia para los equipos en el momento de seleccionar jugadores para competir y para los patrocinadores quienes apoyan económicamente las carreras de los jugadores. 

Durante años esta empresa ha realizado este proceso de forma manual, basándose en grupos de expertos que asignan un **LeagueIndex** a cada uno de los jugadores profesionales. 
El equipo in house de analítica ha realizado diferentes ejercicios de estimación automática en el pasado, pero sin mucho éxito, logrando únicamente un  R<sup>2</sup> de 0.35. Es precisamente por esto que han contratado a su equipo, ya que quieren tener una opinión experta sobre la posibilidad de extraer este ranking de forma automática, usando aprendizaje supervisado. Su tarea consiste en estudiar el desempeño de un modelo de regresión para predecir la variable, evaluar su viabilidad e identificar las características que mas afectan el ranking de un jugador.

La empresa a puesto a su disposición una [base de datos histórica](data/SkillCraftHistoric.csv), con diferentes estadísticas de jugadores de StarCraf II (https://starcraft2.com/en-us/) durante varios partidos. 
El detalle de su contenido lo puede encontrar en el diccionario de datos disponible en este [enlace](data/data_dictionary.md).

Adicionalmente, separó unos [datos más recientes](data/SkillCraftRecent.csv) que tienen la misma estructura que los datos entregados, únicamente le falta la variable objetivo (**LeagueIndex**). La empresa ya tiene los rankings de estos jugadores, pero decidió no compartirlos ya que quiere evaluar personalmente el desempeño del modelo sobre datos reales.


### Instrucciones 

La empresa quiere parar de utilizar expertos para el ranking de sus jugadores y comenzar a utilizar modelos basados en aprendizaje de máquina. 
Para lo cual, su equipo debe desarrollar un modelo que permita estimar el ranking de un cierto jugador dadas sus estadísticas de juego y evaluar su desempeño, al igual que seguir los siguientes pasos para garantizar el uso de la metodología "ASUM-DM":

1. **Limpieza de los datos y preparación de datos:** en esta etapa su equipo debe identificar y solucionar cualquier problema de inconsistencia o ruido que se pueda tener en los datos. Además, deben tener en cuenta el preprocesamiento necesario para el uso de regresiones. No olvide ejecutar un esquema de manejo de variables faltantes, identificación de datos atípicos y de normalizar en caso de ser necesario.

2. **Identificación de variables a utilizar**: su equipo debe identificar las variables más relevantes que puedan utilizarse en el proceso de estimación. 

3. **Modelamiento:** a partir de las variables identificadas anteriormente, se debe plantear una regresión que estime la variable objetivo y medir su desempeño.

4. **Validación de supuestos:** realice los ajustes necesarios para que su modelo cumpla con las suposiciones necesarias para la inferencia estadística con regresiones.

5. **Interpretación de los coeficientes:** realice una interpretación de los coeficientes de la regresión, identificando los mas relevantes para la tarea y como afectan la variable objetivo.

6. **Exportar el modelo:** su equipo debe exportar el modelo para poder ser usado sobre datos recientes en el ambiente de producción del cliente.



## Entregables

* Informe del laboratorio con el desarrollo y la evidencia de las etapas de
	* Limpieza y  preprocesamiento
	* Identificación de variables
	* Ajustes necesarios para cumplir con las suposiciones
	* Estructura del modelo final
	* Métricas de calidad del modelo
	* Interpretación de los coeficientes

Se espera que el informe no supere las 6 páginas y que incluya **JUSTIFICACIONES** de las decisiones tomadas en la construcción e interpretación de los modelos.

* Presentación corta para el negocio respondiendo a las siguientes preguntas:

	* ¿Cuál es  el resultado del ejercicio de regresión?	
	* ¿Cuales son las variables mas influyentes y que tan confiables son los resultados?
	* ¿Su equipo recomienda instalar el modelo de estimación en producción o es mejor continuar usando expertos para la tarea?
	* En caso de no recomendar el uso de un modelo de regresión ¿Que otras posibilidades tiene la empresa?¿Hacia donde debe seguir con esta tarea?

* Modelo completo exportado en un archivo .joblib, usando la librería *joblib*. 



**Nota:** 
El modelo entregado será utilizado para estimar la variable objetivo de unos datos que separó el cliente. El cliente cargará el modelo entregado se lo aplicará a los datos y comparará el resultado con el valor real de la variable  objetivo. Ustedes tienen acceso a una copia de estos datos (sin la variable objetivo). Recuerde que el cliente no planea hacer ningún tipo de alteración sobre estos datos antes de entregárselos al modelo, por lo que su equipo debe exportar un *pipeline* capaz de hacer la manipulaciones  necesarias para hacer la tarea de estimación. Este archivo de datos se llama: *SkillCraftRecent.csv*.

El código que usará el cliente es el siguiente:

```python
import numpy as np
import pandas as pd
import joblib

# Proceso de prubea del cliente
filename = 'modelo.joblib' # Ubicación del archivo entregado
df_recent = pd.read_csv('SkillCraftRecent.csv') # Lectura de los datos recientes

# Lee el archivo y carga el modelo
pipeline = load(filename)

y_true = pd.read_csv('SkillCraftRecentRankings.csv') # La columna que solo el cliente tiene
y_predicted =  pipeline.predict(df_recent)

# Calcula el desempeño del modelo
np.sqrt(mse(y_true, y_predicted))

```



## Instrucciones de Entrega
- El laboratorio se entrega en grupos de máximo 3 estudiantes
- Recuerde hacer la entrega por la sección unificada en Bloque Neón, antes del lunes 27 de septiembre a las 22:00.   
  Este será el único medio por el cual se recibirán entregas.
- En la entrega indique la etapa o etapas realizada por cada uno de los miembros del grupo.

## Rúbrica de Calificación

A continuación se encuentra la rúbrica de calificación.


| Concepto | Porcentaje |
|:---:|:---:|
| Descripción de la limpieza de los datos  | 5% |
| Descripción del proceso de identificación de variables | 15% |
| Implementación de la regresión y extracción de sus métricas de calidad  | 10% |
| Exploración de los supuestos a partir del modelo de regresión planteado | 15% |
| Realizar las transformaciones necesarias  para cumplir los supuestos | 15% |
| Incorporar las transformaciones al modelo en un *pipeline* y exportarlo | 10% |
| Presentación para AlpesGamesInsight con resultados, recomendaciones dadas a la empresa y visualización | 15% |
| Calidad del modelo al estimar el conjunto de datos que separó el cliente | 10% |
| Notebook asociado | 5% |


