# Dashboard 2: visualización y documentación para narrar a un equipo de trabajo

Este desarrollo es parte del curso de Visualización y Storytelling de la Maestría en Inteligencia Analítica de Datos (MIAD). 

* Modelar los datos: En el link, se puede ir al Jupiter Notebook en el que se realizó el modelado de datos.
* Dashboard: En el link, se puede ir al visualizador en Looker Studio.
* Documentación: A continuación, se puede ver la documentación relacionada con el modelado y la actualización de los datos.

**Variables en base de datos original**

Hay que mencionar que los nombres de las variables estan  escritas en inglés, tal cual se encuentran en la base de datos original, mientras que las descripciones sí están escritas en español. 

| Nombre | Tipo de dato | Descripción |
| --- | --- | --- |
| Timestamp | texto/datetime | Fecha y hora de la respuesta a la encuesta |
| How old are you? | texto | Rango de edad del encuestado |
| What industry do you work in? | texto | Industria en la que trabaja el encuestado |
| Job title | texto | Título profesional que desempeña |
| If your job title needs additional context, please clarify here: | texto | Información adicional del título profesional |
| What is your annual salary? (You'll indicate the currency in a later question. If you are part-time or hourly, please enter an annualized equivalent -- what you would earn if you worked the job 40 hours a week, 52 weeks a year.) | número | Salario anual |
| How much additional monetary compensation do you get, if any (for example, bonuses or overtime in an average year)? Please only include monetary compensation here, not the value of benefits. | número | Compensación monetaria adicional |
| Please indicate the currency | texto | Divisa del salario |
| If "Other," please indicate the currency here: | texto | Otro tipo de moneda no incluida en la variable Currency |
| If your income needs additional context, please provide it here: | texto | Información adicional sobre sus ingresos |
| What country do you work in? | texto | País donde trabaja | 
| If you're in the U.S., what state do you work in? | texto | Estado donde trabaja (sí el país donde trabaja es USA) | 
| What city do you work in? | texto | Ciudad donde trabaja |
| How many years of professional work experience do you have overall? | texto | Total de años de experiencia profesional | 
| How many years of professional work experience do you have in your field? | texto | Años de experiencia en su campo | 
| What is your highest level of education completed? | texto | Nivel más alto de educación | 
| What is your gender? | texto | Genero del encuestado | 
| What is your race? (Choose all that apply.) | texto | Raza del encuestado | 

**Variables luego de modeladas**

Luego de realizar la limpieza y modelado de datos, hay 2 nuevas columnas relacionadas a los campos de país y ciudad estadarizadas y 3 nuevas columnas relacionadas al calculo del salario anual, compensaciones e ingresos totales en pesos colombianos. Cabe mencionar que, se decidio renombrar las columnas que habían antes del modelado con el fin de tener mayor claridad en el proceso de limpieza. También hay que resaltar que se decide manejar el nombre de las columnas en inglés. 
Luego de aplicar la limpieza, minado y filtrado de los datos nos quedamos con las siguientes variables, se crean dos nuevas columnas con las versiones modificadas/estandarizadas de país y ciudad, y tres nuevas columnas que corresponde al salario anual, compensaciones e ingresos totales en pesos colombianos.

timestamp', 'age_range', 'industry', 'job_title',
       'additional_context_job', 'annual_salary',
       'additional_monetary_compensation', 'currency', 'other_currency',
       'additional_context_income', 'country', 'state_US', 'city',
       'years_work_experience', 'years_work_experience_field',
       'level_education', 'gender', 'race', 'country_clean', 'salario_anual',
       'compensaciones', 'salario_total', 'city_clean
| Nombre | Tipo de dato | Descripción |
| --- | --- | --- |
| timestamp | texto/datetime | Fecha y hora de la respuesta a la encuesta |
| age_range | texto | Rango de edad del encuestado |
| industry | texto | Industria en la que trabaja el encuestado |
| job_title | texto | Título profesional que desempeña |
| additional_context_job | texto | Información adicional del título profesional |
| annual_salary | número | Salario anual |
| additional_monetary_compensation | número | Compensación monetaria adicional |
| currency | texto | Divisa del salario |
| other_currency | texto | Otro tipo de moneda no incluida en la variable Currency |
| additional_context_income | texto | Información adicional sobre sus ingresos |
| country | texto | País donde trabaja | 
| state_US | texto | Estado donde trabaja (sí el país donde trabaja es USA) | 
| city | texto | Ciudad donde trabaja |
| years_work_experience | texto | Total de años de experiencia profesional | 
| years_work_experience_field | texto | Años de experiencia en su campo | 
| level_education | texto | Nivel más alto de educación | 
| gender | texto | Genero del encuestado | 
| race | texto | Raza del encuestado | 
| country_clean | texto | País donde trabaja, luego de la limpieza y estandarización | 
| salario_anual | número | Salario anual en pesos colombianos basada en la tasa de cambio del día 12/02/2023 |
| compensaciones | número | Compensaciones en pesos colombianos basada en la tasa de cambio del día 12/02/2023 | 
| ingreso_total | número | Ingreso total en pesos colombianos |
| city_clean | texto | Ciudad donde trabaja, luego de la limpieza y estandarización | 


Describir paso a paso lo que una persona debería hacer para actualizar los datos y aplicar el modelado que han diseñado. Piensen esta sección como una ayuda a alguien que los va a reemplazar en el trabajo. Esta persona debe entender con precisión cómo replicar lo que diseñaron. Este paso a paso asume que la estructura de la base de datos original no cambia en nuevas versiones. Puede ser tan detallada como ustedes quieran, pero debe ser muy claro cómo crear los nuevos campos y procedimientos para limpiar.  


