##Ramas y cómo trabajar con ellas.
 
Crea una rama:
git branch Nombre-De-La-Rama
 
Nos movemos a una rama:
git checkout Nombre-De-La-Rama
 
Nos movemos a la rama principal:
git checkout master
 
Crea una rama y nos movemos a ella:
git checkout -b Nombre-De-La-Rama
 
¿En qué rama estoy?
git branch
 
Borra una rama:
git branch -d Nombre-De-La-Rama
 
Mezcla una rama con aquella en la que estés:
git merge Nombre-De-La-Otra-Rama
 
¡Conflicto entre ramas! ¿Qué hacemos?
Git informa detalladamente del problema y 
debemos arreglarlo nosotros mismos y hacer un 
commit.
