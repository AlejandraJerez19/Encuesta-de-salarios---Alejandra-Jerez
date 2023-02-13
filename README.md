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

Variables luego de modeladas. Durante el modelado, ustedes pueden cambiar el nombre de las variables, las pueden dejar en inglés o traducirlas al español. En cualquier caso, por buena práctica, decidan qué idioma van a usar y sean consistentes con esa decisión en todas las variables: 

Tipo de variable. 

Descripción corta, máximo 1 párrafo. 

Describir paso a paso lo que una persona debería hacer para actualizar los datos y aplicar el modelado que han diseñado. Piensen esta sección como una ayuda a alguien que los va a reemplazar en el trabajo. Esta persona debe entender con precisión cómo replicar lo que diseñaron. Este paso a paso asume que la estructura de la base de datos original no cambia en nuevas versiones. Puede ser tan detallada como ustedes quieran, pero debe ser muy claro cómo crear los nuevos campos y procedimientos para limpiar.  


