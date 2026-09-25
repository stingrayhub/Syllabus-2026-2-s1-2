# Documentación Completa del Esquema de Base de Datos

A continuación, se detalla el modelo separando claramente las Entidades Fuertes, Entidades Débiles y Agregaciones, asignando tipos de datos lógicos (como `VARCHAR`, `DATE`, `INTEGER`) a cada atributo.

- **Notas:**
- En la imagen con los diagramas la parte superior tiene las entidades con sus atributos, el resto de esquemas son relaciones necesarias para solucionar distintas necesidades del enunciado, en estos se presentan agregaciones que para simplificar los esquemas son mencionados como entidades débiles al ser usadas en otras relaciones.
- Los atributos heredados son marcados con "[]".
- Cuando la llave de una identidad se usa en una relaciones o agregaciones se marca con la primera letra y un punto, ej: rut director -> D.rut.
- Aunque varias entidades representen personas, solo Jugador y Técnico son hijos de otra ya que son las unicas que comparten la necesidad de cubrir sanciones.
- Cambios sobre estos esquemas son posibles dependiendo de las necesidades de las siguentes entregas.
- Con el fin de manteder flexibilidad para las próximas entregas se decidió que el atributo rut y rut/pasaporte de las personas serán conciderados el mismo bajo el nombre rut/pasaporte.
- De igual manera en los esquemas se usa "nombre" o "nombre completo" pero el titulo de estas variable se pueden conciderar intercambialbes.
- Se puede complejizar/complementar este sistema usando la entidad fecha para los esquemas definidos y otros.
- Si en la descripcion de cada relacion no se especifica com es enconces suponga que puede ser n es a n sin repetición.
- **Uso de IA:**
- Al momento de crear los esquemas se usó solo para dudas conceptuales y para evaluar opciones de notación sobre acciones en las tablas (acciones que al ser evaluadas se llegaba a la conclusion que no eran convenientes y complejizaban más que aportar)
- Para crear la documentación se le entregó el diagrama en formato XML a Gemini para que creara una planilla con las descripciones, se hizo varias correciones manuales al documento pero se mantuvo el formato sugerido.
- Al terminar se preguntó si el esquema respetaba la normalizacón BCNF y a partir de esto se hicieron las correciones necesarias.

---

## 1. Entidades Fuertes

### 1.1 Entidad Padre

* **Sentenciable**
  * `rut/pasaporte` (PK): `VARCHAR(20)`
  * `nombre`: `VARCHAR(100)`
  * `fecha de nacimiento`: `DATE`
  * `nacionalidad`: `VARCHAR(50)`
  * **Descripción:** Entidad padre que guarda el registro general y los datos personales compartidos de todos los individuos (jugadores y técnicos) que participan en el campeonato y son susceptibles a recibir faltas o sentencias disciplinarias.

### 1.2 Entidades Hijas (Subtipos de Personas)

* **Jugador** *(Hereda de Sentenciable)*

  * **Atributos Heredados:**
    * `[rut/pasaporte]` (PK): `VARCHAR(20)`
    * `[nombre]`: `VARCHAR(100)`
    * `[fecha de nacimiento]`: `DATE`
    * `[nacionalidad]`: `VARCHAR(50)`
  * **Atributos Propios (y de Contrato/Equipo):**
    * `sueldo`: `INTEGER` (o `DECIMAL(10,2)`)
  * **Descripción:** Guarda el registro específico de los deportistas, extendiendo la información de la entidad padre.
* **Técnico** *(Hereda de Sentenciable)*

  * **Atributos Heredados:**
    * `[rut/pasaporte]` (PK): `VARCHAR(20)`
    * `[nombre]`: `VARCHAR(100)`
    * `[fecha de nacimiento]`: `DATE`
    * `[nacionalidad]`: `VARCHAR(50)`
  * **Atributos Propios:**
    * *(En este esquema, el Técnico se define principalmente por su rol y hereda todos los datos personales sin atributos adicionales propios mostrados, más allá de sus relaciones con el equipo).*
  * **Descripción:** Almacena a los profesionales encargados de dirigir al equipo, dependiendo de la entidad padre para sus datos personales base.

### 1.3 Otras Entidades de Personas

* **Dirigente**

  * `rut/pasaporte` (PK): `VARCHAR(20)` (En el esquema especificado como rut)
  * `nombre`: `VARCHAR(100)`
  * `fecha de nacimiento`: `DATE`
  * `nacionalidad`: `VARCHAR(50)`
  * `cargo`: `VARCHAR(50)`
  * `email`: `VARCHAR(100)`
  * `teléfono`: `VARCHAR(20)`
  * **Descripción:** Guarda el registro del personal administrativo e institucional.
