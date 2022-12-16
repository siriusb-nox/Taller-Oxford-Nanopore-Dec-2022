## A. LLAMADO DE BASES A PARTIR DE ARCHIVOS .FAST5 USANDO `guppy`
`guppy` es el _programa oficial_ diseñado por Oxford Nanopore, para traducir las señales electricas contenidas en los archivos crudos FAST5 producidos por el dispositivo secuenciador en nucleotidos arreglados en secuencias (archivos FASTQ). Este programa es solo accesible si se posee una cuenta de cliente con Oxford Nanopore. 
El llamado de bases se hace directamente cuando se esta realizando la secuenciación de la libreria (i.e, _live basecalling_), pero este proceso es computacionalmente intenso y hay ventajas en hacer el llamado de bases despues de que la secuenciación haya terminado (p.ej., ejecutar modelos mucho mas precisos de llamado de bases usando computadores mejor equipados).

