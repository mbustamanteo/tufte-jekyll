---
layout: post
title: 'Ubuntu en Macbook: Missing Operating System'
date: '2011-11-17 02:42:00'
tags:
- ubuntu
---

Cuando instalamos ubuntu en un macbook pro junto a mac os x, algunas veces aparece el error “missing operating system” al tratar de arrancar ubuntu. Eso pasa porque Refit busca el sistema operativo en un lugar incorrecto o piensa que es otro sistema operativo, así que para arreglarlo hay que reescribir la tabla GPT del disco duro.

Los pasos para realizarlo son:

- Instalar Gdisk http://sourceforge.net/projects/gptfdisk/
- Arrancar terminal
- Tipear “sudo gdisk /dev/disk0”, entendiendo que disk0 es nuestro disco duro donde esta la partición de arranque.
- Tipear “r”
- Tipear “p”, debería salir un listado con las particiones
- Tipear “h”, para crear una HMBR.
- Tipear el número de la partición segun el listado. Por ejemplo si en #2 está mac y en #6 esta linux, tipear “2 6”.
- Tipear “y” para poner la partición EFI en primer lugar
- Tipear el código MBR segun el sistema operativo. Para mac usar “AF”, para windows “07” y para linux usar “83”. No poner ninguna partición como bootable.
- Tipear “w”
- Tipear “y” para escribir en el disco duro.

Ahora reiniciar y debería poder arrancar linux al seleccionar la opción en Refit.