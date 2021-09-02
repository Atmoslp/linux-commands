# linux-commands
 basic linux commands for beginners :)
 
 
 . Conceptos básicos antes de empezar 
 
	- ¿Qué es GNU/Linux?


LINUX (o GNU/LINUX, más correctamente) es un Sistema Operativo como MacOS, DOS o Windows. Es decir, Linux es el software necesario para que tu ordenador te permita utilizar programas como: editores de texto, juegos, navegadores de Internet, etc. Linux puede usarse mediante un interfaz gráfico al igual que Windows o MacOS, pero también puede usarse mediante línea de comandos como DOS.

 Fuente: https://www.ciberaula.com/articulo/que_es_linux/
 
 Podríamos clasificarlo de la siguiente forma:
 
 GNU 		/ 	Linux
 Aplicaciones		Kernel
 
 Kernel: Software que constituye una parte fundamental del sistema operativo, y se define como la parte que se ejecuta en modo privilegiado. En resumen, es el núcleo del sistema.
 Cada distribución de Linux puede utilizar una interfaz gráfica diferente (la manera en que vemos nuestro escritorio y sus aplicaciones)
 
 . Tipos de entornos gráficos
 
	- KDE, GNOME, PLASMA, UNITY
	
. Tipos de sistema de ficheros en Linux

	- EXT2, EXT3, EXT4
	
	
. Extensiones o ejecutables 
	
	- TAR, RPM (OPENSUSE) Y DEB
	
	
	
	
	
Estructura de ficheros en LINUX

<img>https://ayudalinux.com/wp-content/uploads/2017/03/Sistema-de-archivos-de-Linux-2.jpg</img>
	
	
 <b> Primeros pasos </b>
 
 Una vez arrancada nuestra distro de Linux (Ubuntu, Mint, Kali Linux, Debian, etc..) procedemos a actualizar las librerías:
 
 
. apt-get 

	- upgrade
	- update
	- install aptitude (Gestor de paquetes más actual)
	
Ahora podemos usar aptitude search "nombreprograma" para buscar en nuestros repositorios y saber si un paquete está instalado:

. whereis "aptitude" o cualquier otro programa

. apt	
	
	-install
	-show
	-update
	-check → revisa las dependencias
	--purge remove  <fichero/programa> → elimina programa	
	
. aptitude

	-install
	-update
	-search
	-remove 	→ elimina paquete, pero no los archivos de conf.
	-purge		→ quita todo de ese paquete
	

	
. dpkg 

	--status <nombreprograma>
	--info <nombrefichero>
	-i <fichero.deb> instala paquete
	-r 


Todos los comandos que hacen movimiento en el sistema necesitan permisos de administrador. El permiso se lo otorgamos con el comando SUDO.
Para encontrar el fichero de administradores, 

	sudo nano /etc/sudoers
	
	

Red:
Cambiar la configuracion de red dinamica
 ruta /etc/netplan/<fichero.yaml>
network:
  version: 2
  renderer: networkd
  ethernets: 
    enp0s3:
      dhcp4: true
		
aplicamos cambios con 
. netplan apply
Cambiar la configuracion de red estática
 ruta /etc/netplan/<fichero.yaml>
network:
  version: 2
  renderer: networkd
  ethernets: 
    enp0s3:
      addresses: [ip/mascara]
      gateway4: 192.168.1.1
      nameservers:
        search: [redes.plus]
        addresses: [8.8.8.8, 8.8.4.4]
		
. ip 
	ad 	                   → interfaces 
	ro 	                   → puerta de enlace
	route get <ip>        → dónde sale la consulta a esa ip. Es util si hay más de un adp de red 
	neigh show 	       → tabla arp, asocia mac's a ip. Es como un log
	link set <interfaz> → levantar o tirar la interfaz seleccionada
		-down
		-up
	
. ss -ltpan (puertos de escucha)
Usuarios:

. logname (usuario logeado)
. uname (info del so)
. who (Usuarios conectados)
	 -q            → nº de usuarios
     	> fichero  → ficheros con salida de orden
	-su 	     → cambiar usuario

. nano /etc/sudoers (fichero de administradores)

. useradd
	ejemplo useradd tomas

	-d 	→  directorio principal
	-m 	→ crea auto la carpeta de usuario en /home/"nombreusuario"
	-g 	→ grupo princial
	-G 	→ grupos secundarios
	-s	→ shell por defecto /bin/bash
	-tomas → nombre del usuario

(si el grupo no existe, hay que crearlo primero:)
	. groupadd <nombregrupo>

. passwd <usuario> (Cambia la pw del usuario)
	-l 			→ bloquea usuario
	-u			→ desbloquea
	-e			→ fuerza para que caduque la pw
	-n "dias" "usuario"	→ cambia el valor de "minlife"
 

. usermod (para modificar ususario:)
	
	-l <nombrenuevo> <usuario> 	→ cambia nombre
	-c "comentario" <usuario> 	→  establece breve comentario
	-d "directorio" <usuario>	→ cambia directorio de inicio del usuario
	-g "grupo" <usuario>		→ cambia el grupo principal

