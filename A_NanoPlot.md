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

Esta grafica nos indica como esta distribuida la longitud de las secuencias de ADN producida por ONT vs su calidad (expresada en valores similares a los [Phred]:(https://en.wikipedia.org/wiki/Phred_quality_score)). Una cosa interesante es ver la buena cantidad de secuencias que tienen valores inferiores a Phred 10 (i.e., prob de 1 en 10 nucleotidos de ser llamados incorrectamente).  

Este otro grafico nos muestra la cantidad de secuencias producidas vs su longitud:

<p align="center">
 <img src="https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/WeightedHistogramReadlength.png" alt="Longitud vs cantidad de secuencias"/>
</p>

El reporte completo de un experimento de secuenciación conducido usando el ADN de nuestro organismo misterio se encuentra disponible [aqui](https://drive.google.com/file/d/1jPEOJwQUAObTKwK9kZybFwkhUSoayszy/view?usp=share_link). 

## Literatura recomendada
1. Delahaye C, Nicolas J. 2021. Sequencing DNA with nanopores: troubles and biases. PLoS ONE https://doi.org/10.1371/journal.pone.0257521
