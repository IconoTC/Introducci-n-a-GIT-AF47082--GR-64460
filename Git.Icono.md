# GIT (20h)

- Cliente: SIA Group
- Fechas: 7 – 10 octubre
- Horario: 9:30-13:30h
- Duración: 16 horas
- Modalidad: Virtual

## Contenidos

- Conceptos básicos
  - ¿Qué es y que no es GIT?
  - Cómo usar correctamente GIT
  - Configuración imprescindible
- Fundamentos y arquitectura interna de GIT
  - Diferencias entre el working directory, el stage y el repositorio
  - Qué es exactamente un commit
  - Tipos de referencias (HEAD, ramas y tags)
- Commits
  - Cómo preparar selectivamente un commit
  - Cuando hacer un commit
    -Cómo deshacer commits
  - Buenas prácticas
- Branching
  - Qué es exactamente una rama en GIT
  - Cómo trabajar con ramas y diferentes maneras de fusionarlas
  - Qué es un conflicto, cómo reducir su frecuencia y cómo resolverlos
  - Modelos de branching
  - Git Flow
- Trabajando con repositorios remotos
  - Cómo comunicar los repositorios locales con los remotos
  - Diferentes escenarios cuando trabajamos en equipo contra un repositorio remoto
  - Configuración básica
- Pull Requests
  - Por qué usar PR
  - Cómo hacer correctamente una PR
  - Cómo configurar el repositorio remoto si usamos “PR”

## Día 1. Conceptos básicos

### Introducción

#### Qué es un SCV

Los sistemas de control de versiones (SCV) son una herramienta esencial para manejar proyectos de software; lo que ha hecho de ellos herramientas de uso habitual en el desarrollo profesional de software desde hace décadas.

Proporcionan una serie de funcionalidades claves para el desarrollo de proyectos como es

- el control de cambios en el código,
- la reversibilidad de dichos cambios,
- la posibilidad de colaborar en el desarrollo del código.

Además, los SCV permiten tener en paralelo varias versiones o ramas del proyecto. Las ramas se utilizan para desarrollar funcionalidades aisladas de los cambios en otras partes del proyecto que posteriormente pueden integrarse en la rama principal.

#### Tipos de SCV: centralizados y distribuidos

Los **SCV centralizados** como CVS y Subversion (SVN) son sistemas cliente-servidor donde hay un repositorio canónico en el servidor que contiene toda la información de los cambios mientras que los clientes solo tienen copias de trabajo.

![SVC centralizado](assets/svc-centralized.png)

En **sistemas distribuidos** como Mercurial y Git no existe el concepto de repositorio canónico por lo que cada cliente ha de tener una copia completa del repositorio. Desde 2010, la tendencia es utilizar cada vez más SCV distribuidos, en particular Git

![SVC distribuido](assets/svc-distributed.png)

#### Git: un SCV distribuido: Historia de GIT

Git es un sistema de control de versiones distribuido que fue creado por _Linus Torvalds_ en 2005 para el desarrollo del kernel de Linux. Es un sistema de control de versiones escrito mayoritariamente en **C**, de **código abierto** y **gratuito** que es muy rápido y eficiente.

Git es un software diseñado pensando en la **eficiencia** y la **confiabilidad** del mantenimiento de versiones y aplicaciones cuando éstas tienen un **gran número de archivos** de código fuente.

En comparación con otros sistemas de control de versiones, Git es más rápido y tiene un tamaño de repositorio más pequeño. También tiene una **escalabilidad** muy buena, lo que significa que puede manejar proyectos muy grandes y muy pequeños.

En el contexto en el que fue diseñado, las dos principales opciones eran SVN y Mercurial. Git se diseñó para ser más rápido y eficiente que Mercurial, aunque conservando su estrategia de SVC distribuido, y más fácil de usar que SVN.

#### Características de Git como SCV distribuido

La experiencia del equipo de _Linus Torvalds_ en la gestión de la integración de las diferentes aportaciones en un proyecto distribuido de la magnitud del kernel de Linux determinó los objetivos del proyecto

- Rapidez
- Simplicidad de uso
- Multiplicidad de versiones (Ramas)
- Distribuido: capaz de trabajar sin conexiones
- Preparado para grandes proyectos

Estos objetivos se reflejaron en las siguientes decisiones de implementación:

**Versiones no incrementales**. Git almacena cada cambio como una instantánea de todos los archivos del proyecto. Para ser eficiente, si el archivo no ha sido modificado, sólo se almacena un enlace al archivo idéntico previamente almacenado. Los SCV anteriores a Git habitualmente almacenaban solo una versión base y las modificaciones hechas en cada cambio por archivo.

**Trabajo fuera de línea**. Por ser un sistema distribuido, cada repositorio de Git es un repositorio completo capaz de funcionar sin acceso a la red o al resto de los repositorios distribuidos gracias a que contiene una copia local de la historia completa del desarrollo del proyecto. Los cambios en la historia pueden copiarse de un repositorio a otro como nuevas ramas de desarrollo y se pueden copiar de la misma manera que una rama de desarrollo local.

- Cada operación se realiza en el **repositorio local**.
- No necesita conexión con un servidor.
- Se puede trabajar normalmente sin conexión (**offline**)
- Es más **rápido** que los repositorios centralizados

**Autenticación criptográfica de la historia**. El identificador de un cambio se computa utilizando un algoritmo criptográfico que utiliza como entrada el cambio y la historia completa de cambios. Esto permite que cualquier cambio de la información durante la transmisión o en sistema de archivos sea detectado por Git.

- Todo está identificado por secuencias **hash**, como 24b9da6552252987aa493b52f8696cd6d3b00373
- ELos hashes son **inmutables**: imposible cambiar el contenido de cualquier archivo o directorio sin que Git lo sepa.
- No se puede perder información ni dañar el archivo sin que Git pueda detectarlo.

### Instalación y configuración inicial

