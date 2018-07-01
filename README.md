# dynamic-execute-bash-linux-

```sh
#!/bin/bash

# ruta de la carpeta de los bots
FILES="/Users/user/folder/ficheros/*"

# numero de bots por ejecucion
bots="$(ls /Users/user/folder/ficheros/ | wc -l)"

# iteraciones de ejecucion
nodos=2
totalContador=$((nodos%bots))

# contador de iteraciones
contador=0
inicio=0
tempContador=0
nodosTemp=$((nodos -1))
contadorFicheros=0

# Carga de archivos
rm /Users/user/folder/ficheros.txt
for f in $FILES
do
  echo $f >> /Users/user/folder/ficheros.txt
  # . $f
done

while [ $contador > $totalContador ]
do

    echo "------ INICIO ---------------------" $tempContador
    echo "------ FIN ------------------------" $nodosTemp

    contadorFicheros=0
    while read p; do
      # if [$tempContador -le $inicio -a]; then
      echo $tempContador " . . . . .  . . . . . " $nodosTemp 

      # if [ $tempContador -le  $nodosTemp ]  &&  [   contadorFicheros  ]  ; then
      if [ $tempContador -le $contadorFicheros ] && [ $nodosTemp -ge $contadorFicheros ]  ; then
        # EJECUTAMOS EL PROCESO
        # TO DO !
        ((tempContador++))
        echo "PROCESO......................... " + $p
        sleep 1
      fi
      ((contadorFicheros++))
    done </Users/user/folder/ficheros.txt

    # NOS GUARDAMOS TODOS LOS PROCESOS EN EJECUCCION
     ps | grep 'Users/user/folder/ficheros/' > /Users/user/folder/log.txt

    # ESPERAMOS EL TIEMPO DESEADOPARA LA PROXIMA ITERACION
    echo "Esperando zZzZzZzz......"
    sleep 2

    # MATAMOS LOS PROCESOS
    while read p; do
      echo $p  | cut -d' ' -f 1
      echo "Procedemos a matar el proceso: "  + $p
      # kill $p
    done </Users/user/folder/log.txt


    # inicio=$((inicio + nodos))
    tempContador=$((tempContador + nodos -2))
    nodosTemp=$((nodosTemp + nodos))

    ((contador++))
      
    # REINICIAMOS LOS CONTADORES
    if [ $contador == $totalContador ]; then
      contador=0
      inicio=0
      tempContador=0
      nodosTemp=$((nodos -1))
      echo $totalContador
      echo "RESTART CONUNT!"
    fi
done

echo "done!"
