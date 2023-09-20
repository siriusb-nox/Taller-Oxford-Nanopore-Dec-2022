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
--min_qscore 10 # excluira cualquier secuencia de ADN con un valor de calidad menor a 10 
```
Una idea de que tantos recursos GPU/CPU consumen diferentes modelos de llamado de bases esta disponible [aqui](https://esr-nz.github.io/gpu_basecalling_testing/gpu_benchmarking.html#cfg_files).

Un mensaje de ejecución exitosa de `guppy` se ve asi:

```bash
usuario@maquina:/home/ningunopudoconel/Downloads/software/guppy/ont-guppy/bin/guppy_basecaller -s . -c dna_r9.4.1_e8.1_hac.cfg --compress_fastq --trim_adapters -x auto --min_qscore 10
ONT Guppy basecalling software version 3.1.5+781ed57
config file:        /home/ningunopudoconel/Downloads/software/guppy/ont-guppy/data/dna_r9.4.1_450bps_hac.cfg
model file:         /home/ningunopudoconel/Downloads/software/guppy/ont-guppy/data/template_r9.4.1_450bps_hac.jsn
input path:         raw_data/
save path:          HeredianoGenome_basecalled_20190621_hac/
chunk size:         1000
chunks per runner:  1000
records per file:   4000
fastq compression:  ON
num basecallers:    4
gpu device:         cuda:0
kernel path:
runners per device: 2

Found 1215050 fast5 files to process.
Init time: 12755 ms

0%   10   20   30   40   50   60   70   80   90   100%
|----|----|----|----|----|----|----|----|----|----|
***************************************************
Caller time: 12227895 ms, Samples called: 117512178322, samples/s: 9.61017e+06
Finishing up any open output files.
Basecalling completed successfully.
```
A parte de producir los archivos fastq, `guppy`tambien produce una serie de reportes, entre ellos una compilacion de estadisticas de secuenciación en formato html. Un ejemplo se puede ver [aqui](http://htmlpreview.github.io/?https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/guppy/report_FAU10861_20221116_1415_944237d8.html)

<p align="center">
 <img src="https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/guppy_report_example.png" alt="A section of a guppy report on a seq experiment"/>
</p>
