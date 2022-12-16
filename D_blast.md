## ANALISANDO DATOS DERIVADOS DE ONT: BLAST Y WGA

En esta ultima seccion, haremos una demostración de como utilizar datos de ONT despues de que estos hayan sido corregidos y filtrados. Tal vez una de las aplicaciones mas usadas de datos nanopore "in-situ" es el de la identificacion de organismos mediante metodos de alineamiento, e.g. usando [BLAST](https://www.ncbi.nlm.nih.gov/books/NBK279690/). En este ejercicio, ejecutaremos una busqueda de secuencias producidas a partir de un organismos misterioso, encontradoen las vicinidades del jardin botanico Kew. Intentaremos determinar su identidad buscando en una base de datos predeterminada. Para esto ejecutaremos busquedas locales creando bases dedatos en makebklastdb:

```bash
makeblastdb -in refgenomes_org.test.fasta -out refgenomes_org.test_refDB -parse_seqids -dbtype nucl
```

```bash
export NCBI_API_KEY=09ddca88b438c887b83f8d58fcc890c32109
blastn -query misterious_seqs.ONT.fasta -db nt -remote -task blastn-short -evalue 0.01 -entrez_query "Asparagales [organism]" -outfmt 6 -out blast_result_misteriousplant.table -max_target_seqs 10 -max_hsps 5
```
