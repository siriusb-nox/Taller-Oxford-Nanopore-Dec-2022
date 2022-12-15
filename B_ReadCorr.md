## B. Corrección y recorte (filtrado) de secuencias ONT

## filtering magicblast
sed 's/ /_/g' *_9_0.tab.out | awk '{print $1 " " $16}' | head
