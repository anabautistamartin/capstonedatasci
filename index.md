
# PROYECTO M0ISES: Where Psycholinguistics and Machine Learning Meet

En esta página encontrarás toda la información sobre el Proyecto M0ISES, un proyecto que reúne los avances en Psicolingüística y Machine Learning para alcanzar soluciones prácticas e innovadoras en el estudio del procesamiento del lenguaje. 

## Introducción

Hace tan solo unos años que la ciencia cognitiva y el estudio del lenguaje han visto un gran avance en tanto a las nuevas tecnologías de Machine Learning. Dentro de la psicolingüística, la ciencia que estudia los mecanismos cognitivos del procesamiento del lenguaje, existen muchas preguntas por resolver, y gran parte de ellas se pueden empezar a responder implementando modelos automáticos que simulen el procesamiento. Además, estas técnicas pueden crear herramientas muy precisas en la evaluación de los sujetos que es necesaria para este tipo de investigaciones. 

El presente proyecto se dirige a tratar de dar una respuesta a dos problemas principales empleando las técnicas de aprendizaje automático. Estos problemas emergen de una interesante [investigación sobre la ilusion de Moisés](https://moises-bilingue.webflow.io/). Ante oraciones como *"Según se dice en la Biblia, Moisés llevó dos animales de cada tipo en el arca"*, pocos individuos son capaces de reconocer el error y producen una falsa ilusión de coherencia semántica. Estas ilusiones son sumamente interesantes para este campo porque revelan un error sistemático de nuestro sistema cognitivo a la hora de integrar la información semántica. En la investigación mencionada anteriormente, se presentaban este tipo de oraciones en castellano y en catalán, y se pedía a los sujetos responder si era correcta o incorrecta. Además, se recogía información sobre el tiempo de lectura de la oración y otras variables sociolingüísticas que indicaban el nivel que tenían los sujetos en cada lengua. Esta investigacion y sus resultados fueron la base del proyecto que se presenta en esta página.

## Datos

Primero, se recogieron los resultados de todos los ensayos llevados a cabo en la investigación. Dichos resultados provienen de 43 sujetos bilingües de castellano y catalán (66% mujeres, edad media = 22,70), y 35 sujetos (70% mujeres, edad media = 22,86) que no conocían el catalán pero eran hablantes nativos de castellano. 

La limpieza de esos datos se realizó en una plataforma externa siguiendo el criterio siguiente: 
- Eliminación de ensayos en los que los participantes no conocían la respuesta correcta a la oración.
- Eliminación de ensayos en los que los sujetos respondían incorrectamente.
- Eliminación de ensayos en los que el tiempo de lectura era mayor o menor que la media en tres desviaciones típicas (MEAN±3SD).

De esta forma, se descartaron los ensayos que no correspondían una integración semántica adecuada por parte de los sujetos. 
Esto supuso la pérdida de aproximadamente un 0,10% de los ensayos iniciales, quedando una nube de datos de **7525 unidades de ensayos**. Esta base de datos está disponible en el repositorio de GitHub bajo el nombre ['M0ISES'](https://github.com/anabautistamartin/capstonedatasci/files/8990332/M0ISES.csv).

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

![prob 1](https://user-images.githubusercontent.com/94480051/175988824-963574fb-7c30-4ef6-a945-cb6f5ea493a9.png)

### Construcción del modelo

De esta forma, se creó una red neuronal profunda con la intención de conseguir predecir el nivel de competencia de los sujetos en la lengua en que realizan los ensayos, con los datos indicados anteriormente. A continuación se presenta un registro de todos los intentos al crear dicha red:

[imagenes registro]

Finalmente, el modelo elegido fue un modelo secuencial con un total de 1723 neuronas densamente conectadas, divididas en 16 capas. Cada dos capas, había un dropout del 20% de neuronas para reducir el riesgo de overfitting del modelo. En la ilustración siguiente se representa dicho modelo neuronal. 

![representacion modelo 1](https://user-images.githubusercontent.com/94480051/175924709-0d5154c5-4001-4d7e-b5c9-cd7c19031c52.png)

La activación de todas las capas fue reLU, menos la última capa que tenía una neurona con activación lineal puesto que debía predecir un valor continuo. Este modelo se entrenó con un tamaño de batch de 40 ejemplos, en 200 epochs, con el optimizador Adam, y obtuvo un error cuadrático medio de aproximadamente 0,000781. En la gráfica siguiente se puede observar la reducción de dicho error a lo largo de los epochs:

![1](https://user-images.githubusercontent.com/94480051/175988743-f6a31b8e-16cb-49d8-890e-798f0ced632a.png)

Este error medio obtenido es bastante positivo teniendo en cuenta la naturaleza de los datos. Siendo valores que oscilan entre 0 y 1, con un máximo de 3 cifras decimales, obtener un error medio aproximado de 0,0008 es aceptable. El ajuste del modelo a los valores reales se puede observar en la siguiente gráfica:

![fitting selected](https://user-images.githubusercontent.com/94480051/175987550-ebb63093-47df-4a08-934b-ec166157ca07.png)

Es importante remarcar que en otros intentos a la hora de crear el modelo, el mismo modelo construido bajo las mismas condiciones de entrenamiento, pero sin las variables de exposición, uso y preferencia de lectura en la lengua del ensayo, no consiguió ajustarse tanto a los datos. El error cuadrático medio que alcanzó fue de 0,005223, mucho mayor que el que se consigue incluyendo las variables. En las siguientes gráficas se observa su reducción en error cuadrático medio y el ajuste a los datos.

![reduction in mse unselected](https://user-images.githubusercontent.com/94480051/175987583-59d1283e-bc8a-4909-9bcb-bd5528ed4fec.png)
![fitting unselected](https://user-images.githubusercontent.com/94480051/175987608-8f353d64-9e90-41b7-ae47-b57680a3b1c5.png)

### Interpretación

Para conseguir predecir el valor en nivel de competencia lingüística que tenían los sujetos que realizaban cada ensayo, se creó una red neuronal que, al introducir los datos que contenía el dataset inicial, conseguía predecir el valor real con un error cuadrático medio de aproximadamente 0,0008. Esto significa que con la estructura neuronal empleada en este modelo se puede obtener eficazmente el nivel de competencia en base al tiempo de lectura de un ítem concreto, el porcentaje de exposición, uso y preferencia de lectura de la lengua en que se lee, y otras variables sobre el contexto experimental. Además, las variables de exposición, uso y preferencia de lectura tienen una contribución importante sobre esa predicción, puesto que el mismo modelo entrenado sin la entrada de esos valores no consigue niveles tan altos de precisión. 

No obstante, y en línea con la motivación inicial que introducía este problema, los valores que este modelo predice siguen siendo valores subjetivos. Es decir, en la introducción a este primer problema se hablaba de que es necesaria una medida rápida y puntera del nivel objetivo de competencia en las diferentes lenguas. Implementando este modelo, lo máximo que se puede conseguir es una medida rápida y lo suficientemente puntera del nivel de competencia subjetivo que se atribuye cada sujeto a sí mismo, pues es con los datos con los que se contaba inicialmente. Para conseguir los objetivos iniciales, las futuras líneas de investigación deberían elaborar un modelo similar que pudiese ser entrenado con los niveles de competencia reales, esto es, los valores objetivos estimados con otros tests. 

## Problema 2

### Objetivos

El segundo problema que el Proyecto M0ISES intentó resolver fue el de crear un modelo capaz de clasificar las oraciones de cada ensayo como semánticamente correctas o incorrectas. 

En psicolingüística, existen algunas medidas objetivas y electrofisiológicas que sirven de indicadores de la integración semántica. Dentro de la técnica de electroencefalografía (EEG), existe el potencial evocado "N400". Este potencial es una onda negativa respecto a la línea base de medidas encefalográficas, que aparece a los 400 milisegundos de haber leído o escuchado una palabra semánticamente incongruente dentro de una oración [(Kutas y Federmeier, 2014)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4052444/). Esta se considera una medida objetiva de lo que el sujeto interpreta en su procesamiento, incluso se ha observado que este potencial aparece en sujetos que están aprendiendo una lengua y aún no saben responder si la oración es semánticamente congruente o no [(Ousterhout et al., 2006)](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-9922.2006.00361.x\). 

Con los datos del presente estudio, es posible configurar un modelo que clasifique las oraciones en correctas o incorrectas, atendiendo entre otras variables al tiempo de lectura. Una prueba T de Student para medidas independientes encontró que el tiempo de lectura es significativamente diferente para los ensayos donde se lee una oración correcta y los ensayos donde se lee una oración incorrecta (t=4,187, p<0,001). En la gráfica inferior se presentan las medias en tiempo de lectura para esas dos condiciones. Las variables de exposición, uso, preferencia de lectura y nivel de competencia en cada lengua pueden ayudar a perfilar los tiempos de lectura según la destreza en la lengua, así como las variables que indican el grupo y el orden de las tareas.

![image](https://user-images.githubusercontent.com/94480051/175783300-90061a9f-0cae-480f-9cf6-d54ab39d7117.png)

Conseguir que este modelo emplee dichas medidas para clasificar en coherencia o incoherencia semántica podría significar un paso más en la búsqueda de otra medida objetiva de la congruencia semántica, esta vez incluyendo tiempos de lectura. Una herramienta como esta sería extremadamente útil apra apoyar la investigación en el procesamiento semántico en tanto que medir el tiempo de lectura es mucho más rápido y menos costoso que emplear medidas electrofisiológicas.

### Construcción del modelo

Para tratar de alcanzar dichos objetivos, se construyó una red neuronal profunda con la intención de que clasificase los ensayos según la versión en que se presentaba la oración. A continuación se muestra un registro de todos los intentos al crear dicho modelo:

imagenes intentos

Finalmente, el modelo elegido fue un modelo secuencial con un total de 1450 neuronas densamente conectadas, divididas en 14 capas. Cada dos capas, se introdujo un dropout del 20% de neuronas para reducir el riesgo de overfitting del modelo. En la ilustración siguiente se representa dicho modelo neuronal.

![representacion modelo 2](https://user-images.githubusercontent.com/94480051/175924823-89f7444e-ed89-4df6-a922-ae0192c10e9b.png)

La activación de todas las capas fue reLU, menos la última capa que tenía dos neuronas con activación softmax puesto que debía realizar una predicción multi-clase. Este modelo se entrenó con un tamaño de batch de 40 ejemplos, en 400 epochs, con el optimizador Adam, y obtuvo una precisión de aproximadamente 0,88. En la gráfica siguiente se puede observar el aumento de la accuracy a lo largo de los epochs.

![image](https://user-images.githubusercontent.com/94480051/175784549-5c7656d2-505f-4558-876f-bca116a089f8.png)

A continuación se muestra también la reducción de la función de pérdida, en Binary Cross-Entropy.

![image](https://user-images.githubusercontent.com/94480051/175784554-963d7636-7aa0-4f28-a845-fa334f0e0b67.png)

El ajuste del modelo a los valores reales se puede observar en la siguiente matriz de confusión:

![image](https://user-images.githubusercontent.com/94480051/175784560-2cad1f7d-3b6a-4bbb-a90c-9683b30b5858.png)

### Prediciendo ilusiones

Una pregunta adicional que surgió creando este modelo, en línea con los objetivos iniciales, fue ver que clasificación haría el modelo sobre aquellos ensayos en los que había habido ilusiones semánticas. Esos ensayos fueron eliminados inicialmente del dataset durante la limpieza, puesto que eran ensayos en los que los sujetos no habían respondido correctamente: presentar la ilusión semántica significa detectar una oración incorrecta como correcta. 

Sobre esos datos, que fueron un total de 501 ensayos, el modelo construido y testeado tuvo una precisión de aproximadamente 0,41. La gráfica siguiente representa la matriz de confusión para esos datos:

![image](https://user-images.githubusercontent.com/94480051/175784636-64dab375-e5db-44c6-86ee-bcfad3ad2d03.png)

### Interpretación

Al construir un modelo que clasificase los ensayos según si la frase leída era correcta o incorrecta, se consiguió una precisión del 0,88. Esta capacidad de clasificación es bastante alta, más que la precisión que se obtendría de una clasificación al azar. Al observar la matriz de confusión, se observa que hay bastantes más casos de clasificaciones correctas que incorrectas. Sin embargo, el modelo parece más preciso a la hora de clasificar ensayos con oraciones correctas como correctas que a la hora de discriminar oraciones incorrectas como incorrectas. También cabe considerar que había ligeramente más ensayos con oraciones correctas (53% de todos los ensayos) que incorrectas (47%) en el dataset empleado para testear el modelo, por lo cual esto podría explicar que haya más casos de clasificación correcta de oraciones correctas en contraste con oraciones incorrectas. En cualquier caso, es un modelo con un rendimiento lo suficientemente adecuado como para extraer conclusiones. 

Más aún, es posible emplear este modelo para intentar clasificar aquellos ensayos en los que los sujetos presentan ilusiones semánticas, esto es, confunden oraciones incorrectas como correctas. A la hora de clasificar estos ensayos, el modelo tiene una precisión menor que la que se esperaría por azar, por lo que no es adecuado para predecir si los ítems son correctos o incorrectos semánticamente. Esto significa que el ítem leído, el tiempo de lectura del sujeto, sus variables sociolingüísticas en la lengua en la que se lee, y otras variables que discriminan el grupo al que pertenece el sujeto no sirven para estimar la congruencia semántica real. El modelo tampoco se equivoca de la misma forma que lo hacen los sujetos, porque en ese caso esperaríamos que clasificase los ensayos con ilusiones como 'correctos', que es lo que interpretan los participantes, y esto ocurre para la mayoría de los ensayos pero definitivamente no para todos. 

En vista de estos resultados, podemos decir que hemos alcanzado un modelo que clasifica satisfactoriamente los ensayos en oraciones correctas e incorrectas. El hecho de que se equivoque para los ensayos que contienen ilusiones semánticas no se debe confundir con que el modelo esté simulando el procesamiento humano, pues en este modelo la entrada de datos es muy diferente a la entrada de datos que obtienen los humanos cuando procesan oraciones. La unica conclusión que se puede extraer es que integrando el número de ítem presentado, la lengua en que se muestra, algunas variables sociolingüísticas y de condición experimental, y el tiempo de lectura de la oración, el modelo se confunde ante casos de ilusiones semanticas. Además, este es un modelo que por el momento tampoco puede servir de medida objetiva de integracion semantic al nivel que lo hace el potencial evocado N400, puesto que para ese objetivo, modelos más extensos que contasen unicamente con el tiempo de lectura de la oracion deberian ser entrenados. Sin embargo, dados los resultados obtenidos, está bien encaminado para alcanzar ese objetivo. 

## Conclusión general

El Proyecto M0ISES aborda dos problemas dentro del campo de la psicolingüística. Por un lado, intenta conseguir una medida rápida y eficiente del nivel de competencia en una lengua mediante una red neuronal de predicción que obtiene este valor teniendo en cuenta variables como el tiempo de lectura de una oración y otras variables sociolingüísticas. Por otro lado, trata de obtener un clasificador entrenando una red neuronal en distinguir ensayos de lectura de oraciones correctas e incorrectas, y comprueba su eficacia al clasificar los ensayos en los que los participantes producen ilusiones semánticas. 

Aunque el rendimiento de los modelos para cada uno de estos dos problemas haya sido adecuado y las conclusiones estén en línea con los resultados esperados, los objetivos iniciales fueron demasiado ambiciosos como para poder resolverse de una forma tan simple. Mucha más investigación y experimentación haría falta para poder darles respuesta. Por suerte, el proceso de construcción de estos problemas ha sido lo suficientemente laborioso y motivador como para continuar explorando el nexo entre psicolingüística y aprendizaje automático. Es evidente que de estas dos disciplinas se pueden obtener los resultados más innovadores y avanzados para desvelar qué ocurre durante el procesamiento del lenguaje, por lo que es imperativo continuar progresando en esta dirección.



> Este es un proyecto creado por Ana M. Bautista Martín. Para más información, [contactar](mailto:anambautistamartin@gmail.com) con la autora. 