borrar usuario y su carpeta
. deluser <usuario>
. deluser –remove-home <usuario> (a veces es necesario reiniciar)


saber si un usuario existe
	cat /etc/passwd | grep <usuario>

. usermod (Modifica usuarios y grupos)
 	-g profes pepe 	    → cambio de grupo de pepe a profes
	-d /home profes pepe	-m → cambia directorio inicio de pepe por /home/profes (-m 				        	         mueve el contenido)
	-l juan pepe		     → cambia nombre a pepe por juan
	-u <numero> <usuario>  → cambia uid
	

. groups <usuario> (para ver los grupos del usuario)
. groupdel <grupo> (debe estar vacio o no ser el principal de ningún user)

Cambiar el UID Y GID del usuario, primero comprobamos id del usuario
. id <usuario>

Basicos:

. man <comando> (ayuda)
. date (fecha)
. cal (calendario)
. history (historial de comandos pasados)
. ln (Crear enlaces)
	-s simbólico (si lo borras el original sigue estando)
	-d duro (lo que hagas en uno pasará en todos)
. ls  (Lista el contenido de los directorios)
	-l  	  → detalles
	-i 	  → nº inodo
	[!a]*	  → que no empiecen por "a"
	[m,o]*   → que empiecen por "m" u "o" 
	*a 	  → que terminen en "a"
	a*	  → que empiecen por "a"
	*a*	  → que contengan "a"
	tty???    → empiece por "tty" y tenga 6 caracteres
   	c*[m,o] → empiece por "c"y terminen en "m" u "o"


. mkdir (Crear carpeta)
. rmdir (Borrar carpeta vacía, usar rm en otro caso)
. touch (Crear fichero)
. rm (Borrar archivos)
	-i 	→ pregunta antes de borrar
	-r	→ recursivo todo lo que encuentre
	-f 	→ no pregunta
	-d 	→ elimina directorios vacios
. cat (Leer texto plano)
	-n	 → nº lineas

. wc (Cuenta)
	-w 	→ palabras
	-l  	→ letras
	-c 	→ caracteres


. grep (Busca cadena )
	-i 	→ no importa mayúsculas
	-n 	→ nº de línea donde se encontró
	-v 	→ muestra líneas donde no está esa cadena
	^a 	→ líneas que empiecen por "a"
	a$	→ líneas que terminen en "a"

. cut (Extracción de segmentos)
	-d 	 → separador
	-f	 → campo 
	-c 	 → caracter
. sort (Ordena)
	-t	→ separador
	-k1,k2	→ campos
	-f	→ mayúsculas iguales
	-n	→ ordena por valor numérico
	-r	→ invertido
. cp (Copia)
	-f	→ sobreescribe si existen
	-r	→ recursivo, copia directorios y sus archivos

. mv (mover ficheros de un lugar a otro, o cambiar nombre)
	-mv ./carpeta1/fichero1.txt ./carpeta2 → mueve fichero a la carpeta2 sin cambiar nombre
	-mv ./probando ./repasando → cambia nombre a carpeta "probando" por "repasando"

. find  (Busca)
	-iname	→ nombre de archivo
	-type	→ tipo de archivos
                       -d        → directorio
		-f        → fichero

	-size +x → tamaño de bloque
	-c	  → caracteres
	-exec 	  → usar tubería "comando" {} \;


	-follow  → -inum "numero" --> busca archivos con ese número
. tr (Substituye palabras o espacios)
	-d	→ borra
	-s 	→ espacios repetidos o "largos"
. tee (Vuelca la info a uno o más archivos)
	-a	→ inserta los datos al final
. tail (Últimas líneas del fichero)
	-n 	→ muestra las "n" últimas líneas del ficheros
	+"numero" → a partir de la línea "numero"
. tar (descomprimir ficheros .gz)
- czvf → empaquetado.tar.gz /carpeta/a/empaquetar/ 
- xzvf → archivo.tar.gz , descomprimir

. more (Paginado)
- nl → muestra un fichero con sus líneas numeradas


Sistema:

. blkid (Información del disco UUID)
. top (Procesos en tiempo real)
. df (Espacio libre y ocupado de particiones)
	-i  	→ punto de montaje, nº inodos
	-v 	→ punto de montaje, nº de bloques
	-h 	→ info en megas
. du (Espacio libre y ocupado de directorio)
	-a 	→ recursiva
	-s 	→ simple
	-h	 → info en megas
. mkfs (Construye nuevo sistema de ficheros en el dispositivo indicado)
	-v	 → muestra lo que se va haciendo
	-t 	→ formatea
	(ejemplo: mkfs -v -t ext4 /dev/sdb)
		
. fsck (Chequea sistema de ficheros estando desmontado)
. fdisk (Crea particiones)
. uname (Conocer el kernel)


Procesos:
. ps (Procesos) 
	-e → todos los procesos
	-a → de otros usuarios
	-u → uso de memoria, cpu...
. jobs (Procesos en segundo plano)
. sleep (Espera un número específico antes de ejecutar el comando)
. fg (Pasa comandos a primer plano)
	


	
	
	
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
