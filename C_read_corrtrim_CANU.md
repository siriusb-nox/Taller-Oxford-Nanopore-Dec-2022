## C. CORRECCION Y FILTRADO DE SECUENCIAS ONT CON `canu`

`canu` es un programa diseñado para hacer diferentes analisis con datos ONT. El programa puede realizar la corrección de las secuencias ONT, filtrado (remocion de bases o fragmentos de las secuencias con bajas calidades) y ensamblado. El programa **requiere muchisimos recuros para su ejecucion** (esto dependiendo del tamanho de los genomas, su comlejidad y que cantidad inicial de datos se estan usando para su ejecución. **El programa recomienda iniciar su ejecución con una cantidad de datos que representen entre un 20x-60x de cobertura teorica (e.g., Sun et al., 2021).**

>The following assemblers were used for the benchmarking, including the long-read only assemblers (Canu [12], Flye [13], Wtdbg2 [14], Miniasm [15], NextDenovo >>(https://github.com/Nextomics/NextDenovo), NECAT [6], Raven [16] and Shasta [7]) and hybrid assemblers (MaSuRCA [17] and QuickMerge [18]). **Canu was not tested on the M. coruscus genome owing to the extremely intensive computing time required for this large genome**. Previous analyses have suggested that using corrected ONT reads could improve the genome assembly [19]. To check the effect that this has on the assemblies, the ONT reads that were corrected and/or trimmed by Canu 

`canu`es un programa modular, esto significa que cada modo (_correction_, _trim_, _assembly_) se puede ejecutar por separado. Esto es recomendado ya que en algunas instancias el programa se puede bloquear por falta de recursos. Ne este caso, es recomendable usar `canu` para las correcciones y filstrados, y otros programas para ensamblar datos corregidos y filtrados (e.g. SMARTdenovo). Para ejecutar el programa en modo correction, usar:

```bash
canu -correct genomeSize=1.1g -nanopore-raw /dir/archivos/fastq/PAD61315_fastq/pass/*.fastq -p prefijo_corrected -d directorio_output 
```

Donde:
```bash
genomeSize # indica el tamaño del genoma del organismo a analizar (en Mb o Gb, etc)
-nanopore-raw # indica que tipo de inputs se estan usando
-p # prefijo de los archivos output
-d # directorio output
```

Para ejecutar canu en modo filtro (_trim_), usar:

```bash
canu -trim genomeSize=1.1g -nanopore-corrected /dir/archivoscorregidos/fastq/PAD61315_fastq/archivo.fastq -p prefijo_trim -d directorio_output 
```

Donde:
```bash
genomeSize # indica el tamaño del genoma del organismo a analizar (en Mb - M o Gb - g, etc)
-nanopore-corrected # indica que tipo de inputs se estan usando
-p # prefijo de los archivos output
-d # directorio output
```

## Literatura recomendada
1. Sun J, Li R, Chen C, Sigwart JD, Kocot KM. (2021) Benchmarking ONT read assemblers for high-quality molluscan genomes. Proc. B Phil Trans. https://doi.org/10.1098/rstb.2020.0160