Disponible en la [web](https://git-scm.com/) para Windows, Mac y Linux.
En este momento (octubre 2024) la versión disponible es la 2.46.2.

En la instalación guiada pueden indicarse algunos elementos de configuración como:

- los complementos incluidos (iconos, integración con el entorno)
- el editor que utilizará Git (e.g. Visual Studio Code o VSC).
- el ajuste del path para permitir su uso en diversos terminales
- el transporte HTTPS, generalmente openSSH
- la codificación de los saltos de línea (CRLF o LF)
- las opciones de terminal (minTTY, cmd, powershell)
- la gestión de las credenciales (credential helper)
- la cache de ficheros y la posibilidad de incluir enlaces simbólicos (desactivada por defecto)

#### Terminales

Git es una herramienta de línea de comandos desarrollada inicialmente para el Bash de Linux. En Windows, Git se instala con un terminal propio que es una versión de MinTTY, un emulador de terminal para Windows que permite el uso de Bash, conocida como **GitBash**.

Sin embargo, Git puede utilizarse en cualquier terminal de Windows, como el **cmd** o el **PowerShell**. Para ello, es necesario ajustar el path de Windows para que el ejecutable de Git esté disponible en todas las terminales, lo que se puede hacer en la instalación de Git.

##### PowerShell

El powershell de Windows es un terminal más potente que el cmd y que el propio GitBash, pero menos utilizado en el desarrollo de software. Puede configurarse para que funcione específicamente con Git añadiendo el plugin [posh-git](https://github.com/dahlbyk/posh-git).

La web de [Git](https://git-scm.com/book/es/v2/Ap%C3%A9ndice-A%3A-Git-en-otros-entornos-Git-en-Powershell) proporciona una guía para la configuración de Git en Windows que incluye la configuración de las powershell.

El primer paso es habilitar la ejecución de scripts en PowerShell con el comando, adecuado, según se trate de hacerlo para el usuario actual o para todos los usuarios del sistema.

```shell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy RemoteSigned -Force
```

El siguiente paso es instalar el módulo de posh-git con el comando

```shell
Install-Module posh-git -Scope CurrentUser -Force
```

Finalmente hay que añadir la importación del módulo en el fichero de configuración de PowerShell, que se encuentra en el directorio de usuario en el fichero `Microsoft.PowerShell_profile.ps1`. Para ello, se pueden utilizar los comandos

```shell
Import-Module <path-to-uncompress-folder>\src\posh-git.psd1
Add-PoshGitToProfile -AllHosts
```

##### El comando less

git muestra la información usando el comande less, que permite desplazarse por la información mostrada. Los comandos básicos son

:f -> scroll next page
:b -> scroll previous page
:q -> quit

#### Configuración

Git se configura a tres niveles

- **Sistema**. Archivo /etc/gitconfig: Contiene valores para todos los usuarios del sistema y todos sus repositorios. Si pasas la opción `--system` a git config, lee y escribe específicamente en este archivo.
- **Global o usuario**. Archivo ~/.gitconfig: Específico a tu usuario. Puedes hacer que Git lea y escriba específicamente en este archivo pasando la opción `--global`.
- **Repositorio**. Archivo config "local", en el directorio de Git (es decir, .git/config) del repositorio que estés utilizando actualmente: Específico a ese repositorio.

Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de .git/config tienen preferencia sobre los de /etc/gitconfig

Para conocer la configuración actual de Git, se puede utilizar el comando

```shell
git config --list
git config --list --show-origin
```

que mostrará la configuración actual de Git y en el segundo caso, el archivo donde se ha definido.

Para ver solo la configuración global, se puede utilizar

```shell
git config --global -l
```

Para editar la configuración global, se puede utilizar el comando `git config --global` añadiendo la clave y el valor que se quiere añadir.

Los valores imprescindibles son

```shell
git config --global user.name "Alejandro Cerezo"
git config --global user.email "alce65@hotmeil.es"
```

Si no se define el name y el email, Git no permitirá hacer commits.

Otros valores que se pueden definir son

```shell
git config --global core.editor "code --wait --new-window"
git config --global init.defaultBranch main
git config --global core.autocrlf false
git config --global core.ignorecase true
```

Los dos primeros, probablemente estarán definidos a nivel system durante la instalación de Git.
El segundo es una opción que se ha añadido en la versión 2.28 de Git para cambiar el nombre de la rama principal de los repositorios de Git de master a main.

En caso de tener un repo cuya rama principal se llame master, se puede cambiar el nombre de la rama principal con el comando

```shell
git branch -m master main
```

El tercero y el cuarto son recomendables para evitar problemas con los saltos de línea en Windows y con la sensibilidad a mayúsculas y minúsculas.

### Referencias

- [Git Reference](https://git-scm.com/docs)
  Documentación oficial de Git.

- [Pro Git](https://git-scm.com/book/en/v2)
  Free book on Git. _Scott Chacon_ and _Ben Straub_. 2014.

- [Gitting Things Done – A Visual and Practical Guide to Git [Full Book]](https://www.freecodecamp.org/news/gitting-things-done-book/) _Omer Rosenbaum_. 2024

- [git - the simple guide](https://rogerdudler.github.io/git-guide/)
  Cheat sheet de git. _Roger Dudler_. 2013.

- [Think Like (a) Git](https://think-like-a-git.net/)

### Quick start

#### Comandos básicos de Git

- `git init`: Inicializa un repositorio local de Git
- `git status`: Muestra el estado de los archivos en el directorio de trabajo (workArea) y el área de preparación
- `git add`: Agrega un archivo al área de preparación (stagedArea)
- `git commit`: Guarda los cambios en el repositorio
- `git log`: Muestra el historial de commits
- `git show`: Muestra los cambios de un commit
- `git clone`: Clona un repositorio de Git

#### Primeros pasos

##### Primer repo (init)

Para crear un repositorio local de Git, se utiliza el comando `git init`. Este comando crea un directorio oculto `.git` en el directorio actual que contiene todos los metadatos necesarios para el control de versiones.

```shell
git init
```

Si no se indica nada, Git creará un repositorio en el directorio actual. Si se quiere crear un repositorio en un directorio específico, se puede indicar el directorio como argumento del comando.

```shell
git init nombre_del_repo
```

Por convención se suelen añadir dos ficheros en el directorio raíz del repositorio:

- `.gitignore`: Fichero que contiene los patrones de nombres de ficheros y directorios que Git ignorará.
- `README.md`: Fichero que contiene información sobre el repositorio.

El primero de ellos debe excluir las dependencias a terceros, los ficheros generados y los ficheros de configuración. Su contenido dependerá del lenguaje de programación y las herramientas que se utilicen en el proyecto.

Por ejemplo, para un proyecto en JS, el fichero `.gitignore` podría contener

```shell
node_modules
dist
```

El `README.md` debe contener información sobre el repositorio, como su propósito, su estructura y su uso. Si nuestro repo va a ser publico en Github, se considera una falta de cortesía no añadir un README.md. Además, es recomendable añadir una licencia y un fichero `LICENSE.md` con la licencia que se va a utilizar.

##### Anatomía de un repositorio git: staging area, index and cache

Para entender el funcionamiento de Git, nuestro modelo mental representara un repositorio de Git como tres áreas:

- `Working Area`: Directorio de trabajo
- `Staging Area`: Área de preparación
- `Repository`: Repositorio -> conjunto de commits y etiquetas

La working area es el directorio de trabajo donde se encuentran los ficheros del proyecto.

La staging area es un área intermedia donde se preparan los cambios antes de hacer un commit. Esto permite seleccionar los cambios que se quieren incluir en el commit ignorando por el momento los que no se quieren incluir.

El repositorio es el lugar donde se almacenan los commits y las etiquetas.

![Areas de un repositorio Git](assets/git-areas.svg)

Los ficheros cambian su estado en función de las operaciones que se realicen con ellos y de su relación con estas áreas de Git. Los estados posibles son

- `Untracked` (sin seguimiento): Fichero no seguido por Git
- `Tracked`(con seguimiento): Fichero seguido por Git
  - `Modified`(modificado): Fichero modificado
  - `Staged` (preparado): Fichero añadido al área de preparación
  - `Committed` (confirmado): Fichero añadido al repositorio

Los comandos básicos de Git son los que permiten mover los ficheros entre estas áreas:

En el sentido habitual de trabajo, los comandos son

- `git add <pattern>`: Mueve los ficheros de la working area a la staging area
- `git commit`: Mueve los ficheros de la staging area al repositorio

En el sentido contrario, los comandos son, como luego veremos

- `git checkout <pattern>`: Mueve los ficheros de la staging area a la working area
- `git reset <pattern>`: Mueve los ficheros de la staging area al working area

##### Añadir contenidos al repositorio. Primer commit

Teniendo en cuenta el modelo mental de un repositorio de Git, nuestro trabajo inicial yy habitualmente seguirá los siguientes pasos:

1. Crear un repositorio local de Git con `git init`
2. Acceder al directorio de trabajo con `cd`
3. Crear los ficheros del proyecto
4. Comprobar el estado del repositorio con `git status`
5. Añadir los ficheros al repositorio con `git add`
6. De nuevo, comprobar el estado del repositorio con `git status`
7. Hacer el primer commit con `git commit`
8. Comprobar el historial de commits con `git log`

```shell
git init sample
cd sample
git status
echo 'Sample One' > sample1.txt
echo 'Sample Two' > sample2.txt
git add .
git status
git commit -m "Initial commit"
git log
git log --graph --decorate --oneline
```

##### Git add

**Git add** es el comando que se utiliza para añadir ficheros al área de preparación. Se puede utilizar de varias formas

`git add <fichero>` añade un solo fichero.
`git add <patrón>` añade todos los ficheros que coincidan con el patrón, e.g. `git add *.txt`
`git add .` añade todos los ficheros del directorio de trabajo al área de preparación.

Git add no añade los ficheros al repositorio, solo los añade al área de preparación. Es el paso previo a hacer un commit.

##### Git status

**Git status** nos muestra el estado de los ficheros en el directorio de trabajo y en el área de preparación.
Nos indica qué ficheros han sido

- modificados (M)
- añadidos (U de untracked)
- eliminados (D)

Igualmente indica si están en el área de preparación o no.

Se puede utilizar `git status -s` para obtener una salida más compacta.

Además de `git status`, muestra información de alguna de las operaciones posibles en función de los ficheros que detacta en el directorio de trabajo y en el área de preparación.

##### Git commit. Mensajes de commit

**Git commit** es el comando que se utiliza para guardar en el repositorio los cambios que previamente se han añadido al área de preparación con `git add`.

```shell
git commit -m "Mensaje del commit"
```

Un commit es una **instantánea** (**snapshot**) de los cambios en el repositorio. En el se guardan los ficheros nuevos o modificados que se han añadido al área de preparación. Cada commit tiene una serie de elementos

- un SHA (Secure Hash Algorithm) que es un identificador único
- un autor
- un mensaje que describe los cambios realizados
- una fecha y hora de creación
- una referencia al commit padre (excepto el primer commit)
- un árbol cambios en los archivos y directorios

Más adelante veremos en que consisten exactamente los commits desde un punto de vista técnico, y como se combinan con otros elementos de git, **blobs** y **trees**, para construir el repositorio.

Los **mensajes de commit** son una parte muy importante de Git. Un buen mensaje de commit debe

- solo la primera palabra en mayúsculas
- comienza con un verbo en imperativo
- no se termina el mensaje con un punto
- no ser más largo de 50 (70) caracteres
- no ser un resumen de los cambios
- ser conciso y descriptivo
- contar su qué y sobre todo por qué, cómo
- reflejar la granularidad del commit

##### git log / git show

**Git log** es el comando que se utiliza para ver el historial de commits de un repositorio. Muestra los commits en orden cronológico inverso, es decir, el último commit en la parte superior.

```shell
git log
```

Es un comando con gran número de opciones que permiten personalizar la salida del comando. Por ejemplo, `git log --oneline` muestra los commits en una sola línea. Más adelante volveremos a hablar de este comando.

**Git show** es el comando que se utiliza para ver los cambios de un commit. Muestra los cambios realizados en un commit en relación con su padre.

```shell
git show
```

### Comandos de Git: Referencias y paths

#### Anatomía de comandos típicos, referencias vs paths

Los comandos de Git siguen una estructura común que se compone de

- Comando y opciones
- Flags
- Paths
- Referencias

Por ejemplo

```shell
git log --graph --decorate --oneline
```

- `git`: Comando
- `log`: Opción
- `--graph`, `--decorate`, `--oneline`: Flags

```shell
git add *.js
```

- `git`: Comando
- `add`: Opción
- `*.js`: Paths

```shell
git show HEAD~1
```

- `git`: Comando
- `show`: Opción
- `HEAD~1`: Referencia

En algunos contexto puede ser válida tanto una referencia como un path. Por ejemplo, en el comando `git checkout`, el path puede ser un fichero o directorio o una referencia a un commit.
El **doble guion** permite separar un nombre de archivo explícitamente identificado

- Checkout the tag named “main.c”

```shell
git checkout main.c
```

- Checkout the file named “main.c”

```shell
git checkout -- main.c
```

#### Paths

Los paths son los ficheros y directorios que se quieren incluir en una operación de Git. Su estructura sigue los criterios del sistema operativo y utiliza los siguientes caracteres especiales

- `.`: Directorio actual
- `..`: Directorio padre
- `/`: Separador de directorios
- `~`: Directorio home del usuario
- `*`: Comodín para cualquier cadena de caracteres
- `?`: Comodín para un solo carácter
- `[]`: Comodín para un rango de caracteres

#### Tipos de referencias

Las referencias son los commits y las ramas a los que se quiere hacer referencia.

- Absolutas: SHA1 que identifica un commit o su sub-cadena (5 primeros caracteres)
- Simbólicas: mediante etiquetas: HEAD, master (otras ramas) y otras referencias útiles (tags)
- Relativas: desde cualquiera de las anteriores, se puede acceder a commits anteriores o posteriores
- Por mensaje de commit (:/cadena)

#### Referencias simbólicas

Las referencias simbólicas son las etiquetas de Git:

- HEAD: Puntero a la rama actual
- Rama: puntero al commit actual (normalmente el ultimo)
- Etiquetas (Tags): Pueden ser anotadas o ligeras

#### Referencias relativas

Las referencias relativas permiten acceder a commits anteriores o posteriores a un commit dado.

Utilizan los siguientes operadores

- ~ (tilde): seguido de un número, indica el commit al que acceder
- ^ (circunflejo): el padre

Por ejemplo

- `HEAD~1`: El padre del commit actual
- `HEAD~n`: El n-ésimo padre del commit actual
- `HEAD^`: El padre del commit actual
- `HEAD^^`: El abuelo del commit actual

### Integración con otras herramientas y entornos

#### Clientes gráficos

Cliente incluido en la instalación de Git ¿alguien lo usa?

Otros clientes gráficos según la [web de Git](https://git-scm.com/download/gui/windows)

- GitHub Desktop
  Platforms: Mac, Windows
  Price: Free
  License: MIT

- SourceTree
  Platforms: Mac, Windows
  Price: Free
  License: Proprietary

- TortoiseGit
  Platforms: Windows
  Price: Free
  License: GNU GPL

#### Entornos de desarrollo

##### VSCode

VSC (Visual Studio Code) incluye soporte nativo para Git, permitiendo realizar las operaciones más comunes desde el propio editor.

Además existen numerosos plugins que amplían las funcionalidades de Git en VSC

- Git Graph
- GitLens
- Git History

#### Repositorios remotos (hosting de repositorios)

Con el fin de hacer disponible los repositorios de Git en la red, existen en Git 2 tipos de repositorios

- **Bare** (desnudo, simple): no tiene directorio de trabajo. No se usa para el directamente en el desarrollo de aplicaciones ya que en él no se pueden realizar directamente commits. De este tipo son los repositorios que se publican, en servidores estándar o especializados en el alojamiento (hosting) de repositorios
- **Desarrollo**: repositorio típico. Mantiene la rama en la que se trabaja, proporciona una copia extraída de dicha rama en el **directorio de trabajo**

El primero de estos formatos se utiliza para publicar los repositorios en servidores de Git públicos, como **Github**, **GitLab** o **Bitbucket** o pertenecientes a una determinada empresa.

El establecimiento de la relación entre el repositorio local y el remoto se puede realizar en cualquiera de las dos direcciones:

- Desde el repositorio local al remoto, mediante el comando `git remote add`

```shell
git remote add origin <url>
git push -u origin main
```

- Desde el repositorio remoto al local, mediante el comando `git clone`

```shell
git clone <url>
```

![Relaciones entre repositorios local y remoto](assets/local_n_remote.svg)

Cualquiera que sea la forma en que se han creado, una vez que existe un remote, los dos operaciones principales en relación xcon el son

- `git push`: Sube todos los cambios locales al repositorio remoto
- `git pull`: Descarga los cambios del repositorio remoto al repositorio local

#### Comandos de conexión y uso del repositorio remoto (resumen)

- `git clone <url>`
- `git remote add origin https://github.com/alce65/nombre_del_repo.git`
- `git push -u origin main`
- `git push`
- `git pull`

## Dia 2. Fundamentos. Comits

### Fundamentos y arquitectura interna de Git

#### Git internals: Plumbing commands

Para conocer/manipular la estructura interna de Git, se utilizan los **plumbing commands** (comandos de fontanería).
Estos comandos son los que utiliza el propio Git internamente para construir los comandos de más alto nivel conocidos como **porcelain commands**.

#### La carpeta .git

En términos de sistema de ficheros, un repositorio Git es una carpeta que incluye un directorio oculto `.git`.
Éste contiene toda la información necesaria para el control de versiones:

- **Objetos**: blobs, trees, commits, tags anotadosls
- **Referencias**: HEAD, master branch, tags ligeros
- Hooks: scripts que se ejecutan en determinados eventos
- Info y Logs: información extra sobre el repo y los commits
- fichero Index: área de preparación
- fichero de configuración local

```shell
tree .git
tree .git/objects /f
```

Se puede ver que el resultado muestra como la carpeta objects consta de una serie de cartetas/archivos que contienen los objetos de Git, por el momento.

- blobs (los archivo)
- trees (los directorios)
- commits (los snapshots)

Más adelante veremos un cuarto tipo de objeto, los tags (anotadas).

#### Hashes: creación y lectura

La siguiente descripción refleja la forma de explicar estos conceptor propuesta por _Paolo Perrotta_ en su conferencia _Understanding Git_, 3 diciembre 2016, disponible en [YouTube](https://www.youtube.com/watch?v=nHkLxts9Mu4).

En su capa más profunda Git es un **mapa de objetos** de acuerdo con un patrón clave/valor. Cada objeto es un cierto contenido (valor) que tiene un hash que lo identifica (clave).

Existe un comando de git que permite obtener el hash de un objeto, `git hash-object`. Este comando toma un archivo o cualquier contenido y devuelve el hash del objeto creado.

```shell
echo "Hello, World" | git hash-object --stdin
// 110fdc0ce1c7582e08f31e17bbcfdec1b50a478c
```

En este comando, el hash para un mismo contenido y en el mismo shell siempre será el mismo. El shell influye porque en cada uno de ellos el stdin es distinto.

El mismo contenido de un archivo siempre tendrá el mismo hash de 40 bytes, sin importar el nombre del archivo o la ubicación en el sistema de archivos. Este hash es único para el contenido con una probabilidad tan alta que se puede considerar único.

> Un hash SHA-1 es un número hexadecimal de 40 caracteres que se utiliza para identificar de forma única los objetos de Git. Se calcula a partir del contenido del objeto y de su tipo.

Si añadimos al comando la opción `-w`, para guardar el objeto obtendremos un mensaje de error porque no nos encontramos en un repositorio de Git.

```shell
echo "Hello, World" | git hash-object -w --stdin
// fatal: not a git repository (or any of the parent directories): .git
```

El mapa de hashes creado por Git se convierte en **persistente** gracias a la existencia de un **repositorio**, que es básicamente un directorio `.git/objects` que contiene todos los objetos de git. Cada objeto es guardado en un archivo con el nombre del hash del objeto.

Creamos un repositorio vacío y guardamos el objeto en el repositorio.

```shell
git init sample-repo
cd sample-repo
dir /a:hd // [= ls -a]
echo "Hello, World" | git hash-object -w --stdin //110fdc0ce1c7582e08f31e17bbcfdec1b50a478c
cd git
dir
cd objects
dir
cd 11
dir // 0fdc0ce1c7582e08f31e17bbcfdec1b50a478c
```

> El repositorio es una **base de datos de objetos** que se almacena en la carpeta oculta `.git`, que contiene los objetos de git en la carpeta objects.
> Por **cada hash** se crea una carpeta con los primeros dos caracteres del hash y dentro de esta carpeta se crea un fichero cuyo nombre es el resto del hash, que contiene la información correspondiente a ese hash en un formato comprimido.

De cada objeto guardado en un archivo se puede recuperar la información que contiene a partir del hash del objeto.

```shell
git cat-file -t 110fdc0 // blob
git cat-file -p 110fdc0 // Hello, World
```

Cada objeto es accesible por los 5 primeros caracteres de su hash:
la carpeta (2 caracteres) + inicio del fichero (3 caracteres)

#### Elementos de un repositorio- Primer commit

Creamos un proyecto muy simple.

```shell
cd cook.book
```

C:.
│ menu.txt // Apple Pie
└───recipes
apple_pie.txt
readme.txt

```shell
cd cook.book
type menu.txt
// Apple Pie
type .\recipes\readme.txt
// Put your recipes in this folder, one for file.
type .\recipes\apple_pie.txt
//Apple Pie
```

Creamos un **repositorio** en el proyecto con un **commit inicial**.

```shell
cd cook.book
git init
git status
git add .
git commit -m "Initial commit"
```

Vemos el resultado en la carpeta objects del repositorio.

```shell
cd .git
cd dir /w // [25]   [5d]   [77]   [8d]   [9e]
cd 1f
```

Comprobamos los **logs** del repositorio

```shell
git log

commit 5da6f7b4682638317b18a5fe0f9edca98aeb1f7c (HEAD -> main)
Author: Alejandro Cerezo <alce65@hotmail.es>
Date:   Sat Sep 28 13:14:18 2024 +0200

    Initial commit
```

El **commit** corresponde al objeto 5d-a6f7b4682638317b18a5fe0f9edca98aeb1f7c que podemos leer con `git cat-file`.

```shell
git cat-file -p 5da6f7b

tree 8de329e56d2bf59ad7ce6df33df79e91a2a4a5a8
author Alejandro Cerezo <alce65@hotmail.es> 1727522058 +0200
committer Alejandro Cerezo <alce65@hotmail.es> 1727522058 +0200

Initial commit
```

Un resultado similar se consigue con el comando `git show --pretty=raw`, aunque en este caso se añade la información del diff.

```shell
git show 5da6f7b

commit 5da6f7b4682638317b18a5fe0f9edca98aeb1f7c
tree 8de329e56d2bf59ad7ce6df33df79e91a2a4a5a8
author Alejandro Cerezo <alce65@hotmail.es> 1727522058 +0200
committer Alejandro Cerezo <alce65@hotmail.es> 1727522058 +0200

    Initial commit

diff --git a/menu.txt b/menu.txt
new file mode 100644
```

Un commit no es mas que un texto, que como cualquier otro objeto de git, tiene un hash que lo identifica. En este texto se incluye la metadata del commit, como el autor, el committer, el mensaje al crearlo y la referencia uno o varios hashes.

En este caso, el commit apunta a un objeto de tipo tree que podemos leer con `git cat-file`.

```shell
git cat-file -p 8de329e

100644 blob 9eed377bbdeb4aa5d14f8df9cd50fed042f41023    menu.txt
040000 tree 25036a158dfdf583f672c11ef79f45c6b0e6347a    recipes
```

El **tree** guarda los nombres de los archivos y directorios (otros tree) que incluye, junto con sus hashes. En este caso, el tree apunta a dos objetos, uno de tipo blob y otro de tipo tree, que nuevamente podemos leer con `git cat-file`.

```shell
git cat-file -p 9eed377

Apple Pie
```

```shell
git cat-file -p 25036a1

100644 blob 9eed377bbdeb4aa5d14f8df9cd50fed042f41023    apple_pie.txt
100644 blob 7708256b70bf5e956ea609a785911a31fc14929f    readme.txt
```

En el caso del tree, la misma información se puede obtener con `git ls-tree`.

```shell
git ls-tree 8de329e

100644 blob 9eed377bbdeb4aa5d14f8df9cd50fed042f41023    apple_pie.txt
100644 blob 7708256b70bf5e956ea609a785911a31fc14929f    readme.txt
```

El objeto tree `25036a1` apunta a dos objetos de tipo blob que . Uno de ellos es nuevamente 9eed377, porque el contenido de `apple_pie.txt` es el mismo que el de `menu.txt`. El otro objeto blob lo podemos leer con `git cat-file`.

```shell
git cat-file -p 7708256

Put your recipes in this folder, one for file.
```

![Primer commit](assets/commit1.svg)

#### Modificación de un archivo

Añadimos otra línea en el archivo `menu.txt` y comprobamos los cambios.

```shell
cd ..\..\..\cook.book
echo Cheesecake>> menu.txt
type menu.txt
```

Creamos un nuevo commit para incorporar los cambios.

```shell
git add .
git commit -m "Add Cheesecake to menu"
git log

commit f1dff43f97543e83cab3f52f054cdcf9b26e8d55 (HEAD -> main)
Author: Alejandro Cerezo <alce65@hotmail.es>
Date:   Sat Sep 28 14:03:08 2024 +0200

    Add Cheesecake to menu
```

De nuevo, el commit es un objeto de tipo que podemos leer con `git cat-file`.

```shell
git cat-file -p f1dff4

tree 972e64a00a72e413bd158352ab3e6e98461bfbea
parent 5da6f7b4682638317b18a5fe0f9edca98aeb1f7c
author Alejandro Cerezo <alce65@hotmail.es> 1727524988 +0200
committer Alejandro Cerezo <alce65@hotmail.es> 1727524988 +0200

Add Cheesecake to menu
```

El commit apunta a un objeto de tipo commit, el commit anterior y a un nuevo objeto de tipo tree que podemos leer con `git cat-file`.

```shell
git cat-file -p 972e64a

100644 blob 48459e5685c4561d0fa6e26a7371041e982c0ff4    menu.txt
040000 tree 25036a158dfdf583f672c11ef79f45c6b0e6347a    recipes
```

El tree sigue siendo el mismo, pero el objeto blob `48459e5` es diferente al anterior.
Si lo leemos con `git cat-file` vemos que contiene la nueva línea.

```shell
git cat-file -p 48459e5

Apple Pie
Cheesecake
```

![Primer commit](assets/commit2.svg)

Utilizando un commit como punto de entrada es posible recorrer todos los objetos de un repositorio de git correspondientes al momento en que se creó el commit, reconstruyendo a partir de ellos el estado del proyecto en ese momento, lo que denominamos una **snapshot del proyecto**.

Cuando un fichero no cambia, git no guarda una nueva versión del fichero, sino que guarda una referencia al fichero anterior. De esta forma, git ahorra espacio en disco y tiempo de ejecución.

En resumen, un commit es un objeto que apunta a un objeto de tipo tree que apunta a uno o varios objetos de tipo blob. Un objeto de tipo blob es un archivo, un objeto de tipo tree es un directorio y un objeto de tipo commit es un snapshot del proyecto en un momento dado.

> Técnicamente, un repositorio es un **grafo dirigido acíclico** donde los nodos son objetos de git (de tipo commit, tree o blob) y las aristas son referencias entre ellos. Con ello se consigue un **filesystem** de alto nivel, inmutable, eficiente y seguro, por encima del filesystem del sistema operativo. Además, gracias a los commits, se convierte en un **version filesystem**, con **control de versiones**.

#### References: Branches and HEAD

Las **ramas** en git son simplemente **punteros a commits**. En detalle son archivos de texto plano almacenados en la carpeta `.git/refs/heads` que contienen el hash del commit al que apuntan.

```shell
dir .git\refs\heads /b

main
```

```shell
type .git\refs\heads\main

f1dff43f97543e83cab3f52f054cdcf9b26e8d55
```

**Crear una nueva rama** se reduce a crear un nuevo archivo en la carpeta `.git/refs/heads` con el nombre de la rama y como contenido el hash del commit un commit, que de momento será el mismo que en la rama anterior.

```shell
git branch feature
dir .git\refs\heads /b

feature
main
```

```shell
type .git\refs\heads\feature

f1dff43f97543e83cab3f52f054cdcf9b26e8d55
```

Si en el SO creamos un fichero con el nombre de la rama y el contenido del hash del commit, git reconocerá la rama.

```shell
echo f1dff43f97543e83cab3f52f054cdcf9b26e8d55 > .git\refs\heads\bad-way
git branch

bad-way
feature
* main
```

```shell
del .git\refs\heads\bad-way

git branch

feature
* main
```

La rama main aparece indicada con un asterisco porque es la **rama actual** (current branch). Eso es lo que indica el **puntero `HEAD`**

El puntero `HEAD` es un archivo de texto plano almacenado en la carpeta `.git` que contiene el nombre de la rama actual. Como se ve en el contenido del archivo, es una referencia a una referencia

```shell
type .git\HEAD
ref: refs/heads/main
```

En realidad por cada rama se crea una referencia simbólica en la carpeta `.git/refs/heads` que apunta al hash del commit al que apunta la rama.

```shell
dir .git\refs\heads /b

feature
main
```

```shell
type .git\refs\heads\main

f1dff43f97543e83cab3f52f054cdcf9b26e8d55
```

Como veremos más adelante, algunos de los comandos más importasntes de Git son aquellos que permiten **mover el puntero `HEAD`** y **cambiar de rama**.

#### Taller: Crear un nueva repositorio desde cero

En su libro _Gitting Things Done_, 2021, disponible en [Amazon](https://www.amazon.com/-/es/Omer-Rosenbaum/dp/1801070004), _Omer Rosenbaum_ propone un interesante ejercicio destinado a comprender a fondo en que consiste un repositorio deGit, consistente en crearlo desde cero y añadirle un primer commit.

##### Creando un repositorio desde cero

Creamos una nueva carpeta y accedemos a ella.

```shell
mkdir scratch-repo
cd scratch-repo
```

Como es previsible git status nos indica que no estamos en un repositorio de git.

```shell
git status
// fatal: not a git repository (or any of the parent directories): .git
```

Creamos la estructura de carpetas básica de un repositorio.

```shell
mkdir -p .git
cd .git
mkdir objects
mkdir refs
cd refs
mkdir heads
cd..
cd..
tree
```

Obtenemos la siguiente estructura y volvemos a comprobar el estado del repositorio.

```shell
C:.
└───.git
    ├───objects
    └───refs
        └───heads
```

```shell
git status
fatal: not a git repository (or any of the parent directories): .git
```

El paso que nos falta es crear el fichero `HEAD` en la carpeta `.git` que apunte a la rama `main`.

```shell
echo ref: refs/heads/main > .git\HEAD
```

En este punto, git ya reconoce la carpeta como un repositorio.

```shell
git status
// On branch main
// No commits yet
// nothing to commit (create/copy files and use "git add" to track)
```

A pesar de que no existe la rama main en la carpeta `refs/heads/main`, git reconoce la rama `main` como la rama actual porque la tiene referenciada en el fichero HEAD.

##### Gestionando el repositorio con comandos plumbing

Hemos creado el repositorio simplemente con los comandos del SO, sin utilizar `git init`. Vamos a añadir un fichero al área de preparación y hacer el primer commit, pero sin utilizar los comandos porcelain, `git add` o `git commit`. En su lugar utilizaremos los comandos plumbing que subyacen a los de más alto nivel que utilizamos habitualmente.

Para crear un objeto blob, utilizamos el comando `git hash-object`, tal y como ya hemos visto, pasándole información desde el stdin.

```shell
echo Aprendiendo Git | git hash-object --stdin
// 7b31213ab333bd7eab40ce5de1185bd6565f120e
```

También sabemos que el modificados -w guarda el objeto en el repositorio.

```shell
echo Aprendiendo Git | git hash-object -w --stdin
tree .git
dir .git\objects\7b
```

```shell
C:.
└───.git
    ├───objects
    │   └───7b // 31213ab333bd7eab40ce5de1185bd6565f120e
    └───refs
        └───heads
```

Se ha creado un objeto blob en la carpeta `objects` del repositorio, con una sub-carpeta `7b` y un fichero con el nombre del resto del hash del objeto.
El comando `git cat-file` nos permite leer el tipo y el contenido del objeto.

```shell
git cat-file -t 7b31213 // blob
git cat-file -p 7b31213 // Aprendiendo Git
```

A pesar de ello, vemos que git status no refleja esta cambio

```shell
git status
```

Para añadir el objeto al área de preparación, necesitamos crear el indice, el fichero que contiene información sobre los hashes de los objetos que se han añadido al área de preparación. Para ello utilizaremos el comando `git update-index`.

```shell
git update-index --add --cacheinfo 100644 7b31213ab333bd7eab40ce5de1185bd6565f120e README.md
```

Indicamos la mascara del fichero a nivel del SO (100644), el hash del objeto y el nombre del fichero, que aun no existe.

EL resultado a nivel de git, es

```shell
git status

// Changes to be committed: new file:   README.md
// Changes not staged for commit: deleted:    README.md
```

El fichero está en el area de preparación, pero no en el directorio de trabajo. Para añadirlo al directorio de trabajo, crearemos el fichero con el mismo contenido que el objeto blob.

```shell
echo Aprendiendo Git > README.md
```

Y comprobamos que el fichero ha sido añadido al directorio de trabajo y aparece como staged en el área de preparación, seg´´un nos indica `git status`.

```shell
git status

// Changes to be committed: new file:   README.md
```

##### Creando un commit con comandos plumbing

El paso de la información desde la staged area al repositorio exige que creemos un objeto tree que contenga la información de los objetos que se han añadido al área de preparación. Para ello utilizamos el comando `git write-tree`. Para comprobar el contenido del objeto tree, utilizamos el comando `git cat-file`.

```shell
git write-tree // 3976f2ec82f4d61250cac1b1b26fa053439dbcae
git cat-file -t 3976f2e // tree
git cat-file -p 3976f2e // 100644 blob 7b31213ab333bd7eab40ce5de1185bd6565f120e    README.md
```

A nivel de carpetas, veremos que se a creado un objeto tree en la carpeta `objects` del repositorio.

```shell
tree .git
dir .git\objects\39
```

```shell
C:.
└───.git
    ├───objects
    │   └───39 // 76f2ec82f4d61250cac1b1b26fa053439dbcae
    │   └───7b // 31213ab333bd7eab40ce5de1185bd6565f120e
    └───refs
        └───heads
```

A partir del objeto tree, creamos un commit con el comando `git commit-tree`. Para ello necesitamos el hash del objeto tree, que ya conocemos.

```shell
git commit-tree 3976f2ec82f4d61250cac1b1b26fa053439dbcae -m "Initial commit" // 79aa70c84454bd9e928f0224139170837c8563c8
```

Nuestro objeto commit puede comprobarse con `git cat-file`.

```shell
git cat-file -t 79aa70c // commit
git cat-file -p 79aa70c // tree 3976f2ec82f4d61250cac1b1b26fa053439dbcae
```

Y nuestro repositorio refleja su existencia a nivel de carpetas pero no en el resultado de `git status`.

```shell
tree .git
dir .git\objects\79
```

```shell
C:.
└───.git
    ├───objects
    │   └───39 // 76f2ec82f4d61250cac1b1b26fa053439dbcae
    │   └───79 // aa70c84454bd9e928f0224139170837c8563c8
    │   └───7b // 31213ab333bd7eab40ce5de1185bd6565f120e
    └───refs
        └───heads
```

```shell
git status
// Changes to be committed:  new file:   README.md
```

El problema es simplemente que no se ha actualizado el puntero de la rama `main` al nuevo commit. En realidad, el fichero refs/heads/main al que hace referencia HEAD ni siquiera existe. Debemos crearlo con el hash del nuevo commit.

```shell
echo 79aa70c84454bd9e928f0224139170837c8563c8 > .git\refs\heads\main
```

De esta forma tanto `git status` como `git log` reflejarán la existencia del nuevo commit.

```shell
git status
// nothing to commit, working tree clean
git log
// commit 79aa70c84454bd9e928f0224139170837c8563c8 (HEAD -> main)
```

##### En resumen del Taller

Crear un nueva repositorio desde cero ha sido posible gracias a los comandos del SO y a los comandos de bajo nivel de Git, los **plumbing commands**.

Hemos creado un objeto blob, un objeto tree y un objeto commit, y hemos actualizado los punteros de la rama y HEAD para reflejar la existencia del nuevo commit. Pare ello hemos usado los siguientes comandos:

- `git hash-object`: para crear un objeto blob
- `git update-index`: para añadir el objeto al área de preparación
- `git write-tree`: para crear un objeto tree
- `git commit-tree`: para crear un objeto commit
- `git cat-file`: para leer el contenido de los objetos

### Commits: Herramientas para gestionar los commits

#### Comprobar el repositorio. Git log

```shell
git log
git log --graph --decorate --oneline
```

Log es uno de los comandos de git con más opciones. Algunas de las más útiles son

- `--graph`: Muestra el historial de commits en forma de grafo
- `--decorate`: Muestra las referencias de los commits (HEAD, master, ...)
- `--oneline`: Muestra los commits en una sola línea
- `--all`: Muestra todos los commits, no solo los de la rama actual
- `--author`: Filtra los commits por autor
- `--since`: Filtra los commits por fecha
- `--until`: Filtra los commits por fecha
- `--grep`: Filtra los commits por mensaje
- `--no-merges`: Muestra solo los commits que no son merges
- `--stat`: Muestra estadísticas de los cambios en los commits
- `--patch`: Muestra los cambios en los commits

Se suelen combinar varias opciones para obtener la información deseada

- `--graph --oneline --decorate --all`: Muestra el historial de commits en forma de grafo, en una sola línea, con las referencias y todos los commits

Si estas combinaciones se utilizan con frecuencia, se pueden añadir a la configuración de git como alias

```shell
git config --global alias.lol "log --graph --decorate --oneline"
git lol
```

Se puede indicar a partir de que commit debe de empezar la serie
git log <commit-name>

```shell
git log master~2
```

Se puede especificar un rango (desde .. hasta)
git log <commit-name>..<commit-name>

```shell
git log master~12..master~10
```

Se pueden mostrar los commits que afectan a un determinado path (carpeta, fichero…)
git log -- <path>

```shell
git log -- README3.txt
```

Se pueden mostrar los commits que coincidan con una expresión regular
git log --grep=‘reg-exp’

Se pueden excluir del listado los commits resultantes de un merge

```shell
git log --no-merges
```

Se pueden mostrar los cambios producidos durante un tiempo

```shell
git log --since={2010-04-18}
git log --before={2010-04-18}
git log --after={2010-04-18}
```

Dado lo complejo de la sintaxis de git log, y las limitaciones gráficas de la consola, se pueden utilizar herramientas gráficas para visualizar el historial de commits.

Por ejemplo, **gitk**, que se instala con Git, o **gitg**, que es una herramienta gráfica de Git para Gnome.

En **VSC** se puede utilizar la extensión **Git Graph**

#### Alias

Los alias fueron añadidos en Git 1.4.0

Evitan tener que teclear repetidas veces el mismo comando completo

Se pueden configurar en cualquiera de los ámbitos de configuración mencionados (system, global, local) tanto por línea de comandos como directamente en el fichero de configuración correspondiente

```shell
git config --global alias.lol "log --graph --decorate --oneline"
git lol
```

Un ejemplo de alias más complejo

```shell
git config --global alias.hist git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short
git hist
```

Los alias de git admiten los mismos parámetros y modificadores que los comandos originales

```shell
git config --global alias.ch git checkout
git ch -b feature/branch
```

#### Operaciones en la Staging Area (Index)

##### Añadir ficheros

Como ya hemos visto, el comando `git add` añade ficheros al área de preparación (staging area). Se puede añadir un solo fichero, todos los ficheros de un directorio o todos los ficheros del directorio de trabajo.

```shell
md samples
echo 'Sample One' > samples\sample1.txt
echo 'Sample Two' > samples\sample2.txt
tree samples /f
```

Se puede añadir al index

- un conjunto de ficheros
- todos los disponibles

```shell
git add <file>
git add .
git status
```

##### Eliminar de la Staging Area (Index)

Eliminar elementos de la zona de preparación (staging area), i.e. revertir add, se puede hacer de varias formas

Cuando aun no se ha hecho commit, se utiliza un formato especial, ya que aún no existe el HEAD

```shell
git rm --cached <file>
```

Si ya se ha hecho algún commit, el comando anterior, ademas de eliminar el fichero de la staging area, lo elimina del directorio de trabajo.

En estas circunstancias, se puede utilizar

```shell
git reset <file>
```

O la opción moderna, recomendada en el git status

```shell
git restore --staged <file>
```

git restore es un nuevo comando que reproduce una parte de la funcionalidad de git checkout: recover an earlier commit.

Una variación de git reset permite eliminar un archivo de la staging area y enviando al directorio de trabajo su estado en el último commit

```shell
git reset HEAD <file>
```

Por otra parte, el comportamiento de git checkout con ficheros trazados por git (tracked) es un poco diferente

- git checkout -- path: el path se toma como un fichero o directorio, si es un directorio, significa todos los ficheros dentro de ese directorio, recursivamente, y Git copia la copia actual del fichero tal como se encuentra en el índice a su árbol de trabajo.
- git checkout HEAD -- path: el path se toma en la misma forma que antes, y Git copia la copia actual del fichero tal como se encuentra en el commit HEAD al índice y al árbol de trabajo.

```shell
git checkout -- <file>
git checkout HEAD -- <file>
```

#### Eliminar ficheros

Puede hacerse en dos fases

- eliminar de la workArea (mediante el SO)
- subir el cambio a la Staging Area

```shell
del samples\sample1.txt
git status
git add samples\sample1.txt
git status
```

Es preferible hacerlo en un solo paso
Al ser un borrado definitivo, es necesario el modificador f

```shell
git status
git rm samples\sample2.txt
git status
git rm -f samples\sample2.txt
git status
```

##### Problemas con .gitignore

En algún caso puede que añadamos a git ignore nuevos elementos que ya estaban en el repositorio. En este caso, git no los ignorará, ya que ya los conoce. Para que los ignore, hay que eliminarlos del repositorio

Con el comando rm podremos borrar los archivos del repositorio, pero si lo ejecutamos tal cual nos eliminará también el archivo de nuestro directorio de trabajo.

Si queremos conservarlo tendríamos que poner lo siguiente:

```shell
git rm --cached <file>
```

Si lo que queremos eliminar es un directorio con todo su contenido el comando sería el siguiente:

```shell
git rm -r --cached <directory>
```

El modificador -r indica que se trata de un directorio procesado de forma recursiva, es decir con todos sus ficheros y directorios, con todos los niveles de anidamiento que pueda tener.

En este punto tendremos pendiente de commit la eliminación del archivo o carpeta del repositorio, por lo que tendremos que hacer un commit para que se aplique el cambio.

```shell
git commit -m "Eliminado archivo de referido en .gitignore"
```

Finalmente actualizaremos con nuestros cambios el remoto

```shell
git push
```

#### Cambiar nombre de ficheros

```shell
md samples
echo 'Sample One' > samples\sample_bad1.txt
echo 'Sample Two' > samples\sample_bad2.txt
tree samples /f
git add .
```

Igual que en el caso anterior, puede hacerse en un paso o en dos

En dos fases

- cambiar el nombre en la workArea (mediante el SO)
- subir el cambio a la Staging Area

```shell
ren samples\sample_bad1.txt sample1.txt
git status
git add samples\sample_bad1.txt
git add samples\sample1.txt
git status
```

En una sola fase

```shell
git mv samples\sample_bad2.txt samples\sample2.txt
git status
```

#### git diff

Permite ver los cambios entre dos commits, dos ramas, dos ficheros, etc.

Por defecto, compara el directorio de trabajo con el index (staging area)

```shell
git diff
```

Para comparar el directorio de trabajo con el último commit

```shell
git diff HEAD
```

Para comparar el directorio de trabajo con un commit concreto

```shell
git diff <commit>
```

Para comparar dos commits

```shell
git diff <commit1> <commit2>
```

Para comparar dos ramas

```shell
git diff <branch1> <branch2>
```

Para comparar dos ficheros

```shell
git diff <file1> <file2>
```

En todos los casos, git tiene que calcular las diferencias, por lo que el resultado no es inmediato. Hay que recordar que en git no se almacenan las diferencias, sino los estados de los ficheros en cada commit.

#### git blame

Permite conocer el autor de la última modificación de cada línea de un fichero y en que commit se incluyó el cambio.

```shell
git blame <file>
```

Es una herramienta muy útil para la revisión de código, que permite quién ha hecho un cambio en un fichero y para saber por qué se ha hecho un cambio.

Esta también disponible cuando se accede al repositorio en GitHub

### Recapitulando: Git básico

- `git config`: Configura Git; permite añadir alias
- `git init`: Inicializa un repositorio local de Git
- `git clone`: Clona un repositorio de Git
- `git status`: Muestra el estado de los archivos en el directorio de trabajo (workArea) y el área de preparación
- `git add`: Agrega un archivo al área de preparación (stagedArea)
- `git commit`: Guarda los cambios en el repositorio
- `git log`: Muestra el historial de commits
- `git show`: Muestra los cambios de un commit
- `git rm`: Elimina un archivo del repositorio
- `git mv`: Cambia el nombre de un archivo
- `git reset`: Mueve el puntero de la rama; en consecuencia restablece el estado de los archivos al commit indicado
  - `git reset <file>`: Elimina el fichero de la staging area
- `git checkout <file>` mueve los ficheros entre el repositorio, el área de preparación y el directorio de trabajo
  - `git restore --staged <file>`: Elimina el fichero de la staging area
- `git diff`: Muestra las diferencias entre dos commits, dos ramas, dos ficheros, etc.
- `git blame`: Muestra el autor de la última modificación de cada línea de un fichero y en que commit se incluyó el cambio
- `git remote`: Conecta el repositorio local con un repositorio remoto
- `git push`: Sube todos los cambios locales al repositorio remoto
- `git pull`: Descarga los cambios del repositorio remoto al repositorio local
-

### REESCRIBIENDO LA HISTORIA

#### amend

#### git checkout

git checkout mueve el puntero de referencia HEAD a un commit específico. - en otra rama (lo habitual) - en la misma rama:

```shell
git checkout HEAD~1

You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may do so (now or later) by using -c with the switch command. Example: git switch -c [new-branch-name]

Or undo this operation with: git switch -
```

##### git checkout a nivel de archivo

En lugar de mover el HEAD del repositorio, lo que hace es llevar al directorio de trabajo el fichero al que hemos hecho checkout con el contenido que tenía en el commit especificado

```shell
git checkout HEAD~1 README.md
```

El resultado es que el fichero README.md en el area de trabajo vuelve a tener el contenido que tenía en el commit anterior al HEAD.

```shell
git checkout HEAD~1 README.md --stage
```

En este caso, el fichero README.md en el área de preparación vuelve a tener el contenido que tenía en el commit anterior al HEAD.
