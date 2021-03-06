---
title: Conseguir una TTY Shell interactiva
author: Buzzerage
date: 2020-11-22 11:33:00 +0800
categories: [Tutorials]
tags: [Pentesting, Hacking, Shell, Truco, Terminal, TTY]
math: true
---

En este tutorial veremos como conseguir una terminal TTY totalmente interactiva una vez se ha conseguido hacer una *reverse shell* con *netcat*.

Conseguir esta terminal nos dará muchas facilidades a la hora de introducir comandos y nos asegurará que sin querer la cerremos con un **Ctrl+C**, evitando que tengamos que repetir todo el proceso de obtener la *reverse shell*.

Partiremos sobre un escenario donde se ha conseguido obtener control de una shell escuchando con el comando `nc -nlvp 4444`:


Con el anterior escenario, procederemos a introducir el siguiente comando:

```shell
python -c 'import pty; pty.spawn("/bin/bash")'
```

Puede darse el caso en que la máquina en cuestión no tenga python. En este caso podemos optar por utilizar el siguiente comando, el cual es el que más suelo utilizar:

```shell
script /dev/null -c bash
```


A continuación pondremos la terminal de la escucha en segundo plano:
```terminal
[Ctrl+Z]
```
Con el shell aún en segundo plano, ahora configuraremos el STTY actual para que escriba sin procesar y decirle que repita los caracteres de entrada con el siguiente comando:

```terminal
stty raw -echo
fg
[INTRO]
```

Con `fg` se volverá a abrir la *reverse shell*, pero el formateo estará desactivado. Al presionar el *'INTRO'* ya debería verse normal nuevamente.

El último paso es configurar la shell con algunos de los parámetros que tenemos en nuestra terminal. Para ver cuáles son las medidas que debemos aplicar, desde nuestra terminal  usaremos el comando `stty -a`. La información que necesitaremos serán los valores de rows y columns que se encuentran en la primera línea. Una vez tenemos anotadas las medidas de la stty procedemos: 

```terminal
export $TERM=xterm
stty rows R columns C
```
Donde R y C serán los mismos valores que teníamos en nuestra terminal.

Con esto ya tendremos nuestra shell TTY totalmente interactiva ^^.