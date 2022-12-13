# Taller virtual "Principios del analisis de datos de secuencias de ADN derivadas de tecnologías Oxford Nanopore" - 15, 16 Diciembre 2022
##### Organizadores: Oscar A. Pérez Escobar (Royal Botanic Gardens, Kew), Diego Bogarín (UCR) & Melania Fernandez (UCR)
##### Instituciones patrocinadoras: Universidad de Costa Rica (UCR) - OAICE - Royal Botanic Gardens, Kew (RBG Kew) - Antonelli Lab

## Introducción
Este repositorio contiene un tutorial guia para el analisis de datos crudos derivados de tecnologias Oxford Nanopore (ONT) y los pasos iniciales para conducir un ensamblado de genomas. Adicionalmente, incluye una demostración de como conducir busquedas de secuencias en una base de datos predeterminada usando ncbi blast. _Este tutorial esta dirigido a personas con un conocimiento basico en programación y esta diseñado para ejecutarse en ambientes UNIX. El participante idealmente debe tener experiencia en uso de terminales, y programas de manejo de archivos de texto como **awk, sed, grep, entre otros.**_ 

Este tutorial requiere los siguientes programas (dependencias) para correr:
1. NCBI blast (https://blast.ncbi.nlm.nih.gov/Blast.cgi?PAGE_TYPE=BlastDocs&DOC_TYPE=Download): Este programa permite la construcción de bases de datos blast, y la busqueda (alineamiento) de secuencias de ADN o AA (formato fasta) en bases de datos blast. 
2. NCBI magicblast (https://ncbi.github.io/magicblast/doc/download.html): Este programa permite la busqueda de secuencias de ADN derivadas de secuenciación masiva (formato fasta o fastq) en bases de datos blast.
3. CANU (https://github.com/marbl/canu): este programa permite la corrección y filtrado de secuencias de ONT/PacBio.  
4. SMARTdenovo (https://github.com/ruanjue/smartdenovo): este programa ensambla "de-novo" secuencias corregidas y recortadas de ONT/PacBio.
5. NanoPlot (https://github.com/wdecoster/NanoPlot - version ejecutable en linea: https://nanoplot.bioinf.be/): este programa produce graficas con informaciones asociadas a experimentos de secuenciación conducidos en teconologias ONT 

## Estructura del tutorial/pipeline
Este tutorial esta dividio en tres pasos principales:
1. 

