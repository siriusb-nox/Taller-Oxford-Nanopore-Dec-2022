## A. LLAMADO DE BASES A PARTIR DE ARCHIVOS .FAST5 USANDO `guppy`
`guppy` es el _programa oficial_ diseñado por Oxford Nanopore, para traducir las señales electricas contenidas en los archivos crudos FAST5 producidos por el dispositivo secuenciador en nucleotidos arreglados en secuencias (archivos FASTQ). Este programa es solo accesible si se posee una cuenta de cliente con Oxford Nanopore. 
El llamado de bases se hace directamente cuando se esta realizando la secuenciación de la libreria (i.e, _live basecalling_), pero este proceso es computacionalmente intenso y hay ventajas en hacer el llamado de bases despues de que la secuenciación haya terminado (p.ej., ejecutar modelos mucho mas precisos de llamado de bases usando computadores mejor equipados).

Los archivos instaladores de `guppy` vienen en dos sabores: **CPU** (usa recursos de procesador) y **GPU** (usa recursos de la tarjeta grafica - disponible para un tipo limitado de tarjetas, e.g., NVIDIA). _La version GPU es muchisimo mas eficiente que la CPU._ 

Para ejecutar guppy, se puede ejectuar el siguiente comando:

```bash
ls /directorio/personal/*.fast5 | guppy_basecaller -s . -c dna_r9.4.1_e8.1_hac.cfg --compress_fastq --trim_adapters -x auto --min_qscore 10
```
Donde:

```bash
-s # indica el directorio para guardar los outputs del analisis
-c # indica el modelo para llamar las bases (dna_r9.4.1_e8.1_hac.cfg es uno de los modelos con mayor precision)
-x # activa la opcion de deteccion automatica de que dispositivo GPU esta disponible en el computador
```
Una idea de que tantos recursos GPU consumen diferentes modelos de llamado de bases esta disponible [aqui](https://esr-nz.github.io/gpu_basecalling_testing/gpu_benchmarking.html#cfg_files).
