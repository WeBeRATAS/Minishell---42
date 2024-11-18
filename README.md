# Minishell-42
# Empezando a comprender lo que se debe hacer

A continuación se describe brevemente el funcionamiento del shell cuando lee y ejecuta un comando. Básicamente, el shell hace lo siguiente
*******************************************************************************************************************************************


1) Lee su entrada desde un archivo (ver Scripts de Shell), desde una cadena suministrada como argumento a la opción de invocación -c (ver Invocando Bash), o desde la terminal del usuario.

2) Divide la entrada en palabras y operadores, obedeciendo las reglas de entrecomillado descritas en Entrecomillado. Estos tokens están separados por metacaracteres. La expansión de alias se realiza en este paso (ver Aliases).

3) Convierte los tokens en comandos simples y compuestos (véase Comandos del shell).

4) Realiza las distintas expansiones del intérprete de comandos (consulte Expansiones del intérprete de comandos), dividiendo los tokens expandidos en listas de nombres de archivo (consulte Expansión de nombres de archivo) y comandos y argumentos.

5) Realiza las redirecciones necesarias (ver Redirecciones) y elimina los operadores de redirección y sus operandos de la lista de argumentos.

6) Ejecuta el comando (consulte Ejecución de comandos).

7) Opcionalmente, espera a que el comando finalice y recoge su estado de salida (consulte Estado de salida).

Enlaces y documentacion para revisar: https://www.gnu.org/software/bash/manual/bash.html#Shell-Operation




# Minishell debe: 
*****************************************************
Mostrar una entrada mientras espera un comando nuevo.

Tener un historial funcional.

Buscar y ejecutar el ejecutable correcto (basado en la variable PATH o mediante el uso de rutas relativas o absolutas).

Evita utilizar más de una variable global para indicar la recepción de una señal. Piensa en lo que implica: Esta aproximación evita que tu gestor de señales acceda a tus estructuras de datos principales.

No interpretar comillas sin cerrar o caracteres especiales no especificados en el enunciado como \ (barra invertida) o ; (punto y coma).

Gestionar que la ’ evite que el shell interprete los metacaracteres en la secuencia entrecomillada.

Gestionar que la " evite que el shell interprete los metacaracteres en la secuencia entrecomillada exceptuando $ (signo de dólar).

Implementar redirecciones:
< debe redirigir input.
> debe redirigir output.
<< debe recibir un delimitador, después leer del input de la fuente actual hasta que una línea que contenga solo el delimitador aparezca. Sin embargo, no necesita actualizar el historial.
>> debe redirigir el output en modo append.

Implementar pipes (carácter |). El output de cada comando en la pipeline se conecta a través de un pipe al input del siguiente comando.

Gestionar las variables de entorno ($ seguidos de caracteres) que deberán expandirse a sus valores.

Gestionar $?, que deberá expandirse al estado de salida del comando más reciente ejecutado en la pipeline.

Gestionar ctrl-C ctrl-D ctrl-\, que deberán funcionar como en bash.

Cuando sea interactivo:
ctrl-C imprime una nueva entrada en una línea nueva.
ctrl-D termina el shell.
ctrl-\ no hace nada.

Deberá implementar los built-ins:
echo con la opción -n.
cd solo con una ruta relativa o absoluta.
pwd sin opciones.
export sin opciones.
unset sin opciones.
env sin opciones o argumentos.
exit sin opciones.
*************************************************************************************************************************************************


# Proceso
*************************************************************************************************
Utilizamos la libreria readline de GNU que ya está permitido su uso. ver manual.
Esta libreria, a su vez, nos proporciona el historial que solicita la consigna.

Análisis lexicológico
Esta etapa consiste en identificar tokens. Leemos caracter a caracter la línea que obtubimos en el paso anterior y guardamos en una estructura clasificando en word o token siguiendo las reglas de encomillado de bash.

Análisis sintáctico
La lista de nodos generada por el paso anterior se libera y se generan nuevos nodos para la instancia de ejecución. Aquí también, revisamos si hay redirecciones y generamos los file descriptors para cada uno de los procesos que vayamos a ejecutar más adelante. Cada nodo que generemos es el conjunto de word y token hasta llegar a un PIPE en caso de encontrar uno.

Expansiones
Antes de enviar la lista de nodos al ejecutor hay que realizar las expansiones necesarias de acuerdo a las reglas de encomillado de bash.

Redirecciones y liberación de memoria
Una vez hecho el fork() libramos todas las estructuras en memoria del proceso hijo y duplicamos los file descriptors en caso de haber redirecciones.

Ejecución
Por último, ejecutamos uno a uno todos los nodos que generamos, liberamos memoria, cerramos file descriptors y lanzamos el prompt esperando la nueva secuencia a ejecutar.

*****************************************************************
Uso
Clona el repositorio
git clone ... minishell
Compila el proyecto con make
make
Como se menciona anteriormente, este proyecto requiere de la libreria readline. En caso de no tenerla instalada ejecuta:

En sistemas basados en Debian/Ubuntu:
sudo apt-get update
sudo apt-get install libreadline-dev

En sistemas basados en Red Hat/Fedora:
sudo yum install readline-devel

En macOS (usando Homebrew):
brew install readline
Ejecuta la minishel
./minishell

# Documentación
***************************************
BASH manual https://www.academia.edu/33910321/Manual_0_6_MAS_COMPLEO_BASH

GNU readline https://tiswww.case.edu/php/chet/readline/rltop.html

# Autores de este pedazo de tutorial, dos grandes
Autores
@Fefeco
@Daviichii89

