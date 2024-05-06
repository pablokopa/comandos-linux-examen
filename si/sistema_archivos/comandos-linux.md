# Unidad 5: Sistema de arquivos
## 1. pwd (Mostrar directorio)
**Muestra el directorio** actual en el que nos encontramos:
```bash
pwd
```

## 2. ls (Mostrar contenido del directorio)
Sirve para **visualizar el contenido** de un directorio:
```bash
ls
```
Para visualizar archivos que **empiecen o acaben por una letra**:
1.  Empieza por la letra **'a'**
2.  Termina por la letra **'o'**
```bash
ls -d a*
ls -d *o
```
Para visualizar archivos que **contengan una letra** (en este caso la 'o'): 
```bash
ls -d *o*
```
Para visualizar archivos que **contengan un número de caracteres** (cada interrogación es un carácter, en este caso 3): 
```bash
ls -d ???
```
Para visualizar archivos que **no empiecen por un carácter** (en este caso la 't'):
```bash
ls –d [^t]*
```
Para visualizar archivos que **de forma inversa**: 
```bash
ls -r
```
Para visualizar archivos que **están ocultos**:
```bash
ls -a
```
Para visualizar archivos **y los de su subdirectorio**:
```bash
ls -R
```
## 3. cd (Cambiar directorio)
Sirve para **cambiar de directorio**:
```bash
cd directorio
```
Para volver al **directorio anterior**:
```bash
cd ..
```
## 4. mkdir (Crear directorio)
Sirve para **crea una carpeta**:
```bash
mkdir Contactos
```
Crea multiples carpetas a la vez (crea Contactos, con las carpetas Clientes y Proovedores dentro, y cada una de estas con las carpetas Pedidos y Facturas dentro). Quedaría la siguiente estructura:
- Contactos
    - Clientes
        - Pedidos
        - Facturas
    - Proovedores
        - Pedidos
        - Facturas
```bash
mkdir -p Contactos / {Clientes, Proveedores} / {Pedidos, Facturas}

mkdir textos/apuntes/resumen
```

Crea directorio con los permisos establecidos según las dos notaciones de chmod.
```bash
mkdir -m
```
## 5. rmdir (Eliminar directorio)
Sirve para **eliminar una carpeta**:
```bash
rmdir veggies3
```
Si se escribe **rm -r** se **elimina la carpeta y su contenido**:
```bash
rm -r veggies3
```
Si se escribe **rm -p** se **elimina una estructura entera si los directorios están vacíos**:
```bash
rm -p veggies3
```
## 6. mv (Mover, renombrar y ocultar directorios)
Sirve para **mover y renombrar directorios**:
En este caso mueve la carpeta **dir1** al directorio **dam1/dir2**, cambiando su nombre de dir1 a dir2:
```bash
mv dir1 dam1/dir2
```
Para mover un directorio sin modificar su nombre su utiliza (mueve **dir3** al directorio **dam1**):
```bash
mv dir3 dam1
```
Para **cambiar el nombre** de una carpeta (cambia el nombre de dir1 a dir2.a, si ya existe un archivo con ese nombre, se sustituirá el contenido del interior):
```bash
mv dir1 dir2.a
```
Para **ocultar un fichero** se cambia el nombre y se pone un punto delante paran ocultarlo:
```bash
mv archivo.txt .archivo.txt
```
## 7. cp (Copiar archivos)
Sirve para **copiar archivos** entre directorios:
```bash
cp archivo_origen directorio_destino/archivo_destino

cp [-if] fichero1 fichero2
```

| Tipo   | Uso                                                                                                            |
| ------ | -------------------------------------------------------------------------------------------------------------- |
| **-i** | Pregunta al usuario si quiere copiar sobre el destino ya existente.                                            |
| **-p** | Al hacer la copia mantiene fecha, hora, propietario y permisos.                                                |
| **-f** | Sobrescribe el destino en caso de existir, pero es necesario tener permiso sobre el directorio en el que está. |
| **-R** | Copia de forma recursiva todo lo que hay en un directorio en el otro.                                          |

