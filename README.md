# Dashboard 2: visualización y documentación para narrar a un equipo de trabajo

Este desarrollo es parte del curso de Visualización y Storytelling de la Maestría en Inteligencia Analítica de Datos (MIAD). 

* Modelar los datos: En el link, se puede ir al Jupiter Notebook en el que se realizó el modelado de datos.
* Dashboard: En el link, se puede ir al visualizador en Looker Studio.
* Documentación: A continuación, se puede ver la documentación relacionada con el modelado y la actualización de los datos.

**Variables en base de datos original**

Hay que mencionar que los nombres de las variables estan  escritas en inglés, tal cual se encuentran en la base de datos original, mientras que las descripciones sí están escritas en español. 

Nombre | Timestamp | How old are you? | What industry do you work in? | Job title | If your job title needs additional context, please clarify here: | What is your annual salary? (You'll indicate the currency in a later question. If you are part-time or hourly, please enter an annualized equivalent -- what you would earn if you worked the job 40 hours a week, 52 weeks a year.) | How much additional monetary compensation do you get, if any (for example, bonuses or overtime in an average year)? Please only include monetary compensation here, not the value of benefits. | Please indicate the currency | If "Other," please indicate the currency here:  | If your income needs additional context, please provide it here: | What country do you work in? | If you're in the U.S., what state do you work in? | What city do you work in? | How many years of professional work experience do you have overall? | How many years of professional work experience do you have in your field? | What is your highest level of education completed? | What is your gender? | What is your race? (Choose all that apply.)
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---
Tipo de dato | texto/datetime | texto | texto | texto | texto | número | número | texto | texto | texto | texto | texto | texto | texto | texto | texto | texto | texto
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---
Descripción | Fecha y hora de la respuesta a la encuesta | Rango de edad del encuestado | Industria en la que trabaja el encuestado | Título profesional que desempeña | Información adicional del título profesional | Salario anual | Compensación monetaria adicional | Divisa del salario | Otro tipo de moneda no incluida en la variable Currency | Información adicional sobre sus ingresos | País donde trabaja | Estado donde trabaja (sí el país donde trabaja es USA) | Ciudad donde trabaja | Total de años de experiencia profesional | Años de experiencia en su campo | Nivel más alto de educación | Genero del encuestado | Raza del encuestado

Variables luego de modeladas. Durante el modelado, ustedes pueden cambiar el nombre de las variables, las pueden dejar en inglés o traducirlas al español. En cualquier caso, por buena práctica, decidan qué idioma van a usar y sean consistentes con esa decisión en todas las variables: 

Tipo de variable. 

Descripción corta, máximo 1 párrafo. 

Describir paso a paso lo que una persona debería hacer para actualizar los datos y aplicar el modelado que han diseñado. Piensen esta sección como una ayuda a alguien que los va a reemplazar en el trabajo. Esta persona debe entender con precisión cómo replicar lo que diseñaron. Este paso a paso asume que la estructura de la base de datos original no cambia en nuevas versiones. Puede ser tan detallada como ustedes quieran, pero debe ser muy claro cómo crear los nuevos campos y procedimientos para limpiar.  