* **Árbitro**

  * `rut/pasaporte` (PK): `VARCHAR(20)`
  * `nombre`: `VARCHAR(100)`
  * `fecha de nacimiento`: `DATE`
  * `nacionalidad`: `VARCHAR(50)`
  * `email`: `VARCHAR(100)`
  * `teléfono`: `VARCHAR(20)`
  * **Descripción:** Almacena la nómina de jueces habilitados para dirigir y sancionar los encuentros.
* **Integrantes Tribunal**

  * `rut/pasaporte` (PK): `VARCHAR(20)`
  * `nombre`: `VARCHAR(100)`
  * `fecha de nacimiento`: `DATE`
  * `email`: `VARCHAR(100)`
  * `teléfono`: `VARCHAR(20)`
  * **Descripción:** Registra a las autoridades encargadas de revisar los informes arbitrales y dictaminar sentencias o castigos.

### 1.4 Otras Entidades Fuertes

* **Equipo**

  * `rut` (PK): `VARCHAR(20)`
  * `nombre`: `VARCHAR(100)`
  * `dirección`: `VARCHAR(200)`
  * `email`: `VARCHAR(100)`
  * `presidente`: `VARCHAR(100)`
  * **Descripción:** Guarda el registro oficial de los clubes deportivos que compiten en los campeonatos.
* **Estadio**

  * `dirección` (PK): `VARCHAR(200)`
  * `nombre` : `VARCHAR(100)`
  * `cantidad espectadores`: `INTEGER`
  * `tipo`: `VARCHAR(50)`
  * **Descripción:** Almacena la información de la infraestructura donde se disputan los partidos, se decide usar la dirección como clave dos estadios no pueden estar en la misma dirección.
* **Campeonato**

  * `nombre` (PK): `VARCHAR(100)`
  * `tipo`: `VARCHAR(50)`
  * **Descripción:** Registra la instancia competitiva general que enmarca la participación de los equipos.
* **Fecha-Hora**

  * `hora`: `TIME`
  * `fecha`: `DATE`
  * **Descripción:** Se usa para crear relaciones de otras entidades con periodos de tiempos.

---

## 2. Entidades Débiles

Las entidades débiles no existen por sí solas; requieren de las claves primarias de las entidades fuertes (o agregaciones) a las que están vinculadas para ser identificadas unívocamente. Basado en el esquema, se definen las siguientes entidades débiles y los atributos que guardan (claves heredadas y atributos propios):

### 2.1 Entidades Débiles relacionadas a Equipos (Nóminas)

* **Cuerpo Técnico**

  * **Atributos:**
    * `E.rut`: `VARCHAR(20)` (Clave heredada de Equipo)
    * `T.rut/pasaporte`: `VARCHAR(20)` (Clave heredada de Técnico)
    * `rol`: `VARCHAR(50)`
  * **Descripción:** Modela la pertenencia de un técnico al cuerpo técnico de un equipo, especificando el rol particular que cumple.
* **Plantel Jugadores**

  * **Atributos:**
    * `E.rut`: `VARCHAR(20)` (Clave heredada de Equipo)
    * `J.rut/pasaporte`: `VARCHAR(20)` (Clave heredada de Jugador)
    * `rol`: `VARCHAR(50)`
    * `fecha inicio`: `DATE`
    * `fecha fin`: `DATE`
    * `posición`: `VARCHAR(30)`
  * **Descripción:** Modela la pertenencia de un jugador al plantel de un equipo, especificando su rol y el periodo de tiempo asociado. Un jugador no puede estar en dos equipos o con dos posiciones al mismo tiempo.
* **Grupo Dirigentes**

  * **Atributos:**
    * `E.rut`: `VARCHAR(20)` (Clave heredada de Equipo)
    * `D.rut/pasaporte`: `VARCHAR(20)` (Clave heredada de Dirigente)
    * `cargo`: `VARCHAR(50)` (Atributo propio/heredado de la relación con Dirigente)
    * `fecha inicio`: `DATE`
    * `fecha fin`: `DATE`
  * **Descripción:** Define la conformación de la directiva de un equipo mediante la asociación de los dirigentes, sus respectivos cargos y el periodo de tiempo asociadoun. Un dirigente no puede estar de dos equipos o complir dos roles al mismo tiempo.

### 2.2 Entidades Débiles relacionadas a Partidos (Eventos/Roles)

* **Árbitro de partidos**

  * **Atributos:**
    * `fecha`: `DATE` (Clave heredada de Partido)
    * `hora`: `TIME` (Clave heredada de Partido)
    * `dirección`: `VARCHAR(200)` (Clave heredada de Partido)
    * `A.rut/pasaporte`: `VARCHAR(20)` (Clave heredada de Árbitros)
    * `rol`: `VARCHAR(50)`
  * **Descripción:** Asigna a un árbitro a un partido específico y define qué rol cumple, para esta entidad debil la combinación fecha hora y A.rut/pasaporte son únicas ya que un arbitro no puede estár en dos lugares al mismo tiempo.