## 8. rm (Eliminar archivos)
Sirve para **eliminar un fichero** de un directorio:
```bash
rm archivoejemplo.txt
```
Se pueden **eliminar varios ficheros** a la vez (en este caso 3):
```bash
rm archivoejemplo.txt segundo_archivoejemplo.txt tercer_archivosejemplo.txt
```
**Elimina la carpeta _dam1_ y todo su contenido**:
```bash
rm -r /dam1
``` 

| Tipo   | Uso                                                                                                                                       |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **-i** | Pregunta antes de borrar cada archivo.                                                                                                    |
| **-f** | Fuerza la eliminación de un archivo aunque no tengamos permiso para suprimirlo, pero se debe tener permiso de escritura en el directorio. |

## 9. ln (Links)
### Enlace completo físico
Crea un enlace físico entre fichero1 y fichero2. Por lo tanto, tendrán el mismo número de i-nodo.

```bash
ln fichero1 fichero2
```
Con ***ls -i*** podemos comprobar que los ficheros tienen el mismo número de i-nodo.
### Enlaces simbólicos
El contenido de un enlace simbólico es la ruta correspondiente al archivo o directorio con el que está enlazado.

```bash
ln -s fuente-1 [fuente-2] enlace
```
- ***fuente-1***: Ruta correspondiente al archivo o directorio que va a ser representado por el enlace.
- ***enlace***: Puede ser un directorio existente o un archivo no existente.
Con ***ls -l*** podemos comprobar.
# Unidad 6: Permisos do sistema de arquivos
## chmod (Cambiar permisos)
Formato utilizado:  
- **chmod (quien) (op) (permisos) archivo**
- Ejemplo: ****chmod u=rwx,g+r,o=r fich1****

| Tipo           | Uso                                                                                                                          |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **(quien)**    | Es el código de cada tipo de usuario:<br><br>***u*** Propietario<br>***g*** Grupo<br>***o*** Otros<br>***a*** Todos          |
| **(op)**       | Especifica el código del tipo de operación:<br><br>***+*** Añade permiso<br>***-*** Retira permiso<br>***=*** Asigna permiso |
| **(permisos)** | Especifica el código de permiso de acceso:<br><br>***r*** Lectura<br>***w*** Escritura<br>***x*** Ejecución                  |

## Permisos en octal
**¿Es -rw- r- - r- -  igual a 644 en octal?**
1. Primer guion: indica que es un archivo (una ‘d’ sería un directorio)
2. El resto se se dividen en grupos de 3:
	- **rw-**
	- **r--**
	- **r--**
3. Siempre que hay una letra (r, w, x), se pone el 1 binario, si hay guion se pone un 0 binario.
5. Para cada elemento se asigna un valor en ‘octal’, siguiendo el orden 4-2-1
6. Si el binario es igual a 1 se coge ese número, si es 0 no se coge.
7. Para este ejemplo tenemos:
	- **rw-** → 110 en binario, que pasando al octal sería 4+2+0 = 6
	- **r--** → 100 en binario, que pasando al octal sería 4+0+0 = 4
	- **r--** → 100 en binario, que pasando al octal sería 4+0+0 = 4
9. Lo que quiere decir que se cumple.
10. En este ejemplo, el 6 es el usuario (principal), el 4 del medio es otros usuarios y el último 4 otros grupos (siempre serán los mismos, solo cambian los valores dependiendo de los permisos que queramos dar a cada uno).
11. Los más comunes suelen ser:
	- **700**: rwx --- ---
	- **755**: rwx r-x r-x
	- **644**: rw- r-- r--
## umask (Permisos predeterminados)
Para cada tipo de fichero existe un valor por defecto:
- **777**- Para directorios (todos los permisos)
- **666** - Para archivos (todos los permisos, menos ejecución)
Se invierten los binarios y se pasa a octal de igual manera:

|     |     |     |       |     |
| --- | --- | --- | ----- | --- |
| rwx | rwx | rwx |       |     |
| 111 | 100 | 000 | ----> | 777 |
| 000 | 011 | 111 | ----> | 037 |

