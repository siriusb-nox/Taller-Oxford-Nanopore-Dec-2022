## A. ANALISIS DE CALIDAD DE DATOS CON `NanoPlot`
`NanoPlot` es un programa diseñado para producir graficas y resumenes de los resultados de experimentos de secuenciación producidos por ONT. El programa recibe como input una serie de archivos fastq (usando la opción `--fastq`), o un archivo de texto producido por ONT (por default llamado "sequencing_summary.txt"). Analizando directamente los archivos fastq se pueden producir graficas con información mas detallada.

En este tutorial, trabajaremos con el archivo de texto "sequencing_summary.txt" (disponible [aqui](https://drive.google.com/file/d/1dy6Sf3TZVkq7S0GOjyy8UlWolUeFEsxv/view?usp=share_link)): 

```bash
NanoPlot --summary sequencing_summary.txt --loglength -o summary-plots-log-transformed
```

Como resultado, el programa creara una gran cantidad de graficas en archivp .png mas una compilacion de las mismas en formato html. Estos archivos estaran depositados en una carpeta llamada "summary-plots-log-transformed" (disponibles [aqui](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/tree/main/NanoPlot/), carpeta comprimida en `gzip`).

Un ejemplo del output es el siguiente:
