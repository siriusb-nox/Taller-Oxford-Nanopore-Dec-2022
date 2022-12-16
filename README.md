# Taller virtual "Principios del analisis de datos de secuencias de ADN derivadas de tecnologías Oxford Nanopore" - 15, 16 Diciembre 2022
## Instructor: [Oscar A. Pérez Escobar](https://www.tropicalphylodiv.com/) [(Royal Botanic Gardens, Kew)](https://scholar.google.co.uk/citations?user=tSzyp6QAAAAJ&hl=en)
### Organizadores: Diego Bogarín [(UCR)](https://www.researchgate.net/profile/Diego-Bogarin-2) & Melania Fernandez [(UCR)](https://www.researchgate.net/profile/Melania-Fernandez)
### Contribuyentes: Natalia Przelomska [(RBG Kew)](https://www.kew.org/science/our-science/people/natalia-przelomska), Alexandre Antonelli [(RBG Kew, GU)](https://www.kew.org/science/our-science/people/alexandre-antonelli)
##### Instituciones patrocinadoras: Universidad de Costa Rica (UCR) - OAICE - Royal Botanic Gardens, Kew (RBG Kew) - Antonelli Lab (RGB Kew, Gothenburg University)

## 1. Introducción
Este repositorio contiene un tutorial guia para el analisis de datos crudos derivados de tecnologias Oxford Nanopore (ONT) y los pasos iniciales para conducir un ensamblado de genomas. Adicionalmente, incluye una demostración de como conducir busquedas de secuencias en una base de datos predeterminada usando ncbi blast. El tutorial esta en parte basado en datos generados por Canales et al. (2022, articulo disponible [aqui](https://gigabytejournal.com/articles/71), usando un [GridION](https://nanoporetech.com/products/gridion), los cuales se utilizaron para ensamblar el genoma nuclear del arbol de la quina (_Cinchona pubescens_, Rubiaceae). Para las demonstraciones con BLAST, se utilizaran algunos datos no publicados de un organismo misterio (!), producidos por Natalia Przelomska, Alexandre Antonelli, Diego Bogarín & Oscar A Pérez-Escobar).

_Este tutorial esta dirigido a personas con un conocimiento basico en programación y esta diseñado para ejecutarse en ambientes UNIX. El participante idealmente debe tener experiencia en uso de terminales, y programas de manejo de archivos de texto como **awk, sed, grep, entre otros.**_ El taller se ejecutará en el servidor [Kabré](https://kabre.cenat.ac.cr/), o en computadores previamente configurados. 

_Para aquellos usuarios con muy poca experiencia (o nula) en programación en ambientes UNIX, un breve tutorial se encuentra disponible [aquí](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/bash_tutorial.md)_. 

Este tutorial requiere los siguientes programas (dependencias) para correr (es muy recomendable tener estos programas instalados antes de comenzar el tutorial). **Por favor cersiorarse de que las dependencias en que estos programas corren tambien estan disponibles**:
1. [**NCBI blast:**](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download) Este programa permite la construcción de bases de datos blast, y la busqueda (alineamiento) de secuencias de ADN o AA (formato fasta) en bases de datos blast. 
2. [**NCBI magicblast:**](https://ncbi.github.io/magicblast/doc/download.html) Este programa permite la busqueda de secuencias de ADN derivadas de secuenciación masiva (formato fasta o fastq) en bases de datos blast.
3. [**CANU:**](https://github.com/marbl/canu) este programa permite la corrección y filtrado de secuencias de ONT/PacBio.  
4. [**SMARTdenovo:**](https://github.com/ruanjue/smartdenovo) este programa ensambla "de-novo" secuencias corregidas y recortadas de ONT/PacBio.
5. [**NanoPlot:**](https://github.com/wdecoster/NanoPlot) Una version ejecutable en linea esta disponible [aquí](https://nanoplot.bioinf.be/); este programa produce graficas con informaciones asociadas a experimentos de secuenciación conducidos en teconologias ONT 
6. [**Guppy:**](https://nanoporetech.com/nanopore-sequencing-data-analysis) Este programa se encarga de llamar las bases a partir de archivos FAST5 generados por ONT. Solo esta disponible para usuarios ONT (esta parte del tutorial, aunque se explicará, no se ejecutara).

## 2. Estructura del pipeline
Este tutorial esta dividio en tres pasos principales (Figura 1):

A. [**Llamado de bases**](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/edit/main/A_basecall.md)

B. [**Analisis de la calidad de datos**](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/B_NanoPlot.md)

C. [**Corrección y recorte de los datos**](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/C_read_corrtrim_CANU.md)

D. [Operaciones de busqueda y/o ensamblado de genomas](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/D_blast.md)

![Figure 1](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/pipeline_overview_v0_OP_15122022.png?raw=true)
**Figura 1**: Vista simplificada del tutorial/pipeline

**IMPORTANTE:** Los datos base necesarios para ejectuar este tutorial estan disponibles en:

```
/directorio/personal/Taller-Oxford-Nanopore-Dec-2022/NGSdat/  # datos crudos de Cinchona y el organismo misterio (fastq)
/directorio/personal/Taller-Oxford-Nanopore-Dec-2022/NanoPlot/ # datos para ejecutar NanoPlot (archivo de texto)
```

## 2.1. Configuración del pipeline
En cualquier pipeline de bioinformatica, es esencial relacionar de que programas depende el pipeline y saber donde estan los archivos input, etc. Para ejecutar este tutorial, se debe copiar este repositorio en un directorio de su escogencia. Para ello, favor ejecutar:

`git clone https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022.git`

**Para usuarios asociados a la Universidad de Costa Rica (UCR) y del Kabré**, los programas necesarios para correr este tutorial estarán disponibles como modulos y deben ser llamados usando el sistema SLURM. Pasos detallados de como conectarse al Kabre, como intercambiar datos entre un computador local y el servidor, como solicitar recursos y modulos/programas estan disponibles [aqui](https://kabre.cenat.ac.cr/guia-usuario/). 

Para solicitar los modulos requeridos, ejecutar:

`module load programa`

Por ejemplo, para cargar los ejecutables de blast+ y canu, ejecutar:

```bash
module load blast+/2.11.0
module load canu
```

Adicionalmente, los recursos necesarios para ejecutar programas tambien deberan ser solicitados bajo el mismo sistema SLURM. Un ejemplo basico de como solicitar recursos se provee aqui:

```bash
#!/bin/bash
#SBATCH --job-name=blast+
#SBATCH --cpus-per-task=4
#SBATCH --partition=dribe
#SBATCH --ntasks=1
#SBATCH --time=72:00:00
#SBATCH -o result_%N_%j.out      # File to which STDOUT will be written
#SBATCH -e result_%N_%j.err      # File to which STDERR will be written
#SBATCH --mail-type=ALL
#SBATCH --mail-user=username@ucr.ac.cr
```

**Para usuarios con los programas instalados en un ambiente UNIX en computadoras personales**, estos se pueden introducir en la sesión actual (terminal) usando el siguiente comando, por ejemplo:

`PATH=$PATH:/directorio/de/la/carpeta/programax`

Para el caso particular de mi ordenador, yo ejecuto este comando (_NO EJECUTAR_ - es solo un ejemplo!):

```bash
# Canu
PATH=$PATH:/home/siriusb/softwares/genomics/canu/canu-1.9/Linux-amd64/bin/
# Racon 
PATH=$PATH:/home/siriusb/softwares/genomics/racon/build/bin
# Minimap2
PATH=$PATH:/home/siriusb/softwares/genomics/minimap2-2.17_x64-linux/
# samtools
PATH=$PATH:/home/siriusb/softwares/genomics/samtools-1.10
# magicblast
PATH=$PATH:/home/siriusb/softwares/genomics/ncbi-magicblast-1.5.0/bin/
# ncbi blast
PATH=$PATH:/home/siriusb/softwares/genomics/ncbi-blast-2.10.0+/bin/
# SMARTdenovo
PATH=$PATH:/home/siriusb/softwares/genomics/
export PATH
```
## AGRADECIMIENTOS
Natalia Przelomska y Alexandre Antonelli produjeron datos no publicados. Ilia Letich procuro datos de sequencia de OT para Cinchona