* **Falta de Partido**

  * **Atributos:**
    * `fecha`: `DATE` (Clave heredada de Partido)
    * `hora`: `TIME` (Clave heredada de Partido)
    * `dirección`: `VARCHAR(200)` (Clave heredada de Partido)
    * `S.rut/pasaporte`: `VARCHAR(20)` (Clave heredada de Sentenciable)
    * `color`: `VARCHAR(20)` (Atributo propio)
    * `minuto`: `INTEGER` (Atributo propio)
  * **Descripción:** Registra una infracción cometida por un "Sentenciable" (jugador/técnico) durante un partido, indicando el minuto y el color de la tarjeta, se usa la fecha hora minuto y S.rut/pasaporte como llave de esta entidad.
* **Gol de partido**

  * **Atributos:**
    * `fecha`: `DATE` (Clave heredada de Partido)
    * `hora`: `TIME` (Clave heredada de Partido)
    * `dirección`: `VARCHAR(200)` (Clave heredada de Partido)
    * `J.rut/pasaporte`: `VARCHAR(20)` (Clave heredada de Jugador)
    * `minuto`: `INTEGER` (Atributo propio)
  * **Descripción:** Registra una anotación realizada por un jugador específico durante un partido, indicando el minuto exacto del gol, se usa la fecha hora minuto y J.rut/pasaporte como llave de esta entidad.

---

## 3. Agregaciones

Las agregaciones empaquetan una relación (entre varias entidades) y la tratan como una entidad de orden superior para poder relacionarla con otras. Basado en el esquema, se definen las siguientes agregaciones y los atributos (globos verdes) que estas conservan para identificar el evento o la relación:

* **Equipos de campeonato**

  * **Atributos:**
    * `E.rut`: `VARCHAR(20)` (Clave de Equipo)
    * `nombre`: `VARCHAR(100)` (Clave de Campeonato)
  * **Descripción:** Agrupa la relación de pertenencia o inscripción de los equipos dentro de un campeonato específico.
* **Equipo ganador de Campeonato**

  * **Atributos:**
    * `E.rut`: `VARCHAR(20)` (Clave de Equipo)
    * `nombre`: `VARCHAR(100)` (Clave de Campeonato)
  * **Descripción:** Encapsula el hito o registro de que un equipo específico se ha consagrado como ganador de un campeonato determinado, un campeonato solo puede tener un equipo campeon, pero un equipo puede tener varios campeonatos ganados.
* **Equipo puede ser local de Estadio**

  * **Atributos:**
    * `E.rut`: `VARCHAR(20)` (Clave de Equipo)
    * `dirección`: `VARCHAR(200)` (Clave de Estadio)
  * **Descripción:** Relaciona a un equipo con el o los estadios donde tiene permitido o asignado ejercer su localía.
* **Partido**

  * **Atributos:**
    * `hora`: `TIME`
    * `fecha`: `DATE`
    * `dirección`: `VARCHAR(200)` (Clave de Estadio)
  * **Descripción:** define el contexto en el que se puede hacer un partido, vinculando una fecha y hora específicas con el estadio donde se lleva a cabo, estas combinaciones no se pueden repetir.
* **Partido de Campeonato**

  * **Atributos:**
    * `C.nombre`: `VARCHAR(100)` (Clave de Campeonato)
    * `hora`: `TIME`
    * `fecha`: `DATE`
    * `dirección`: `VARCHAR(200)` (Claves provenientes de la agregación de Partido)
  * **Descripción:** Conecta la agregación base de "Partido" con un "Campeonato", indicando a qué torneo pertenece dicho encuentro, un campeonato puede tener varios partidos pero un partido no puede ser de varios campeonatos.

---

## 4. Esquemas de Relaciones Finales

En esta sección se documentan los esquemas que resultan estrictamente en tablas de relaciones (relaciones que interconectan entidades o modelan interacciones que no son entidades por sí mismas).

* **Relación Partido (Local vs Visita)**
  * **Claves Foráneas (Composición):**
    * `E.L.rut` (FK): `VARCHAR(20)` (Referencia a Equipo)
    * `E.V.rut` (FK): `VARCHAR(20)` (Referencia a Equipo)
    * `campeonato` (FK): `VARCHAR(100)` (Referencia a Campeonato)
    * `direccion` (FK): `VARCHAR(200)` (Referencia a Estadio)
    * `fecha`: `DATE` (Referencia a Fecha-Hora)
    * `hora`: `TIME` (Referencia a Fecha-Hora)
  * **Relación Final:** Tabla que almacena el enfrentamiento deportivo entre dos equipos E.L.rut y E.V.rut referencian al Equipo Local y Equipo Visita respectivamente dentro de un Campeonato y en un Estadio específico, registrando la fecha y hora del partido, como la agregación Partido no tiene repetidos se podria conciderar que fecha, hora y direccion son la llave de esta relación, cmpeonato depende directamente de estas y las combinaciones de los equipos se pueden repetir por campeonato según la naturaleza de estos.
