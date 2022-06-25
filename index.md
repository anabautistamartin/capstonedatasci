
# PROYECTO M0ISES: Where Psycholinguistics and Machine Learning Meet

En esta página encontrarás toda la información sobre el Proyecto M0ISES, un proyecto que reúne los avances en Psicolingüística y Machine Learning para alcanzar soluciones prácticas e innovadoras en el estudio del procesamiento del lenguaje. 

## Introducción

Hace tan solo unos años que la ciencia cognitiva y el estudio del lenguaje han visto un gran avance en tanto a las nuevas tecnologías de Machine Learning. Dentro de la psicolingüística, la ciencia que estudia los mecanismos cognitivos del procesamiento del lenguaje, existen muchas preguntas por resolver, y gran parte de ellas se pueden empezar a responder implementando modelos automáticos que simulen el procesamiento. Además, estas técnicas pueden crear herramientas muy precisas en la evaluación de los sujetos que es necesaria para este tipo de investigaciones. 

El presente proyecto se dirige a tratar de dar una respuesta a dos problemas principales empleando las técnicas de aprendizaje automático. Estos problemas emergen de una interesante [investigación sobre la ilusion de Moisés](https://moises-bilingue.webflow.io/). Ante oraciones como *"Según se dice en la Biblia, Moisés llevó dos animales de cada tipo en el arca"*, pocos individuos son capaces de reconocer el error y producen una falsa ilusión de coherencia semántica. Estas ilusiones son sumamente interesantes para este campo porque revelan un error sistemático de nuestro sistema cognitivo a la hora de integrar la información semántica. En la investigación mencionada anteriormente, se presentaban este tipo de oraciones en castellano y en catalán, y se pedía a los sujetos responder si era correcta o incorrecta. Además, se recogía información sobre el tiempo de lectura de la oración y otras variables sociolingüísticas que indicaban el nivel que tenían los sujetos en cada lengua. Esta investigacion y sus resultados fueron la base del proyecto que se presenta en esta página.

## Datos

Primero, se recogieron los resultados de todos los ensayos llevados a cabo en la investigación. Dichos resultados provienen de 43 sujetos bilingües de castellano y catalán (66% mujeres, edad media = 22,70), y 35 sujetos (70% mujeres, edad media = 22,86) que no conocían el catalán pero eran hablantes nativos de castellano. La limpieza de esos datos se realizó en una plataforma externa siguiendo el criterio siguiente: 
- Eliminación de ensayos en los que los participantes no conocían la respuesta correcta a la oración.
- Eliminación de ensayos en los que los sujetos respondían incorrectamente.
- Eliminación de ensayos en los que el tiempo de lectura era mayor o menor que la media en tres desviaciones típicas (MEAN±3SD).
De esta forma, se descartaron los ensayos que no correspondían una integración semántica adecuada por parte de los sujetos. 
Esto supuso la pérdida de aproximadamente un 0,10% de los ensayos iniciales, quedando una nube de datos de **7525 unidades de ensayos**. Esta base de datos está disponible en el repositorio de GitHub bajo el nombre ['dataset'](https://github.com/anabautistamartin/capstonedatasci/files/8984239/dataset.csv).

Cada ensayo del experimento corresponde a cada línea de la base de datos mencionada anteriormente, e incluye las variables o columnas indicadas en la tabla de a continuación:

Variable | Nombre | Descripción
--- | :---: | :---: | :---:
**Versión de la oración**  | version | Corresponde a la versión de la oración presentada al sujeto, en tanto que cada ítem se podía presentar a los sujetos en su versión correcta o incorrecta. '0' indica la versión incorrecta (e.g., *'Según se dice en la Biblia, Moisés llevó dos animales de cada tipo en el arca'*), y '1' indica la versión correcta (e.g., *'Según se dice en la Biblia, Noé llevó dos animales de cada tipo en el arca'*). 
**Ítem**  | item | Indica el número de ítem leído en el ensayo, de un listado de 146 ítems.
**Milisegundos de lectura de la oración** | ms | Indica cuánto tarda el sujeto en ese ensayo en leer el ítem, medido en milisegundos ponderados según la longitud de la oración en número de caracteres. 
 **Lengua** | lang | Corresponde a la lengua en la que se lee en la oración, ya que el grupo de sujetos bilingüe hacía la tarea en castellano y en catalán. '0' indica que se lee en castellano, y '1' indica que se lee en catalán.
**Frecuencia de exposición** | expo | Indica, de 0 al 1, la frecuencia con la que los sujetos están expuestos a la lengua en la que leen el ítem. Esto se incluyó con la pregunta "Del 0 al 10, ¿cuánto estás expuesto/a al (castellano/catalán) actualmente?" en el experimento original. 
**Preferencia de lectura** | pref | Corresponde, de 0 a 1, a la preferencia que tienen los sujetos por leer una pieza de información en la lengua en la que leen el ítem. En el experimento, se incluyó bajo la pregunta "Si pudieses leer un texto en cualquiera de las lenguas que conoces, indica del 0 al 10 en qué medida elegirías leerlo en (castellano/catalán)".
**Uso de la lengua** | uso | Supone el promedio de respuestas de los sujetos, de 0 a 1, a una serie de preguntas sobre cuánto usan la lengua en que leen el ítem. Las preguntas preguntaban a los participantes por el porcentaje de uso de cada lengua en situaciones diversas: ambientes familiares, profesionales, ocio, uso de redes sociales, etc.
**Nivel de competencia en la lengua** | profic | Es el promedio de cuánto indican los sujetos que saben hablar, escribir, entender y leer cada lengua. Es una medida subjetiva del nivel de competencia total en la lengua, y su rango es de 0 a 1. 
**Grupo** | grupo | Corresponde al grupo al que pertenecía el sujeto, si era el grupo bilingüe de castellano y catalán ('1'), o si era el grupo nativo de castellano que no conoce el catalán ('0').
**Orden** | orden | Es el orden de los bloques en el experimento para el sujeto que lee la oración. Los sujetos bilingües realizaban la tarea en castellano y en catalán, y el orden de esos bloques se contrabalanceó. Esta variable indica con un '0' que la primera tarea que recibió el sujeto fue en castellano, y con un '1' que la primera tarea fue en catalán. 
**Condición experimental** | contextlab1 y contextlab2 | Son dos variables dicotómicas que, conjuntamente, indican la condición experimental a la que pertenece el ensayo. 

<img width="691" alt="image" src="https://user-images.githubusercontent.com/94480051/175779314-e51420a9-9a00-418e-a711-db400cdaa690.png">


## Problema 1

El primer problema que el Proyecto M0ISÉS trató de resolver fue el de encontrar un indicador objetivo y rápido del nivel de competencia de un individuo en una lengua. 

En los estudios en psicolingüística, es extremadamente importante conocer el nivel que tienen los individuos en las lenguas que se pretenden analizar. Sin embargo, pocas veces se puede aplicar un test exhaustivo del nivel de competencia objetivo que se tiene en una lengua, ya que normalmente se trata de pruebas largas que interrumpen el curso de los experimentos y pueden crear fatiga al individuo. En consecuencia, usualmente se recurre a preguntar al sujeto cómo se valora a sí mismo en las destrezas de escritura, habla, lectura y escucha para una lengua. Esta medida es considerablemente menos costosa, pero incluye una gran dosis de subjetividad que en algunos casos es probable que distorsione las respuestas.

Es evidente que el tiempo de lectura está relacionado con el nivel de competencia en una lengua: a más competencia existe un menor coste de integración que genera más agilidad al leer. En los datos que se incluyen en este proyecto, el tiempo de lectura también está ligera pero significativamente relacionado con la autoestimación de los sujetos en nivel de competencia (r=-0,069; p<0,001). Adicionalmente, el nivel de competencia en una lengua tambien está relacionado significativamente con la frecuencia de exposición (r=0,144; p<0,001), la preferencia de lectura (r=0,220; p<0,001) y el uso de la lengua (r=0,270; p<0,001). Este conglomerado de variables que tienen una leve pero significativa relación con el nivel de competencia podrían servir para conseguir predecir esta última variable de una forma eficaz. 

De esta forma, se creó una red neuronal profunda que consiguiese predecir el valor de nivel de competencia en la lengua con los valores de entrada indicados como 'datos' anteriormente. A continuación, se observa un registro de todos los intentos al crear dicha red:

![ML Project Diary-6](https://user-images.githubusercontent.com/94480051/175072540-5c8a60f6-8c1d-4f17-bb62-73970ca4181b.jpg)
![ML Project Diary-7](https://user-images.githubusercontent.com/94480051/175072562-e76632f0-bd2f-47b6-968c-bdaf42a97b66.jpg)
![ML Project Diary-8](https://user-images.githubusercontent.com/94480051/175072572-f5da6c99-c591-448c-a032-1e5434e1f048.jpg)

Finalmente, el modelo elegido fue un modelo secuencial con un total de 1291 neuronas densamente conectadas, divididas en 15 capas de 86 neuronas cada una, además la última capa con 1 neurona. Cada dos capas, había un dropout del 20% de neuronas para reducir el overfitting del modelo. La activación de todas las capas fue reLU, menos la última que tenía una activación lineal puesto que debía predecir un valor continuo. Este modelo, valorado con el error cuadrático medio, obtuvo un error medio de 0,001029. En la gráfica siguiente se puede observar la reducción de dicho error a lo largo de los epochs:

![image](https://user-images.githubusercontent.com/94480051/175074100-e5f0c1e9-c0ea-471a-a4c4-487485bf6689.png)

Este error medio obtenido es bastante positivo teniendo en cuenta la naturaleza de los datos. Siendo valores que oscilan entre 0 y 1, con un máximo de 3 cifras decimales, obtener un error medio de aproximadamente 0,001 es aceptable. El ajuste del modelo a los valores reales se puede observar en la siguiente gráfica:

![image](https://user-images.githubusercontent.com/94480051/175078742-dbf0a1dd-3e45-4f62-99bc-8486ec8ac6ad.png)




## Welcome to Ana's Capstone Project

You can use the [editor on GitHub](https://github.com/anabautistamartin/capstonedatasci/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3


- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/anabautistamartin/capstonedatasci/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
