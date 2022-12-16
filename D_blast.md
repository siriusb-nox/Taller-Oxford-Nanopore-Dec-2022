## ANALISANDO DATOS DERIVADOS DE ONT: BLAST Y WGA

En esta ultima seccion, haremos una demostración de como utilizar datos de ONT despues de que estos hayan sido corregidos y filtrados. Tal vez una de las aplicaciones mas usadas de datos nanopore "in-situ" es el de la identificacion de organismos mediante metodos de alineamiento, e.g. usando [BLAST](https://www.ncbi.nlm.nih.gov/books/NBK279690/). En este ejercicio, ejecutaremos una busqueda de secuencias producidas a partir de un organismos misterioso, encontradoen las vicinidades del jardin botanico Kew. Intentaremos determinar su identidad buscando en una base de datos predeterminada. Para esto ejecutaremos busquedas locales creando bases de datos en `makebklastdb` y `magicblast`. Ejemplos de comandos:

```bash
makeblastdb -in refgenomes_org.test.fasta -out refgenomes_org.test_refDB -parse_seqids -dbtype nucl

magicblast -query archivo_fastq -db refgenomes_org.test_refDB -out ab.out -outfmt tabular -no_unaligned -infmt fastq
```

Pero tambien ejectuaremos busquedas en NCBI (nu dbase) de manera remota (**importante tener acceso a un NCBI API KEY, accessible desde la cuenta individual NCBI de cada uno**):

```bash
export NCBI_API_KEY=09ddca88b438c887b83f8d58fcc890c321XX
blastn -query misterious_seqs.ONT.fasta -db nt -remote -task blastn-short -evalue 0.01 -entrez_query "Asparagales [organism]" -outfmt 6 -out blast_result_misteriousplant.table -max_target_seqs 10 -max_hsps 5
```
El output de este comando se ve asi:

```
93c9b0d6-2802-485b-8998-435462f77771	MW375124.1	93.294	1178	39	13	34	1190	71181	70023	0.0	1659
93c9b0d6-2802-485b-8998-435462f77771	MW375125.1	93.248	1170	48	12	34	1190	71757	70606	0.0	1635
93c9b0d6-2802-485b-8998-435462f77771	NC_043905.1	93.469	1133	42	12	76	1190	70163	69045	0.0	1604
93c9b0d6-2802-485b-8998-435462f77771	MW375128.1	92.760	1174	53	12	34	1189	72076	70917	0.0	1598
93c9b0d6-2802-485b-8998-435462f77771	MW375126.1	93.412	1108	47	11	101	1190	71407	70308	0.0	1560
231acd9d-2063-4509-9ccc-c822ff4f66d7	MF861028.1	94.057	774	23	6	33	799	758	1	0.0	1156
231acd9d-2063-4509-9ccc-c822ff4f66d7	MF861030.1	93.928	774	23	7	33	799	757	1	0.0	1140
231acd9d-2063-4509-9ccc-c822ff4f66d7	MF861029.1	93.928	774	23	7	33	799	757	1	0.0	1140
231acd9d-2063-4509-9ccc-c822ff4f66d7	MF860862.1	94.802	731	22	5	33	756	737	16	0.0	1130
231acd9d-2063-4509-9ccc-c822ff4f66d7	MF860864.1	94.665	731	22	6	33	756	736	16	0.0	1114
0d3193bd-6dca-4f57-bf00-665e9cc55904	MW375130.1	97.489	1314	20	7	30	1339	36038	37342	0.0	2300
0d3193bd-6dca-4f57-bf00-665e9cc55904	MW375125.1	97.184	1314	22	7	31	1339	36381	37684	0.0	2272
0d3193bd-6dca-4f57-bf00-665e9cc55904	MW375127.1	97.260	1314	22	8	31	1339	36864	38168	0.0	2268
0d3193bd-6dca-4f57-bf00-665e9cc55904	NC_043905.1	97.108	1314	24	8	31	1339	35271	36575	0.0	2252
0d3193bd-6dca-4f57-bf00-665e9cc55904	MH979332.1	97.108	1314	24	8	31	1339	35271	36575	0.0	2252
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	KP205432.1	94.507	1693	38	32	27	1683	92658	90985	0.0	2411
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	KP205432.1	94.507	1693	38	32	27	1683	149723	151396	0.0	2411
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375129.1	94.507	1693	38	32	27	1683	92824	91151	0.0	2411
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375129.1	94.507	1693	38	32	27	1683	149917	151590	0.0	2411
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375125.1	94.507	1693	38	32	27	1683	92767	91094	0.0	2411
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375125.1	94.507	1693	38	32	27	1683	149860	151533	0.0	2411
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375130.1	94.448	1693	39	32	27	1683	91332	89659	0.0	2403
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375130.1	94.448	1693	39	32	27	1683	142685	144358	0.0	2403
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375124.1	93.938	1699	42	31	27	1683	92255	90576	0.0	2365
44e5b206-fb13-48d7-9cdc-0b2c51fdc921	MW375124.1	93.938	1699	42	31	27	1683	146901	148580	0.0	2365
b20fe3db-c68c-4c1f-9a3b-c3b27ee92a6d	LC193510.1	97.478	1705	15	11	22	1703	105931	104232	0.0	2985
b20fe3db-c68c-4c1f-9a3b-c3b27ee92a6d	LC193510.1	97.478	1705	15	11	22	1703	129447	131146	0.0	2985
b20fe3db-c68c-4c1f-9a3b-c3b27ee92a6d	NC_044644.1	96.487	1708	24	14	22	1703	104417	102720	0.0	2843
b20fe3db-c68c-4c1f-9a3b-c3b27ee92a6d	NC_044644.1	96.487	1708	24	14	22	1703	132888	134585	0.0	2843

```

Por ultimo, ensamblar genomas con datos ONT ya corregidos es bastante sencillo, dependiendo de que algoritmo se use. En nuestro caso, ejecutaremos `SMARTdenovo`:

```bash
/home/siriusb/softwares/genomics/smartdenovo/smartdenovo.pl -c 1 -t 64 -p prefijo_output /directorio/archivos/fastq.fastq > prefijo_output.mak

make -f *.mak
```
Los archivos base para ejecutar este comando se encuentran en la caperta [NGSdat](https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/tree/main/NGSdat) de este repositorio. **Adicionalmente, favor descargar los archivos fasta disponibles en esta liga:** https://drive.google.com/drive/folders/1zTgYw0CjRzhMqDqoMHpDEdq21G8P1ARv?usp=share_link
