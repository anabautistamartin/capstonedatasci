# PROYECTO M0ISES
## WHERE PSYCHOLILNGUISTICS AND MACHINE LEARNING MEET



INTRODUCCION

En esta página encontrarás todo el contenido del Proyecto M0ISES!

a. Los orígenes del proyecto
b. Los datos
b. Problema 1: Proficiency
c. Problema 2: Correctness semántica

Continúa leyendo para saber más...

## Orígenes

Antes que nada, lee la siguiente pregunta y piensa la respuesta antes de continuar leyendo:

Con algún conocimiento sobre la Biblia y la religión cristiana, habrás tardado poco en averiguar que Moisés llevó **2** animales de cada especie en su arca. Sin embargo, quizás no te habrás percatado de que no fue Moisés, sino Noé quien llevó esos animales en el arca. Si es así, enhorabuena, ¡has caido en la **ilusión de Moisés**!

Este efecto de falsa congruencia semántica fue investigado por primera vez en el área de la psicolingüística en 1981 por Erickson y Mattsew (link). Durante las décadas posteriores se llevaron a cabo múltiples estudios para averiguar bajo qué condiciones se daba o no dicho efecto. Los modelos que trataron de explicar esta ilusión llegaron a la conclusión de que el procesamiento lingüístico es tan eficiente que nos lleva a asumir coherencia semántica en una pregunta o oración que cumple los mínimos de relación semántica (link). En casos como la pregunta anterior, los elementos de la oración están relacionados semánticamente ...

Sin embargo, no ha sido hasta el año pasado que se ha estudiado por primera vez la ilusión de Moisés en las distintas lenguas de personas bilingües (Dehaene, link). Esto plantea una cuestión importante en el ámbito del procesamiento multilingüe ya que integra el concepto de **eficiencia semántica** en múltiples lenguas. El coste cognitivo que supone procesar en una lengua en la que somos menos competentes podría hacer que suceda en mayor medida la ilusión de Moisés, ya que se destinan menos recursos a comprobar la coherencia semántica, o bien hacer que suceda en menor medida la ilusión, ya que al añadir más esfuerzos para procesar, tambien es más probable detectar una incongruencia. Esta prematura línea de estudio aún no tiene la respuesta. 

Los orígenes del Proyecto M0ISES se encuentran en uno de los estudios destinados a analizar la ilusión de Moisés, en este caso en personas bilingües de castellano y catalán. Esta investigación pertenece al Trabajo de Fin de Máster de la autora, Ana María Bautista Martín, desarrollado desde la Universidad de Barcelona y la Universidad Rovira i Virgili, con la colaboración de la Universidad de Minho (Portugal).

## El estudio

En este estudio, 78 sujetos (53 mujeres y 25 hombres) de edades comprendidas entre los 18 y 30 años (Mean=22,78; SD=...) completaron una tarea online de lectura de oraciones sobre las que debían responder si eran correctas o incorrectas. El procedimiento para los sujetos bilingües seguía el siguiente orden: consentían a participar en el experimento, recibían los ensayos de entrenamiento, contestaban a 73 oraciones en una de las dos lenguas (castellano o catalán), contestaban a otras 73 oraciones en la otra lengua (castellano o catalán) y finalmente completaban una serie de preguntas sociolingüísticas sobre cada lengua.

Es importante destacar que estos sujetos bilingües de castellano y catalán fueron seleccionados precisamente por tener altos niveles de competencia en las dos lenguas. Además, la situación sociolingüística en territorios catalanoparlantes hace que estos bilingües sean normalmente altamente balanceados en ambas lenguas. 

## Los datos

Para este proyecto, se contó con los datos del estudio descrito anteriormente. Los datos se limpiaron de la siguiente forma:
- Eliminación de ensayos en los que el sujeto no conocía la respuesta correcta a la oración. 
- Eliminación de ensayos en los que el sujeto tenía la ilusión (respondía 'correcta' a una oración incorrecta). Estos ensayos podrían crear confusión para el modelo, ya que se trata de oraciones que se integran semánticamente como correctas pero en realidad son incorrectas. 
- Eliminación de ensayos en los que el tiempo de lectura era mayor o menor que la media en tres desviaciones típicas (MEAN±3SD). Estos ensayos son poco informativos ya que indican despiste o fatiga del sujeto al llevar a cabo el experimento. 

De esta forma, se perdió aproximadamente un 0,10% de los ensayos iniciales, quedando una nube de datos de **7525 unidades de ensayos**. Esta base de datos está disponible en el siguiente enlace:

Cada ensayo contenía inicialmente las siguientes columnas:
1. Versión de la oración: correcta o incorrecta, indicado con 1 y 0 respectivamente. 
2. Número de ítem leído, de un listado de 146 ítems.
3. Milisegundos de lectura de la oración, ponderados según la longitud de la oracion en número de caracteres. 
4. Lengua en la que se lee la oración: castellano o catalan, indicado con 0 y 1 respectivamente. 
5. Frecuencia de exposición a la lengua leída, indicado con valores del 0 al 1 por el propio sujeto. 
6. Preferencia de lectura en la lengua leída (i.e., en qué porcentaje elegirían leer en la lengua del ensayo si pudiesen elegir cualquier lengua), indicado con valores del 0 al 1. 
7. Uso de la lengua: promedio de respuestas a un inventario de uso de la lengua en distintas situaciones (ambientes familiares, profesionales, ocio, etc.), indicado con valores del 0 al 1.
8. Nivel de competencia en la lengua: promedio de la autoestimación en nivel de competencia de la lengua en escritura, lectura, escucha y habla, indicado con valores del 0 al 1.
9. Grupo: grupo al que pertenecía el sujeto, si es el monolingüe (control) o el bilingue, indicado con 0 y 1 respectivamente. 
10. Orden: orden de los bloques en el experimento, si se realiza primero la tarea en castellano o en catalán, indicado con 0 y 1 respectivamente. 
11. Contextlab1 y contextlab2: variables dicotómicas que indican, conjuntamente, la condición experimental a la que pertenece el ensayo.

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
