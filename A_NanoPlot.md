## A. ANALISIS DE CALIDAD DE DATOS CON `NanoPlot`
`NanoPlot` es un programa diseñado para producir graficas y resumenes de los resultados de experimentos de secuenciación producidos por ONT. El programa recibe como input una serie de archivos fastq (usando la opción `--fastq`), o un archivo de texto producido por ONT (por default llamado "sequencing_summary.txt"). Analizando directamente los archivos fastq se pueden producir graficas con información mas detallada.

En este tutorial, trabajaremos con el archivo de texto "sequencing_summary.txt" (disponible [aqui](https://drive.google.com/file/d/1dy6Sf3TZVkq7S0GOjyy8UlWolUeFEsxv/view?usp=share_link)): 

```bash
NanoPlot --summary sequencing_summary.txt --loglength -o summary-plots-log-transformed
```

Como resultado, el programa creara una gran cantidad de graficas en archivp .png mas una compilacion de las mismas en formato html. Estos archivos estaran depositados en una carpeta llamada "summary-plots-log-transformed" (disponibles [aqui](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/tree/main/NanoPlot/), carpeta comprimida en `gzip`).

Un ejemplo del output es el siguiente:

<p align="center">
 <img src="https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/LengthvsQualityScatterPlot_dot.png" alt="Longitud vs Calidad de la secuencia"/>
</p>

Esta grafica nos indica como esta distribuida la longitud de las secuencias de ADN producida por ONT vs su calidad (expresada en valores similares a los [Phred]:(https://en.wikipedia.org/wiki/Phred_quality_score)). Una cosa interesante es ver la buena cantidad de secuencias que tienen valores inferiores a Phred 10 (i.e., prob de 1 en 10 nucleotidos de ser llamados incorrectamente). De paso, hay ciertas regiones del genoma que son mas dificiles de secuenciar ([low complexity regions](https://academic.oup.com/nar/article/32/suppl_2/W628/1040725)), y ONT va a tender a producir datos de secuencias de estas regiones con menores calidades (i.e., mayor probabilidad de bases mal llamadas, ver seccion "literatura recomendada").  

Este otro grafico nos muestra la cantidad de secuencias producidas vs su longitud:

<p align="center">
 <img src="https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/WeightedHistogramReadlength.png" alt="Longitud vs cantidad de secuencias"/>
</p>

Aparte del output grafico, `NanoPlot` genera un reporte sucinto sobre la secuenciacion en general, donde se proveen valores como longitudes medias y medianas de las secuencias, calidad, numeros de reads etc. Este archivo usualmente se llama "NanoStats.txt" y se ve así:

```
General summary:         
Active channels:                    488.0
Mean read length:                 1,363.1
Mean read quality:                   13.0
Median read length:                 783.0
Median read quality:                 13.8
Number of reads:              4,488,678.0
Read length N50:                  2,330.0
STDEV read length:                1,727.3
Total bases:              6,118,383,425.0
Number, percentage and megabases of reads above quality cutoffs
>Q5:	4196018 (93.5%) 5827.1Mb
>Q7:	3944100 (87.9%) 5526.7Mb
>Q10:	3515763 (78.3%) 5019.4Mb
>Q12:	2986773 (66.5%) 4403.6Mb
>Q15:	1635361 (36.4%) 2634.3Mb
Top 5 highest mean basecall quality scores and their read lengths
1:	29.7 (2194)
2:	29.7 (2100)
3:	28.6 (279)
4:	28.1 (178)
5:	28.0 (464)
Top 5 longest reads and their mean basecall quality score
1:	317219 (3.7)
2:	262893 (3.6)
3:	234317 (3.8)
4:	213357 (3.8)
5:	194829 (4.1)

```

El reporte completo de un experimento de secuenciación conducido usando el ADN de nuestro organismo misterio se encuentra disponible [aqui](https://drive.google.com/file/d/1jPEOJwQUAObTKwK9kZybFwkhUSoayszy/view?usp=share_link), o en la carpeta de este [repositorio](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/tree/main/NanoPlot) - archivo llamado "summary-plots-log-transformed.zip" (primero descomprimir con `gunzip`). 

## Literatura recomendada
1. Delahaye C, Nicolas J. 2021. Sequencing DNA with nanopores: troubles and biases. PLoS ONE https://doi.org/10.1371/journal.pone.0257521
2. Orlov YL, Potapov VN. 2004. Complexity: an internet resource for analysis of DNA sequence complexity. Nuc. Ac. Res. 32 https://doi.org/10.1093%2Fnar%2Fgkh466
