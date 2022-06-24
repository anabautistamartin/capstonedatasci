
# PROYECTO M0ISES: Where Psycholinguistics and Machine Learning Meet

En esta página encontrarás toda la información sobre el Proyecto M0ISES, un proyecto que reúne los avances en Psicolingüística y Machine Learning para alcanzar soluciones prácticas e innovadoras en el estudio del procesamiento del lenguaje. 

## Introducción

Hace tan solo unos años que la Ciencia Cognitiva y el estudio del lenguaje han visto un gran avance en tanto a las nuevas tecnologías de Machine Learning. tal y como ocurre en el cerebro ...

Sin embargo, muchas preguntas aun quedan por resolver, y muchas de ellas encuentran soluciones muy eficientes en implementaciones de Machine Learning. Algunas de esas preguntas tienen que ver con la integración semántica durante el procesamiento del lenguaje. El presente proyecto se dirige, pues, a tratar de dar una solución avanzada a dos problemas principales, en base a una interesante [investigación sobre la ilusion de Moisés](https://moises-bilingue.webflow.io/).

## Datos

Cada ensayo del estudio mencionado anteriormente consistía en la lectura y respuesta a una oración que podía ser semánticamente correcta o incorrecta. Para llevar a cabo este proyecto, se recogieron los resultados de todos los ensayos llevados a cabo en el estudio. La limpieza de esos datos se realizó en una plataforma externa siguiendo el criterio siguiente: 
- Eliminación de ensayos en los que los participantes no conocían la respuesta correcta a la oración.
- Eliminación de ensayos en los que el sujeto respondía incorrectamente.
- Eliminación de ensayos en los que el tiempo de lectura era mayor o menor que la media en tres desviaciones típicas (MEAN±3SD).
De esta forma, se descartaron los ensayos que no correspondían una integración semántica adecuada por parte de los sujetos. 
Esto supuso la pérdida de aproximadamente un 0,10% de los ensayos iniciales, quedando una nube de datos de **7525 unidades de ensayos**. Esta base de datos está disponible en el repositorio de GitHub asociado a esta página. 

Cada ensayo, esto es cada línea de la base de datos, contiene las siguientes columnas:
**1. Versión de la oración**. Cada oración tenía dos versiones: Incorrecta (0) o Correcta (1). Los sujetos leen todas las oraciones únicamente en una de las dos versiones.
**2. Ítem.** Indica el número de ítem leído en el ensayo, de un listado de 146 ítems.
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
