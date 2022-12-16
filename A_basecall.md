## A. LLAMADO DE BASES A PARTIR DE ARCHIVOS .FAST5 USANDO `guppy`
`guppy` es el _programa oficial_ diseñado por Oxford Nanopore, para traducir las señales electricas contenidas en los archivos crudos FAST5 producidos por el dispositivo secuenciador en nucleotidos arreglados en secuencias (archivos FASTQ). Este programa es solo accesible si se posee una cuenta de cliente con Oxford Nanopore. 
El llamado de bases se hace directamente cuando se esta realizando la secuenciación de la libreria (i.e, _live basecalling_), pero este proceso es computacionalmente intenso y hay ventajas en hacer el llamado de bases despues de que la secuenciación haya terminado (p.ej., ejecutar modelos mucho mas precisos de llamado de bases usando computadores mejor equipados).

Los archivos instaladores de `guppy` vienen en dos sabores: **CPU** (usa recursos de procesador) y **GPU** (usa recursos de la tarjeta grafica - disponible para un tipo limitado de tarjetas). _La version GPU es muchisimo mas eficiente que la CPU._ 

```
ls /mnt/NOX1_12082022/Pleurothallidinae_compGenomics/NGSdat/rawNano/Lepanthes_quisqueyana_DomRep/Lepanthes_flowcell_I/Lep_quisqueyana_1611022_cultB
```
