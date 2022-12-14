## A. ANALISIS DE CALIDAD DE DATOS CON `NanoPlot`
`NanoPlot` es un programa diseñado para producir graficas y resumenes de los resultados de experimentos de secuenciación producidos por ONT. El programa recibe como input una serie de archivos fastq (usando la opción `--fastq`), o un archivo de texto producido por ONT (por default llamado "sequencing_summary.txt"). Analizando directamente los archivos fastq se pueden producir graficas con información mas detallada.

En este tutorial, trabajaremos con el archivo de texto: 

```bash
NanoPlot --summary sequencing_summary.txt --loglength -o summary-plots-log-transformed
```