# Unidad 7: Gestión de usuarios
## useradd (Añadir usuario)
```bash
useradd [opciones] nombre_usuario

useradd –m alumno1
```

| Tipo                  | Uso                                                                                                                                                                                              |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **-c** comentario     | Para poner un comentario sobre el usuario.                                                                                                                                                       |
| **-d** directorio     | Especificamos la trayectoria absoluta del directorio de conexión (HOME).                                                                                                                         |
| **-m**                | Si el directorio de conexión no existe lo crea. Si se produce un error en la creación del directorio se crea la cuenta, pero no podremos conectarnos a ella debido a la ausencia del directorio. |
| **-g** grupo          | El grupo de usuarios al que se conecta el usuario. Debe existir previamente.                                                                                                                     |
| **-G** grupo1, grupo2 | Otros grupos a los que se añadirá el usuario.                                                                                                                                                    |
| **-s** shell          | Trayectoria absoluta del shell de conexión.                                                                                                                                                      |
## usermod (Modificar usuario)
```bash
sudo usermod [opciones] nombre_usuario

sudo usermod -aG nuevo_grupo nuevo_usuario (Añadir usuario a grupo)
```

| Tipo                  | Uso                                                                                                                                                            |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **-c** comentario     | Para poner o cambiar un comentario sobre el usuario.                                                                                                           |
| **-d** directorio     | Especificamos la trayectoria absoluta del directorio de conexión (HOME).                                                                                       |
| **-l**                | Nombre que el usuario utiliza para la conexión.                                                                                                                |
| **-g** grupo          | El grupo de usuarios al que se conecta el usuario. Debe existir previamente.                                                                                   |
| **-G** grupo1, grupo2 | Otros grupos a los que se añadirá el usuario.                                                                                                                  |
| **-s** shell          | Trayectoria absoluta del shell de conexión.                                                                                                                    |
| **-p** passwd         | Se utiliza para cambiar la contraseña. Esta contraseña la escribirá sin encriptar. Para guardar la contraseña encriptada utilizar el comando encrypt o passwd. |
| **-f**                | Número de días en los que la cuenta puede permanecer inactiva antes de eliminarla.                                                                             |
| **-e**                | Fecha en la que acaba la validez de la cuenta de usuario.                                                                                                      |
| **-L**                | Bloqueo de la cuenta de usuario.                                                                                                                               |
| **-U**                | Desbloqueo de la cuenta de usuario.                                                                                                                            |
| **-aG**               | Añade el usuario al grupo sin eliminarlo de sus grupos actuales.                                                                                               |
## userdel (Quitar usuario)
Quita la cuenta del usuario pero no borra su directorio ni sus objetos en propiedad:
```bash
userdel [opciones] nombre_usuario
```

| Tipo   | Uso                                                                                                        |
| ------ | ---------------------------------------------------------------------------------------------------------- |
| **-r** | Borra los ficheros contenidos en el directorio home y los del directorio usr del directorio spool de mail. |

## passwd
Cambiar contraseña, usando la orden sin opciones ni nombre de usuario. Se preguntará la antigua contraseña y, si es correcta, permitirá cambiarla después de ponerla 2 veces correctamente.
```bash
 passwd [opciones] nombre_usuario
```

