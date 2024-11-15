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


