
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
**Uso de la lengua** | use | Supone el promedio de respuestas de los sujetos, de 0 a 1, a una serie de preguntas sobre cuánto usan la lengua en que leen el ítem. Las preguntas preguntaban a los participantes por el porcentaje de uso de cada lengua en situaciones diversas: ambientes familiares, profesionales, ocio, uso de redes sociales, etc.
**Nivel de competencia en la lengua** | profic | Es el promedio de cuánto indican los sujetos que saben hablar, escribir, entender y leer cada lengua. Es una medida subjetiva del nivel de competencia total en la lengua, y su rango es de 0 a 1. 
**Grupo** | grupo | Corresponde al grupo al que pertenecía el sujeto, si era el grupo bilingüe de castellano y catalán ('1'), o si era el grupo nativo de castellano que no conoce el catalán ('0').
**Orden** | orden | Es el orden de los bloques en el experimento para el sujeto que lee la oración. Los sujetos bilingües realizaban la tarea en castellano y en catalán, y el orden de esos bloques se contrabalanceó. Esta variable indica con un '0' que la primera tarea que recibió el sujeto fue en castellano, y con un '1' que la primera tarea fue en catalán. 
**Condición experimental** | contextlab1 y contextlab2 | Son dos variables dicotómicas que, conjuntamente, indican la condición experimental a la que pertenece el ensayo. 

<p align="center">
<img width="691" alt="image" src="https://user-images.githubusercontent.com/94480051/175779314-e51420a9-9a00-418e-a711-db400cdaa690.png"></p>

## Problema 1

### Objetivos

El primer problema que el Proyecto M0ISES trató de resolver fue el de encontrar un indicador objetivo y eficiente del nivel de competencia de un individuo en una lengua. 

En los estudios en psicolingüística, es extremadamente importante conocer el nivel que tienen los individuos en las lenguas que se pretenden analizar. Sin embargo, pocas veces se puede aplicar un test exhaustivo del nivel de competencia objetivo que se tiene en una lengua, ya que normalmente se trata de pruebas largas que interrumpen el curso de los experimentos y que pueden fatigar al participante. En consecuencia, usualmente se recurre a preguntar al sujeto cómo se valora a sí mismo en las destrezas de escritura, habla, lectura y escucha para una lengua. Esta medida es considerablemente menos costosa, pero incluye una gran dosis de subjetividad que puede estar distorsionando las repsuestas. Por esta razón, en este campo de estudio se busca una medida objetiva del nivel de competencia en una lengua que sea rápida de conseguir en situaciones experimentales. 

Es evidente que el tiempo de lectura está relacionado con el nivel de competencia en una lengua: a más competencia, existe un menor coste de integración que genera más agilidad al leer. En los datos que se incluyen en este proyecto, el tiempo de lectura también está ligera pero significativamente relacionado con la estimación subjetiva de los sujetos en nivel de competencia (r=-0,069; p<0,001). Adicionalmente, el nivel de competencia en una lengua tambien está relacionado significativamente con la frecuencia de exposición (r=0,144; p<0,001), la preferencia de lectura (r=0,220; p<0,001) y el uso de la lengua (r=0,270; p<0,001). En las gráficas inferiores se observa cómo, a simple vista, estas variables parecen tener poca relacion con el nivel de competencia. Sin embargo, todas estas medidas en conjunto podrían servir para conseguir predecir la variable de nivel de competencia de una forma eficaz.

