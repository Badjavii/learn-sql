# Aprende SQL | Documentacion Personal

## Objetivo del Repositorio

Este repositorio es un espacio colaborativo para compartir ejercicios y contenido teórico referente al **Nivel Fisico** en la creación de un Sistema de Base de Datos. Para eso, nos enfocaremos en el uso exclusivo del **Lenguaje de Consultas Estructuradas** (SQL).

## Introducción 

Una base de datos es una herramienta informática cuyo objetivo es almacenar, organizar y recuperar información de manera eficiente. A diferencia de otros medios de almacenamiento como archivos de texto o hojas de cálculo, las bases de datos están diseñadas para manejar grandes volúmenes de datos, garantizar su integridad y permitir el acceso concurrente de múltiples usuarios o aplicaciones.

### ¿Por qué existen las bases de datos?

Las organizaciones (empresas, instituciones, gobiernos, etc) generan y consumen información constantemente como registros de clientes, inventarios, transacciones, historial médico, entre otros. Gestionar toda esa información de forma manual o con archivos planos se vuelve inviable a medida que el volumen y la complejidad crecen.

De esta necesidad surgen los **Sistemas de información**, cuyo propósito es capturar, procesar y distribuir datos para apoyar la toma de decisiones dentro de una organización. Cuando un Sistema de Información implementa una base de datos para modelar y persistir esos datos de forma estructurada, hablamos de un **Sistema de Base de Datos (SBD)**.

La constructión de un Sistema de Base de Datos se compone por varias capas o niveles. Este repositorio se sitúa en el **nivel físico**, que es donde pasamos del diseño abstracto a la implementación concreta. Aquí definimos tablas, tipos de datos, índices y relaciones que el motor de base de datos puede ejecutar directamente.

Para trabajar en este nivel utilizamos SQL, el estándar universal para interactuar con bases de datos relacionales. 

### Funcionamiento interno de una base de datos

Cuando se interactua con una base de datos, no se hace directamente con los archivos en disco. Entre el usuario y el almacenamiento físico existe una capa de software llamada **Sistema Manejador de Base de Datos (SMBD)**, también conocido como *motor de base de datos* o simplemente *manejador*. Este se encarga de:

- **Interpretar** las consultas que el usuario escribe.
- **Optimizar** la forma en que se accede a los datos internamente.
- **Garantizar** la integridad y consistencia de la información.
- **Gestionar** el acceso concurrente de múltiples usuarios sin que los datos se corrompa.
- **Controlar** los permisos y la seguridad sobre los datos.

En otras palabras, el manejador es el intermediario entre el usuario y los datos. Algunos manejadores ampliamente utilizados son PostgreSQL, MySQL, SQLite, MariaDB y Oracle Database. 

### Entornos de trabajo

Para trabajar con una base de datos necesitamos al menos dos componentes:

**1. El manejador (SMBD)**
Es el motor que corre en un servidor (local o remoto) y gestiona los datos. Puede correr como un proceso en la propia máquina o en un servidor dedicado en la nube.

**2. El cliente de base de datos**
Es la herramienta que hace la conexión con el manejador para enviarle instrucciones. Puede ser:

- Una **interfaz gráfica (GUI)** como DBevaer, TablePlus, SQLDeveloper, DataGrip, que ofrecen un entorno visual para explorar tablas y ejecutar consultas.
- Un **cliente de línea de comandos (CLI)** como psql (PostgreSQL) o mysql (MySQL), donde escribimos instrucciones directamente en la terminal.

La comunicación entre cliente y manejador ocurre a través de un protocolo de red, incluso cuando ambos corren en la misma máquina. Es decir, se activa el manejador por un lado y por otro lado el cliente. 

### SQL y sus subdivisiones

SQL es el lenguaje estándar para interactuar con base de datos relacionales. A diferencia de lenguajes como Python o JavaScript, SQL es un lenguaje declarativo; es decir, no se le dice al motor *cómo* obtener los datos paso a paso, sino *qué* datos se quieren, y el motor decide la forma más eficiente de conseguirlos. 

Lo que sí hace a SQL particular es que opera directamente sobre la estructura de los datos, sin capas de abtracción intermedias. Esto lo hace más cercano al funcionamiento real del sistema. 

SQL se divide en varios sublenguajes según el tipo de operación que realizan:

- **DDL (Data Definition Language):** Definir y modificar la estructura de la base de datos (CREATE, ALTER, DROP).

