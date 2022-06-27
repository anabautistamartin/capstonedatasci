
# Proyecto M0ISES

## Organización del repositorio

En este repositorio de GitHub se encuentran todos los ficheros empleados al llevar a cabo el Proyecto M0ISES:
- Los datasets: [M0ISES](https://github.com/anabautistamartin/capstonedatasci/files/8990332/M0ISES.csv) y [M0ISESILLUSION](https://github.com/anabautistamartin/capstonedatasci/files/8990333/M0ISESILLUSION.csv).
- Los scripts de los modelos: [Problema 1](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/Problema%201.ipynb) y [Problema 2](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/Problema%202.ipynb).
- Este fichero [README](https://github.com/anabautistamartin/capstonedatasci/edit/gh-pages/README.md), y los ficheros [index](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/index.md) y [config](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/_config.yml) para soportar la página de GitHub, y el fichero [environment](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/environment.yaml) para trabajar en el mismo contexto de desarrollo de este código. 

## Requerimientos

El código del Proyecto M0ISES fue creado desde Python 3.8.8. Se necesita esta versión de Python (o posteriores) para ejecutar el código que se incluye en este repositorio. Se puede crear y activar un entorno apropiado para ejecutar el código con:

```
conda env create -f environment.yaml python=3.8
conda activate contextmoses
```

## Datos

El Proyecto M0ISES se basa en dos datasets, que se pueden descargar en los siguientes enlaces.

Dataset | Tamaño | Tipo | Descarga
--- | :---: | :---: | :---:
M0ISES | 355 KB | CSV | [Descargar](https://github.com/anabautistamartin/capstonedatasci/files/8990332/M0ISES.csv)
M0ISESILLUSION | 21 KB | CSV | [Descargar](https://github.com/anabautistamartin/capstonedatasci/files/8990333/M0ISESILLUSION.csv)

Además, cada problema contiene el código necesario para abrir y usar estos ficheros. 

## Modelos

El **Problema 1** implementa un modelo que trata de predecir el nivel de competencia lingüística del sujeto que realiza cada ensayo. Este modelo fue creado desde Jupyter Notebooks y su script se encuentra bajo el nombre ['Problema 1'](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/Problema%201.ipynb). Para activar este modelo es necesaria la versión Python 3.8.8.

El **Problema 2** implementa un modelo que trata de clasificar la oración de cada ensayo como 'Correcta' o 'Incorrecta'. Este modelo fue creado desde Jupyter Notebooks y su script se encuentra bajo el nombre ['Problema 2'](https://github.com/anabautistamartin/capstonedatasci/blob/gh-pages/Problema%202.ipynb). Para activar este modelo es necesaria la versión Python 3.8.8.


##  Confidencialidad

Los datos que se usan en este proyecto provienen de una [investigación](https://moises-bilingue.webflow.io) que cumplió con los requisitos de ética y protección de datos. Todos los sujetos eran adultos sanos y las técnicas que se emplearon para la recogida de datos fueron no invasivas. La participación fue completamente voluntaria y los individuos que participaron en el experimento proporcionaron consentimiento informado para que sus datos se tratasen anónimamente.