| Tipo          | Uso                                                                                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **-d**        | Borra la contraseña del usuario especificado si este está autorizado para no tener.                                                                     |
| **-f**        | Fuerza al usuario a cambiar su contraseña la próxima vez que se conecte.                                                                                |
| **-n** dias   | Mínimo número de días que tienen que pasar entre cambios de contraseña.                                                                                 |
| **-x** dias   | Días que durará la contraseña sin ser cambiada. Terminados éstos, el sistema obligará al usuario a cambiarla.                                           |
| **-r** número | Número de intentos permitidos para cambiar una contraseña y ponerla correcta.                                                                           |
| **-s**        | Visualiza un informe de las características de la contraseña del usuario. Si el usuario está bloqueado, veremos LK, si tiene contraseña PS y si no, NP. |
| **-w**        | Días de advertencia en los cuales el usuario debe cambiar la contraseña.                                                                                |
| **-i**        | Número de días que despues de desactivar la cuenta, está se elimina.                                                                                    |
## groupadd (Gestión de grupos de usuario)
Los usuarios pueden estar organizados en grupos, que permiten compartir ciertos recursos entre distintos usuarios. Cuando se crea un usuario, se le especifica el grupo por defecto ***group***, y se le puede hacer miembro de otros grupos adicionales.
```bash
groupadd [-x fichero] nombre_grupo
```
También existen opciones para modificar (cambiar nombre en este caso) y borrar grupos:
```bash
groupmod –n nom_nuevo nom_actual

groupdel nombre_grupo
```
## Bases de datos de seguridad (/etc/)
### Fichero /etc/passwd
Fichero de texto que todos los usuarios pueden ver, pero sólo **root** puede modificar, aunque por seguridad se debe evitar manipularlo. 
Este fichero contiene una línea para cada usuario en el sistema (con información del usuario), cada campo de información está separado por dos puntos ***:*** siguiendo el siguiente orden:
1) Nombre de usuario.
2) x: indica que el usuario tiene o puede tener contraseña que se encuentra cifrada.
3) Número de identificación del usuario (UID).
4) Número de identificación del grupo (GID) al que pertenece el usuario.
5) Comentario sobre el usuario.
6) Directorio propio de conexión del usuario ($HOME).
7) Shell de conexión del usuario.

La información del **root** se encuentra  en la primera línea y su UID es siempre 0.
### Fichero /etc/shadow
Fichero de texto que no pueden ver los usuarios normales. Cada campo de información está separado por dos puntos **_:_** siguiendo el siguiente orden:
1) Nombre de usuario.
2) Contraseña cifrada del usuario.
### Fichero /etc/group
El fichero **letclgroup** es un fichero de texto con la misma organización que los anteriores, siguiendo el siguiente orden:
1) Nombre del grupo.
2) Número de identificación del grupo (GID).
3) Lista de usuarios pertenecientes al grupo.
## su (Superusuario)
Permite al administrador pasar a trabajar como tal, aunque en principio se haya conectado en una cuenta de características normales:
```bash
su
```

# Comandos de consola útiles
### Documentación (man)
Muestra información sobre un comando en concreto.
```bash
man [-a] [ sección] título
man -e título
man -k palabra
```
### Visualizar (cat)
Visualiza el contenido de uno o varios archivos por pantalla:
```bash
cat fich1
```
### Generar (touch)
Genera un fichero vacío:
```bash
touch fich1
```
### Tipo de fichero (file)
Genera un fichero vacío:
```bash
file -f nomfich [nomfich]
```

| Tipo   | Uso                                                                                                |
| ------ | -------------------------------------------------------------------------------------------------- |
| **-f** | Determina las características de los nombres de los ficheros contenidos en otro fichero (nomfich). |

### Superuser do (sudo)
Se utiliza para permitir a los usuarios ejecutar comandos con privilegios de otro usuario, típicamente el superusuario o root:
```bash
sudo ...
```
Se utiliza poniendo ***sudo*** delante del comando que vayamos a ejecutar.
### Cambiar propietario (chown)
Se utiliza para cambiar el propietario:
```bash
chown [opciones] nuevo_propietario[:nuevo_grupo] archivo(s)
```
- `nuevo_propietario`: Especifica el nuevo propietario del archivo o directorio.
- `nuevo_grupo` (opcional): Especifica el nuevo grupo del archivo o directorio. Si no se proporciona, el grupo no se modifica.
- `archivo(s)`: Especifica los archivos o directorios a los que se aplicará el cambio de propietario/grupo. Pueden ser uno o más archivos o directorios.
1. Cambiar propietario de un archivo.
```bash
chown nuevo_propietario archivo

chown usuario1 archivo.txt
```
2. Cambiar el propietario y el grupo de un archivo.
```bash
chown nuevo_propietario:nuevo_grupo archivo

chown usuario1:grupo1 archivo.txt
```