##Saludos

*Angel Pablo Hinojosa*

www.psicobyte.con

@psicobyte_

*Oficina de software libre de la UGR*

osl.ugr.es

@OSLUGR


##Instalar git

###Con tu gestor de paquetes favorito

`sudo aptitude install git`

###O descargándolo de

[http://git-scm.com/downloads](http://git-scm.com/downloads)


##Crear repositorio en la web de github

Clic. clic, clic

(No olvidemos licencia y readme.md)


##Configuración mínima

`git config --global user.name "Usuario"`

`git config --global user.email "Correo"`


##Claves SSH

`ssh-keygen -t rsa`


##Clonar un repositorio en local

`git clone REPOSITORIO`

`git clone https://github.com/oslugr/repo-ejemplo.git`


##Trabajando

Perpara archivo

`git add ARCHIVO`

`git add DIRECTORIO`

`git add A*`

`git add .`

Guarda archivo

`git commit`

Ver estado

`git status`


##Sincronizando

Recibir del repositorio remoto:

`git pull REPOSITORIO_REMOTO RAMA`

`git pull origin master`

`git pull`

Enviar al repositorio remoto:

`git push REPOSITORIO_REMOTO RAMA`

`git push origin master`

`git push`


##Gracias

© 2014 Angel Pablo Hinojosa

Esta presentación se distribuye bajo una licencia libre
*CC By SA*

(puede descargarse de http://www.psicobyte.com/info/descargas)