<p align="center">
![image](https://user-images.githubusercontent.com/94480051/175779962-3e65340d-db0c-4dd4-993d-0fdf3ddfbe36.png)
![image](https://user-images.githubusercontent.com/94480051/175779970-aa7cd286-094a-49de-a81e-aea278dd7663.png)
![image](https://user-images.githubusercontent.com/94480051/175779977-33b1d958-4c02-4d4f-a731-2baf856a745b.png)
![image](https://user-images.githubusercontent.com/94480051/175779984-9f6826de-a073-4d00-91a8-ad10298b791f.png)</p>

### Construcción del modelo

De esta forma, se creó una red neuronal profunda con la intención de conseguir predecir el nivel de competencia de los sujetos en la lengua en que realizan los ensayos, con los datos indicados anteriormente. A continuación se presenta un registro de todos los intentos al crear dicha red:

(imagenes registro)

Finalmente, el modelo elegido fue un modelo secuencial con un total de 1723 neuronas densamente conectadas, divididas en 16 capas. Cada dos capas, había un dropout del 20% de neuronas para reducir el riesgo de overfitting del modelo. La activación de todas las capas fue reLU, menos la última capa que tenía una neurona con activación lineal puesto que debía predecir un valor continuo. Este modelo se entrenó con un tamaño de batch de 40 ejemplos, en 200 epochs, con el optimizador Adam, y obtuvo un error cuadrático medio de aproximadamente 0,000781. En la gráfica siguiente se puede observar la reducción de dicho error a lo largo de los epochs:

<p align="center">
![image](https://user-images.githubusercontent.com/94480051/175780444-8db3e0c5-45ce-48fd-80a0-fb156c06b61e.png)</p>

Este error medio obtenido es bastante positivo teniendo en cuenta la naturaleza de los datos. Siendo valores que oscilan entre 0 y 1, con un máximo de 3 cifras decimales, obtener un error medio aproximado de 0,0008 es aceptable. El ajuste del modelo a los valores reales se puede observar en la siguiente gráfica:

<p align="center">
![image](https://user-images.githubusercontent.com/94480051/175780456-6f9ab25b-ef9f-4bf0-a6b5-7abffb787af9.png)</p>

Es importante remarcar que en otros intentos a la hora de crear el modelo, el mismo modelo construido bajo las mismas condiciones de entrenamiento, pero sin las variables de exposición, uso y preferencia de lectura en la lengua del ensayo, no consiguió ajustarse tanto a los datos. El error cuadrático medio que alcanzó fue de 0,005223, mucho mayor que el que se consigue incluyendo las variables. En las siguientes gráficas se observa su reducción en error cuadrático medio y el ajuste a los datos.

<p align="center">
![1_ReductionMSE(UNSELECTED)](https://user-images.githubusercontent.com/94480051/175780510-628cdee7-fc32-4d11-860c-d63d987ea95e.png)
![1_ModelFitting(UNSELECTED)](https://user-images.githubusercontent.com/94480051/175780514-21794061-65b9-4aec-b0c8-f10e98459be3.png)</p>

### Interpretación

Para conseguir predecir el valor en nivel de competencia lingüística que tenían los sujetos que realizaban cada ensayo, se creó una red neuronal que, al introducir los datos que contenía el dataset inicial, conseguía predecir el valor real con un error cuadrático medio de aproximadamente 0,0008. Esto significa que con la estructura neuronal empleada en este modelo se puede obtener eficazmente el nivel de competencia en base al tiempo de lectura de un ítem concreto, el porcentaje de exposición, uso y preferencia de lectura de la lengua en que se lee, y otras variables sobre el contexto experimental. Además, las variables de exposición, uso y preferencia de lectura tienen una contribución importante sobre esa predicción, puesto que el mismo modelo entrenado sin la entrada de esos valores no consigue niveles tan altos de precisión. 

No obstante, y en línea con la motivación inicial que introducía este problema, los valores que este modelo predice siguen siendo valores subjetivos. Es decir, en la introducción a este primer problema se hablaba de que es necesaria una medida rápida y puntera del nivel objetivo de competencia en las diferentes lenguas. Implementando este modelo, lo máximo que se puede conseguir es una medida rápida y lo suficientemente puntera del nivel de competencia subjetivo que se atribuye cada sujeto a sí mismo, pues es con los datos con los que se contaba inicialmente. Para conseguir los objetivos iniciales, las futuras líneas de investigación deberían elaborar un modelo similar que pudiese ser entrenado con los niveles de competencia reales, esto es, los valores objetivos estimados con otros tests. 




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