- **DML (Data Manipulation Language):** Insertar, modificar y eliminar datos (INSERT, UPDATE, DELETE).

- **DQL (Data Query Language):** Consultar y recuperar datos (SELECT).

- **DCL (Data Control Language):** Gestionar permisos y accesos (GRANT, REVOKE).

- **TCL (Transaction Control Language):** Controlar, aprobar o revertir transacciones (COMMIT, ROLLBACK, SAVEPOINT). 

Este repositorio recorre estos sublenguajes de forma progresiva, comenzando por la definición de estructuras con DDL y avanzando hacia consultas más complejas con DQL.

también se toca 

### Manejador de trabajo: Oracle Database

Para los ejercicios y ejemplos de este repositorio, se utiliza **Oracle Database** como manejador principal. Oracle es uno de los SMBD más robustos y utilizados en entornos empresariales, lo que lo convierte en una herramienta de gran valor profesional. 

Además de practicar SQL estándar, se explora componentes internos y objetos propios del motor que no siempre se cubren en cursos introductorios. 

#### Archivos internos del manejador

Oracle organiza su almacenamiento y operación a través de distintos tipos de archivos que el motor gestiona internamente: 

- **Datafiles (.dbf):** Contiene los datos reales de las tablas e índices.

- **Redo Log Files:** Registran todos los cambios realizados, usados para recuperación ante fallos. 

- **Control Files:** Contienen metadatos críticos sobre la estructura de la base de datos. 

- **Archive Log Files:** Copias históricas de los redo logs, usados para recuperación completa de los datos.

- **Parameter File (SPFILE/PFILE):** Configuración de inicio del motor. 

## Contenido del Repositorio

Oracle expone una rica variedad de objetos y propiedades con los que se puede construir sistemas completos. Este repositorio abarca lo siguiente: 

### 1. Clasificación y Ciclo de Vida de los Datos
- **Clasificación de Tablas por Comportamiento**
    - Tablas de Entrada, Tablas de Salida y Tablas Mixtas (Entrada/Salida)
- **Volatibilidad y Gestión de Memoria**
    - Tipos y escalas de Volatibilidad
    - Mecanismos de persistencia en disco
        - Gestión de buffers de memoria y Segmentos de Rollback 
    - Impacto de la volatibilidad en la concurrencia 
    - Dificultad de confirmación transaccional

### 2. Fundamentos de Operaciones y Sublenguajes (SQL Físico)
- **El Ecosistema Transaccional (DML, DDL, TCL)**
    - Buenas prácticas de modificación de datos
    - Control transaccional (TCL)
        - Commits explícitos y Commits Implícitos
- **Procesamiento de Consultas (DQL) y Expresiones**
    - Manipulación de datos elementales
        - Operadores lógicos
        - Concatenación 
        - Funciones de conversión 
        - Formatos de fecha
    - Funciones de grupo y Funciones escalares

### 3. Consultas Avanzadas y Estructuras Relacionales
- **Mecánica y Álgebra de JOINS**
    - EQUI JOIN, NON-EQUI JOIN, OUTER JOIN y JOIN Recursivo (SELF JOIN)
- **Anatomía de las Subconsultas** 
    - Subconsultas en cláusula WHERE
    - Subconsultas correlacionadas (EXISTS)
    - Subconsultas como origen de datos (FROM)
    - Subconsultas en valores de inserción (INSERT)
- **Optimización y Complejidad Algorítmica**
    - Notación Big O aplicada a bases de datos 
        - Complejidad Espacial y Complejidad Temporal
    - Análisis de rendimiento mediante Planes de Ejecución del SMBD

### 4. Objetos del Esquema y Optimización del Almacenamiento
- **Índices de Alto Rendimiento**
    - Anatomía del acceso rápido
        - Estructuras basadas en ROWID, llaves primarias y columnas indexadas
    - Criterios técnicos para la creación de índices adicionales
- **Vistas como Mecanismos de Abstracción**
- **Secuencias**

### 5. Programación con PL/SQL Procedimental 
- **Programas Almacenados Básicos**
    - Procedimientos (Procedures)
    - Funciones (Functions)
- **Paquetes (Packages)**
- **Disparadores (Triggers)**
    - Dependencia estructural estricta de los Triggers
    - Niveles de ejecución de Triggers

### 6. Seguridad Discreta y Auditoría del Sistema
- **Modelo de Propiedad**
- **Ciclo de Control de Acceso**
- **Control de Roles**
- **Auditoría del Sistema**
