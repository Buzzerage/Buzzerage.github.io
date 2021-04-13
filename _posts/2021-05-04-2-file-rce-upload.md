---
title: File Upload to Remote Code Execution (PHP)
author: Buzzerage
date: 2021-04-05 11:33:00 +0800
categories: [Utilities]
tags: [File Upload, Hacking, Shell, Truco, RCE, Commandos]
math: true
---

Para cuando nos encontremos una vulnerabilidad en la cual se puedan subir ficheros en un servidor y este pueda interpretar código en PHP, he construido un fichero con una interfaz para poder pasar a ejecutar comandos desde el lado del servidor de una forma más sencilla y fácil. El fichero se puede encontrar en el siguiente repositorio:

<https://github.com/Buzzerage/rce_shell/blob/main/gekkshell_rce.php>

Se mostraria la siguiente pàgina si se consigue subir el archivo y acceder a la ubicación del mismo:

![gekkshell_image]({{ "/assets/img/img1.png" | relative_url }})