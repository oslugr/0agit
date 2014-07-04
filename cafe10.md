## Etiquetas y nuevas versiones

>Este texto está adaptado del [curso de Git de Pablo Hinojosa y mío](https://github.com/oslugr/curso-git) e incluido en el [libro Aprende Git](https://www.amazon.es/dp/B00K515GL2?tag=atalaya-21&camp=3634&creative=24822&linkCode=as4&creativeASIN=B00K515GL2&adid=0KR8Z3QJ5H6G7M1AZQZ2&), que puedes adquirir en Amazon por menos de un euro. 

Una *etiqueta* permite *guardar* el estado del repositorio en un
momento determinado, siendo como una especie de *foto* del estado el
proyecto. Se suele asociar a hitos en la historia del mismo: entrada
en producción, despliegue de los resultados, o versión mayor o menor. 

Para [etiquetar](http://git-scm.com/book/en/Git-Basics-Tagging) se usa
la orden `tag`

	git tag v0.0.2
	
`tag` etiqueta o añade metainformación al último *commit*, es decir, asigna una cadena adicional al
estado en el que estaba el respositorio tras el último commit. La
etiqueta aparecerá de forma inmediata (sin necesidad de hacer *push*),
puesto que se añade al último commit y se puede listar con

```
git tag
jmerelo@penny:~/txt/docencia/repo-tutoriales/repo-ejemplo$ git tag
v0.0.1
v0.0.2
```

![La etiqueta se muestra adosada a un commit](img/tag.png)

Como se ve, una etiqueta es, en realidad, un apodo o *alias* para un commit
determinado cuyo *hash* puede ser difícil de recordar. Pero por esa
misma razón se pueden usar como salvaguarda del estado del repositorio
en un momento preciso que, más adelante, se puede recuperar o
fusionar con una rama.

Las ramas se pueden también anotar, lo que añade una explicación
adicional a lo que ya esté almacenado en el commit correspondiente. 
	
	git tag -a v0.0.2.1

abrirá un editor (el que tengamos especificado por defecto) para
añadir una anotación a esta etiqueta, lo que nos podemos ahorrar si
usamos (siguiendo el mismo formato de los commits)

	git tag -a v0.0.2.1 -m "Estado estacionario del repositorio"
	
por ejemplo. Esta información aparecerá añadida al commit
correspondiente (el último que hayamos hecho) cuando hagamos, por
ejemplo, `git show v0.0.2.1` 

```
tag v0.0.2.1
Tagger: JJ Merelo <jjmerelo@gmail.com>
Date:   Sun Apr 6 09:58:12 2014 +0200
Poco antes de pasar a producción el tema de tags
en realidad, sólo es un ejemplo
commit b958b16b8261fa3ca8159b3ae45e237ae1fa1dce
Author: JJ Merelo <jjmerelo@gmail.com>
Date:   Sun Apr 6 09:45:38 2014 +0200
    Añadido de nuevos ficheros al servidor
    Y edición del README para que sirva para algo
```

(Suprimidos espacios en blanco para que aparezca como un sólo
mensaje). Que, como se ve, añade un pequeño mensaje (al principio) al
propio del commit (a continuación). 

Finalmente, `git describe` es una orden creada precisamente para
trabajar con las etiquetas: te indica el camino que va desde la última
etiqueta al commit actual o al que se le indique

```
git describe
v0.0.2.1-1-g6dd7a8c
```

que, de una forma un tanto críptica, indica que a partir de la
etiqueta `v0.0.2.1` hay un commit `-1-` y el nombre del último objeto,
en este caso el único `6dd7a8c`. Es otra forma de
[*etiquetar* un punto en la historia de una rama](http://gitfu.wordpress.com/2008/05/25/git-describe-great-another-way-to-refer-to-commits/),
o simplemente otra 
forma de llamar a un commit. Es más descriptivo que simplemente el
hash de un commit en el sentido que te indica de qué etiqueta has
partido y lo lejos que estás de ella.

Por eso precisamente conviene, como una buena práctica, etiquetar la
rama principal con estas *ramas ligeras* cuando suceda un hito
importante en el desarrollo (una fusión de rama, incorporación de alguna característica, fin de un *sprint*). Y también conviene recordar que, dado que
son anotaciones locales,
[hay que hacer explícitamente `git push --tags`](http://alblue.bandlem.com/2011/04/git-tip-of-week-tags.html)
para que se comuniquen al repositorio remoto. 

## Listo para el lanzamiento: publicación en GitHub

GitHub, como cualquier otro repositorio git, permite usar una rama específica para depositar las versiones descargables; una forma de hacerlo, por ejemplo, es usar la rama `gh-pages` para no mezclarlo con el resto de los ficheros que están en el repositorio y, por tanto, versionados. Sin embargo, no es una buena idea poner ficheros binarios bajo control de git, porque es muy fácil provocar conflictos con ellos y no tan fácil resolverlos (o es un fichero o es otro, los algoritmos de diferencias de texto no trabajan sobre ficheros que no sean binarios); además, en general, estos ficheros se generan a partir del fuente de una forma más o menos automática: usando `Makefiles`, por ejemplo, en C, o en general compilando; si se trata de paquetes, cada lenguaje tiene mecanismos específicos para crearlos a partir de los fuentes, por lo tanto no es necesario colocar tales ficheros en el repositorio. Por eso es mejor colocarlos *fuera* del repositorio, y es lo que hace GitHub, en un apartado llamado *archivos*.

Crear un lanzamiento es fácil en GitHub: simplemente se crea una etiqueta como se ha visto anteriormente, con `git tag`. Por ejemplo, [este es el fichero correspondiente a la etiqueta `v0.0.1` que se definió en el repositorio de ejemplo](https://github.com/oslugr/repo-ejemplo/releases/tag/v0.0.1). Al pinchar en [*Releases*](https://github.com/oslugr/repo-ejemplo/releases) te aparecen las versiones que ya has creado o un botón con *Draft a new release* para crear una nueva.

Desde este interfaz web se puede añadir alguna información más que desde la línea de comandos: se puede crear la etiqueta si no existe y se pueden añadir imágenes, ficheros binarios generados de cualquier otra forma (o automáticamente) y, en general, lo que uno desee. También se puede marcar como *pre-release* y [darle un título como a las versiones de Ubuntu, con animalitos o nombres de días de la semana o lo que sea](https://github.com/oslugr/repo-ejemplo/releases/tag/v0.0.3). 

En general, si no se usa ningún repositorio de módulos o aplicaciones para publicar la aplicación, o simplemente se quiere publicar junto con los fuentes, manuales y lo que se desee, es conveniente usar esta característica de GitHub para mantener un archivo de versiones descargables de la misma y también para que puedan acceder a ella fácilmente quienes no quieran usar `git` para descargársela.

>Vais a decir que ya podían instalarse `git` y demás herramientas necesarias para compilar o ejecutar la aplicación, pero en muchos casos no tiene por qué ser fácil o factible; no se va a instalar uno un compilador de `fortran` simplemente para compilar una aplicación nuestra, por ejemplo. 

