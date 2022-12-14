<p align="center">
  <img src="https://github.com/siriusb-nox/Taller-Oxford-Nanopore-Dec-2022/blob/main/IMG/bash_logo_bashlogo.com.png" alt="bash logo from bash webpage"/>
</p>
  
## Tutorial basico para navegar una terminal en ambientes UNIX

#### 1. Introducción
UNIX es una familia de sistemas operativos (OS) desarrollado en 1960. Tal vez los OSs mas famosos son [Ubuntu](https://ubuntu.com/), [Linux](https://www.linux.org/) y [MacOS](https://www.apple.com/uk/macos/ventura/). En bioinformatica, la _shell_ (i.e., terminal, o el traductor entre las operaciones que el computador hace y las instrucciones en lenguaje "humano") de UNIX es bastante usada ya que contiene una serie de programas basicos pero poderosos para manejar archivos de texto (e.g., secuencias fasta, fastq, genomas, etc). Adicionalmente, muchos programas en bioinformatica estan mas disponibles para ambientes UNIX que otras plataformas (e.g. DOS de Microsoft... urgh!). 

#### 2. Sintaxis
La sintaxis de UNIX en la terminal es muy facil. En cualquier momento que en la terminal aparezca "$" o "%", es porque la terminal esta lista para recibir instrucciones.  Basicamente:

`$programa opcion1 opcion2 input > output`

Las opciones en UNIX son usualmente parametros (en ingles _flags_) que permiten modificar el comportamiento usual/default  de un programa. Estas usualmente se especifican con un "-", Por ejemplo: 

`ls` vs `ls -lrt` - Cual es la diferencia entre ambos comandos?

#### 3. Programas esenciales para navegar la terminal en UNIX e interactuar/visualizar archivos
Aquí una breve lista de programas basicos de UNIX que utilizaremos con mucha frequencia
