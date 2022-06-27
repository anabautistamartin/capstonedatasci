
# PROYECTO M0ISES: Where Psycholinguistics and Machine Learning Meet

En esta página encontrarás toda la información sobre el Proyecto M0ISES, un proyecto que reúne los avances en Psicolingüística y Machine Learning para alcanzar soluciones prácticas e innovadoras en el estudio del procesamiento del lenguaje. 

## Introducción

Hace tan solo unos años que las grandes preguntas de la ciencia cognitiva y el lenguaje han empezado a responderse gracias a las nuevas tecnologías de aprendizaje automático. Dentro de la psicolingüística, la ciencia que estudia los mecanismos cognitivos del procesamiento del lenguaje, existen múltiples cuestiones abiertas que actualmente pueden emplear modelos de Machine Learning para fines tan útiles como simular el procesamiento humano. Además, las herramientas de predicción que proporcionan estos modelos pueden emplearse para crear herramientas increíblemente precisas a la hora de evaluar a sujetos en este tipo de investigaciones.

El presente proyecto se dirige a tratar de resolver dos problemas principales dentro de la psicolingüística empleando las técnicas de aprendizaje automático. Estas cuestiones emergen de una interesante [investigación sobre la ilusion de Moisés](https://moises-bilingue.webflow.io/). En la ilusión de Moisés, ante oraciones como *"Según se dice en la Biblia, Moisés llevó dos animales de cada tipo en el arca"*, pocos individuos son capaces de reconocer el error y generan una falsa ilusión de coherencia semántica. Estas ilusiones son sumamente interesantes para este campo porque revelan un error sistemático de nuestro sistema cognitivo a la hora de integrar la información semántica. En la investigación mencionada anteriormente, se presentaban este tipo de oraciones en castellano y en catalán a hablantes bilingües de estas dos lenguas, y se les pedía responder si eran correctas o incorrectas. Además, se recogía información sobre el tiempo de lectura de la oración y otras variables sociolingüísticas que indicaban la destreza que tenían los sujetos en cada lengua. Esta investigacion y sus resultados fueron la base del proyecto que se presenta en este repositorio. 

## Datos

Primero, se recogieron los resultados de todos los ensayos llevados a cabo en la investigación. Dichos resultados provienen de 43 sujetos bilingües de castellano y catalán (66% mujeres, edad media = 22,70), y 35 sujetos que no conocían el catalán pero eran hablantes nativos de castellano (70% mujeres, edad media = 22,86). El grupo bilingüe leyó y respondió a un total de 146 oraciones, la mitad en castellano y la otra mitad en catalán. El grupo que no conocía el catalán respondió solo a 73 oraciones, todas en castellano. Este último grupo servía de control, para comparar el rendimiento del grupo bilingüe en la tarea en castellano. 

La limpieza de los datos se realizó en una plataforma externa siguiendo el criterio siguiente: 
- Eliminación de ensayos en los que los participantes no conocían la respuesta correcta a la oración.
- Eliminación de ensayos en los que los sujetos respondían incorrectamente.
- Eliminación de ensayos en los que el tiempo de lectura era mayor o menor que la media en tres desviaciones típicas (MEAN±3SD).

De esta forma, se descartaron los ensayos que no correspondían una integración semántica adecuada por parte de los sujetos. 
Esto supuso la pérdida de aproximadamente un 0,10% de los ensayos iniciales, quedando una nube de datos de **7525 unidades de ensayos**. Esta base de datos está disponible en el repositorio de GitHub bajo el nombre ['M0ISES'](https://github.com/anabautistamartin/capstonedatasci/files/8990332/M0ISES.csv).

Cada ensayo del experimento, o cada línea de la base de datos, incluye las variables indicadas en la siguiente tabla:

Variable | Nombre | Descripción
--- | :---: | :---: | :---:
**Versión de la oración**  | version | Corresponde a la versión de la oración presentada al sujeto, en tanto que cada ítem se podía presentar a los sujetos en su versión correcta o incorrecta. '0' indica la versión incorrecta (e.g., *"Según se dice en la Biblia, Moisés llevó dos animales de cada tipo en el arca"*), y '1' indica la versión correcta (e.g., *"Según se dice en la Biblia, Noé llevó dos animales de cada tipo en el arca"*). 
**Ítem**  | item | Indica el número de ítem leído en el ensayo, de un listado de 146 ítems.
**Milisegundos de lectura de la oración** | ms | Indica cuánto tarda el sujeto en ese ensayo en leer el ítem, medido en milisegundos ponderados según la longitud de la oración en número de caracteres. 
 **Lengua** | lang | Corresponde a la lengua en la que se lee la oración, ya que el grupo de sujetos bilingüe hacía la tarea en castellano y en catalán. '0' indica que se lee en castellano, y '1' indica que se lee en catalán.
**Frecuencia de exposición** | expo | Indica, de 0 al 1, la frecuencia con la que los sujetos están expuestos a la lengua en la que leen el ítem. Esto se incluyó con la pregunta "Del 0 al 10, ¿cuánto estás expuesto/a al (castellano/catalán) actualmente?" en el experimento original. 
**Preferencia de lectura** | pref | Corresponde, de 0 a 1, a la preferencia que tienen los sujetos por leer una pieza de información en la lengua en la que leen el ítem. En el experimento, se incluyó bajo la pregunta "Si pudieses leer un texto en cualquiera de las lenguas que conoces, indica del 0 al 10 en qué medida elegirías leerlo en (castellano/catalán)".
**Uso de la lengua** | use | Supone el promedio de respuestas de los sujetos, de 0 a 1, a una serie de preguntas sobre cuánto usan la lengua en la que leen el ítem. Las preguntas preguntaban a los participantes por el porcentaje de uso de cada lengua en situaciones diversas: ambientes familiares, profesionales, ocio, uso de redes sociales, etc.
**Nivel de competencia en la lengua** | profic | Es el promedio de cuánto indican los sujetos que saben hablar, escribir, entender y leer cada lengua. Es una medida subjetiva del nivel de competencia total en la lengua, y su rango es de 0 a 1. 
**Grupo** | grupo | Corresponde al grupo al que pertenecía el sujeto, si era el grupo bilingüe de castellano y catalán ('1'), o si era el grupo nativo de castellano que no conoce el catalán ('0').
**Orden** | orden | Es el orden de los bloques en el experimento para el sujeto que lee la oración, ya que en el grupo bilingüe se contrabalanceó el orden de las tareas. Esta variable indica con un '0' que la primera tarea que recibió el sujeto fue en castellano, y con un '1' que la primera tarea fue en catalán. 
**Condición experimental** | contextlab1 y contextlab2 | Son dos variables dicotómicas que, conjuntamente, indican la condición experimental a la que pertenece el ensayo. 

<p align="center">
<img width="691" alt="image" src="https://user-images.githubusercontent.com/94480051/175779314-e51420a9-9a00-418e-a711-db400cdaa690.png"></p>

## Problema 1

### Objetivos

El primer problema que el Proyecto M0ISES trató de resolver fue el de encontrar un indicador eficaz y objetivo del nivel de competencia de un individuo en una lengua. 

En las investigaciones en psicolingüística, es extremadamente importante conocer el nivel que tienen los participantes en las lenguas que se pretenden estudiar. Sin embargo, pocas veces se puede aplicar un test exhaustivo para obtener un indicador objetivo del nivel de competencia que se tiene en una lengua, ya que normalmente se trata de pruebas largas que interrumpen el curso de los experimentos y que pueden fatigar a los participantes. En consecuencia, usualmente se recurre a preguntar al sujeto cómo se valora a sí mismo en las destrezas de escritura, habla, lectura y escucha para una lengua. Esta medida es considerablemente menos costosa, pero incluye una gran dosis de subjetividad que puede estar distorsionando las repuestas. Por esta razón, en esta rama de estudio se busca una medida objetiva del nivel de competencia en una lengua que sea rápida y fácil de conseguir en situaciones experimentales. 

Es evidente que la velocidad de lectura está relacionada con el nivel de competencia en una lengua: leer en aquellas lenguas en las que uno tiene menos nivel supone un mayor esfuerzo, y por tanto tiempos de lectura más altos. En los datos que se incluyen en este proyecto, el tiempo de lectura también está ligera pero significativamente relacionado con la estimación subjetiva de los sujetos en su nivel de competencia (r=-0,069; p<0,001). Adicionalmente, el nivel de competencia en una lengua tambien está relacionado significativamente con la frecuencia de exposición (r=0,144; p<0,001), la preferencia de lectura (r=0,220; p<0,001) y el uso de la lengua (r=0,270; p<0,001). En las gráficas inferiores se observa cómo, a simple vista, estas variables parecen tener poca relación con el nivel de competencia, pese a tener una correlación significativa estadísticamente. En consecuencia, es posible que todas estas medidas en conjunto sirvieran para conseguir predecir la variable de nivel de competencia de una forma eficaz.

![prob 1](https://user-images.githubusercontent.com/94480051/175990147-2b7e110e-c1ab-45f7-afc0-3ffed8ab6ca1.png)

### Construcción del modelo

De acuerdo con los propósitos descritos anteriormente, se creó una red neuronal profunda con la intención de conseguir predecir el nivel de competencia de los sujetos en la lengua en que realizan los ensayos. Las variables de entrada incluyeron las variables de ítem, versión del ítem, milisegundos de lectura, lengua, frecuencia de exposición, preferencia de lectura, uso de la lengua, grupo, orden y condición experimental. A continuación se presenta un registro de todos los intentos al crear dicha red:

[imagenes registro]

Finalmente, el modelo elegido fue un modelo secuencial con un total de 1723 neuronas densamente conectadas, divididas en 16 capas. Cada dos capas, se añadió un dropout del 20% de neuronas para reducir el riesgo de overfitting del modelo. En la ilustración siguiente se representa dicho modelo neuronal. 

![representacion modelo 1](https://user-images.githubusercontent.com/94480051/175924709-0d5154c5-4001-4d7e-b5c9-cd7c19031c52.png)

La activación de todas las capas fue reLU, menos la última capa que contenía una neurona con activación lineal puesto que debía predecir un valor continuo. Este modelo se entrenó con un tamaño de batch de 40 ejemplos, en 200 epochs, con el optimizador Adam, y obtuvo un error cuadrático medio (MSE) de aproximadamente 0,0008. En la gráfica siguiente se puede observar la reducción de dicho error a lo largo de los epochs:

![reduction mse selected](https://user-images.githubusercontent.com/94480051/175990192-3177eb01-00a0-4bf9-8eec-41c2bffb7313.png)

El error cuadrático medio obtenido es bastante positivo teniendo en cuenta la naturaleza de los datos. Siendo valores de nivel de competencia que oscilan entre 0 y 1, con un máximo de 3 cifras decimales, obtener un error medio aproximado de 0,0008 es bastante aceptable. El ajuste del modelo a los valores reales se puede observar en la siguiente gráfica:

![fitting selected](https://user-images.githubusercontent.com/94480051/175987550-ebb63093-47df-4a08-934b-ec166157ca07.png)

Es importante mencionar que en otro intento a la hora de crear el modelo, el mismo modelo construido bajo las mismas condiciones de entrenamiento, pero sin introducir las variables de exposición, uso y preferencia de lectura en la lengua del ensayo, no consiguió ajustarse tan adecuadamente a los datos. El error cuadrático medio que alcanzó fue de 0,0052, mucho mayor que el que se consigue incluyendo dichas variables. En las siguientes gráficas se observa su reducción en error cuadrático medio y el ajuste a los datos.

![reduction in mse unselected](https://user-images.githubusercontent.com/94480051/175987583-59d1283e-bc8a-4909-9bcb-bd5528ed4fec.png)
![fitting unselected](https://user-images.githubusercontent.com/94480051/175987608-8f353d64-9e90-41b7-ae47-b57680a3b1c5.png)

### Interpretación

Para conseguir predecir el valor en nivel de competencia lingüística que tenían los sujetos que realizaban cada ensayo, se creó una red neuronal que, al introducir los datos que contenía la base de datos inicial, conseguía predecir el valor real con un error cuadrático medio de aproximadamente 0,0008. Esto significa que con la estructura neuronal empleada en este modelo se puede obtener eficazmente el nivel de competencia del sujeto que realiza un ensayo, a raíz de las predicciones que elabora un modelo entrenado con el tiempo de lectura de un ítem concreto, el porcentaje de exposición, uso y preferencia de lectura del sujeto en la lengua en que lee, y otras variables sobre el contexto experimental del ensayo. Además, las variables de exposición, uso y preferencia de lectura tienen una contribución importante sobre esa predicción, puesto que el mismo modelo entrenado sin la entrada de esos valores no consigue una precisión tan considerable.

No obstante, y en línea con la motivación inicial que introducía este problema, los valores que este modelo predice siguen siendo valores subjetivos. El objetivo principal de este problema era encontrar una medida rápida y puntera del nivel objetivo de competencia en las diferentes lenguas. Implementando este modelo, lo máximo que se puede conseguir es una medida rápida y lo suficientemente puntera del nivel de competencia subjetivo que se atribuye cada sujeto a sí mismo, pues es con los datos con los que se contaba inicialmente. Para alcanzar dichos objetivos, las futuras líneas de investigación deberían elaborar un modelo similar que pudiese ser entrenado con los niveles de competencia reales, esto es, los valores objetivos estimados con otros tests. 

Además, se debería aumentar el número de datos con los que se entrena el modelo. En este caso, se ha elaborado un modelo que funciona adecuadamente a la hora de predecir la variable de nivel de competencia. Sin embargo, estos resultados se han obtenido entrenándolo con datos muy limitados de una serie de sujetos específicos. Un modelo más generalizable debería ser capaz de indicar un valor de nivel de competencia con un error cuadrático medio mínimo para cualquier individuo.


## Problema 2

### Objetivos

El segundo problema que el Proyecto M0ISES intentó resolver fue el de crear un modelo capaz de clasificar las oraciones de cada ensayo como semánticamente correctas o incorrectas. 

En psicolingüística, existen algunas medidas objetivas y electrofisiológicas que sirven de indicadores de la integración semántica. Dentro de la técnica de electroencefalografía (EEG), existe el potencial evocado "N400". Este potencial es una onda negativa que se observa sobre algunos electrodos unos 400 milisegundos después de haber leído o escuchado una palabra semánticamente incongruente dentro de una oración [(Kutas y Federmeier, 2014)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4052444/). La onda N400 se considera una medida objetiva de cómo los individuos procesan e integran información semánticamente, e incluso se ha observado en sujetos que están aprendiendo una lengua y aún no saben reconocer la coherencia semántica en esa lengua [(Ousterhout et al., 2006)](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-9922.2006.00361.x\). 

Con los datos del presente estudio, es posible configurar un modelo que clasifique las oraciones en correctas o incorrectas, atendiendo entre otras variables al tiempo de lectura. Una prueba T de Student para medidas independientes encontró que el tiempo de lectura es significativamente diferente para los ensayos donde se lee una oración correcta y los ensayos donde se lee una oración incorrecta (t=4,187, p<0,001). En la gráfica inferior se presentan las medias en tiempo de lectura para esas dos condiciones. Adicionalmente, las variables que indican exposición, uso, preferencia de lectura y nivel de competencia en cada lengua pueden ayudar a perfilar los tiempos de lectura según la destreza en la lengua, así como las variables que indican el grupo y el orden de las tareas.

![ms por version](https://user-images.githubusercontent.com/94480051/175992985-9852a22e-d8ad-4950-9a54-9177af990d33.png)

Conseguir que este modelo emplee dichas medidas para clasificar en coherencia o incoherencia semántica podría significar un paso más en la búsqueda de otro estimador objetivo de la congruencia semántica, esta vez incluyendo tiempos de lectura. Una herramienta como esta sería extremadamente útil apra apoyar la investigación en el procesamiento semántico en tanto que sería más rápida y menos costosa que utilizar medidas electrofisiológicas.

### Construcción del modelo

Para tratar de alcanzar dichos objetivos, se construyó una red neuronal profunda con la intención de que clasificase los ensayos según la versión en que se presentaba la oración. A continuación se muestra un registro de todos los intentos al crear dicho modelo:

[imagenes registro]

Finalmente, el modelo elegido fue un modelo secuencial con un total de 1450 neuronas densamente conectadas, divididas en 14 capas. Cada dos capas, se introdujo adicionalmente un dropout del 20% de neuronas para reducir el riesgo de overfitting del modelo. En la ilustración siguiente se representa dicho modelo neuronal.

![representacion modelo 2](https://user-images.githubusercontent.com/94480051/175924823-89f7444e-ed89-4df6-a922-ae0192c10e9b.png)

La activación de todas las capas fue reLU, a excepción de la última capa que contenía dos neuronas con activación softmax puesto que debía realizar una predicción de clasificación multiclase. Este modelo se entrenó con un tamaño de batch de 40 ejemplos, en 400 epochs, con el optimizador Adam, y obtuvo una precisión de aproximadamente 0,88. En la gráfica siguiente se puede observar el aumento de la precisión (i.e., accuracy) del modelo a lo largo de los epochs.

![accuracy](https://user-images.githubusercontent.com/94480051/175993016-c3b5493e-d8cc-4e9e-948c-04e4421f39c9.png)

A continuación se muestra también la reducción de la función de pérdida, en binary cross-entropy ya que se trataba de un problema de clasificación binaria.

![loss](https://user-images.githubusercontent.com/94480051/175993034-dcf400d8-f25e-4590-900a-2954dad4ebed.png)

El ajuste del modelo a los valores reales se puede observar en la siguiente matriz de confusión:

![confusion](https://user-images.githubusercontent.com/94480051/175993070-ef2adbc3-3d53-4aaf-861e-87d1b9e555cd.png)

### Prediciendo ilusiones

Una pregunta adicional que surgió creando este modelo, en línea con los objetivos iniciales, fue ver qué clasificación haría el modelo sobre aquellos ensayos en los que había habido ilusiones semánticas. Esos ensayos fueron eliminados inicialmente del dataset durante la limpieza, puesto que eran oraciones a las que los sujetos no habían respondido correctamente: que se de la ilusión semántica significa detectar una oración incorrecta como correcta. Si el modelo entrenado es útil para predecir la integración semántica, en estos casos debería clasificar los ensayos como si la versión de la oración fuese correcta, puesto que es lo que los participantes han interpretado. En otras palabras, el modelo debería fallar sistemáticamente al clasificar estos ensayos.

Sobre esos datos, que fueron un total de 501 ensayos, el modelo construido y testeado tuvo una precisión de aproximadamente 0,41. La gráfica siguiente representa la matriz de confusión para esos datos:

![confusion illusions](https://user-images.githubusercontent.com/94480051/175993114-62afc39a-dafa-4402-a2cf-201589363528.png)

### Interpretación

Para conseguir obtener un modelo que clasificase ensayos según la congruencia semántica del ítem que se incluía, se construyó un modelo que alcanzó una precisión del 0,88. Esta capacidad de clasificación es bastante alta, más que la precisión que se obtendría de una clasificación al azar. Esto indica que la red neuronal elaborada puede clasificar en versión de ítem 'correcta' e 'incorrecta', con los datos de entrada de número de ítem, tiempo de lectura del ítem, grupo y orden experimental, y otras variables sobre la competencia y experiencia que se tiene con la lengua en que se presenta la oración.

Adicionalmente, este modelo fue implementado para intentar clasificar aquellos ensayos en los que los sujetos presentan ilusiones semánticas, esto es, ensayos en los que confundían oraciones incorrectas como correctas. De acuerdo con las asunciones iniciales, este modelo obtuvo una precisión de 0,44, menor que la que se esperaría por azar. Esto indica que la clasificación que el modelo realiza no se establece sobre la congruencia semántica real, sino sobre la que los participantes elaboran durante su procesamiento. En consecuencia, estos resultados van en línea con que el modelo sirva de medida de la congruencia semántica durante el procesamiento, favoreciendo los objetivos principales. 

Sin embargo, y con el mismo argumento que la reflexión sobre el primer problema, para que este modelo funcionase mejor, debería entrenarse con una base de datos con más ensayos y con casos de integración semántica más variados. Los resultados son positivos e indican que un modelo en esta línea podría cumplir los objetivos descritos anteriormente: podría convertirse en una medida más eficiente de la integración semántica que realizan los individuos en su procesamiento. Aunque dados los resultados obtenidos se puede deducir que este modelo está en buena dirección, es necesario elaborar más este dominio para conseguir unas predicciones más precisas. 

## Conclusión general

El Proyecto M0ISES aborda dos problemas dentro del campo de la psicolingüística empleando las técnicas de aprendizaje automático. Por un lado, intenta conseguir una medida rápida y eficiente del nivel de competencia en una lengua mediante una red neuronal que predice ese valor teniendo en cuenta variables como el tiempo de lectura de una oración y otros indicadores sociolingüísticos. Por otro lado, trata de obtener un clasificador de integración semántica correcta e incorrecta entrenando otro modelo neuronal, y comprueba su eficacia al clasificar los ensayos en los que los sujetos presentan ilusiones semánticas. 

Pese a ser objetivos ambiciosos, el rendimiento de los modelos para cada uno de estos dos problemas fue adecuado y la interpretación que se hizo de los resultados los colocó en línea con los resultados esperados. Para conseguir que estas medidas tan significativas para el campo de la psicolingüística funcionen, es necesaria mucha más investigación y experimentación. Por suerte, el proceso de construcción de estos problemas ha sido lo suficientemente laborioso y motivador como para continuar explorando el nexo entre psicolingüística y aprendizaje automático. En definitiva, es necesario progresar en este ámbito, puesto que es evidente que de estas dos disciplinas se pueden obtener los resultados más innovadores y avanzados para ayudar a descubrir qué ocurre durante el procesamiento del lenguaje. 

> Este es un proyecto creado por Ana M. Bautista Martín. Para más información, [contactar](mailto:anambautistamartin@gmail.com) con la autora. 
