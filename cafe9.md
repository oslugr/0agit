##Obtener Ayuda

`git help`

`git help COMANDO`

`git help commit`

##Viendo el historial

`git log`

`git log -4`

`git log --graph --oneline` 

especial:

`git log --all`

##Deshacer cambios en un archivo (recuperar el del HEAD)

`git checkout -- NOMBRE_DEL_ARCHIVO`

##Retrocediendo al pasado

**DANGER**

retorna el head a un estado anterior

`git reset --hard HASH_DEL_COMMIT_A_RECUPERAR`


retorna el head y el directorio de trabajo a un estado anterior

`git reset --hard HASH_DEL_COMMIT_A_RECUPERAR`


##Viendo (y recuperando) archivos antiguos

Puedes ver los cambios que hiciste en un commit si haces 

`git show HASH_DE_UN_COMMIT`

`git show HASH_DE_UN_COMMIT:ruta/a/un/archivo` mostrará el estado de ese archivo en aquel commit.

Esto nos va a servir para hacer un pequeño truco:

`git show HASH_DE_UN_COMMIT:ruta/a/un/archivo > archivo_copia`

