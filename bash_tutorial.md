<p align="center">
  <img src="https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/bash_logo_bashlogo.com.png" alt="bash logo from bash webpage"/>
</p>
  
## Tutorial basico para navegar una terminal en ambientes UNIX

#### 1. Introducción
UNIX es una familia de sistemas operativos (OS) desarrollado en 1960. Tal vez los OSs mas famosos son [Ubuntu](https://ubuntu.com/), [Linux](https://www.linux.org/) y [MacOS](https://www.apple.com/uk/macos/ventura/). En bioinformatica, _bash_ (i.e., "bourne Again Shell") o la _shell_ (i.e., terminal, o el traductor entre las operaciones que el computador hace y las instrucciones en lenguaje "humano") de UNIX es un lenguaje bastante usado ya que contiene una serie de programas basicos pero poderosos para manejar archivos de texto (e.g., secuencias fasta, fastq, genomas, etc). Adicionalmente, muchos programas en bioinformatica estan mas disponibles para ambientes UNIX que otras plataformas (e.g. DOS de Microsoft... urgh!). 

#### 2. Sintaxis
La sintaxis de UNIX en la terminal es muy facil. En cualquier momento que en la terminal aparezca "$" o "%", es porque la terminal esta lista para recibir instrucciones.  Basicamente:

`$programa opcion1 opcion2 input > output`

Las opciones en UNIX son usualmente parametros (en ingles _flags_) que permiten modificar el comportamiento usual/default  de un programa. Estas usualmente se especifican con un "-", Por ejemplo: 

`ls` vs `ls -lrt` - Cual es la diferencia entre ambos comandos?

#### 3. Programas esenciales para navegar la terminal en UNIX e interactuar/visualizar archivos
Aquí una breve lista de programas basicos de UNIX que utilizaremos con mucha frequencia:

#### 3.1 `cd`
"Change directory" se usa para cambiar de una carpeta/directorio a otro. Por ejemplo:

```bash
cd
```
Para subir una carpeta arriba, usar. Adicionalmente, _cd_ acpeta una direccion de directorio completa, p.ej **/home/usr/etc**:

```bash
cd ..
cd /home/usr/etc
```

### 3.2 `mkdir`
Crea nuevas carpetas.  

```bash
mkdir carpetanueva
```
Varias carpetas se pueden crear de manera simultanea, p.ej.:
```bash
mkdir carpeta1 carpeta2 carpeta3
```
Directorios completos se pueden crear con la opcion _-p_, así:
```bash 
mkdir -p /home/usr/foo/bla/
```
Carpetas se pueden tambien crear en subdirectorios ya existentes, usando una direccion ya existente. Por ejemplo, crear 'bioinf' en '/home/usr/foo/bla/':

```bash 
mkdir /home/usr/foo/bla/bioinf
```

### 3.3 `pwd`
Muestra el directorio en el que uno se encuentra
```bash
pwd
```

### 3.4 `ls`
Hace un listado de los archivos o carpetas presentes en un directorio. `ls` tiene muchas opciones... Por ejemplo, la opcion `-l` presenta una lista detallada de los archivos/carpetas, mostrando info como tamaño exacto de los archivos, propietario, acceso, y fecha de modificacion.

```bash
ls
ls -l
```

### 3.5 `cat`
Se usa para visualizar archivos "no binarios", e.g.: 
* Ver archivos de texto en la terminal
* Combinar archivos de texto  
 
```bash
cat archivo.txt
cat archivo1.txt archivo2.txt
cat archivo1.txt archivo2.txt > archivocombinado.txt
cat < archivo1.txt > archivo2.txt
```

### 3.6 `less`
Se usa para navigar archivos "no binarios", e.g.: 

```bash
less input.txt
```
Por ejempo, `less`puede ser utilizado para dar una mirada rapida a un archivo fastq, asi (archivo disponible en el tutorial, primero descomprimir usando `gunzip`):

```bash
cat /directorio/personal/Taller-Oxford-Nanopore-Dec-2022/NGSdat/Cinchona_PAD61320_sizeSelect_1Kseq_99.fastq
```

### 3.7 `grep`
Este programa busca patrones de texto, incluyendo [_expresiones regulares_](https://sospedia.net/el-shell-bash-de-gnulinux-4-expresiones-regulares/). 

```bash
grep opcion1 opcion2 input
```

Por ejemplo, podemos buscar el nombre de una secuencia ("@7318713f-55b4-4e19-8fb1-4bd89b35568e") en especifico en un archivo fastq asi: 

```bash
grep "^@7318713f-55b4-4e19-8fb1-4bd89b35568e" /directorio/personal/Taller-Oxford-Nanopore-Dec-2022/NGSdat/NGSdat/Cinchona_PAD61320_sizeSelect_1Kseq_99.fastq
```

... hay muchos otros programas mas que nos permiten visualizar datos que recomendamos aprender. Algunos ejemplos están disponibles [aqui](https://www.biostars.org/p/17680/).

### 3.8 `man`
Este programa provee información detallada sobre programas basicos de UNIX.

```bash
man programa
man ls
```
